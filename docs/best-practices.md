# Best Practices for Interleaved Retrieval Experiments with STELLA

**Last updated:** August 2026

This guide walks through what you need to run a valid interleaved retrieval experiment with STELLA from setup to interpretation.

---

## 1. Understand interleaving

<p class="faq-question">What is interleaving?</p>

Interleaving is an online evaluation technique used to compare two or more ranking systems (e.g., search engines, recommendation systems) directly against each other using real user behavior.

The core idea is simple: for a single user query, STELLA fetches results from both a **baseline** system (`base`) and an **experimental** system (`exp`). Both rankings are then combined: "interleaved" into a single, unified list, which is shown to the user as one blended result set. The better system is determined by which system's documents the user actually clicks on.

We use interleaving because it's a highly sensitive and efficient way to measure user preference between two rankers in a live environment. Rather than inferring preference indirectly from aggregate metrics, interleaving directly asks: *given these two sets of results, which do you prefer?*

<p class="faq-question">Why bother with interleaving instead of A/B testing?</p>

A/B tests compare two separate user groups. Interleaving compares two rankers on the **same query, same user, same moment**. While traditional A/B testing is a powerful tool, interleaving is often superior for evaluating ranking changes. In an A/B test, a change in Click Through Rate (CTR) could stem from your system update or from different user cohorts, varying query types, time-of-day effects or random chance. Interleaving cancels out most of that noise because both systems are judged by the same user on the same query simultaneously.

**Rule of thumb:** use interleaving when you're evaluating ranking quality. Use A/B when you're changing something that affects the whole experience (UI redesign, pricing, onboarding).

<p class="faq-question">What algorithm does STELLA use?</p>

Team Draft Interleaving (TDI).

<p class="faq-question">How does TDI work in plain terms?</p>

It works like picking teams for a school sports game:

1. Two team captains are designated: one for Team Baseline and one for Team Experimental.
2. To fill the first slot in the interleaved list, we flip a coin to decide which captain picks first.
3. The chosen captain picks the best player (document) from their original result list that hasn't been picked yet.
4. The other captain then does the same.
5. Then we start again from step 2 by flipping a coin again and continue taking turns until the interleaved list is full.

STELLA tags every slot as `BASE` or `EXP` so clicks can be attributed correctly. If one system returns fewer results or times out, baseline results are used to pad the list (see section: [*What biases do I need to prevent?*](#2-design-your-experiment)).

<p class="faq-question">Are there other interleaving methods?</p>

Yes. Balanced Interleaving is more prone to positional biases; Probabilistic Interleaving is more experimental. STELLA ships with TDI as the standard. It is best to not swap algorithms mid-experiment.

---



## 2. Design your experiment

Careful planning is crucial for a successful experiment with valid results. This phase ensures your experiment is well-defined, properly scoped and free from common biases.

**What you need:** one baseline system, one experimental system, one hypothesis and a valid configuration.

<p class="faq-question">What are the two systems I'm comparing?</p>

Every experiment involves at least two retrieval systems:


| Role             | What it is                                                                                                                                                                              |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Baseline**     | Current production ranker/recommender. The standard you compare against what the experiment system could replace.                                                                               |
| **Experimental** | Your new system. It should incorporate **one specific change** tied to your hypothesis. If you change the model, the features, *and* the diversification logic at once, you won't know what helped. |


<p class="faq-question">What should I change in the experimental system?</p>

Only what your hypothesis requires. Some typical changes:


| Hypothesis type               | Example change                                                                   |
| ----------------------------- | -------------------------------------------------------------------------------- |
| Semantic vs keyword retrieval | Swap a phrase/keyword search backend for a vector/embedding-based search backend |
| New re-ranker                 | Add a post-retrieval scoring step before returning results                       |
| Different index               | Swap the underlying index or vector collection                 |


Whatever you change, keep the response shape identical: same fields, same document identifier key, same number of results per page. If the experimental wrapper returns a different schema than the baseline, STELLA can't merge and attribute clicks correctly.

<p class="faq-question">What does a good hypothesis look like?</p>

It's tempting to skip this and just ask "which system performs better?" but that question is too broad to design an experiment around. It doesn't tell you what to change, what to expect or how to interpret a win. A hypothesis narrows this down: it names the one change you're making and the effect you expect from it, so the result is actually actionable regardless of outcome.

A good hypothesis is specific and testable. Examples:

- *"Vector search will outperform phrase search on natural-language queries."*
- *"Re-ranking with metadata boosts will lift click-through on facet-filtered searches."*
- *"A larger embedding model improves win rate on ambiguous single-word queries."*

<p class="faq-question">What biases do I need to prevent?</p>

Interleaving removes a lot of the noise inherent in A/B testing, but it isn't automatically bias-free. A few specific biases can invalidate an otherwise well-designed experiment:


| Bias                                            | What goes wrong                                                                                                                                                                                                                                                         | What to do                                                                                                                                       |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Presentation**                                | The results from both systems must look identical. Differences in titles, snippets, fonts or images will invalidate the experiment, since users might click based on presentation rather than relevance.                                                                | Render both rankers/recommenders through the same UI template. Users must not be able to tell which system served a given result.                |
| **Attractiveness**                              | If results expose their source such as a specific brand, author or publisher, users might prefer one source over another regardless of how well the ranker actually performed.                                                                                          | Strip or normalize source indicators so both rankings are judged on relevance alone, not on where the result came from.                          |
| **System performance (latency / availability)** | A candidate system can lose an experiment unfairly due to technical issues rather than genuine ranking quality. If a system does not respond in a timely manner, STELLA falls back to the baseline system, meaning the candidate never actually competed for that slot. | Monitor error rates and response times closely. A broken or slow candidate can look like it's losing fairly when it was never given a fair shot. |
| **Result padding**                              | If a system can't provide enough results, the ranking list is padded with baseline results. This keeps the user experience intact, but it also dilutes the comparison since padded slots aren't a genuine test of the experiment.                                        | Check padding rates in your logs. High padding rates mean your experimental system isn't really in the fight for a meaningful share of the list.           |


---



## 3. Plan experiment duration

With the hypothesis in place, the duration of the experiment can be planned. 

**What you need:** a target minimum detectable effect (MDE), significance level, power, tie-rate estimate and a fixed stopping point before launch.

The idea here is to plug in a few honest estimates about your traffic and how big a change you expect and get back a number of clicks and days to run for. The calculator at the end of this section does that for you; the rest is just explaining what the inputs mean.

<p class="faq-question">How many clicks do I need?</p>

 You need enough **decisive** sessions — sessions where one system clearly got more clicks than the other. Ties don't count toward the sample size because when both systems are equally good, the session is inconclusive.

Before you start, decide on three things:


| Parameter                           | Typical value      | What it means in practice                                                                                                                                                                          |
| ----------------------------------- | ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **α (significance)**                | 0.05               | How often you're willing to call a fluke a real win. Lower (e.g. 0.01) is more conservative but needs more data.                                                                                   |
| **Power (1 − β)**                   | 0.80               | How confident you want to be that you will catch a real improvement if one exists. Higher (e.g. 0.90) needs more data.                                                                             |
| **MDE (minimum detectable effect)** | 0.51–0.55 win rate | Smallest lift you actually care about. 0.50 = tie. 0.51 = 51 wins per 100 decisive sessions. A radical change might justify 55%; a small tweak might target 51%. Smaller MDE needs a much larger sample. |


<p class="faq-question">Why does the sample size grow so fast for small changes?</p>

Intuitively, a big obvious improvement (say, one system wins 55 times out of 100) is easy to spot with a small sample, it stands out from noise quickly. A subtle improvement (51 out of 100) looks almost identical to a coin flip in a small sample, so you need to collect a lot more sessions before the pattern is reliably distinguishable from chance. This is why a 55% MDE experiment finishes far sooner than a 51% MDE experiment.

The math behind this is a standard two-proportion statistical test. For day-to-day planning, the calculator below does this calculation for you.

<p class="faq-question">How do we account for a large proportion of ties in our sample size?</p>

The sample size above only counts decisive sessions, but in practice many queries end in ties, especially when the experimental system introduces only a small change, since similar rankings tend to produce similar clicks. That means you need to collect more total clicks than the decisive count alone.

Estimate a **tie rate**: how often you expect both systems to get an equal number of clicks. The similarity of both rankings is a good starting point for a guess, and it's safer to overestimate than underestimate. Similar rankers often tie 30–50% of the time, if you are unsure, start there.

<p class="faq-question">How do I convert clicks to calendar days?</p>

Once you know the total clicks you need, divide by how many clicks your platform actually produces per day (your daily queries × your click-through rate). That gives you a rough minimum number of days to run the experiment. Always add some buffer on top for weekends, traffic spikes and the uncertainty in your tie-rate guess.

### Ready-to-use calculator

Fill in your own `alpha`, `power`, `mde`, `tie_rate`, `daily_queries` and `ctr` and run this to get a sample-size and duration estimate:

```python
from scipy.stats import norm
 
# --- Inputs: adjust these for your experiment ---
alpha = 0.05           # significance level
power = 0.80           # statistical power (1 - beta)
mde = 0.51             # minimum detectable effect, e.g. 0.51 for a small lift
tie_rate = 0.40        # estimated fraction of sessions that end in a tie
daily_queries = 5000   # average daily search queries on your platform
ctr = 0.10             # average click-through rate per query
 
# --- Calculation ---
p0 = 0.5
p1 = mde
 
z_alpha = norm.ppf(1 - alpha / 2)   # two-sided critical value for alpha
z_beta = norm.ppf(power)            # critical value for power
 
numerator = (z_alpha * (p0 * (1 - p0)) ** 0.5 + z_beta * (p1 * (1 - p1)) ** 0.5) ** 2
denominator = (p1 - p0) ** 2
n_decisive = numerator / denominator
 
n_total_clicks = n_decisive / (1 - tie_rate)
days_needed = n_total_clicks / (daily_queries * ctr)
 
print(f"Decisive sessions needed:   {n_decisive:,.0f}")
print(f"Total clicks needed:        {n_total_clicks:,.0f}")
print(f"Estimated experiment days:  {days_needed:,.1f}")
```

Example output with `alpha=0.05`, `power=0.80`, `mde=0.51`, `tie_rate=0.40`, `daily_queries=5000`, `ctr=0.10`:

```
Decisive sessions needed:   ~19,620
Total clicks needed:        ~32,700
Estimated experiment days:  ~65.4
```

Tighten `mde` toward 0.50 or lower `tie_rate` estimates conservatively since both increase the required sample size, so treat the output as a floor, not a target.

---



## 4. Execute and measure

Once the experiment is designed, the next phase is running it, collecting data and reading the results correctly. This section covers what to look at while the experiment runs and how to know when a result is trustworthy.

**What you need:** the experiment running to your pre-planned sample size, with health checks only and no early stopping based on p-values.

<p class="faq-question">What metrics matter for interleaving?</p>

Interleaving moves away from absolute metrics like standard CTR and focuses on a **relative** comparison between the two systems. When a user interacts with results, STELLA tracks which system "drafted" the clicked items:


| Outcome  | Definition                                                          |
| -------- | ------------------------------------------------------------------- |
| **Win**  | Experimental system received more clicks than baseline in a session |
| **Loss** | Baseline received more clicks                                       |
| **Tie**  | Equal clicks on both (excluded from win-rate calculation)           |



The STELLA Server dashboard shows these impressions, clicks split by `BASE`/`EXP`, and overall CTR for monitoring, but the ultimate decision metric is: 

**win rate** = `wins / (wins + losses)`

<p class="faq-question">Where is this calculated?</p>

Within the STELLA Server's codebase, `stella-server/web/app/dashboard.py` aggregates feedback per session and computes wins/losses/ties from click `type` fields (`BASE` or `EXP`).

<p class="faq-question">How do I know if the result is real?</p>

Your experiment might show a 52% win rate, slightly outperforming baseline.  But is that a genuine, repeatable improvement or just noise?

The more decisive sessions you collect, the more confidently a win rate above 50% reflects a real preference rather than luck. After you have collected your pre-planned sample, plug your win and loss counts into the calculator below. It tells you two things:

**Is this likely to be a fluke?**

If the chance of seeing a result this strong purely by luck is low (below 5%), the result is considered statistically significant.

**What's the plausible range for the true win rate?**

Rather than trusting the single number (like "52%") exactly, you get a range it probably falls within. If that whole range is above 50%, that's a strong sign the experimental system is a genuine winner. STELLA's dashboard shows the win/loss/tie breakdown as it accumulates, but running the numbers yourself once the experiment is complete gives you the clearest answer.

### Ready-to-use significance calculator

Fill in your actual `wins` and `losses` (ties don't count) and run this to get a straight answer (there is no need to change anything below the inputs)

```python
from scipy.stats import binomtest

# --- Inputs: your actual results from the completed experiment ---
wins = 2600     # sessions where the experimental system got more clicks
losses = 2400   # sessions where the baseline got more clicks

# --- Calculation ---
decisive = wins + losses
win_rate = wins / decisive

result = binomtest(wins, decisive, p=0.5, alternative='greater')
p_value = result.pvalue
ci_low, ci_high = result.proportion_ci(confidence_level=0.95)

print(f"Win rate:              {win_rate:.1%}")
print(f"p-value:               {p_value:.4f}")
print(f"95% confidence range:  [{ci_low:.1%}, {ci_high:.1%}]")

if p_value < 0.05 and ci_low > 0.5:
    print("\n→ Statistically significant: the experimental system looks like a real winner.")
else:
    print("\n→ Not statistically significant: can't rule out this result is due to chance.")
```

Example output with `wins=2600`, `losses=2400`:

```
Win rate: 52.0%
p-value: 0.0024
95% confidence range: [50.8%, 100%]
Statistically significant, but the lower bound is close to 50% — a modest win.
```

<p class="faq-question">Monitoring the dashboard during the run</p>

 The STELLA server dashboard gives an up-to-date view of results. Use it to monitor whether the experiment is running successfully, not to draw premature conclusions.

<p class="faq-question">What is peeking and why is it bad?</p>

 It is tempting to stop an experiment the moment it looks like the candidate is winning. This practice is known as **peeking** and it dramatically increases your risk of declaring a false win. Even an evenly matched experiment will naturally drift back and forth early on and if you happen to check at a moment it looks good and stop there, you'll ship a result that isn't real.

**Do:** Stick strictly to the sample size you planned before launch (the click count from your sample-size planning). Run until you hit it. Then evaluate.

**Don't:** Refresh the dashboard every hour and call it as soon as the chart looks favorable.

<p class="faq-question">When is early stopping OK?</p>

If the experimental system is performing much weaker than expected: high error rate, severe latency, user complaints, you may safely cancel early to protect the user experience. That's an operational call, not a statistical one. Document why you stopped.

---


## 5. Interpret

**What you need:** a decision based on win rate, statistical significance and practical impact.

<p class="faq-question">The experimental system won statistically. Should I ship it?</p>

A statistically significant win isn't automatically a win worth shipping. Ask:

- Is the win rate large enough to justify the operational cost (infra, latency, maintenance)?
- Did wins hold across query types or only on a narrow slice?
- Are there regressions in latency, empty-result rate or diversity?

A 50.8% win rate can be statistically real with enough traffic, but still barely worth a complex migration.

<p class="faq-question">The experiment tied. Now what?</p>

Either the change genuinely doesn't matter for user behavior or the lift you were targeting was too small to detect with the traffic you had. Some options are to run longer with a bigger expected lift in mind or try a bolder change.

<p class="faq-question">The experimental system lost. What do I check first?</p>

1. Was it actually serving results? (padding / fallback rate)
2. Were there presentation differences between baseline and experimental slots?
3. Was it a latency issue as slow results get fewer clicks regardless of relevance?
4. Is the hypothesis wrong or is the implementation buggy?

Interleaved testing is one of the most sensitive and efficient tools for evaluating ranking systems. When planned and executed with care, it lets you move with speed and confidence. The core principles are simple:

- **Plan rigorously**: Define a clear hypothesis and estimate your sample size before you begin. A week of planning can save a month of wasted traffic.
- **Execute with discipline**: Stick to your pre-defined stopping point. Avoid peeking at results early; it undermines the reliability of your test.

---

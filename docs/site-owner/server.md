### Feedback

GET details of all feedbacks (see also `util/GET_feedbacks.py`):  
`/feedbacks`

GET details of feedback with `id` (see also `util/GET_feedback.py`):  
`/feedbacks/<int:id>`

POST new feedback for session with `id` (see also `util/POST_feedback.py`):  
`/sessions/<int:id>/feedbacks`

The payload should be provided as follows:  

```json
{
    "start": "2019-11-04 00:06:23",
    "end": "2019-11-04 00:10:38",
    "interleave": "True",
    "clicks": [
               {"1": {"doc_id": "doc1", "clicked": "False", "date": "None", "system": "EXP"}},
               {"2": {"doc_id": "doc11", "clicked": "True", "date": "2019-11-04 00:08:15", "system": "BASE"}},
               {"3": {"doc_id": "doc2", "clicked": "False", "date": "None", "system": "EXP"}},
               {"4": {"doc_id": "doc12", "clicked": "True", "date": "2019-11-04 00:06:23", "system": "BASE"}},
               {"5": {"doc_id": "doc3", "clicked": "False", "date": "None", "system": "EXP"}},
               {"6": {"doc_id": "doc13", "clicked": "False", "date": "None", "system": "BASE"}},
               {"7": {"doc_id": "doc4", "clicked": "False", "date": "None", "system": "EXP"}},
               {"8": {"doc_id": "doc14", "clicked": "False", "date": "None", "system": "BASE"}},
               {"9": {"doc_id": "doc5", "clicked": "False", "date": "None", "system": "EXP"}},
               {"10": {"doc_id": "doc15", "clicked": "False", "date": "None", "system": "BASE"}}         
              ]
}
```

PUT details for feedback with `id` (see also `util/PUT_feedback.py`):  
`/feedbacks/<int:id>'`

The payload should be provided as follows:  

```json
{
    "start": "2019-11-04 00:06:23",
    "end": "2019-11-04 00:10:38",
    "interleave": "True",
    "clicks": [
               {"1": {"doc_id": "doc1", "clicked": "False", "date": "None", "system": "EXP"}},
               {"2": {"doc_id": "doc11", "clicked": "True", "date": "2019-11-04 00:08:15", "system": "BASE"}},
               {"3": {"doc_id": "doc2", "clicked": "False", "date": "None", "system": "EXP"}},
               {"4": {"doc_id": "doc12", "clicked": "True", "date": "2019-11-04 00:06:23", "system": "BASE"}},
               {"5": {"doc_id": "doc3", "clicked": "False", "date": "None", "system": "EXP"}},
               {"6": {"doc_id": "doc13", "clicked": "False", "date": "None", "system": "BASE"}},
               {"7": {"doc_id": "doc4", "clicked": "False", "date": "None", "system": "EXP"}},
               {"8": {"doc_id": "doc14", "clicked": "False", "date": "None", "system": "BASE"}},
               {"9": {"doc_id": "doc5", "clicked": "False", "date": "None", "system": "EXP"}},
               {"10": {"doc_id": "doc15", "clicked": "False", "date": "None", "system": "BASE"}}         
              ]
}
```

### Participant

GET all systems of participant with `id` (see also `util/GET_systems_of_participant.py`):  
`/participants/<int:id>/systems`

GET all sessions of participant with `id` (see also `util/GET_sessions_of_participant.py`):  
`/participants/<int:id>/sessions`

### Ranking

GET details of ranking with `id` (see also `util/GET_ranking.py`):  
`/rankings/<int:id>`

GET a list of all ranking `id`s (see also `util/GET_rankings.py`):  
`/rankings`

POST ranking for feedback with `id` (see also `util/POST_rankings.py`):  
`/feedbacks/<int:id>/rankings`

The payload should be provided as follows:  

```json
{
    "q": "this is the query text",
    "q_date": "2019-11-04 00:04:00",
    "q_time": 325,
    "num_found": 100,
    "page": 1,
    "rpp": 10,
    "items": [
              {"1": "doc1", "2": "doc2", "3": "doc3", "4": "doc4", "5": "doc5", 
               "6": "doc6", "7": "doc7", "8": "doc8", "9": "doc9", "10": "doc10"}
             ]
}
```

PUT ranking with `id` (see also `util/PUT_ranking.py`):  
`/rankings/<int:id>`

The payload should be provided as follows:  

```json
{
    "q": "this is the query text",
    "q_date": "2019-11-04 00:04:00",
    "q_time": 325,
    "num_found": 100,
    "page": 1,
    "rpp": 10,
    "items": [
              {"1": "doc1", "2": "doc2", "3": "doc3", "4": "doc4", "5": "doc5", 
               "6": "doc6", "7": "doc7", "8": "doc8", "9": "doc9", "10": "doc10"}
             ]
}
```

### Recommendation

GET details of recommendation with `id` (see also `util/GET_ranking.py` that works analogously):  
`/recommendations/<int:id>`

GET a list of all recommendation `id`s (see also `util/GET_rankings.py` that works analogously):  
`/recommendations`

POST recommendation for feedback with `id` (see also `util/POST_rankings.py` that works analogously):  
`/feedbacks/<int:id>/recommendations`

The payload should be provided as follows:  

```json
{
    "q": "docid",
    "q_date": "2019-11-04 00:04:00",
    "q_time": 325,
    "num_found": 100,
    "page": 1,
    "rpp": 10,
    "items": [
              {"1": "doc1", "2": "doc2", "3": "doc3", "4": "doc4", "5": "doc5", 
               "6": "doc6", "7": "doc7", "8": "doc8", "9": "doc9", "10": "doc10"}
             ]
}
```

PUT recommendation with `id` (see also `util/PUT_ranking.py` that works analogously):  
`/recommendations/<int:id>`

The payload should be provided as follows:  

```json
{
    "q": "docid",
    "q_date": "2019-11-04 00:04:00",
    "q_time": 325,
    "num_found": 100,
    "page": 1,
    "rpp": 10,
    "items": [
              {"1": "doc1", "2": "doc2", "3": "doc3", "4": "doc4", "5": "doc5", 
               "6": "doc6", "7": "doc7", "8": "doc8", "9": "doc9", "10": "doc10"}
             ]
}
```

### Session

GET session with `id` (see also `util/GET_session.py`):  
`/sessions/<int:id>`

GET feedback from session with `id` (see also `util/GET_feedbacks_of_session.py`):  
`/sessions/<int:id>/feedbacks` 

GET systems used in session with `id`:  
`/sessions/<int:id>/systems`

### Site

GET site details, e.g. `id`, with the help of the `name` (see also `util/GET_systems_at_site.py`):  
`/sites/<string:name>`

GET sessions at site with `id` (see also `util/GET_session_at_site.py`):  
`/sites/<int:id>/sessions`

GET systems deployed at site with `id` (see also `util/GET_systems_at_site.py`):  
`/sites/<int:id>/systems`

POST new session at site with `id` (see also `util/POST_sessions.py`):  
`/sites/<int:id>/sessions`

The payload should be provided as follows:  

```json
{
    "site_user": "123.123.123.123",
    "start": "2020-02-20 20:02:20",
    "end": "2020-02-20 20:02:20",
    "system_ranking": "rank_exp_a",
    "system_recommendation": "rec_exp_a"
}
```
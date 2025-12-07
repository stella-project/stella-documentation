The **STELLA micro-template** provides experimenters with a standardized way to integrate their ranking and recommendation systems into the STELLA infrastructure.

### Dockerized Experimental Systems 

STELLA **supports experimental systems that are integrated as Dockerized microservices**.  
Each experimental system runs as an independent container and exposes a REST interface that is consumed by the STELLA App at runtime.

Using the microservice-based approach:

- each system is deployed as its own Docker container
- systems are integrated directly into the STELLA App via Docker Compose
- ranking and recommendation results are generated dynamically on request
- systems can access the full user interaction context

This approach enables:

- real-time ranking and recommendation
- interactive experimentation with live user queries
- richer and more flexible experimental workflows
- experimentation beyond fixed or pre-defined queries and items

### Why the Microservice Template

The STELLA micro-template provides a ready-to-use scaffold that:

- defines the required API contract
- standardizes request and response formats
- simplifies deployment and integration
- ensures compatibility with the STELLA App and Server

Experimenters are expected to adapt the micro-template to wrap their ranking or recommendation logic and deploy it as a Docker service within the STELLA App environment.

This microservice-based architecture is the **only supported mechanism** for integrating experimental systems into the STELLA infrastructure.



## Ranking


REST endpoint:
**GET** `container_name/ranking?query=<string:qstr>&page=<int:pnum>&rpp=<int:rppnum>`

Explanation:

- **container_name**: name of the container that contains either the baseline or one of the experimental systems
- **query**: the query string
- **page**: the number of the start page
- **rpp**: the number of results per page


Output:

```
{'itemlist': ['M26721328',
              'M26923455',
              'M25600519',
              'M27515393',
              'M27572122',
              'M27357208',
              'M27309042',
              'M27237391',
              'M27279275',
              'M26813237',
              'M27049797',
              'M27531820',
              'M27338346',
              'M27999240',
              'M26613600',
              'M27356552',
              'M27783754',
              'M27278100',
              'M27531823',
              'M26860287'],
 'num_found': 20,
 'page': 0,
 'query': 'vaccine',
 'rpp': 20}
```

Explanation:

- **itemlist**: a list containing the document identifiers
- **num_found**: the total number of documents found for the given `query`
- **page**: the number of the start page
- **query**: the query string
- **rpp**: the number of results per page
 
## Recommendation

REST endpoint:
**GET** `container_name/recommendation/datasets?itemid=<string:itemidstr>&page=<int:pnum>&rpp=<int:rppnum>`  
**GET** `container_name/recommendation/publications?itemid=<string:itemidstr>&page=<int:pnum>&rpp=<int:rppnum>`

Explanation:

- **container_name**: name of the container that contains either the baseline or one of the experimental systems
- **datasets/publications**: specify if datasets of publications should be recommended
- **itemid**: the target item of the recommendations
- **page**: the number of the start page
- **rpp**: the number of results per page

Output:

```
{'itemid': 'M26923455',
 'itemlist': ['M27852061',
              'M26673108',
              'M27894536',
              'M27293030',
              'M27133708',
              'M26841192',
              'M27144310',
              'M27353833',
              'M27287107',
              'M27658597'],
 'num_found': 10,
 'page': 0,
 'rpp': 10}
```

Explanation:

- **itemid**: the target item of the recommendations
- **itemlist**: a list containing the document identifiers
- **num_found**: the total number of documents found for the given `query`
- **page**: the number of the start page
- **rpp**: the number of results per page
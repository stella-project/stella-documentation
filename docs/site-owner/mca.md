This document lists and explains all available STELLA API endpoints, their parameters and example responses.

Once the STELLA App is running, you can also view and test these endpoints interactively by visiting http://localhost:8080/docs
in your browser.

## Ranking

### REST endpoint:

**GET** ```/stella/api/v1/ranking?query=<string:query>&page=<int:page>&rpp=<int:rpp>&sid=<int:sid>&container=<string:container>```  

#### Explanation:

- **query**: the query string
- **page**: the number of the start page (optional)
- **rpp**: the number of results per page (optional)
- **container**: name of the container that contains either the baseline or one of the experimental systems (optional)
- **sid**: the session identifier (optional)

### Output (interleaved ranking):
```
{'body': {'1': {'docid': 'M27622217', 'type': 'BASE'},
          '2': {'docid': 'M27251231', 'type': 'EXP'},
          '3': {'docid': 'M27692969', 'type': 'BASE'},
          '4': {'docid': 'M26350569', 'type': 'EXP'},
          '5': {'docid': 'M26715777', 'type': 'EXP'},
          '6': {'docid': 'M26650940', 'type': 'BASE'},
          '7': {'docid': 'M27098271', 'type': 'EXP'},
          '8': {'docid': 'M28381438', 'type': 'BASE'},
          '9': {'docid': 'M27763523', 'type': 'EXP'},
          '10': {'docid': 'M27157745', 'type': 'BASE'},
          '11': {'docid': 'M28066266', 'type': 'EXP'},
          '12': {'docid': 'M26874427', 'type': 'BASE'},
          '13': {'docid': 'M27133457', 'type': 'EXP'},
          '14': {'docid': 'M26791355', 'type': 'BASE'},
          '15': {'docid': 'M27157753', 'type': 'BASE'},
          '16': {'docid': 'M27167258', 'type': 'EXP'},
          '17': {'docid': 'M27524068', 'type': 'EXP'},
          '18': {'docid': 'M26824628', 'type': 'BASE'},
          '19': {'docid': 'M26967532', 'type': 'EXP'}},
 'header': {'container': {'base': 'rank_elastic_base', 'exp': 'rank_elastic'},
            'page': 0,
            'q': 'vaccine',
            'rid': 3,
            'rpp': 20,
            'hits': 12312,
            'sid': 1}}
```

#### Explanation:

- **header**: header containing meta information about the returned result
- **body**: body with rank positions, identifiers, and type of the corresponding system
- **docid**: the document identifier
- **type**: type of system can be either `BASE` or `EXP`
- **container**: dictionary with names of the experimental system and optional baseline system
- **page**: the number of the start page
- **q**: the query string
- **rid**: the ranking identifier
- **rpp**: the number of results per page
- **hits**: the number of total hits
- **sid**: the session identifier

### Output (non-interleaved ranking):

```
{'body': {'1': {'docid': 'M27622217', 'type': 'EXP'},
          '2': {'docid': 'M27251231', 'type': 'EXP'},
          '3': {'docid': 'M27692969', 'type': 'EXP'},
          '4': {'docid': 'M26350569', 'type': 'EXP'},
          '5': {'docid': 'M26715777', 'type': 'EXP'},
          '6': {'docid': 'M26650940', 'type': 'EXP'},
          '7': {'docid': 'M27098271', 'type': 'EXP'},
          '8': {'docid': 'M28381438', 'type': 'EXP'},
          '9': {'docid': 'M27763523', 'type': 'EXP'},
          '10': {'docid': 'M27157745', 'type': 'EXP'},
          '11': {'docid': 'M28066266', 'type': 'EXP'},
          '12': {'docid': 'M26874427', 'type': 'EXP'},
          '13': {'docid': 'M27133457', 'type': 'EXP'},
          '14': {'docid': 'M26791355', 'type': 'EXP'},
          '15': {'docid': 'M27157753', 'type': 'EXP'},
          '16': {'docid': 'M27167258', 'type': 'EXP'},
          '17': {'docid': 'M27524068', 'type': 'EXP'},
          '18': {'docid': 'M26824628', 'type': 'EXP'},
          '19': {'docid': 'M26967532', 'type': 'EXP'}},
 'header': {'container': {'exp': 'rank_elastic'},
            'page': 0,
            'q': 'vaccine',
            'rid': 1,
            'rpp': 20,
            'hits': 12312,
            'sid': 1}}
```
#### Explanation:

See above.



### Feedback
---
### REST endpoint:

**POST** ```/stella/api/v1/ranking/rid=<int:rid>/feedback```

#### Explanation:

- **sid**: the session identifier
- **rid**: the ranking identifier

### Payload:
```
{'clicks': {'1': {'clicked': False,
                  'date': None,
                  'docid': 'M26923455',
                  'type': 'EXP'},
            '2': {'clicked': False,
                  'date': None,
                  'docid': 'M25600519',
                  'type': 'EXP'},
            '3': {'clicked': True,
                  'date': '2020-07-29 16:06:51',
                  'docid': 'M27515393',
                  'type': 'EXP'},
            '4': {'clicked': False,
                  'date': None,
                  'docid': 'M27572122',
                  'type': 'EXP'},
            '5': {'clicked': False,
                  'date': None,
                  'docid': 'M27357208',
                  'type': 'EXP'},
            '6': {'clicked': True,
                  'date': '2020-07-29 16:06:51',
                  'docid': 'M27309042',
                  'type': 'EXP'},
            '7': {'clicked': False,
                  'date': None,
                  'docid': 'M27237391',
                  'type': 'EXP'},
            '8': {'clicked': False,
                  'date': None,
                  'docid': 'M27279275',
                  'type': 'EXP'},
            '9': {'clicked': False,
                  'date': None,
                  'docid': 'M26813237',
                  'type': 'EXP'}
            '10': {'clicked': False,
                   'date': None,
                   'docid': 'M27049797',
                   'type': 'EXP'},
            '11': {'clicked': False,
                   'date': None,
                   'docid': 'M27531820',
                   'type': 'EXP'},
            '12': {'clicked': False,
                   'date': None,
                   'docid': 'M27338346',
                   'type': 'EXP'},
            '13': {'clicked': False,
                   'date': None,
                   'docid': 'M27999240',
                   'type': 'EXP'},
            '14': {'clicked': False,
                   'date': None,
                   'docid': 'M26613600',
                   'type': 'EXP'},
            '15': {'clicked': False,
                   'date': None,
                   'docid': 'M27356552',
                   'type': 'EXP'},
            '16': {'clicked': False,
                   'date': None,
                   'docid': 'M27783754',
                   'type': 'EXP'},
            '17': {'clicked': False,
                   'date': None,
                   'docid': 'M27278100',
                   'type': 'EXP'},
            '18': {'clicked': False,
                   'date': None,
                   'docid': 'M27531823',
                   'type': 'EXP'},
            '19': {'clicked': False,
                   'date': None,
                   'docid': 'M26860287',
                   'type': 'EXP'}},
 'end': '2020-07-29 16:12:53',
 'interleave': True,
 'start': '2020-07-29 16:06:51'}
```

#### Explanation:

- **start**: time of session start, has to be provided as datetime-formatted string like 'YYYY-MM-DD HH:MM:SS'
- **interleave**: boolean value indicating if the result list has been interleaved
- **end**: time of session end, has to be provided as datetime-formatted string like 'YYYY-MM-DD HH:MM:SS'
- **clicks**: dicitionary containing document identifiers and their corresponding clicks
- **clicked**: boolean values indicating whether document has been clicked or not
- **date**: time when click happend, has to be provided as datetime-formatted string like 'YYYY-MM-DD HH:MM:SS'
- **docid**: the document identifier
- **system**: string value indicating if the corresponding system is baseline (`BASE`) or experimental (`EXP`)

## Recommendations

### REST endpoint:

#### Datasets

**GET** ```/stella/api/v1/recommendation/datasets?itemid=<string:itemid>&page=<int:page>&rpp=<int:rpp>&sid=<int:sid>&container=<string:container>```  

#### Explanation:

- **itemid**: the target item of the recommendations
- **page**: the number of the start page (optional)
- **rpp**: the number of results per page (optional)
- **sid**: the session identifier (optional)
- **container**: name of the container that contains either the baseline or one of the experimental systems (optional)

#### Publications

**GET** ```/stella/api/v1/recommendation/publications?itemid=<string:itemid>&page=<int:page>&rpp=<int:rpp>&sid=<int:sid>&container=<string:container>```  

#### Explanation:

See above.

### Output (interleaved recommendation):

```
{'body': {'1': {'docid': 'M27388739', 'type': 'BASE'},
          '2': {'docid': 'M27338344', 'type': 'EXP'},
          '3': {'docid': 'M26207529', 'type': 'EXP'},
          '4': {'docid': 'M27216378', 'type': 'BASE'},
          '5': {'docid': 'M26938486', 'type': 'BASE'},
          '6': {'docid': 'M26612070', 'type': 'EXP'},
          '7': {'docid': 'M27641359', 'type': 'BASE'},
          '8': {'docid': 'M27567522', 'type': 'EXP'},
          '9': {'docid': 'M27897418', 'type': 'BASE'}},
 'header': {'container': {'base': 'recom_tfidf_base', 'exp': 'recom_tfidf'},
            'itemid': 'M26923455',
            'page': 0,
            'rid': 4,
            'rpp': 10,
            'hits': 24,
            'sid': 2,
            'type': 'PUB'}}
```

#### Explanation:

- **header**: header containing meta information about the returned result
- **body**: body with positions, identifiers, and type of the corresponding system
- **docid**: the document identifier
- **type**: type of system can be either `BASE` or `EXP`
- **container**: dictionary with names of the experimental system and optional baseline system
- **itemid**: the target item of the recommendations
- **page**: the number of the start page
- **rid**: the recommendation identifier
- **rpp**: the number of results per page
- **hits**: the number of total hits
- **sid**: the session identifier
- **type**: type of system can be either `BASE` or `EXP`

### Output (non-interleaved recommendation):

```
{'body': {'1': {'docid': 'M27038470', 'type': 'EXP'},
          '2': {'docid': 'M27342969', 'type': 'EXP'},
          '3': {'docid': 'M26774951', 'type': 'EXP'},
          '4': {'docid': 'M27912945', 'type': 'EXP'},
          '5': {'docid': 'M26797943', 'type': 'EXP'},
          '6': {'docid': 'M25359468', 'type': 'EXP'},
          '7': {'docid': 'M26969740', 'type': 'EXP'},
          '8': {'docid': 'M27613427', 'type': 'EXP'},
          '9': {'docid': 'M27976545', 'type': 'EXP'}},
 'header': {'container': {'exp': 'recom_tfidf'},
            'itemid': 'M26923455',
            'page': 0,
            'rid': 2,
            'rpp': 10,
            'hits': 11,
            'sid': 2,
            'type': 'PUB'}}
```

#### Explanation:

See above.

### Feedback
---
### REST endpoint:
**POST** ```/stella/api/v1/recommendation/rid=rid=<int:rid>/feedback```

#### Explanation:

- **rid**: the recommendation identifier

```
{'clicks': {'1': {'clicked': False,
                  'date': None,
                  'docid': 'M27160449',
                  'type': 'EXP'},
            '2': {'clicked': False,
                  'date': None,
                  'docid': 'M27888935',
                  'type': 'BASE'},
            '3': {'clicked': False,
                  'date': None,
                  'docid': 'M27088628',
                  'type': 'EXP'},
            '4': {'clicked': False,
                  'date': None,
                  'docid': 'M27064543',
                  'type': 'BASE'},
            '5': {'clicked': False,
                  'date': None,
                  'docid': 'M27717979',
                  'type': 'EXP'},
            '6': {'clicked': True,
                  'date': '2020-07-29 17:11:18',
                  'docid': 'M27077760',
                  'type': 'BASE'},
            '7': {'clicked': False,
                  'date': None,
                  'docid': 'M27638054',
                  'type': 'BASE'},
            '8': {'clicked': False,
                  'date': None,
                  'docid': 'M26360828',
                  'type': 'EXP'},
            '9': {'clicked': False,
                  'date': None,
                  'docid': 'M27554937',
                  'type': 'BASE'}},
 'end': '2020-07-29 17:59:24',
 'interleave': True,
 'start': '2020-07-29 17:11:18'}
```
#### Explanation:

- **start**: time of session start, has to be provided as datetime-formatted string like 'YYYY-MM-DD HH:MM:SS'
- **interleave**: boolean value indicating if the result list has been interleaved
- **end**: time of session end, has to be provided as datetime-formatted string like 'YYYY-MM-DD HH:MM:SS'
- **clicks**: dicitionary containing document identifiers and their corresponding clicks
- **clicked**: boolean values indicating whether document has been clicked or not
- **date**: time when click happend, has to be provided as datetime-formatted string like 'YYYY-MM-DD HH:MM:SS'
- **docid**: the document identifier
- **system**: string value indicating if the corresponding system is baseline (`BASE`) or experimental (`EXP`)

## Indexing 

GET ```/stella/api/v1/index/bulk```

#### Explanation:

Start indexing all containers in parallel.

GET ```/stella/api/v1/index/<string:container_name>```

#### Explanation:

- **container_name**: Name of the specific container to be indexed.

## Exit sessions

GET ```/stella/api/v1/sessions/<int:sid>/exit```

#### Explanation:

- **sid**: Identifier of the session to be exited.

## Proxy


### REST Endpoint
The STELLA Proxy Endpoint allows arbitrary query parameters to be forwarded to the STELLA App and returns the response back to the Portal/Site. This endpoint is useful when parameters go beyond the standard ranking/recommendation API.

All parameters intended for STELLA must be prefixed with `stella-`.

REST endpoint:

GET `/proxy/<string:url>?stella-container=<string:container>&stella-sid=<string:sid>&stella-system-type=<string:system-type>&stella-page=<int:page>&<additional query params>`

### Explanation:

+ url: the URL path (including subpaths) to forward the request to (required)
+ stella-container: name of the container/system to which the request should be forwarded (optional; if omitted, the least-served system is used)
+ stella-sid: session identifier; if invalid or missing, a new session is created by STELLA (optional)
+ stella-system-type: type of system, either ranking or retrieval (optional, default = ranking)
+ stella-page: page number for cached responses (optional)
+ additional query params: any other key-value pairs forwarded unchanged to the underlying system (e.g., query, page, rpp, etc.)


### The `url` Parameter

Specifies the target endpoint path (including subpaths) on the backend system that STELLA should forward the request to.
This allows portals to access backend functionalities through STELLA’s unified proxy layer, without needing to know internal service addresses.

### How It Works

The url value is appended to the base URL of the systems defined in STELLA’s container (base and experimental) configuration. STELLA automatically constructs the complete backend request URL using this base and the provided url path. The proxy then forwards the portal’s request (and query parameters) to the correct backend service, retrieves its response and augments it with _stella metadata.


### Example Response Structure:

The response from the STELLA Proxy endpoint contains two main sections:

1. Root-level body:
This is the original response from the portal/site. Its key name can vary depending on the portal implementation, e.g., results, items, data, etc. This contains the actual content or items returned by the site.

2. `_stella`:
This is metadata injected by the STELLA proxy. It tracks session, container, and interleaving information used by STELLA.

Fields include:

+ sid: Session identifier used or created by STELLA
+ rid: Ranking/recommendation identifier
+ q: Original query string forwarded to STELLA
+ page: Page number of the results
+ rpp: Results per page
+ container: Names of containers used (exp and optional base)
+ body: Standard STELLA body response with details about the returned system type and interleaving


```
{
  "results": [
    {"id": "M27622217", "title": "abcd", "url": "https://example.com/doc/M27622217"},
    {"id": "M26350569", "title": "efgh", "url": "https://example.com/doc/M26350569"},
    {"id": "M27167258", "title": "ijkl", "url": "https://example.com/doc/M27167258"}
  ],
  "_stella": {
    "sid": "abc123sessionid",
    "rid": 5,
    "query": "artificial intelligence",
    "page": 1,
    "rpp": 10,
    "container": {"base": "rank_elastic_base", "exp": "rank_elastic"},
    "system_type": "ranking"
    "body": {
      "1": {
        "docid": "M27622217",
        "type": "BASE"
      },
      "2": {
        "docid": "M26350569",
        "type": "EXP"
      },
      "3": {
        "docid": "M27167258",
        "type": "BASE"
      },
  }
}
}
```

### Configuring STELLA APP for Proxy endpoint

To enable the Proxy Endpoint, the STELLA App must be correctly configured in the `docker-compose.yml` file.
This configuration informs STELLA about how to locate and interpret result items in the portal’s response structure.

Update the `SYSTEMS_CONFIG` variable under the `app` service in your `docker-compose.yml` file as shown below:

```
# Systems
SYSTEMS_CONFIG: |
      {
      "rank_elastic_base": {"type": "ranker", "base": true, "docid": "db_identifier", "hits_path": "$.hits"},
      "rank_elastic": {"type": "ranker", "docid": "db_identifier", "hits_path": "$.hits"}
      }
```

Explanation:

+ docid:
The field name corresponding to the document identifier in the portal’s response.
This should match the key used in your portal’s data model (e.g., id, docid, or similar).

+ hits_path:
The JSON path indicating where the list of results (ranked or retrieved items) can be found in the response.

For example:

`$.hits` - if the results are under a hits key.

`$.models` — if results are under a models key.

`$.results` — if the portal returns results under a results field.

`$.data.items` — for nested structures.

Make sure these mappings reflect the actual output structure of your portal or site API so that STELLA can correctly parse and interleave the responses.

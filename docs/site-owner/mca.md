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

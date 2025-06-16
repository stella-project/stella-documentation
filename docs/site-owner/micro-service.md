## Ranking

### REST endpoint:
**GET** `container_name/ranking?query=<string:qstr>&page=<int:pnum>&rpp=<int:rppnum>`

#### Explanation:

- **container_name**: name of the container that contains either the baseline or one of the experimental systems
- **query**: the query string
- **page**: the number of the start page
- **rpp**: the number of results per page


### Output:

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

#### Explanation:

- **itemlist**: a list containing the document identifiers
- **num_found**: the total number of documents found for the given `query`
- **page**: the number of the start page
- **query**: the query string
- **rpp**: the number of results per page
 
## Recommendation

### REST endpoint:
**GET** `container_name/recommendation/datasets?itemid=<string:itemidstr>&page=<int:pnum>&rpp=<int:rppnum>`  
**GET** `container_name/recommendation/publications?itemid=<string:itemidstr>&page=<int:pnum>&rpp=<int:rppnum>`

#### Explanation:

- **container_name**: name of the container that contains either the baseline or one of the experimental systems
- **datasets/publications**: specify if datasets of publications should be recommended
- **itemid**: the target item of the recommendations
- **page**: the number of the start page
- **rpp**: the number of results per page

### Output:

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

#### Explanation:

- **itemid**: the target item of the recommendations
- **itemlist**: a list containing the document identifiers
- **num_found**: the total number of documents found for the given `query`
- **page**: the number of the start page
- **rpp**: the number of results per page
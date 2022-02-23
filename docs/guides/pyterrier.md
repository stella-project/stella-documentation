# Multi-container application based on Pyterrier

This guide provides setup instructions for a simple instance of the [`stella-app`](https://github.com/stella-project/stella-app) with micro-services based on [Pyterrier](https://github.com/terrier-org/pyterrier). The resulting multi-container application contains several Pyterrier-based micro-services with different ranking methods, and additionally, the dashboard service of the [`stella-server`](https://github.com/stella-project/stella-server). 

## Prerequisites

- [Python>=3.6](https://www.python.org/)
- [Docker](https://www.docker.com/)
- [docker-compose](https://docs.docker.com/compose/)

## Setup

### 1. Download the data and prepare the index

[Pyterrier](https://github.com/terrier-org/pyterrier) has a good support of the data catalog [`ir_datasets`](https://ir-datasets.com/index.html). In this guide, we will use [`ir_datasets`](https://ir-datasets.com/index.html) to prepare index files before starting the [`stella-app`](https://github.com/stella-project/stella-app). First, install the Python package:

```
pip install --upgrade ir_datasets
```

We make use of the [Cord19 dataset](https://www.semanticscholar.org/cord19) (more specifically, the metadata) that was also used as part of [TREC Covid](https://ir.nist.gov/trec-covid/). Execute the following code cell to write the index files into the specified subfolder:

```python
import pyterrier as pt
pt.init()
dataset = pt.get_dataset('irds:cord19')
# Index cord19
indexer = pt.IterDictIndexer('./indices/cord19')
index_ref = indexer.index(dataset.get_corpus_iter(), fields=['title', 'doi', 'date', 'abstract'])
```

### 2. Clone `stella-app` and copy the index files

Next, clone the repository of the [`stella-app`](https://github.com/stella-project/stella-app) from Github:

```
git clone https://github.com/stella-project/stella-app.git
```

And afterward, move the index files into the `index` directory of the [`stella-app`](https://github.com/stella-project/stella-app). All micro-services will share this index.

```
mv ./indices/cord19 stella-app/index/
```

### 3. Start `stella-app`

In order to run the multi-container application, make sure you have [Docker](https://www.docker.com/) and [docker-compose](https://docs.docker.com/compose/) installed.

```
docker-compose -f stella-app/yml/pyterrier.yml up -d
```

It will take some time to build the application. You can verify if every container is running via the CLI commands or with an administration interface like [Portainer](https://www.portainer.io/).
 
### 4. Send a request to the `stella-app`

Below you will find an example request of how to retrieve a ranking for the query `coronavirus origin`:

```
curl localhost:8080/stella/api/v1/ranking?query=coronavirus%20origin&rpp=10
```

In response, you receive a JSON-formatted output like the following:

```JSON
{
  "body": {
    "1": {
      "docid": "pl48ev5o",
      "type": "EXP"
    },
    "2": {
      "docid": "75773gwg",
      "type": "BASE"
    },
    "3": {
      "docid": "kn2z7lho",
      "type": "BASE"
    },
    "4": {
      "docid": "xwi9pdd2",
      "type": "EXP"
    },
    "5": {
      "docid": "irkjiqll",
      "type": "EXP"
    },
    "6": {
      "docid": "4fb291hq",
      "type": "BASE"
    },
    "7": {
      "docid": "kqqantwg",
      "type": "BASE"
    },
    "8": {
      "docid": "jpnbppry",
      "type": "EXP"
    },
    "9": {
      "docid": "es7q6c90",
      "type": "EXP"
    },
    "10": {
      "docid": "ne5r4d4b",
      "type": "BASE"
    }
  },
  "header": {
    "container": {
      "base": "pyterrier_bm25",
      "exp": "pyterrier_pl2"
    },
    "hits": 10,
    "page": 0,
    "q": "coronavirus origin",
    "rid": 3,
    "rpp": 10,
    "sid": "30fae19ec7574ad68af0bff23409adb5"
  }
}
```

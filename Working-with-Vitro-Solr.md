# View Solr service-level statistics

`$ curl 'http://rialto-vitro-dev.stanford.edu:8080/vitrosolr/admin/cores?wt=json'`

```json
{
  "responseHeader": {
    "status": 0,
    "QTime": 2
  },
  "defaultCoreName": "collection1",
  "initFailures": {
    
  },
  "status": {
    "collection1": {
      "name": "collection1",
      "isDefaultCore": true,
      "instanceDir": "\/opt\/app\/vitro\/home\/solr\/.\/",
      "dataDir": "\/opt\/app\/vitro\/home\/solr\/data\/",
      "config": "solrconfig.xml",
      "schema": "schema.xml",
      "startTime": "2018-05-17T20:54:21.718Z",
      "uptime": 349453178,
      "index": {
        "numDocs": 123498,
        "maxDoc": 266271,
        "deletedDocs": 142773,
        "indexHeapUsageBytes": 2069343,
        "version": 12770,
        "segmentCount": 12,
        "current": true,
        "hasDeletions": true,
        "directory": "org.apache.lucene.store.NRTCachingDirectory:NRTCachingDirectory(MMapDirectory@\/opt\/app\/vitro\/home\/solr\/data\/index lockFactory=NativeFSLockFactory@\/opt\/app\/vitro\/home\/solr\/data\/index; maxCacheMB=48.0 maxMergeSizeMB=4.0)",
        "userData": {
          "commitTimeMSec": "1526919790645"
        },
        "lastModified": "2018-05-21T16:23:10.645Z",
        "sizeInBytes": 172823300,
        "size": "164.82 MB"
      }
    }
  }
}
```
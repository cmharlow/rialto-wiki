Note that these `curl` commands must be run on the rialto-vitro-dev host because port 8080 is not exposed.

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

# View documents in a given collection

`$ curl 'http://rialto-vitro-dev.stanford.edu:8080/vitrosolr/collection1/select?q=*:*&wt=json'`

```json
{
  "responseHeader": {
    "status": 0,
    "QTime": 1,
    "params": {
      "q": "*:*",
      "wt": "json"
    }
  },
  "response": {
    "numFound": 123498,
    "start": 0,
    "maxScore": 1,
    "docs": [
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-210568-1",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521193,
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/UR-210568-1",
        "nameRaw": [
          "Bartnik, AC",
          "[Bartnik, AC]"
        ],
        "etag": "2e0fcb846dfc6c8d",
        "_version_": 1.6010911638576e+18,
        "timestamp": "2018-05-21T16:18:41.196Z",
        "score": 1
      },
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-339540-2",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521196,
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/UR-339540-2",
        "nameRaw": [
          "Bartnik, AC",
          "[Bartnik, AC]"
        ],
        "etag": "a6e779b13a8fb612",
        "_version_": 1.6010911638587e+18,
        "timestamp": "2018-05-21T16:18:41.197Z",
        "score": 1
      },
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-141705-2",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521193,
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/UR-141705-2",
        "nameRaw": [
          "Bartnik, AC",
          "[Bartnik, AC]"
        ],
        "etag": "513cf219736cbd41",
        "_version_": 1.6010911638597e+18,
        "timestamp": "2018-05-21T16:18:41.198Z",
        "score": 1
      },
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/acb20",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521198,
        "ALLTEXT": [
          "1029079 acb20"
        ],
        "mostSpecificTypeURIs": [
          "http:\/\/vivoweb.org\/ontology\/core#NonFacultyAcademic"
        ],
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/acb20",
        "nameRaw": [
          "Bartnik, Adam Christopher",
          "[Bartnik, Adam Christopher]"
        ],
        "etag": "3148d81d9f9ef6a4",
        "_version_": 1.6010911638608e+18,
        "timestamp": "2018-05-21T16:18:41.199Z",
        "score": 1
      },
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/acb249",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521202,
        "ALLTEXT": [
          "3961355 acb249"
        ],
        "mostSpecificTypeURIs": [
          "http:\/\/vivoweb.org\/ontology\/core#NonFacultyAcademic"
        ],
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/acb249",
        "nameRaw": [
          "Brown, Amanda Claire",
          "[Brown, Amanda Claire]"
        ],
        "etag": "a262b4f59edea4cd",
        "_version_": 1.601091163865e+18,
        "timestamp": "2018-05-21T16:18:41.203Z",
        "score": 1
      },
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-675720-1",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521201,
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/UR-675720-1",
        "nameRaw": [
          "Brown, AC",
          "[Brown, AC]"
        ],
        "etag": "b60bc8764236cafc",
        "_version_": 1.601091163865e+18,
        "timestamp": "2018-05-21T16:18:41.203Z",
        "score": 1
      },
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-675721-2",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521204,
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/UR-675721-2",
        "nameRaw": [
          "Brown, AC",
          "[Brown, AC]"
        ],
        "etag": "f566b231a2ea62f3",
        "_version_": 1.6010911638712e+18,
        "timestamp": "2018-05-21T16:18:41.209Z",
        "score": 1
      },
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/acb328",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521209,
        "ALLTEXT": [
          "3410332 acb328"
        ],
        "mostSpecificTypeURIs": [
          "http:\/\/xmlns.com\/foaf\/0.1\/Person"
        ],
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/acb328",
        "nameRaw": [
          "Mandelbaum, Amy Catherine",
          "[Mandelbaum, Amy Catherine]"
        ],
        "etag": "0c8ed761edb1a5a3",
        "_version_": 1.6010911638723e+18,
        "timestamp": "2018-05-21T16:18:41.21Z",
        "score": 1
      },
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/gnt74012",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521209,
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/gnt74012",
        "nameRaw": [
          "NATIONAL RESOURCE CENTER",
          "[NATIONAL RESOURCE CENTER]"
        ],
        "etag": "175d0e4d8945cb19",
        "_version_": 1.6010911638723e+18,
        "timestamp": "2018-05-21T16:18:41.21Z",
        "score": 1
      },
      {
        "DocId": "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/gnt75087",
        "THUMBNAIL_URL": "",
        "indexedTime": 1526919521215,
        "THUMBNAIL": "0",
        "URI": "http:\/\/scholars.cornell.edu\/individual\/gnt75087",
        "nameRaw": [
          "FOREIGN LANGUAGE AND AREA STUDIES FELLOWSHIPS",
          "[FOREIGN LANGUAGE AND AREA STUDIES FELLOWSHIPS]"
        ],
        "etag": "376fe846df5f0c64",
        "_version_": 1.6010911638786e+18,
        "timestamp": "2018-05-21T16:18:41.216Z",
        "score": 1
      }
    ]
  },
  "highlighting": {
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-210568-1": {
      
    },
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-339540-2": {
      
    },
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-141705-2": {
      
    },
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/acb20": {
      
    },
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/acb249": {
      
    },
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-675720-1": {
      
    },
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/UR-675721-2": {
      
    },
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/acb328": {
      
    },
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/gnt74012": {
      
    },
    "vitroIndividual:http:\/\/scholars.cornell.edu\/individual\/gnt75087": {
      
    }
  }
}
```
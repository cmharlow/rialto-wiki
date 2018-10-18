# Introduction

The purpose of this page is to capture an initial performance assessment of various components of RIALTO Core, tested within the development environment in AWS.

# RIALTO Core Ingest

**Note**: The following data is based on ingesting via ([Rialto ETL](https://github.com/sul-dlss-labs/rialto-etl)) for Stanford Organizations and Researchers Data.

## Procedure

### Run ETL (Extract - Transform - Load)
1. Install ([Rialto ETL](https://github.com/sul-dlss-labs/rialto-etl))
2. [Extract, transform, and load organization and researcher data](https://github.com/sul-dlss-labs/rialto-etl/wiki/RIALTO-Combine-Load-Procedure). **Note**: you can omit pubs and grants from this process.

### Extract CloudWatch Log Data

Each iteration of the Rialto sparql-loader outputs profile data to the logs like:

```
START RequestId: cd3ca114-c28d-11e8-8bcd-eb363f165b17 Version: $LATEST
2018/09/27 19:44:52 Neptune begin: 2018-09-27 19:44:52.650918936 +0000 UTC m=+0.050914288
2018/09/27 19:44:54 Neptune elapsed time: 1.68649536s
2018/09/27 19:44:54 SPARQL parse begin: 2018-09-27 19:44:54.337488395 +0000 UTC m=+1.737483730
2018/09/27 19:44:54 SPARQL parse elapsed time: 544.82917ms
2018/09/27 19:44:54 SNS publish begin: 2018-09-27 19:44:54.882359193 +0000 UTC m=+2.282354506
2018/09/27 19:44:54 SNS publish elapsed time: 100.815745ms
END RequestId: cd3ca114-c28d-11e8-8bcd-eb363f165b17
```

1. Filter the logs on `Neptune elapsed time` and extract
1. Filter the logs on `SPARQL parse elapsed time` and extract
1. Filter the logs on `SNS publish elapsed time` and extract (Note: SNS publishing is incredibly fast. All calls were under .01 seconds at most - so I did not include that data in the review below.)

## Overall

| Data | Records | Ingest Time |
|------|---------|-------------|
| Organizations | 7047 | 273 seconds / 4.55 minutes |
| Researchers | 258875 | 5650 seconds / 94.17 minutes |

### AWS Neptune Insert Performance

**This test was against a single AWS Neptune instance, with a _db.r4.large_ class.**

1. **Shortest**: .150s
2. **Longest**: 2.91s
3. **Average**: 1.38s
4. **TOTAL**: 928.82 seconds / 15.48 minutes

#### Neptune Breakdown

| Execution Time | Percentage of Responses | Total Time | Percentage of Total Time |
|---|---|---|---|
| < 1 Second | 14.6 | 72 seconds | 7.8 |
| 1 - 2 Seconds |  84.8 | 847 seconds | 91.2 | 
| 2 - 3 Seconds | 0.6 | 9 seconds | 1.0 |

#### Neptune Summary

The response time from Neptune to the SPARQL Proxy is very consistently between 1 and 2 seconds. When averaging only the responses in that time frame, most fall between 1.4 and 1.6 seconds. In this testing, no calls took more than 3 seconds. In a subsequent test with a larger (**db.r4.xlarge**) instance, these response times were not significantly different. Indicating that boosting a single instance type will not likely improve performance.

### SPARQL Parsing Performance

1. **Shortest**: .277s
2. **Longest**: 6.22s
3. **Average**: .763s
4. **Total**: 510.23 seconds / 8.50 minutes

#### SPARQL Parsing Breakdown

| Execution Time | Percentage of Responses | Total Time | Percentage of Total Time |
|---|---|---|---|
| < 1 Second | 87.5 | 318 seconds | 61.6 |
| 1 - 2 Seconds |  5.2 | 55 seconds | 10.8 | 
| 2 - 3 Seconds | 4.6 | 74 seconds | 14.3 |
| 3 - 4 Seconds | 2.5 | 57 seconds | 11.1 |
| > 5 Seconds | 0.2 | 11 seconds | 2.2 |

#### SPARQL Parsing Summary

As expected, the SPARQL parsing process of the ingest takes much less time since it doesn't do any external calls. Further, less than 13% of the processes added almost 40% of the run time. This seems to indicate that system resources and states out of our control are contributing to the slow down for such a small number of calls. It is not likely that we could easily recover this time, and would likely not provide enough value (at this point) to attempt.

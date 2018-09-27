# Introduction

The purpose of this page is to capture an initial performance assessment of various components of RIALTO Core.

# RIALTO Core Ingest

**Note**: The following data is based on ingesting via (LINK to Rialto ETL) for Stanford Organizations and Researchers Data. (TODO: verify/explain the data and it's source for this test)

## Overall

| Data | Records | Ingest Time |
|------|---------|-------------|
| Organizations | 7047 | 7201 seconds |
| Researchers | 258875 | 5650 seconds |

### AWS Neptune Insert Performance

1. **Shortest**: .150s
2. **Longest**: 2.91s
3. **Average**: 1.38s
4. **TOTAL**: 928.82 seconds / 15.48 minutes
### SPARQL Parsing Performance

1. **Shortest**: .277s
2. **Longest**: 6.22s
3. **Average**: .763s
4. **Total**: 510.23 seconds / 8.50 minutes



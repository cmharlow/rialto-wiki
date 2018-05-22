This document describes how we load data into Vitro using the Jena tdbloader(2) tool.

# tdbloader2

1. [Install Apache Jena](https://jena.apache.org/download/index.cgi)
1. [Set up your shell](https://jena.apache.org/documentation/tdb/commands.html#script-set-up-bash-scripts)
1. Clear out your TDB database (`tdbloader2`, the faster/newer version of `tdbloader`, only operates on empty databases):   
    `rm /path/to/vitro/tdbContentModels/*`
1. Run tdbloader:  
    `tdbloader2 --loc /path/to/vitro/tdbContentModels /path/to/vivo/agents/*.nt`

# tdbloader

**TODO**

# Troubleshooting

If running the loader step above throws an `Argument list too long` error, you may need to bump up that limit. On Linux, you can do this using `ulimit -s 65536`.

# Preliminary Results

```
...
INFO  Total: 4,522,586 tuples : 59.09 seconds : 76,542.43 tuples/sec [2018/05/22 11:47:52 PDT]
 11:47:52 INFO Data Load Phase Completed
 11:47:52 INFO Index Building Phase
 11:47:52 INFO Creating Index SPO
 11:47:52 INFO Sort SPO
 11:48:03 INFO Sort SPO Completed
 11:48:03 INFO Build SPO
log4j:WARN No appenders could be found for logger (Jena).
log4j:WARN Please initialize the log4j system properly.
log4j:WARN See http://logging.apache.org/log4j/1.2/faq.html#noconfig for more info.
 11:48:06 INFO Build SPO Completed
 11:48:06 INFO Creating Index POS
 11:48:06 INFO Sort POS
 11:48:31 INFO Sort POS Completed
 11:48:31 INFO Build POS
log4j:WARN No appenders could be found for logger (Jena).
log4j:WARN Please initialize the log4j system properly.
log4j:WARN See http://logging.apache.org/log4j/1.2/faq.html#noconfig for more info.
 11:48:33 INFO Build POS Completed
 11:48:33 INFO Creating Index OSP
 11:48:33 INFO Sort OSP
 11:48:42 INFO Sort OSP Completed
 11:48:42 INFO Build OSP
log4j:WARN No appenders could be found for logger (Jena).
log4j:WARN Please initialize the log4j system properly.
log4j:WARN See http://logging.apache.org/log4j/1.2/faq.html#noconfig for more info.
 11:48:45 INFO Build OSP Completed
 11:48:45 INFO Index Building Phase Completed
 11:48:45 INFO -- TDB Bulk Loader Finish
 11:48:45 INFO -- 4184 seconds

real    70m20.648s
user    42m56.784s
sys     16m24.580s
```
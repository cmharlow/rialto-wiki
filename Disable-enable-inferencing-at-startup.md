Whether inferencing is enabled or disabled when Vitro starts up is dependent on the contents of `webapp/src/main/webapp/WEB-INF/resources/startup_listeners.txt`. If the following line is not found, inferencing will be turned off:

> edu.cornell.mannlib.vitro.webapp.servlet.setup.SimpleReasonerSetup

Else, it is enabled. You can see where we removed it in sul-dlss-labs/Vitro#3: https://github.com/sul-dlss-labs/Vitro/pull/2/files#diff-d33445b89aedcf20cae03b97d873457fL32

To re-enable it, add the line above directly beneath: 

> edu.cornell.mannlib.vitro.webapp.application.ApplicationImpl$ReasonersSetup

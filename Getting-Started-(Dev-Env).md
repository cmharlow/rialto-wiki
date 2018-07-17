# Architecture

Review the [[RIALTO Architecture]] to become familiar with the different components within RIALTO Core and how they interconnect.

# Localstack

Some of the "glue" that connects components within RIALTO Core is supported by [localstack](https://github.com/localstack/localstack), a framework for testing AWS services locally (*i.e.*, without making any connections to AWS). Those components are SNS, Lambda, and API Gateway. If you're looking to to dev or testing with these components, localstack may in fact be a good place to start your work. Read more about [[working with localstack]]. (Unfortunately, localstack does **not** currently support Neptune, the center of RIALTO Core, but you should be able to tweak the URI our components connect to, in order to e.g. point them at a local Blazegraph instance which is a reasonably good stand-in for Neptune for some tests.)

Set up Dev Readme here for RIALTO core: RIALTO Ingest to Triplestore to SNS to Lambda to derivative stores

Add bit about setting up Stanford VPN in full-tunnel mode.

(When done with first draft of this document, close https://github.com/sul-dlss/rialto/issues/113)
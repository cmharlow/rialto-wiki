# Development

Most of the repositories for the RIALTO project are in the [DLSS labs organization](https://github.com/sul-dlss-labs). The two exceptions are the [main RIALTO repository](https://github.com/sul-dlss/rialto), which is our umbrella repo containing issues and this wiki, and our [sample data repository](https://github.com/sul-dlss/rialto-sample-data), which is private because it contains campus data that we cannot share openly.

All of the code repositories are in either Go or Ruby, so you have working environments for both. (There's some useful information in the [TACO README](https://github.com/sul-dlss-labs/taco#go-local-development-setup) about setting up Go for development.)

# Architecture

Review the [[RIALTO Architecture]] to become familiar with the different components within RIALTO Core and how they interconnect. Generally, the data flow works as follows:

* A SPARQL Update request hits the API Gateway fronting the [SPARQL Proxy lambda](https://github.com/sul-dlss/rialto/wiki/RIALTO-SPARQL-Proxy-Lambda-(Dev-Env)). Assuming a [valid API key](https://github.com/sul-dlss/rialto/wiki/RIALTO-SPARQL-Proxy-Lambda-(Dev-Env)#authorization) is provided, the request is routed to the lambda.
* The SPARQL Proxy lambda parses entities out of the SPARQL Update request and does two things:
  * Sends a message (conforming to the [messaging specification](https://github.com/sul-dlss/rialto/wiki/RIALTO-Core-Messaging-Specification)) to the environment-specific RIALTO Core messaging topic via AWS Simple Notification Service ([SNS](https://aws.amazon.com/sns/)) letting downstream systems know that certain entity URIs have changed; and
  * Forwards the SPARQL Update request to [Amazon Neptune](https://aws.amazon.com/neptune/), a triplestore serving as the canonical datastore within the RIALTO architecture.
* SNS messages sent to the env-specific RIALTO Core messaging topic, such as the one sent by the SPARQL Proxy, trigger spinning up the [RIALTO Derivatives lambda](https://github.com/sul-dlss/rialto/wiki/RIALTO-Derivatives-Lambdas-(Dev-Env)).
* The RIALTO Derivatives lambda parses the incoming message and based on the content of the message either:
  * Rebuilds the derivative datastore (Solr) based on the contents of the canonical datastore (Amazon Neptune), dropping all documents in Solr and reindexing the entirety of what's in Neptune (determined via a SPARQL query directly to Neptune); or
  * Indexes one or more entities from Neptune (via SPARQL query) into Solr, for piecemeal updates.
* The derivative datastore we're using for RIALTO is Solr (read more about our [Solr setup](https://github.com/sul-dlss/rialto/wiki/RIALTO-Solr-Setup-(Dev-Env))).

There are other components in the architecture not involved with the data flow above, and they include:

* the [RIALTO Ingest service](https://github.com/sul-dlss/rialto/wiki/RIALTO-Ingest-Service-(Dev-Env)), which is a Go-based codebase that runs on EC2 and is an alternative to the SPARQL Proxy. We decided to put our energy into the proxy rather than the ingest service since the proxy provides greater community overlap opportunities, because VIVO/Vitro exposes a SPARQL Update API for loading data.
* the [Rebuild Trigger lambda](https://github.com/sul-dlss/rialto/wiki/RIALTO-Rebuild-Trigger-Lambda-(Dev-Env)), which allows us to schedule a nightly rebuild (and trigger manual rebuilds) of the derivative datastore from what's in Neptune.


# Localstack

Some of the "glue" that connects components within RIALTO Core is supported by [localstack](https://github.com/localstack/localstack), a framework for testing AWS services locally (*i.e.*, without making any connections to AWS). Those components are SNS, Lambda, and API Gateway. If you're looking to to dev or testing with these components, localstack may in fact be a good place to start your work. Read more about [[working with localstack]]. (Unfortunately, localstack does **not** currently support Neptune, the center of RIALTO Core, but you should be able to tweak the URI our components connect to, in order to e.g. point them at a local Blazegraph instance which is a reasonably good stand-in for Neptune for some tests.)

# AWS Setup

Before you begin working with our AWS-based development environment, you'll need to walk through the [setup](https://github.com/sul-dlss/rialto/wiki/AWS-DLSS-Dev-Env-Setup) document. Note that if you do not yet have a `sul-dlss-users` AWS login, you can request one in the `#dlss-operations` channel within the Stanford Libraries Slack workspace.

# Authorization

Both the RIALTO SPARQL Proxy lambda and the Rebuild Trigger lambda expose HTTP APIs. We control access to these APIs using API keys, via AWS API Gateway. Clients, such as the tools we build for the RIALTO Combine (data pipeline/ETL, if you will), can connect to RIALTO Core using these API keys. Read more about [Combine/Core integration](https://github.com/sul-dlss/rialto/wiki/RIALTO-Combine-Core-Integration).

# Network

The AWS security group we have set up for the RIALTO development environment allows network access for some of the above services to IP addresses within [Stanford University's VPN](https://uit.stanford.edu/service/vpn) range. To be able to connect (*e.g.,* via SSH) to these boxes, make sure you are running the Stanford VPN in "full-tunnel" mode rather than "split-tunnel" mode. If you connect in the latter mode, Amazon sees your IP address as originating from your internet provider, not the Stanford VPN.

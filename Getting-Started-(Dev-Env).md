# Development

Most of the repositories for the RIALTO project are in the [DLSS labs organization](https://github.com/sul-dlss-labs). The two exceptions are the [main RIALTO repository](https://github.com/sul-dlss/rialto), which is our umbrella repo containing issues and this wiki, and our [sample data repository](https://github.com/sul-dlss/rialto-sample-data), which is private because it contains campus data that we cannot share openly.

All of the code repositories are in either Go or Ruby, so you have working environments for both. (There's some useful information in the [TACO README](https://github.com/sul-dlss-labs/taco#go-local-development-setup) about setting up Go for development.)

# Architecture

Review the [[RIALTO Architecture]] to become familiar with the different components within RIALTO Core and how they interconnect. Generally, the data flow works as follows:

* A SPARQL Update request hits the [SPARQL Proxy lambda](https://github.com/sul-dlss/rialto/wiki/RIALTO-SPARQL-Proxy-Lambda-(Dev-Env))


# Localstack

Some of the "glue" that connects components within RIALTO Core is supported by [localstack](https://github.com/localstack/localstack), a framework for testing AWS services locally (*i.e.*, without making any connections to AWS). Those components are SNS, Lambda, and API Gateway. If you're looking to to dev or testing with these components, localstack may in fact be a good place to start your work. Read more about [[working with localstack]]. (Unfortunately, localstack does **not** currently support Neptune, the center of RIALTO Core, but you should be able to tweak the URI our components connect to, in order to e.g. point them at a local Blazegraph instance which is a reasonably good stand-in for Neptune for some tests.)

# AWS Setup

Before you begin working with our AWS-based development environment, you'll need to walk through the [setup](https://github.com/sul-dlss/rialto/wiki/AWS-DLSS-Dev-Env-Setup) document. Note that if you do not yet have a `sul-dlss-users` AWS login, you can request one in the `#dlss-operations` channel within the Stanford Libraries Slack workspace.

# Resources

* links to READMEs here



Add bit about setting up Stanford VPN in full-tunnel mode.

(When done with first draft of this document, close https://github.com/sul-dlss/rialto/issues/113)
# cite-services-spec

This repository hosts specifications for microservices implementing the abstract models of the CITE Architecture.  It complements the specification of the CITE Exchange Format (CEX),  a line-oriented, plain-text format for exchanging data following the models of the CITE Architecture (https://github.com/cite-architecture/citedx).

Taken together, CEX and CITE microservices make it possible for CITE-aware applications to exchange data and interact with services.


## General principles

We want to design microservices that function like traditional UNIX programs, in that they are:

- focused on a single task, with well defined inputs and outputs
- can therefore be composed to create larger structures


## Basic architecture

0. Requests and replies are exchanged using HTTP.
1. Requests are formatted as URLs with no request parameters, structured as documented in the individual microservice specifications.  The general syntax of a request in CITE microservices is `/service name/request?/URN value?/format?`.
2. Replies are structured in a dynamically specified format chosen from a set of defined options, or in a defined *default* format.  At present, the only defined format is the default JSON format.


## Initial specifications

- `texts` microservice.  Current version: **1.0.0**. See the [specification](texts/1.0/texts-specification-1.0.DRAFT.md).
- `textcatalog` microservice. See an [initial draft for discussion](textcatalog/1.0/textcatalog-specification-1.0.DRAFT.md).

## Planned specifications


- `citedata` microservice
- `citecatalog` microservice
- `citerelations` microservice
- `citeextensions` microservice
- `dse` microservice
- `orca` microservice

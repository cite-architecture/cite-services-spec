# cite-services-spec

This repository is for developing specifications for microservices implementing the abstract models of the CITE Architecture.  It complements the specification of the CITE Exchange Format (CEX),  a line-oriented, plain-text format for exchanging data following the models of the CITE Architecture (https://github.com/cite-architecture/citedx).

Taken together, CEX and CITE microservices make it possible for CITE-aware applications to exchange data and interact with services.


## General principles

We want to design microservices that function like traditional UNIX programs, in that they are:

- focused on a single task, with well defined inputs and outputs
- can therefore be composed to create larger structures


## Initial specifications

We are working first on a `texts` microservice.  See draft notes [here](texts-specification.md)


## Planned specifications

- `textcatalog` microservice
- `citedata` microservice
- `citecatalog` microservice
- `citerelations` microservice
- `citeextensions` microservice
- `dse` microservice
- `orca` microservice

## Status

Early discussions only.

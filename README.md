# Processing SPARQL TOP-k Queries Online with Web Preemption

This repository contains an implementation of a Web preemptive server as defined in the paper [SaGe: Web Preemption for Public SPARQL Query services](https://hal.archives-ouvertes.fr/hal-02017155/document). To support TOP-k queries, the Web preemptive server has been extended with TOP-k operators as defined in the paper [Processing SPARQL TOP-k Queries Online with Web Preemption](...).

# Installation

The SaGe server can be easily installed using the [poetry](https://github.com/sdispater/poetry) dependency manager.

```bash
git clone https://github.com/SaGeTOPK/sage-engine.git
cd sage-engine
poetry install --extras "hdt"
```

# Getting started

## Server configuration

A SaGe server is configured using a YAML configuration file.
You will find below a minimal working example of such a configuration file.

```yaml
name: SaGe Test server
maintainer: Chuck Norris
quota: 75 # duration of a quantum
max_results: 2000 # maximum number of results returned per quantum
max_limit: 2000 # same as max_results for TOP-k queries
stateless: True # False to store saved plans on the server, True otherwise
graphs:
-
  name: dbpedia # name of the RDF graph
  uri: http://example.org/dbpedia # IRI of the RDF graph
  backend: hdt-file # here we use the HDT backend
  file: datasets/dbpedia.2016.hdt # HDT file of the RDF graph
```

## Starting the server

The `sage` executable, installed alongside the SaGe server, allows to easily start a SaGe server from a configuration file using [Uvicorn](https://www.uvicorn.org/), a Python ASGI HTTP Server.

```bash
# launch Sage server with 4 workers on port 8080
sage my_config.yaml -w 4 -p 8080
```

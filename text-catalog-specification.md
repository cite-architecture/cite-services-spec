# `textcatalog` microservice



## Version and status

This document specifies version **1.0.0** of the `textcatalog` microservice. It is in **draft** status.


## What it does

1. The `textcatalog` microservice supports *identification* and *retrieval* of entries in a catalog of texts, and nothing more.
2. A cataloged text entry is always identified by CTS URN.



## Relation to CEX

The `textcatalog` microservice works with content encoded in CEX in a `ctscatalog` block.


## Data model

1. CTS URN for a version or exemplar
2. list of labels for each tier of the citation hierarchy
3. name of the text group
4. title of the work
5. label of the edition or translation
6. label of the specific exemplar, if any
7. language of the specific version or exemplar

## Request syntax and return values

The general syntax of a request in CITE microservices is

    /service name/request?/URN value?/format?

The `texts` service, the request URL can assume the following patterns (where `{URN}` stands for a syntactically valid URN string).

| URL                     | Meaning                                           | Return value                                    |
|:------------------------|:--------------------------------------------------|:------------------------------------------------|
| `/textcatalog`                | lists the set of catalog entries for all cataloged texts | (unordered) list of work-level URNs             |
| `/textcatalog/{URN}`          | lists catalog entries matching the given URN                        | (possibly empty, ordered) list of ccatalog entries |
| `textcatalog/size` | gives the  number of catalog entries in the catalog | an integer value |
| `textcatalog/size/{URN}` | gives the  number of catalog entries matching the given URN | an integer value |
| `textcatalog/version` | gives the  version of the specification implemented | a string in semantic version format |

The `/textcatalog` request returns the full set of cataloged entries.

The `/textcatalog/{URN}` request returns the set of cataloged entries matching the given URN, according to the rules of URN matching.


## Reply format


### JSON

Replies are single JSON objects.

Catalog entries are serialized as a Map of seven values labelled:


1. `URN`
2. `language`
3. `citation`
4. `group`
5. `work`
6. `version`
7. `exemplar`



### Default format

JSON is the default reply forma (and currently the only defined format).

## Exceptions

In any request, a syntactically invalid URN is an exception.

Requests including syntactically valid URNs that match no results are valid. In these cases, replies include an empty list of catalog entries.

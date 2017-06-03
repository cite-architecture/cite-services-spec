# `texts` microservice



> ## Version and status
>
>This document specifies version **1.0.0** of the `texts` microservice.
> It is in **draft** status.


## What it does

1. The `texts` microservice supports *identification* and *retrieval* of passages of texts in the OHCO2 model, and nothing more.
2. Passages of texts are always identified by CTS URN.



## Relation to CEX

The `texts` microservice works with content encoded in CEX in a `ctsdata` block.


## Data model

The `texts` microservice works with the smallest unit of the OHCO2 model: citable nodes of text.  Queries to the microservice will return *either* citable nodes of text, *or* URNs identifying citable nodes.

In the `text` microservice, citable nodes are modelled as objects with five properties:

1. an identifying URN
2. text contents of the node
3. URN of the preceding node, or null value
4. URN of the following node, or null value
5. a numeric sequence value that can be used to sort a set of nodes into document order

## Request syntax and return values

In `texts` microservice, request URLs  can assume the following patterns (where `{URN}` stands for a syntactically valid URN string):

| URL                     | Meaning                                           | Return value                                    |
|:------------------------|:--------------------------------------------------|:------------------------------------------------|
| `/texts`                | list distinct works appearing in cited text nodes | (unordered) list of work-level URNs             |
| `/texts/{URN}`          | retrieve a passage of text                        | (possibly empty, ordered) list of citable nodes |
| `/texts/first/{URN}`    | retrieve first node of text                       | 0 or 1 citable node                             |
| `/texts/last/{URN}`     | retrieve last node of text                        | 0 or 1 citable node                             |
| `/texts/previous/{URN}` | retrieve node preceding {URN}                     | (possibly empty, ordered) list of citable nodes |
| `/texts/next/{URN}`     | retrieve node following {URN}                     | (possibly empty, ordered) list of citable nodes |


> I'd like one further request:  `texts/version` giving the version of the services specification implemented.  Specifications should be identified with semantic versioning. When we get to an iniital release, we would begin with `1.0.0`.

When the value `{URN}` identifies a single citable node, the requests `texts`, `texts/previous` and `texts/next` will each return 0 or 1 citable node.

When the value `${URN}` identifies a *range* from one citable node to a second citable node, `texts` returns the ordered list of all nodes in the range.  `texts/previous` returns a list of all citable nodes preceding the range up to a maximum number equal to the number of citable nodes in the range.  `texts/next` returns a list of all citable nodes following the range up to a maximum number equal to the number of citable nodes in the range.

When the value `${URN}` identifies a *single containing component* of the passage hierarchy,  `texts` returns the ordered list of all nodes contained in that URN.  `texts/previous` returns the list of preceding citable nodes contained in the preceding containing element at the same hierarchical level, or none. `texts/next` returns the list of following citable nodes contained in the preceding containing element at the same hierarchical level, or none.

When the value `${URN}` identifies a *range from one containing component to a second containing component*, `texts` returns the ordered list of all nodes contained in that range of containing components.   `texts/previous` contains the list of citable nodes contained in all preceding containing components at the same hierarchical level up to a maximum number of containing components equal to the number of containing components in the given range. `texts/next` contains the list of citable nodes contained in all following containing components at the same hierarchical level up to a maximum number of containing components equal to the number of containing components in the given range.

In all cases, lists of more than one citable node are given in document order.



## Reply format


### JSON

Replies are single JSON objects.

URNs are serialized as String values following the CTS URN specification.

Citable nodes are serialized as a Map of five values labelled:

1. `URN`
2. `text`
3. `previous`
4. `following`
5. `sequence`


### Default format

JSON is the default reply forma (and currently the only defined format).

## Exceptions

In any request, a syntactically invalid URN is an exception.

Requests including syntactically valid URNs that match no results are valid. In these cases, replies include an empty list of URNs or citable nodes.

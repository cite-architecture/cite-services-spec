# `texts` microservice

>Sections of this document formatted like this (markdown quoted blocks) are used for **proposed** content.  Comments solicited!
>
> Suggested formatting of comments:  [Critic Markup](http://criticmarkup.com/), with editing history maintained by your version control system.



## What it does

1. The `texts` microservice supports *identification* and *retrieval* of passages of texts in the OHCO2 model, and nothing more.
2. Passages of texts are always identified by CTS URN.



## Relation to CEX

The `texts` microservice works with content encoded in CEX in a `ctsdata` block.


## Data model

The `texts` microservice works with the smallest unit of the OHCO2 model: citable nodes of text.  Queries to the microservice will return *either* citable nodes of text, *or* URNs identifying citable nodes.

> Citable nodes are implemented as objects with five properties:
>     1. an identifying URN
>     2. text contents of the node
>     3. URN of the preceding node, or null
>     4. URN of the following node, or null
>     5. a numeric sequence value that can be used to sort a set of nodes into document order

## Request syntax

>The general syntax of a request is
>
> `/service name/request?/URN value?/format?`

| URL                     | Meaning                                           | Return value                                    |
|:------------------------|:--------------------------------------------------|:------------------------------------------------|
| `/texts`                | list distinct works appearing in cited text nodes | (unordered) list of work-level URNs             |
| `/texts/{URN}`          | retrieve a passage of text                        | (possibly empty, ordered) list of citable nodes |
| `/texts/first/{URN}`    | retrieve first node of text                       | 0 or 1 citable node                             |
| `/texts/last/{URN}`     | retrieve last node of text                        | 0 or 1 citable node                             |
| `/texts/previous/{URN}` | retrieve node preceding {URN}                     | 0 or 1 citable node                             |
| `/texts/next/{URN}`     | retrieve node following {URN}                     | 0 or 1 citable node                             |


## Replies


### JSON

> JSON is the default reply format.
>
> URNs are serialized as String values following the CTS URN specification.
> Citable nodes are serialized as a Map of five values labelled
>
>     1. `URN`
>     2. `text`
>     3. `previous`
>     4. `following`
>     5. `sequence`

## Exceptions

In any request, a syntactically invalid URN is an exception.

Requests including syntactically valid URNs that match no results are valid. In these cases, replies include an empty list of URNs or citable nodes.

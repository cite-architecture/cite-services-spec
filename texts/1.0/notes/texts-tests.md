# `texts` tests

>Sections of this document formatted like this (markdown quoted blocks) are used for **proposed** content.  Comments solicited!
>
> Suggested formatting of comments:  [Critic Markup](http://criticmarkup.com/), with editing history maintained by your version control system.

## Test Data

> Test data in the form of `.cex` files is in the <resources> directory.

## Tests

| Test File                | Request                                            | Return value                                      |
|:-------------------------|:---------------------------------------------------|:--------------------------------------------------|
| <resources/test1.cex>    | `/texts`                                           | `urn:cts:citeArch:groupA.work1.ed1:`              |
|                          |                                                    | `urn:cts:citeArch:groupA.work1.ed2:`              |
|                          |                                                    | `urn:cts:citeArch:groupA.work1.ed2.ex1:`          |
|                          |                                                    | `urn:cts:citeArch:groupA.work2.ed1:`              |
| <resources/test1.cex>    | `/texts/urn:cts:citeArch:groupA.work1.ed1:1.1`     | Citable Node for                                  |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.1`     |
| <resources/test1.cex>    | `/texts/urn:cts:citeArch:groupA.work1.ed1:1`       | Citable Nodes for                                 |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.1`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.2`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.3`     |
| <resources/test1.cex>    | `/texts/urn:cts:citeArch:groupA.work1.ed1:1.1-1.3` | Citable Nodes for                                 |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.1`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.2`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.3`     |
| <resources/test1.cex>    | `/texts/urn:cts:citeArch:groupA.work1:1.1-1.2`     | Citable Nodes for                                 |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.1`     |
|                          | (Work-level URN. Returns all valid Nodes, sorted)  |       `urn:cts:citeArch:groupA.work1.ed1:1.2`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed2:1.1`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed2:1.2`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed2.ex1:1.1` |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed2.ex1:1.2` |
| <resources/test1.cex>    | `/texts/urn:cts:citeArch:groupA.work1.ed1:1-2.2`   | Citable Nodes for                                 |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.1`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.2`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.3`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:2.1`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:2.2`     |
| <resources/test1.cex>    | `/texts/urn:cts:citeArch:groupA.work1.ed1:1.3-2`   | Citable Nodes for                                 |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:1.3`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:2.1`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:2.2`     |
|                          |                                                    |       `urn:cts:citeArch:groupA.work1.ed1:2.3`     |






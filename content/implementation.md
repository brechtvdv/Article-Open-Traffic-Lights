## Implementation
{:#implementation}

### hetarchief.be

Every newspaper webpage is annotated with JSON-LD snippets containing domain-specific metadata and hypermedia controls. The former metadata is described using acknowledged vocabularies such as [Dublin Core Terms](http://dublincore.org/documents/dcmi-terms/) (DCTerms), [Friend of a Friend](http://xmlns.com/foaf/spec/) (FOAF), [Schema.org](https://schema.org/) etc. The latter is described using the [Hydra](https://www.hydra-cg.com/spec/latest/core) vocabulary for hypermedia-driven Web APIs. Although hetarchief.be contains several human-readable hypermedia controls (free text search bar, search facets, pagination for every [newspaper](https://hetarchief.be/nl/media/brief-van-den-soldaat-aan-zijne-verdrukte-medeburgers/I2STYUAOpmFKmbFRXNmV0PTp) ) only Hydras partial collection view controls are implemented: hydra:next describes the next newspaper, vice versa hydra:previous. Also an estimate of the amount of triples on a page is added using hydra:totalItems and void:triples. This helps user agents to build more efficient query plans.

<figure id="partial-collection-controls" class="listing">
````/code/hydra-partial-collection-view.txt````
<figcaption markdown="block">
Every newspaper describes its next and previous newspaper using Hydra partial collection view controls. This wires Linked Data Fragments together into a dataset.
</figcaption>
</figure>

In order to lower the barrier for automated Open Data reuse, information responses add the [Cross-Origin Resource Sharing](https://www.w3.org/TR/cors/) (CORS) header: _Access-Control-Allow-Origin: *_ . 
Not all metadata of a newspaper falls under an Open License. In the process of digitizing these newspapers, [Optical Character Recognition](https://nl.wikipedia.org/wiki/Optical_character_recognition) (OCR) is applied. According to the [European copyright legislation](https://eur-lex.europa.eu/eli/dir/2001/29/oj) content is still reserved by default 70 years after the death of the last author. This implies that these scanned texts cannot be published provisionally as Open Data. This is solved by publishing the OCR text in a seperate Linked Data document covered by a different [terms of use](https://hetarchief.be/nl/gebruiksvoorwaarden). This also keeps the fragment size lean as such a [document](https://hetarchief.be/nl/media/brief-van-den-soldaat-aan-zijne-verdrukte-medeburgers/I2STYUAOpmFKmbFRXNmV0PTp/ocr) measures easily 50 kilobytes for four newspaper pages.

### Building blocks Comunica

To make Comunica work with hetarchief.be, two additional actors were needed.
First, we needed a generic actor to support pagination over any kind of hypermedia interface.
Secondly, an actor was needed to parse JSON-LD data snippets from HTML documents.
We will explain these two actors in more detail hereafter.

`BusRdfResolveHypermedia` is a bus in Comunica that resolves hypermedia controls from sources,
Currently, this bus only contains an actor that resolves controls for TPF interfaces.
We added a new actor (`ActorRdfResolveHypermediaNextPage`) to this bus that returns a search form containing a next page link, vice versa for previous page links.

The parsing of most common Linked Data formats ([Turtle](https://www.w3.org/TR/turtle/), [TriG](https://www.w3.org/TR/trig/), [RDF/XML](https://www.w3.org/TR/rdf-syntax-grammar/), [JSON-LD](https://www.w3.org/2018/jsonld-cg-reports/json-ld/)...) are already supported by Comunica.
However, no parser for extracting data snippets from HTML documents existed yet.
That is why we added an actor (`ActorRdfParseHtmlScript`) for parsing such HTML documents.
This intermediate parser searches for data snippets and forwards these to their respective RDF parser.
In case of a JSON-LD snippet, the body of a script tag  `<script type="application/ld+json">` will be parsed by the JSON-LD parse actor.

By adding these two actors to Comunica, we can now query over a paged collection that is declaratively described with data snippets. As federated querying comes out-of-the-box with Comunica, this cultural heritage collection can now be queried together with other knowledge bases (cfr. Wikidata). For example, [](#federated-querying-comunica) crawls over 17 newspaper pages. The first result appears after reading the first page. All results are available after 1,5 minutes. This is caused by deficiency of indexes where all pages need examination before having a complete answer.

<figure id="federated-querying-comunica" class="listing">
````/code/federated-querying-comunica.txt````
<figcaption markdown="block">
SPARQL-query over a paged collection of hetarchief.be and the TPF interface of Wikidata using the JavaScript-based command line interface of Comunica.
</figcaption>
</figure>

In next section we will demonstrate how SPARQL-querying can be applied for extracting a spreadsheet.
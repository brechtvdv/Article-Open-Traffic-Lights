## Implementation
{:#implementation}

### hetarchief.be

Every newspaper webpage is annotated with JSON-LD snippets containing domain-specific metadata and hypermedia controls. The former metadata is described using acknowledged vocabularies such as Dublin Core Terms (DCTerms), Friend of a Friend (FOAF), Schema.org etc. The latter is described using the Hydra vocabulary for hypermedia-driven Web APIs. Although hetarchief.be contains several human-readable hypermedia controls (free text search bar, search facets, pagination for every [newspaper](https://hetarchief.be/nl/media/brief-van-den-soldaat-aan-zijne-verdrukte-medeburgers/I2STYUAOpmFKmbFRXNmV0PTp) ) only Hydras partial collection view controls are implemented: hydra:next describes the next newspaper, vice versa hydra:previous. Also an estimate of the amount of triples on a page is added using hydra:totalItems and void:triples. This helps user agents to build more efficient query plans.

<figure id="partial-collection-controls" class="listing">
````/code/hydra-partial-collection-view.txt````
<figcaption markdown="block">
Every newspaper describes its next and previous newspaper using Hydra partial collection view controls. This makes Linked Data Fragments searcheable like a dataset.
</figcaption>
</figure>

{:todo} CORS, license

### Building blocks Comunica

{:.comment data-author="RT"}
Consider moving this first paragraph to the introduction or a related work section.

Every piece of functionality in Comunica can be implemented as seperate building blocks based on the _actor_ programming model, where each actor can respond to a specific action. Actors that share same functionality, but with different implementations, can be grouped with a communication channel called a _bus_. Interaction between actors is possible through a _mediator_ that wraps around a bus to get an action's result from a single actor. This result depends on the configuration of the mediator, e.g. a race mediator will return the response of the actor that is able to reply the earliest.

To make Comunica work with hetarchief.be, two additional actors were needed.
First, we needed a generic actor to support pagination over any kind of hypermedia interface.
Secondly, an actor was needed to parse JSON-LD data snippets from HTML documents.
We will explain these two actors in more detail hereafter.

{:.comment data-author="RT"}
I would not go into the specifics of things like "Hydra partial collection view next link" here, I would just call this a "next page link". But you can elaborate on that in another section/paragraph.

`BusRdfResolveHypermedia` is a bus in Comunica that resolves hypermedia controls from sources,
Currently, this bus only contains an actor that resolves controls for TPF interfaces.
We added a new actor (`ActorRdfResolveHypermediaNextPage`) to this bus that returns a search form containing a Hydra partial collection view next link, vice versa for previous links.
<del class="comment" data-author="RT">Extracting hydra controls from RDF quads is already implemented with the actor ActorRdfMetadataExtractHydraControls. This shows that modularizing code pays off when similar functionalities are needed.</del>

The parsing of most common Linked Data formats (Turtle, TriG, RDF/XML, JSON-LD...) are already supported by Comunica.
However, no parser for extracting data snippets from HTML documents existed yet.
That is why we added an actor (`ActorRdfParseHtmlScript`) for parsing such HTML documents.
This intermediate parser searches for data snippets and forwards these to their respective RDF parser.
In case of a JSON-LD snippet, the body of a script tag  `<script type="application/ld+json">` will be parsed by the JSON-LD parse actor.

By adding these two actors to Comunica, we can now query over a paged collection that is declaratively described with data snippets. As federated querying comes out-of-the-box with Comunica, this cultural heritage collection can now be queried together with other knowledge bases (cfr. Wikidata). For example, [](#federated-querying-comunica) fetches 17 newspaper pages in 1 minute 25 seconds. 

{:.comment .rephrase data-author="RT"}
Don't degrade your own work :-) First start by saying that the first result already appears after x seconds. And all results are available after 1,5 minutes. Be sure to explain why it takes this long, and give TPF as an example of a method to improve performance.

Although this is a bad user perceived performance, composite data dumps can be extracted for more performant Linked Data interfaces.

{:.comment data-author="RT"}
I'm wondering if this query example is needed if you already have the codepen. You could for example setup you own [Comunica jQuery Widget](https://github.com/comunica/jQuery-Widget.js), and plug in your own config file.

<figure id="federated-querying-comunica" class="listing">
````/code/federated-querying-comunica.txt````
<figcaption markdown="block">
SPARQL-query over a paged collection of hetarchief.be and the TPF interface of Wikidata using the JavaScript-based command line interface of Comunica. <del class="comment" data-author="RT">Heterogeneous interfaces can be added without extra effort.</del>
</figcaption>
</figure>

In next section we will demonstrate how SPARQL-querying can be applied for extracting a spreadsheet.
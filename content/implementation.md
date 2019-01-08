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

Every piece of functionality in Comunica can be implemented as a seperate building block with actors. Those that share same functionality, but with different implementations, can be grouped with a communication channel called a 'bus'. Interaction between actors is possible through a mediator which wraps around a bus and makes sure that a requesting actor only gets one result. This result depends on the configuration of the mediator, e.g. a race mediator will return the response of the first actor that answers the call. In order for Comunica to work with hetarchief.be it needs to support pagination controls when the interface is not a TPF interface and needs to be capable of parsing data snippets from HTML documents.

As Comunica already supports a hypermedia interface, the TPF interface, a bus BusRdfResolveHypermedia for resolving hypermedia controls already exists. A new actor ActorRdfResolveHypermediaNextPage that only returns a search form containing a Hydra partial collection view next link, vice versa for previous links, is created and subscribed to the same bus as for the TPF hypermedia controls. Extracting hydra controls from RDF quads is already implemented with the actor ActorRdfMetadataExtractHydraControls. This shows that modularizing code pays off when similar functionalities are needed.

Most common Linked Data formats (Turtle, TriG, RDF/XML, JSON-LD...) are already supported by Comunica. An actor ActorRdfParseHtmlScript for parsing HTML documents is added to the same RDF parsers bus. This intermediate parser searches for data snippets and passes these back into the RDF parsers bus. In case of a JSON-LD snippet, the body of a script tag  `<script type="application/ld+json">` will be parsed by the JSON-LD parse actor.

Adding these two actors allows Comunica to query over a paged collection that is embedded through data snippets. As federated querying comes out-of-the-box with Comunica this cultural heritage collection can now be investigated with other knowledge bases (cfr. Wikidata). [](#federated-querying-comunica) fetches 17 newspaper pages in 1 minute 25 seconds. Although this is a bad user perceived performance, composite data dumps can be extracted for more performant Linked Data interfaces.

<figure id="federated-querying-comunica" class="listing">
````/code/federated-querying-comunica.txt````
<figcaption markdown="block">
SPARQL-query over a paged collection of hetarchief.be and the TPF interface of Wikidata using the command line interface of Comunica. Heterogeneous interfaces can be added without extra effort.
</figcaption>
</figure>

In next section we will demonstrate how SPARQL-querying can be applied for extracting a spreadsheet.
## Abstract
<!-- Context      -->
Maintaining an Open Dataset comes at an extra recurring cost when it is published in a dedicated Web interface.
<!-- Need         -->
As there is not often a direct financial return from publishing a dataset publicly, these extra costs need to be minimized.
<!-- Task         -->
Therefore want to explore reusing existing infrastructure by enriching existing websites with Linked Data.
<!-- Object       -->
In this demonstrator, we advised the data owner to annotate a digital heritage website with JSON-LD snippets, resulting in a dataset of <todo style="color: red;">? (todo) triples</todo> that is now available and officially maintained. <!--TODO: how much data was in te end published? Can we have some stats about the total data dump? -->
<!--Only an initial investment is required to have Linked Data snippets added to its corresponding webpages.-->
The website itself is paged, and thus hydra partial collection view controls were added in the snippets.
We then extended the modular query engine [Comunica](http://comunica.linkeddatafragments.org) to support following page controls and extracting data from HTML documents while querying.
<!-- Findings     -->
This way, a SPARQL or GraphQL query over multiple heterogeneous data sources can power automated data reuse.
While the query performance on such an interface is visibly poor, it becomes easy to create composite data dumps.
<!-- Conclusion and Perspectives -->
As a result of implementing these building blocks in Comunica, any paged collection now becomes queryable by the query engine, as well as any HTML page with or without any of the supported hypermedia building blocks.
This enables heterogenous data interfaces to share functionality and become technically interoperable.

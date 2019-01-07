## Abstract
<!-- Context      -->
One of the biggest challenges of publishing Linked Open Data is the maintainability of its interfaces. Linked Data interfaces exist in multiple shapes, typically datadumps or SPARQL-endpoints, and require different amounts of technical resources. Given that organisations have a website for communicating about their subjects, this interface can be reused and extended with machine-readable data.
<!-- Need         -->
Embedding Linked Data over multiple webpages gives uncertainty on how the organisation or end-users can consume this fragmented data. Data publishers currently lack tooling to test these new kind of interfaces.
<!-- Task         -->
We extended the modular query engine Comunica to support exposing a dataset with partial collection views by implementing pagination controls and reading Linked Data inside HTML documents.
<!-- Object       -->
This paper demonstrates a real-live website annotated with JSON-LD snippets and how a spreadsheet can be harvested from this website by using Comunica. 
<!-- Findings     -->
We found that reusing your website for data publishing enables a cost-efficient interface for maintaining an up-to-date dataset. Only an initial investment is required to have Linked Data snippets added to its corresponding webpages.
Federated querying with your website becomes possible as Comunica already supports heterogeneous interfaces.
<!-- Conclusion   -->
Organisations can test if the Linked Data on their websites is automatically reusable by extracting a spreadsheet. This gives confidence that a Linked Data interface is not necessarily a seperate infrastructure.
<!-- Perspectives -->
In future work, other hypermedia controls then pagination need to be researched to query a website more efficiently.
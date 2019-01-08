## Introduction
{:#introduction}

The Flemish Institute for Audiovisual Archiving (VIAA) is a non-profit organization that preserves petabytes of valuable image, audio or video files. These files and accompanying metadata are covered by distinct licenses, but some can be made accessible under an Open Data license. One initiative is opening up historical newspapers of the first World War with their website [hetarchief.be](https://hetarchief.be). In 2017, the raw data of these newspapers have been published as a Linked Open Data dataset using the low-cost Triple Pattern Fragments (TPF) interface[^tpf]. Although this interface is still accessable, no updates from the website have been exported to the TPF interface due to absence of automatisation.

[^tpf]: http://linkeddatafragments-qas.viaa.be/ 

Maintaining an up-to-date Linked Open Data (LOD) interface brings besides technical resources also an organisational challenge. Content editors often work in a seperate environment such as a Content Management System (CMS) to update a website. The raw data gets exported from that system and published elsewhere leaving the source of truth to the CMS. The question rises whether the data can be published closer to the authorative source in a more sustainable way.

Website maintainers are currently using JSON-LD structured data snippets to attain better search result ranking and visualisation with search engines. These snippets are script tags containing Linked Data in JSON format (JSON-LD) that are embedded inside a HTML webpage. Not only search engine optimalisation (SEO), but also standard LOD publishing is possible. The data should be representative with the main content of the subject page, such as newspaper metadata, to be aligned with the structured data guidelines of search engines. Having n subject pages leads to n Linked Data Fragments that need to be linked together through hypermedia controls so the website can be consumed as a dataset.

{:.comment data-author="RT"}
You should cite Comunica here. But you don't seem to have any other references, so I assume you'll still add those?

Comunica is a Linked Data user agent that can run federated queries over several heterogeneous Web APIs, such as data dumps, SPARQL-endpoints, Linked Data documents and Triple Pattern Fragments. This engine has been developed to make it easy to plug in specific types of functionality as separate modules. Such modules can be added or removed depending on the configuration. As such, this allows hypermedia driven clients to be created.

In this article, first we describe how hetarchief.be is enriched with JSON-LD snippets and how this enables federated querying with Comunica by adding two building blocks. After this, we demonstrate how a data dump can easily be generated. Finally, we discuss our conclusion.


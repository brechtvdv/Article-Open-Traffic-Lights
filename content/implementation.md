## Implementation
{:#implementation}

There are two additional actors implemented to allow support for rich snippets with Comunica.
First, the 'actor-rdf-parse-html-script' takes care of recognizing script-tags containing Linked Data, such as JSON-LD. Secondly, the 'actor-rdf-resolve-hypermedia-next-page' recognizes next page links that allow querying a paged collection of Linked Data Fragments.

'actor-rdf-parse-html-script'

'actor-rdf-resolve-hypermedia-next-page'

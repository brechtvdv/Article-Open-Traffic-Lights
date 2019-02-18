##  Background
{:#sota}

### RDF isomorphism

The Resource Description Framework (RDF) is a graph-based model to describe statements. Every statement corresponds with a triple (subject-predicate-object): the _subject_ is the resource that is related an _object_ through a _predicate_ that defines a relation. For example, 'the traffic light lights green': 'the traffic light' is the subject, 'green' is the object and 'lights' is the predicate. This RDF statement is actually a small graph. Two graphs are isomorph when a bijection is possible as described in the algorithm by (Carrol J.)[cite:cites carroll2002matching]. This algorithm generates a hash for every blank node to allow equivalence checking and attempts to create a bijection between two graphs. If a bijection is created, the graphs are isomorph.

### Linked Data Fragments

[Linked Data Fragments](cite:cites tpf) is a framework that allows to describe the fragmentation of a Linked Data dataset. Fragments are defined with three parts:

* a **selector** defines which parts of the dataset belong to a fragment. For example: only sensor observations who are generated between a certain time interval.
* **metadata** about the fragment. For example: the license that applies to the fragment.
* **controls** help clients to retrieve more relevant data. For example where a previous page of a paged collection can be found.

### Preservation

Digital content can be preserved on tape or disk storage. Tape is in general used by TV broadcasters or audiovisual archives, because of its [low pricing](https://searchdatabackup.techtarget.com/news/1507559/Choosing-a-data-archiving-strategy-Disk-archiving-vs-tape-archiving) for big volumes (>50 TB), especially for long term preservation. A tape drive is cost-effective when writing or reading large files. Small files causes more overhead, because the tape drive reader needs to reset its position for every file. This is solved by archives either by bundling small files together (e.g. zip, tar) or saving them on disk storage. The latter benefits over tape with faster search and retrievable times and the ability to preserve small files more efficiently.

To archive a document, this is traditionally done by generating a hash (e.g. [MD5](https://en.wikipedia.org/wiki/MD5)) from the document, copying the document together with a metadata file (cfr. [sidecar](https://en.wikipedia.org/wiki/Sidecar_file)) , containing the hash, to the archive and verification by re-generating the hash on the archive.
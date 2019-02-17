##  Background
{:#sota}

### Linked Data Fragments

[Linked Data Fragments](cite:cites tpf) is a framework that allows to describe the fragmentation of a Linked Data dataset. Fragments are defined with three parts:

* a **selector** defines which parts of the dataset belong to a fragment. For example: only sensor observations who are generated between a certain time interval.
* **metadata** about the fragment. For example: the license that applies to the fragment.
* **controls** help clients to retrieve more relevant data. For example where a previous page of a paged collection can be found.

### Preservation

Tape is in general used by TV broadcasters or audiovisual archives, because of its [low pricing](https://searchdatabackup.techtarget.com/news/1507559/Choosing-a-data-archiving-strategy-Disk-archiving-vs-tape-archiving) for big volumes (>50 TB), especially in the long run. To write or read from a tape, a tape drive is cost-effective with large files. To preserve small files, archives either make bundle these together (e.g. zip, tar) or save these on disk.
Disk is mostly chosen to search and access files faster and to preserve small files.

Preserving documents are traditionally done by generating a hash (e.g. MD5) from the document that needs to archived, copy the document together with a metadata file containing the hash to the archiving system and re-generating the hash on the archive to verify its content.
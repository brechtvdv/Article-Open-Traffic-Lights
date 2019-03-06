##  Conclusion
{:#conclusion}

Cities can use the Open Traffic Lights [ontology](#ontology) to publish their traffic lights data in a semantically interoperable way.
A TCS Open Data interface following the proposed [specification](#specification) publishes every second one update. This lowers the barrier for Open Data re-users to create visualizations on top of it: they only have to retrieve the latest observation as fast as possible. Still, it is possible to create a more intelligent client that calculates a client-side count-down.
While this can improve the user experience, another information resource would have to be created to inform about priority updates (such as when an ambulance or police car influences the plan of the TCS).

This early work is open to feedback from other cities that want to publish TCS data.
In earlier work, we proposed a [Linked Times Series interface](cite:cites opendataflanders) as part of the publishing strategy for Flanders.
In this paper, archives are able to download the historic data of cities through its hypermedia links, and optimize storage for tape storage.
By linking the archived fragments in a similar way the archive is activated as an Open Data extension of the interface.
In future work, we will work on improving the discoverability of traffic lights datastreams by reusing the [Semantic Sensor Network](cite:cites compton2012ssn) ontology and the [Vocabulary and Catalog for Linked Streams](cite:cites tommasini2018vocals). Also, we will explore how Memento TimeMaps compare to our time sorted Linked Data Fragments solution.
Furthermore, we will benchmark HTTP polling versus publish/subscribe to have a better understanding how the speed of sensor observations impacts the server infrastructure needed to guarantee and acceptable end-user latency for the live updates.

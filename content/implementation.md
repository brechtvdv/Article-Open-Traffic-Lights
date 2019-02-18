## Open Traffic Lights
{:#implementation}

The [Open Traffic Lights](https://opentrafficlights.org) project started from the need to publish the traffic lights data from the [Smart Zone](https://www.imeccityofthings.be/nl/smart-zone) in [Antwerp](https://www.openstreetmap.org/#map=19/51.21205/4.39717) as Open Data. By using the [Resource Description Framework]() (RDF) as a common model for representing knowledge, sensor observations are syntactically interoperable and can be integrated into one Knowledge Graph. To enable this for traffic lights observations, an ontology is needed to describe the signal timing and how this timing influences the intersection.

The ontology is based on two Flemish profiles: the MapData (MAP) and the Signal Phase and Timing (SPAT) profile. MAP focuses on describing the topology of an intersection, while SPAT describes the phase that a traffic light adheres to. Both profiles are conform European Telecommunications Standards Institute (ETSI) standards: [ETSI 103 301](https://www.etsi.org/deliver/etsi_ts/103300_103399/103301/01.01.01_60/ts_103301v010101p.pdf), [ETSI TS102 894-2](https://www.etsi.org/deliver/etsi_ts/102800_102899/10289402/01.01.01_60/ts_10289402v010101p.pdf), but are not available under an Open license. 

The MAP and SPAT messages from the Smart Zone get sent through a closed message broker ([MQTT](https://mosquitto.org/)) with a frequency of 200ms, because the Traffic Control System of the intersection recalculates every 200ms. In the [specification](#Specification) section, we will describe how the amount of data messages can be optimized for Open Data publishing and how historical information is still retrievable, in contrast to the broker interface.

### Ontology
 {:#ontology}

The Open Traffic Lights ontology is currently scoped to the data that is currently published by the Smart Zone. The ontology is publicly available under an Open license: [https://w3id.org/opentrafficlights#](https://w3id.org/opentrafficlights#) with prefix otl. [](#otl-ontology) shows an overview of all the supported classes and properties that are defined.

<figure id="otl-ontology">
<center>
<img src="img/otl-ontology.svg">
</center>
<figcaption markdown="block">
Classes and properties for describing the connection between lanes and a signalgroup that has a certain signal phase and timing.
</figcaption>
</figure>

The MAP profile defines the lane topology of an intersection: according to the driving direction of the road user the lane that goes towards the conflict area of the intersection is called a _otl:departureLane_, mutatis mutandis for the _otl:ArrivalLane_. When a road user can manoevre from a departure lane towards one or more arrival lanes than this is called a _otl:Connection_. 

A connection is subject to a traffic light in the physical world which represents a certain _otl:SignalState_. The SPAT profile coins the term _otl:SignalGroup_ for the collection of traffic lights sharing the same signal state. This state is characterized with following relations:

* **otl:signalPhase**: points to a [SKOS concept](http://www.w3.org/2004/02/skos/core#Concept
) that represents the signal phase. This concept can be represented with a color (green, orange pinking etc.).
* **otl:minEndTime**: the earliest time that the signal phase will change. 
* **otl:maxEndTime**: the maximum time that the signal group will remain in this signal phase.

In the SPAT profile, the signal phase is described using a text field, e.g. 'protected-Movement-Allowed' which means that a road user can safely cross the intersection (green light). To allow semantic interoperability with foreign countries, we made a taxonomy of possible signal phases which can be dereferenced by HTTP clients. The taxonomy is publicly available at [https://w3id.org/opentrafficlights/thesauri/signalphase](https://w3id.org/opentrafficlights/thesauri/signalphase) under an Open license.

In next section, we will describe a Web Application Programming Interface ([API](https://en.wikipedia.org/wiki/Application_programming_interface)) specification to publish traffic light observations for Open Data re-use. 

### Specification
{:#specification}

The specification contains three aspects:

* how every traffic light observation should be described,
* how the server interface should expose the live observations,
* how historical observations should be published

Every observation _must_ be defined using [instantaneous graphs (iGraphs) and stream graphs (sGraphs)](cite:cites barbieri2010proposal). The iGraph contains the observated content, in this case the signal phase and timing of signal group(s). The sGraph describes metadata about the observation: when the observation is generated. [](#example-observation) shows an example observed at 2018-10-31T14:58:23.205Z for signal group *https://opentrafficlights.org/id/signalgroup/K648/6*. 
The original SPAT messages are sent every cycle time of the Traffic Control Sytem. For the intersection of Antwerp this is every 200 ms resulting in 5 observations per second. A server _must_ calculate the final outcome that an end-user will see: the minimum and maximum time in seconds that a signal group will stay in its phase. This results in the generation of one observation per second.

<figure id="example-observation" class="listing">
````/code/example-observation.txt````
<figcaption markdown="block">
Observation that signal group 6 has a certain state at 2018-10-31T14:58:23.205Z.
</figcaption>
</figure>

There are two main strategies to publish live data: a publish/subcribe system where an observation gets pushed to the client and HTTP polling where the client pulls a Linked Data Fragment repeatedly. 
The data publisher _must_ offer HTTP polling and _should_ offer pub/sub:

* **HTTP polling**: a Linked Data Fragment which is a HTTP document containing one or more of the most recent observations (e.g. _https://lodi.ilabt.imec.be/observer/rawdata/latest _). An _ETag_ header must be added to enable HTTP caching.
* **publish/subscribe**: every update corresponds with one observation like [](#example-observation). Preferably, HTTP-based [Server-Sent Events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events) _should_ be chosen.

Historical data is similarly published like the HTTP polling fragment of live data, but contains a collection of past observations. [](#timeseries) shows that all observations are ordered on a time axis. To allow a HTTP client to automatically discover older observations, a _hydra:previous_ link _must_ be added. _Hydra:next_ links _should_ be added to allow time range retrieval in both directions. Also, the URL of the fragment is identified using the datetime of it's first observation, e.g. https://opentrafficlights.org/spat/K648?time=2018-10-31T14:58:23.205Z.

<figure id="timeseries">
<center>
<img src="img/timeseries.svg">
</center>
<figcaption markdown="block">
Timeseries are published as a paged collection of time sorted Linked Data Fragments. 
</figcaption>
</figure>

Another feature that server _must_ expose is *[templated links](https://www.hydra-cg.com/spec/latest/core/#templated-links)* using the Hydra vocabulary: a client should be able to construct a URL to retrieve the fragment that contains observations around a certain *time*. [](#templated-link) gives an example of this control. The server _must_ redirect with a HTTP 302 status code to the closest fragment that has a timestamp before *time*. When there is no fragment before *time*, the last fragment gets returned.

<figure id="templated-link" class="listing">
````/code/templated-link.txt````
<figcaption markdown="block">
A client can search for observations with a datetime as input.
</figcaption>
</figure>

Finally, following metadata _must_ be added to every fragment:

* the **topology** of the intersection (MAP): if available, the identifiers of lanes of the local authorities should be re-used. Otherwise, a lane should be defined and use _http://purl.org/dc/terms/description_ and _http://www.opengis.net/#geosparql/wktLiteral_ to allow humans and machines to select the relevant lane.
* an Open **license** such as [CC0](https://creativecommons.org/publicdomain/zero/1.0/)

<!-- Linked Data Fragments? -->

In next section, a strategy will be proposed for long-term preservation of these data.

### Preservation strategy
{:#preservation}

One observation per second is published with our specification. Given that one observation for one intersection correponds with circa 7 kilobytes, this generates more than a half gigabyte per day. It is important that inactive data is removed from the Open Data API to keep it light-weight, however, these should still be available for retrieval. 

Storage solutions tape and disk require a different approach for preserving traffic lights data. As discussed in the background, tape is cost-efficient for large files. To circumvent this, Linked Data Fragments can be merged into one bigger Linked Data Fragment. This means that not the exact bytes are preserved, but only the statements. Validating with [_graph isomorphism_](cite:cites carroll2002matching) is not possible as the merged graph contains more statements than the graphs that needs to be compared with, but the ideas of generating an equivalence mapping between blank nodes can be re-used for statements preservation. With bigger fragments archiving traffic lights data on tape becomes feasible. For disk archives, there is no need to create bigger files, thus archiving can be done traditionally.

An access point should be exposed by the archive that redirects to the archived document with the most recent observations. [](#timeseries-archive) shows that the last document of the Open Data API points, through the access point, to the archived documents. The archive can continously update by downloading the documents the same way as an Open Data re-user.

<figure id="timeseries-archive">
<center>
<img src="img/timeseries-archive.svg">
</center>
<figcaption markdown="block">
An archive can harvest the historical observations, optionally merge the Linked Data statements of multiple documents into one document, and link them together through previous links.
</figcaption>
</figure>





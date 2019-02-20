<div class="printonly">This is a print-version of a paper first written for the Web. The Web-version is available at https://brechtvdv.github.io/Article-Open-Traffic-Lights</div>

## Introduction
{:#introduction}

Sensors are progressively getting installed in the public domain by cities. This is motivated to attain better data-driven policies, thus becoming a smarter city. Sharing mobility data is crucial due to the rising of new transport modi (steps, shared cars etc.) and the desire to achieve more sustainable traffic planning.

Traffic lights, the first one already dating from [1868](https://en.wikipedia.org/wiki/Traffic_light), are being converted into Internet connected devices, so called intelligent Traffic Control Systems (TCS). In the Netherlands, hundreds of these TCSs are already [converted](http://www.nm-magazine.nl/artikelen/talking-traffic-applicaties-voor-de-ivri/) through the public-private coorporation [Talking Traffic](https://www.talking-traffic.com/nl/). A centralized approach using asynchronous messaging is implemented with the Traffic Live Exchange ([TLEX](https://www.talking-traffic.com/nl/nieuws/stem-op-tlex)) system which distributes data between TCSs and the end-user in both directions. In the city of Antwerp (Belgium), one geographical [zone](https://www.imeccityofthings.be/nl/smart-zone) is accommodated with different kinds of sensors to conduct experiments, such as the publication of it's traffic lights data that is described in this paper.

Traffic lights [data standards](https://www.etsi.org/deliver/etsi_ts/103300_103399/103301/01.02.01_60/ts_103301v010201p.pdf) are already created by the European Telecommunications Standards Institue (ETSI), but identifiers are scoped to the intersection, region or country. With Linked Data ([section 2]()), traffic light streams become interoperable worldwide and allows decentralized data publishing. This would allow routeplanners to discover traffic lights data from other datasets, e.g. the road network.

<!-- Describe archiving need -->
Web archives are increasingly re-used by scholars in the social sciences and humanities for studying phenomena [](cite:cites eveline2019webarchiving). In [section 3](#preservation), we propose a method how these archives also can preserve sensor observations and allow linking from the Open Data publisher to the archive. This way, digital scholars and cities can study phenomena of the city's digital pulse.

This paper describes some background in [section 2](#background). Next, the contributions of the Open Traffic Lights project are explained in [section 3](#implementation). A end-user application is showcased in [section 4](#demonstrator). Finally, we discuss our conclusions in [section 5](#conclusion).
## Introduction
{:#introduction}

Sensors are progressively getting installed in the public domain by cities. The placement of these sensors are motivated to attain better data-driven policies, thus becoming Smart Cities. Sharing mobility data is crucial due to the rising of new transport modi (steps, shared cars etc.) and the desire to achieve smart traffic planning.

Traffic lights, the first one already dating from [1868](https://en.wikipedia.org/wiki/Traffic_light), are being converted into Internet connected devices, so called intelligent Traffic Control Systems. In the Netherlands, hundreds of these TCSs are already [converted](http://www.nm-magazine.nl/artikelen/talking-traffic-applicaties-voor-de-ivri/) through the public-private coorporation [Talking Traffic](https://www.talking-traffic.com/nl/). A centralized approach using asynchronous messaging is implemented with the Traffic Live Exchange ([TLEX](https://www.talking-traffic.com/nl/nieuws/stem-op-tlex)) system which distributes data between TCSs and the end-user in both directions. In the city of Antwerp (Belgium), one [area](https://www.imeccityofthings.be/nl/smart-zone) is provided with different kinds of sensors, such as the traffic lights from one intersection, to conduct experiments.

Traffic lights [datastandards](https://www.etsi.org/deliver/etsi_ts/103300_103399/103301/01.02.01_60/ts_103301v010201p.pdf) are already created by the European Telecommunications Standards Institue (ETSI), but identifiers (e.g. topology of the intersection) are scoped to the intersection, region or country. With Linked Data ([section 2]()), traffic light streams become interoperable worldwide and allows decentralized data publishing, e.g.: TCS maintainers can have an up-to-date intersection topology from the maintainers of the road network.

<!-- Describe archiving need -->

This paper describes the contributions of the Open Traffic Lights project in [section 2](#implementation). A end-user application is showcased in [section 3](#demonstrator). Finally, we discuss our conclusions in [section 4](#conclusion).
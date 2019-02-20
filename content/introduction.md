## Introduction
{:#introduction}

Smarter cities try to make more evidence-based decisions based on, for instance, sensors installed in the city.
In the case of sensors, not only the live values are important, also historical values need to be preserved and available.
This is government data and policy decisions world-wide – such as open by default, the freedom of information act or the public sector information directive – mandate that government data must be made freely available to everyone.
When historic values of smart city datasets become available, everyone can join an evidence-based debate on the city’s future.

The first traffic light was installed in London in [1868](https://en.wikipedia.org/wiki/Traffic_light).
Today, Traffic Control Systems (TCS) do not differ much from the model installed 1.5 centuries ago, yet we can imagine the potential of making TCSs internet-connected and making traffic light statuses available as Open Data.
Not only self-driving cars may benefit, also cyclists seeking green lights on a rainy day, or a citizen willing to analyze the crossroad’s efficiency near their home.
In the Netherlands, [hundreds of these TCSs are already converted](http://www.nm-magazine.nl/artikelen/talking-traffic-applicaties-voor-de-ivri/) through the public-private coorporation [Talking Traffic](https://www.talking-traffic.com/nl/).
A centralized approach using asynchronous messaging is implemented with the Traffic Live Exchange ([TLEX](https://www.talking-traffic.com/nl/nieuws/stem-op-tlex)) system which distributes data between TCSs and the end-user in both directions.
The data so far has not been published publucly, but only been made available in partner applications for end-users.
In the city of Antwerp (Belgium), one geographical [zone](https://www.imeccityofthings.be/nl/smart-zone) is accommodated with different kinds of sensors to conduct experiments, such as the publication of its traffic lights data that is described in this paper.

Traffic lights [data standards](https://www.etsi.org/deliver/etsi_ts/103300_103399/103301/01.02.01_60/ts_103301v010201p.pdf) are already created by the European Telecommunications Standards Institue (ETSI), yet identifiers are scoped to the intersection, region or country. With Linked Data ([Section 2]()), traffic light streams may become interoperable worldwide and may allow for a decentralized data publishing strategy.
This way, any client, whether it is a route planners, a self-driving car or a data analyst, can follow links to and from other datasets while querying.

Preserved data from among others these TCSs can be used by digital scholars, citizens and cities to study the city’s digital pulse.
Such Web archives are already used by scholars in, among others, the social sciences and humanities for studying phenomena [](cite:cites eveline2019webarchiving).
In this paper, we propose a publishing strategy for data from TCSs, and zoom in on the aspect of preservation.

The state of the art is described in [Section 2](#background).
In [Section 3](#preservation), we propose a method how these archives also can preserve sensor observations and allow linking from the Open Data publisher to the archive.
Next, an end-user application with code-snippet is demonstrated in [Section 4](#demonstrator).
Finally, we discuss our conclusions in [Section 5](#conclusion).

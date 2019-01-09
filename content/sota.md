##  State Of The Art
{:#sota}

### Comunica

Every piece of functionality in Comunica can be implemented as seperate building blocks based on the _actor_ programming model, where each actor can respond to a specific action. Actors that share same functionality, but with different implementations, can be grouped with a communication channel called a _bus_. Interaction between actors is possible through a _mediator_ that wraps around a bus to get an action's result from a single actor. This result depends on the configuration of the mediator, e.g. a race mediator will return the response of the actor that is able to reply the earliest.

<figure id="actor">
<center>
<img src="img/actor-mediator-bus.svg">
</center>
<figcaption markdown="block">
Actor 0 initiates an action to a mediator. The mediator communicates through a bus with all actors 1, 2 and 3 that are able to solve the action and gives back the most favorable result according to its configuration.
</figcaption>
</figure>

### Hydra partial collection views


## Demonstrator
{:#demonstrator}

This application shows live traffic lights data of the intersection in [Antwerp](https://www.openstreetmap.org/#map=19/51.21205/4.39717). The source code can be found as a Codepen at [https://codepen.io/brechtvdv/pen/BMQPNX/](https://codepen.io/brechtvdv/pen/BMQPNX/). The dataset is freely available under an Open License at [https://lodi.ilabt.imec.be/observer/rawdata/latest](https://lodi.ilabt.imec.be/observer/rawdata/latest).

First, a user can select a departure and arrival lane, indicating how the intersection will be crossed.
The departure and arrival lane describe an _otl:Connection_ that can be selected from this  information.
A live count-down of the traffic light that is responsible for the chosen otl:Connection is shown.
The count-down is calculated with the minimum ending time of the state (current time - otl:minEndTime). The bigger then ‘>’ sign indicates that the minimum and maximum end time are not equivalent, thus it is uncertain when the signal state ends. 
Note that this application uses HTTP polling every 100 milliseconds.

Underneath the count-down, a historic ‘time-to-green’ is shown. The line chart represents how many seconds a user had to wait before getting a green light. The horizontal lines correspond with a waiting time of 0 seconds, and thus corresponds with a green light.

<figure id="codepen">
<center>
<img src="img/codepen.PNG">
</center>
<figcaption markdown="block">
Visualisation of the live count-down and the amount of seconds to wait before having a green light. Notice that the horizontal lines correspond with green times.
</figcaption>
</figure>

<p class="codepen" data-height="510" data-theme-id="0" data-default-tab="result" data-user="brechtvdv" data-slug-hash="BMQPNX" style="height: 510px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="Time to Green">
  <span>See the Pen <a href="https://codepen.io/brechtvdv/pen/BMQPNX/">
  Time to Green</a> by Brecht Van de Vyvere (<a href="https://codepen.io/brechtvdv">@brechtvdv</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Demonstrator
{:#demonstrator}

This demonstrator will show that a user can use Comunica to create a data dump from hetarchief.be. More specifically, a spreadsheet can be extracted from Hydra paged collection views using SPARQL querying. The application is written in the front-end playground Codepen [https://codepen.io/brechtvdv/pen/ebOzXB](https://codepen.io/brechtvdv/pen/ebOzXB). The custom Comunica configuration can be found on Github (https://github.com/brechtvdv/hetarchief-comunica) under an open license. 

<figure id="codepen">
<center>
<img src="img/codepen.PNG">
</center>
<figcaption markdown="block">
TODO
</figcaption>
</figure>

A user can insert a URL that serves as an access point of the dataset. After pressing the "Start download" button, the browser compatible version of Comunica starts fetching the access URL and all other webpages it can find through embedded hypermedia controls. Also the user can set a SPARQL-query to select the data for the columns in the spreadsheet. While fetching, results get streamed back and can be copied to a spreadsheet software.

<p data-height="542" data-theme-id="0" data-slug-hash="ebOzXB" data-default-tab="result" data-user="brechtvdv" data-pen-title="Converteren van website naar spreadsheet" class="codepen">See the Pen <a href="https://codepen.io/brechtvdv/pen/ebOzXB/">Converteren van website naar spreadsheet</a> by Brecht Van de Vyvere (<a href="https://codepen.io/brechtvdv">@brechtvdv</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
# Meteor route transities
Meteor, het development platform waar veel over gesproken is de laatste maanden. Binnen de minor zijn de meningen verdeeld. Een platform dat uit zo veel libraries en packages bestaat, dat je nauwelijks weet wat het doet. Dat kan op de lange termijn geen goede oplossing zijn.
Ik zal het eerlijk toegeven, ik ben ontzettend fan van Meteor. Voor iemand die tot 5 maanden geleden nog nooit een API call had gedaan is het perfect. Op hoog tempo een platform kunnen bouwen, geen weken versplinnen aan het ontwikkelen van een gebruikerssysteem. Fantastisch. 

Nu begrijp ik ook wel dat het missen van de juiste kennis niet een goed argument is om een bepaalde toolset te kiezen voor een project. Of Meteor een oplossing is waar je jaren op kunt bouwen betwijfel ik, maar voor het bouwen van snelle prototypes is het een uitkomst. 

Na 5 weken intensief met Meteor te hebben gewerkt durf ik wel te zeggen dat ik het systeem goed begrijp. Meteor zelf is een combinatie van verschillende libraries en packages. Aan de basis kun je niet veel aanpassen, maar het idee is dat je naar wens zelf packages toevoegd, zodat het het juiste aansluit bij jou doelstelling.  

## Pagina transities
Transities tussen pagina's worden al veel gebruikt in mobiele applicaties. Google's Material Design maakt hier vele gebruik van. Een goede pagina transitie kan de user experience verbeteren doordat de gebruiker het gevoel heeft dat zij door de applicatie heen 'flowt'. Daarnaast geeft het de ruimte om content te laden, zonder dat de gebruiker enkele milisecondes naar een laadscherm hoeft te kijken. De transities tussen pagina's kunnen ook suggesties geven voor het gebruik van gestures. 

Genoeg redenen dus om hier eens verder in te duiken, en te kijken of dit met Meteor gebouwd kan worden. Meteor zou Meteor niet zijn, als hier geen package voor was, en _flow-transition_ lijkt de juiste voor de taak._flow-transition_ maakt gebruik van  _flow-router_ en _VelocityJS_, een animatie library die gebruik maakt van dezelfde API als Jquey's _$.animate()_

## Demo
Voor de uitleg heb ik een kleine demo gebouwd, bestaande uit 2 pagina's. De homepage, waar een lijst met artikelen te zien is, en een detail-pagina, waar de content van het artikel te vinden is.

Ik ga er vanuit dat Meteor al geinstalleerd is, start een nieuw project door het volgende in te typen:
```
meteor create blog
cd blog
```
Vervolgens zullen we Flowrouter en flow-transition moeten installeren.
```
meteor add kadira:flow-router
meteor add mcissel:flow-transition
meteor
```

Voor de demo zullen we een aantal templates aan de door meteor gegenereerde `client/main.html` toevoegen. Omdat dit een demo betreft zullen we ons niet druk maken om de juiste filestructuur.

```
<body>
  <header>
    {{> Template.dynamic template=header}}
  </header>
  <main>
    {{> Template.dynamic template=body}}
  </main>
</body>

<template name="home">
  <ul>
    {{#each articles}}
      <li>
        <a href="/article/{{id}}">
          <span>{{title}}</span>
          <time>{{getDate}}</time>
        </a>
      </li>
    {{/each}}
  </ul>
</template>

<template name='article'>
  <article>
    <header>
      <img src="{{article.img}}" alt="">
      <h2>{{article.title}}</h2>
    </header>
  <section class="begin">
    <p>{{article.contentHeader}}</p>
  </section>
  <section>
    <p>{{article.content}}</p>
  </section>
  </article>
</template>

```

Zoals je ziet is er een layout aangemaakt, met daarin een template home, waarin de lijst met artikelen wordt weergegeven, en een template voor een detail pagina voor het artikel, waar de tekst wordt weergegeven. Om het allemaal wat gezelliger te maken voegen we ook wat styling toe aan main.css
```
/* CSS declarations go here */
html, body {
	font-family: helvetica, sans-serif;
	margin: 0 0;
}
body > header {
	background: #1abc9c;
	color:white;
	padding:.8em;
	text-align: center;
	box-shadow: 0px 10px 41px 0px rgba(0,0,0,0.1);
}
 header a {
	position: absolute;
	top:1em;
	left:.8em;
	text-decoration: none;
	border:2px solid white;
	padding:.3em 1em;
	color:white;
}
h1, h2, h3 {
	font-weight: normal;
	margin: 0 0;
}
ul {
	list-style: none;
	padding : 0 0;
	margin: 0 0;
}
ul li a {
	color:#4E4E4E;
	display: block;
	padding:.7em 2em;
	border-bottom: 1px solid #ebebeb;
	text-decoration: none;
}
ul a time {
	float:right;
}
article header {
	text-align: center;
	background: #ebebeb;
	color:black;
}
article h2 {
	padding:1em;
}
article img {
	width:100%;
	/*max-width: 40em;*/
}
section.begin {
	font-weight: bold;
}
article p {
	margin:.5em auto;
	max-width: 35em;
	padding:.5em;
}
```
Prachtig. Nu is het tijd om de router aan de praat te krijgen, zodat de pagina's daadwerkelijk te zien zijn. in `client/main.js` plaatsen we het volgende:
```
FlowRouter.route("/", {
    name: "home", // required
    action: function() {
      BlazeLayout.render({head:'header', body: "home"});
    }
  });

  FlowRouter.route("/article/:id", {
    name: "article", // required
    action: function() {
      BlazeLayout.render({head: "header"}, {body: "article"});
    }
  });
  ```
  De templates worden aan de routes gekoppeld. Als je nu naar de localhost gaat waar de applicatie op draait, zul je de geselecteerde templates te zien krijgen. 
  Om de pagina transities toe te voegen verwijder je de regels 
  ```
   BlazeLayout.render({head: "header"}, {body: "article"});
   ```
   en plaats je op die plek 
   ```
   FlowTransition.flow({head: "header"}, {body: "article"});
   ```
   Hier stel je de transitie vast. Deze moet echter nog wel gedefinieerd worden. Dit doe je op de volgende manier:
   ```
 FlowTransition.addTransition({
  section: 'body',
  from: 'home',
  to: 'article',
  txFull: 'left'
});
```
* section: de plek die geanimeerd gaat worden. In dit geval is dit de `<body>` 
* from: vanaf deze route wordt de transitie uitgevoerd.
* to: hier gaat de transitie naartoe.
* txFull: in dit geval een vooringestelde transitie

Als je nu vanaf home op een artikel klikt, wordt de transitie uitgevoerd en zie je de nieuwe pagina inschuiven. Ga je terug, gebeurt er echter niets. Je zult dus voor elke kant een _Flowtransition_ aan moeten geven.  

### Zelf transities maken
aan `txFull` kun je opties toevoegen. Denk hierbij aan duration, easing en fallback functions. De transitions worden opgebouwd uit hooks, waarbij er gebruik gemaakt wordt van CSS properties. Voor een volledige lijst van de css properties die ondersteund worden heeft Valocatiy een [animation tester](http://codepen.io/julianshapiro/full/oHaCy/).

```
FlowTransition.addTransition({
  section: 'body',
  from: 'article',
  to: 'home',
  txIn: {
    hooks: {translateY: '-100%', backgroundColorBlue: '100%'},
    properties: {translateY: [0, '-100%'], backgroundColorBlue:['de ', 0]},
    options: {
      duration: 220,
      easing: 'easeOutCirc',
      queue: false,
      complete: function() {
        console.log('Transitie is klaar!');
      }
    }
  }
});
```
De bovenstaande transitie zorgt er voor dat de nieuwe pagina van boven naar binnenschuift en begint met een blauwe achtergrond. 

## afsluiting
Doordat FlowTransition gebruik maakt van CSS properties opent het een wereld van mogelijkheden voor paginatransities. Daarnaast is het toepassen ook erg gemakkelijk, en dus goed toe te passen met prototypes.

### bronnen:
* https://www.smashingmagazine.com/2016/07/improving-user-flow-through-page-transitions/
* https://libraries.io/meteor/mcissel:flow-transition
* http://velocityjs.org/
* https://material.google.com/motion/material-motion.html#material-motion-why-does-motion-matter
* https://material.google.com/motion/material-motion.html

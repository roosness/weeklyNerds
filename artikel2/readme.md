# Maintainable CSS

Voor mij begint ieder web project hetzelfde. Een goede filestructure, een planning, en de mentaliteit ‘deze keer ga ik het echt netjes houden’. En toch. Elke keer. Deadlines naderen, projecten worden groter, herontwerpen, opnieuw opbouwen, delen weggooien, ga zo maar door. Aan het eind van het project is de filestructure waar ik ooit zo trots op was volledig verdwenen, en heeft ze plaats gemaakt voor tientallen bestanden, die allemaal iets met elkaar te maken hebben, maar geen duidelijke relatie hebben. 

Een van de grote boosdoeners hierin is de CSS. Bij CSS is alles globaal, waar door het in feite bijna altijd werkt. 

```
button {
    background-color:blue;
}
```
Het bovenstaande voorbeeld zal er overal voor zorgen dat de `<button>` blauw is, tenzij anders wordt aangegeven. Het maakt niet uit of dit in `main/style.css` zit, of in `template/header/tinyheader/stylesheets/tinyheader.css`, overal is de `<button>` blauw.
Dit globale CSS systeem is er op gericht om in documenten te werken, waarbij je bij iedere html pagina een aparte stylesheet zou kunnen aanroepen. Maar in dit tijdperk van web applicaties, waarbij alles elkaar dynamisch (en soms zelfs real time) oproept, is dit niet meer praktisch. 
Bij elke verandering in een CSS bestand kan dit gevolgen hebben voor een totaal andere pagina. 

## modulaire css
Met de komst van `@import` en Sass is er een wereld van mogelijkheden open gegaan. Hoewel CSS nogsteeds globaal blijft, is het nu mogelijk om zelf te bepalen wanneer bepaalde CSS bestanden aangeroepen worden, en waneer niet. Voor mijn laatste project heb ik de CSS zo georganiseerd:
```
#stylesheets
    /globals
        /all.scss
        /color.scss
        /typography.scss
        /variables.scss
    /helpers
        /mixins.scss
    /partials
        /buttons.scss
        /lists.scss
        /forms.scss
        /popups.scss
    /pages
        /home.scss
        /detail.scss
    /layout
        /main.scss
        /footer.scss
```

### Globals
Hier wordt de css bewaard die overal gebruikt zal worden. 
Vooral de `color.scss` is een uitkomst. Wil ik een kleur aanpassen in het complete project, hoef ik enkel hier een nieuwe rgba toe te voegen, en de kleur veranderd overal. Daarnaast zorgt het ook voor een consistent kleurenpallet, in plaats van 50 tinten grijs.
Hetzelfde geld voor de `typography.scss` en `variables.scss` .
In de variables worden de globale variabelen bewaard. Denk aan bepaalde margins en paddings, maar ook π, om het gehele project aan de golden ratio te kunnen laten voldoen.
### Helpers
Vergelijkbaar met globals, maar hier gaat het meer om functies en mixins. De bestanden hier zullen dus niet altijd gebruikt worden, maar wel vaak.
### Partials
Hier komt alles samen. Styling van buttons, forms, en andere elementen kunnen hier toegevoegd worden.
### Layout
De globale layout en positionering wordt hier gemaakt. 
### Pages
Mocht er toch nog wat per pagina gestyled worden gebeurt dat hier, maar ik probeer zoveel mogelijk in de partials map te doen. Zo blijft de styling globaal, en vermijd je de kans op inconsistente vormgeving.

Door deze opzet aan te houden zal het gemakkelijk zijn om op later moment nog aanpassingen te maken. Nu nog maar hopen dat het mij gaat lukken het schema aan te houden, en er zelf geen rotzooi van te maken..
## Bronnen
* https://smacss.com/
* https://www.sitepoint.com/architecture-sass-project/

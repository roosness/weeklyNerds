# De 5 dingen waar ik het meeste van heb geleerd tijdens everything web

De minor 'Everything Web' bijna afgerond. Tijd om [emotionele achtergrondmuziek](https://www.youtube.com/watch?v=F2xoJoO_XcY) te draaien, je beeldscherm op zwart/wit in te stellen en terug te denken aan alles wat er wel niet voorbij is gekomen. Alles? Nee, maar zeven. Zeven is een magisch getal.

## #1: Promises
Promises! Als iemand die nog maar net haar eerste AJAX call had gemaakt waren promises echt een uitkomst. Het mij dan ook heel veel pijn en moeite gescheeld als ik er net iets eerder over na had gedacht om "Promises" op google in te tikken. Het hele async-sync fenomeen was ook nog nooit in mijn hoofd opgekomen. Superfijne oplossing dus!

```
var request = function(url) {
  var p1 = new Promise(function(res, rej) {
    var req = new XMLHttpRequest();
    req.open('GET', url);
    req.onload = function() {
    if(req.status == 200) {
        res(req.response);
        }
        else {
        rej(Error(req.statusText);
    }
    req.send();
  });
}
p1.then(function(res) {
    console.log('succes', response);
}, function (err) {
    console.log('error: ', error);
    });
}
request('data.json');
```

## #2 Discussies met medestudenten
Naarmate de weken vorderde en de nachten korter werden kwam ik er langzaam achter. Ga geen discussies aan met medestudenten. De studenten van deze minor zijn in mijn ogen de meest fanatieke die ik ooit ontmoet heb. Waar anderen het tijdens de borrels het voornamelijk over elkaar, zichzelf, en het aankomende festivalseizoen hebben, is dat bij EW wel anders. Hier wordt gesproken over toekomstplannen die verder gaan dan 'dat papiertje halen', over klanten die er niets van snappen, en vooral heel erg veel over alles wat met internet te maken heeft.

Ergens in de eerste weken heb ik per ongenluk laten blijken dat ik stiekem fan ben van frameworks en libraries. Een standpunt waar je dan _natuurlijk_ de complete minor achter moet blijven staan. We hebben het er minstens wekelijks over gehad, soms wel dagelijks. 'Maar dit is ruk!' en 'dat kunnen we zelf veel beter!' zijn zinnen die dan rondgeslingerd worden. Ik kan er niet meer omheen. Er wordt met een hoeveelheid aan goed onderbouwde argumenten gegooid waar je u tegen zegt. Ik ben overtroffen, niet overtuigd. Maar ik ga zeker niet nog een keer de discussie aan.

## #3 Shortcut notations
Shortcut notations. Ik heb het eerder langs zien komen, maar er nooit echt onderzoek naar gedaan. Tot de meesterproef. Bij de zoveelste `if(){}else{})` en 30 `switch`-cases moest ik er toch echt aan geloven.

### if, else
een lange lelijke code als 
```
var number = Math.floor(Math.random() * 20);
if(number > 10){
    return 'High!'
} else {
    return 'low'
}
```
kan vele malen korter geschreven worden als:
```
var number = Math.floor(Math.random() * 20);
return (number > 10) ? 'high' : 'low';
```

### for loops
langer:
```
for(var i = 0;i<items.length;i++) {
...
}
```
korter:
```
for(var i in items) {
...
}
```
### switch cases
langer:
```
switch(kleuren) {
    case: 'rood':
        getRood();
        break;
    case 'blauw':
        getBlauw();
        break;
}
```
naar:
``` 
    var kleuren = {
        'rood': getRood,
        'blauw': getBlauw
    }
    kleuren[kleur]();
```
    
## #4 CSS (selectoren) zijn de bom
'De Bom' is misschien een beetje over enthousiast, maar de hoeveelheid manieren om bepaalde elementen te berijken is overweldigend. Sinds het vak 'CSS to the rescue' probeer ik zelf zo min mogelijk classes en id's als selectoren te gebruiken. Daarnaast ben ik mijzelf steeds meer gaan verdiepen in alle mogelijkheden van CSS, die ook oneindig zijn.
Ik hoop dan ook een stage te vinden die een combinatie van front end en ux doet, met een neiging naar motion design. 

## #5 Semantics are everything
Dat semantiek belangrijk was is natuurlijk vanuit de P er al ingepepert. Maar sinds het gastcoll
1. basketbal

3. discussies
4. meningen
5. real time
6. this
7. console.table
8. screenreaders


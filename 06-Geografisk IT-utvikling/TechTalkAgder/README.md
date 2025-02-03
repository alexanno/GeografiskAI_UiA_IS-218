# Tech Talk Agder - Geografisk IT

## Tema
* Demo: QGIS og ogr2ogr - swiss army knife
* ~~AgderKI-demo: geopandas~~
* Demo: KeplerGL
* Demo: Maplibre
* Workshop: Leaflet
* ~~Geografiske økosystemet i Norge - for Nerder~~

## GIS-verktøy og standarder

**Åpne datasett**
* https://naturalearthdata.com/
* https://geojson.xyz/
* https://www.geonorge.no/

**Projeksjoner**

Geografiske data er annerledes enn rene tabulariske data. Vi trenger å representere geografiske objekter i virkeligheten på en matematisk måte. Jorden er rundt, kartet er flatt. For å representere en 3D-kule som 2D-kart finnes det _projeksjoner_. Det finnes mange ulike, med forskjellige egenskaper. 

[NRK - Kartet er feil](https://www.nrk.no/trondelag/xl/verdenskartet-med-mercator-projeksjon-viser-feil-storrelse-pa-landene-1.17080439)

[Advent of GIS - Projeksjoner](https://github.com/Norkart/AdventOfGIS/blob/2023/01/README.md)

Det finnes mange verktøy som håndterer projeksjoner. Det viktigste er å ikke _blande_ for mye projeksjoner. Det blir fort skrekkelig feil. 

**Dataformater og GeoJSON**

GeoJSON er en utvidelse av JSON som håndterer geografiske data. GIS-verden har ekstremt mange ulike formater. GeoJSON er et av de aller mest brukte i "geografiske-IT-verden". Siden det er vanlig JSON er det god støtte i de fleste språk og biblioteker. 

På https://geojson.io/ kan du "tegne" egne GeoJSON og laste ned i ulike formater for å teste. 

**GIS-programvare: QGIS**

QGIS er en klassisk GIS-desktop-programvare. QGIS støtter "alt", og er praktisk for å "debugge" geografiske data, tjenester og teste analyser m.m.

Vi tar en show&tell intro til QGIS i plenum


## Workshop - webkart

I denne workshopen skal du lære det mest grunnleggende for å programmere en webkart-app. Du må ha installert en kode-editor, fks VSCode, nettleser, og internett. 

Vi skal bruke noen av oppgavene fra fjorårets Advent of GIS som Norkart har. https://github.com/Norkart/AdventOfGIS/blob/2023/. Obs: Noen linker til datasett og API kan være døde i 2023-versjonen. Kanskje kommer det en oppdatert versjon i 2024?

**Oppsett og bakgrunnskart**

Vi skal prøve å løse "Luke 3" i adventskalenderen. Du kan utforske ulike bakgrunnskart/flyfoto med apikeys du får på workshopen og gratistjenester. Bruk enten VSCode lokalt - eller web-editorer som CodePen.

For workshopen anbefaler vi å bruke helt vanilla html/javascript. Leaflet støttes og har wrappere i flere rammeverk når man har behov for det.

Løs [luke 3](https://github.com/Norkart/AdventOfGIS/blob/2023/03/README.md) men bruk URL'er under. Sjekk ut [leaflet.html](./leaflet.html) for jukselapp

Under er en liste med tilecache-strenger. {z}/{x}/{y} er variabler som Leaflet selv finner ut av. Det beskriver tile-matrix-systemet for (som regel) koordinatsystemet EPSG:3857. {apiKey} må byttes til nøkkelen du får på workshopen.
```
https://tile.openstreetmap.org/{z}/{x}/{y}.png

https://tiles.stadiamaps.com/tiles/stamen_toner/{z}/{x}/{y}.png

https://tiles.stadiamaps.com/tiles/stamen_watercolor/{z}/{x}/{y}.jpg

//apiKey får du på workshopen
https://waapi.webatlas.no/maptiles/tiles/webatlas-orto-newup/wa_grid/{z}/{x}/{y}.jpeg?APITOKEN={apiKey}

https://waapi.webatlas.no/maptiles/tiles/webatlas-standard-vektor/wa_grid/{z}/{x}/{y}.png?APITOKEN={apiKey}

https://waapi.webatlas.no/maptiles/tiles/webatlas-1881-vektor/wa_grid/{z}/{x}/{y}.png?APITOKEN={apiKey}
```


**GeoJSON-data i kartet**
Nå skal du legge til egne vektor-data i kartet. Vektordata blir rendret direkte i klienten - og vi kan endre styling, gjøre (enkle) analyser og legge til user events til features i datasettet. 

Oppgave:
1. Legg til en GeoJSON-fil i kartet som hentes med fetch e.l.
1. Endre på stylingen til features
1. Legg til en popup som viser tekst fra properties til featuren

Lag egen GeoJSON-fil fra geojson.io eller bruk ferdig datafiler under:
```
https://adventofgis-data.ams3.digitaloceanspaces.com/ne_10m_populated_places_simple.geojson

https://d2ad6b4ur7yvpq.cloudfront.net/naturalearth-3.3.0/ne_50m_populated_places_simple.geojson

https://d2ad6b4ur7yvpq.cloudfront.net/naturalearth-3.3.0/ne_110m_admin_0_countries.geojson

```

Relevante luker i AoG

* https://github.com/Norkart/AdventOfGIS/blob/2023/02/README.md
* https://github.com/Norkart/AdventOfGIS/blob/2023/04/README.md
* https://github.com/Norkart/AdventOfGIS/blob/2023/08/README.md

Tips til tutorials og datasett:
* https://leafletjs.com/examples/geojson/
* Data: https://www.naturalearthdata.com/
* Data: https://geojson.xyz/
* Data: https://www.openstreetmap.org/
* Data: https://overpass-turbo.eu/
* Data: https://www.geonorge.no/


**WMS-tjenester i kartet**

WMS er en API-standard (OGC-standard) for å hente inn "custom" kartbilder fra en kartserver. WMS-servere rendrer resultatet (ofte) on-the-fly og støtter mye tilpasninger på projeksjoner/koordinatsystemer, styling, datalag m.m.

Løs luke 5: https://github.com/Norkart/AdventOfGIS/blob/2023/05/README.md 

Sjekk ut flere WMS-tjenester her på [GeoNorge](https://kartkatalog.geonorge.no/?DistributionProtocols=WMS-tjeneste&dataaccess=%C3%85pne%20data&spatialscope=Nasjonal)


**GPS-posisjon i kartet**

HTML GeoLocation API gjør at vi kan få GPS-posisjonen til enheten og "tracke" den. Det fungerer aller best på mobile enheter, men støttes OK på desktop-enheter uten GPS.

Oppgave: Hent ut posisjonen til brukeren og lag en markør som viser hvor brukeren er. Prøv først _uten_ plugins i Leaflet.

Relevant luke i AoG: https://github.com/Norkart/AdventOfGIS/blob/2023/07/README.md

HTML5 GeoLocation API: https://www.w3schools.com/html/html5_geolocation.asp 

Plugins i Leaflet: https://leafletjs.com/plugins.html#geolocation


**Bonusoppgaver**

Ble du raskt ferdig? Prøv deg på noen av disse lukene i AoG og andre systemer

1. [9. desember - Vector tiles](https://github.com/Norkart/AdventOfGIS/blob/2023/09/README.md)
1. [19. desember - FlatGeoBuf](https://github.com/Norkart/AdventOfGIS/blob/2023/19/README.md)
1. [22. Desember - COG, snøkart
](https://github.com/Norkart/AdventOfGIS/blob/2023/22/README.md)
1. [Kepler.gl - visualiseringsløsning i nettleseren](https://kepler.gl/)
1. [GirlTechFest - styling av egne vector tiles](https://github.com/Norkart/GirlTechFest)


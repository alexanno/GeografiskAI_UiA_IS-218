# Oppgave 1: Geografiske Informasjonssystemer

## **Målsetting og krav til innlevering**
* Gruppen skal vise forståelse og kompetanse på bruk av geografiske datasett, tematisk kartvisualisering og bruk av QGIS som et GIS-verktøy.
* Levere minst 2 ulike temakart lagd i [QGIS](https://qgis.org) ved å bruke minst 3 ulike datasett/tjenester. Leveres som PDF med utsnitt av kartene. 
* Kartene skal vise frem en tematisk problemstilling innenfor enten klima/miljø eller samfunnsberedskap. Tema velger gruppen selv.

## **Oppgavebeskrivelse**
* Velg dere en tematisk problemstilling. Se eksempler under.
* Velg datasett og/eller tjeneste fra [GeoNorge](https://www.geonorge.no), [OpenStreetMap](https://www.openstreetmap.org), [Natural Earth](https://www.naturalearthdata.com).
* Legg til datakilder i QGIS.
* Filtrer datasettet basert på attributter / felt, geografisk utstrekning e.l.
* Lag eventuelle nye attributter ved å bruke field calculator
* Lag tematisk kart ved å bruke symbolisering av datasettene.
* Lag screenshot med "Project->import/export".
* (valgfritt) lag et PDF-kart med print-composer i QGIS.

## **Eksempler på oppgaver**
**Er beredskapen god nok i grunnkretsen der du bor?**
* Aktuelle datasett: Grunnkretser, Tilfluktsrom -offentlige, befolkningsdata, Brannstasjoner, skredfaresoner, flomsoner, jord- og flomskred aktsomhetsområder.
* Problemstilling: Bor du i et flomutsatt/skredutsatt område? Hvor lang tid vil det ta for brannbilen å kjøre til huset ditt fra brannstasjonen? 
Hvor ligger ditt nærmeste tilfluktsrom? Er det plass til alle som bor i din grunnkrets i det aktuelle tilfluktsrommet?
* Løsningsforslag: 
    * Last ned data (shape, geojson, geopackage m.m.) og finn tjenester (WMS, WFS, OGC API) fra GeoNorge. 
    * Kan du bruke data fra OpenStreetMap?
    * Lage temakart som visualiserer: Tilfluktsrom som symboler(ikon) med labels. Grunnkrets med kun omriss. 
    * Lage temakart som visualiserer: Brannstasjoner, lage et "temporary line layer" hvor du "tegner" kjøreruten fra brannstasjon til ulike interessepunkter
    * Lage temakart som visualiserer: flomsoner som WMS, grunnkretser joinet med befolkningsdata og visualisert som koropleth-kart (tetthet som expression!)
    * Lage kart på ulike målestokker (zoom-nivå) som viser hele byen, kun et nabolag, senterpunkt på en skole

**Hvordan står det til med naturen i ditt nærområde?**
* Aktuelle datasett: Grunnkretser, AR50, Befolkningsdata, Naturskog, Inngrepsfri natur i Norge, Arter av nasjonal forvaltningsinteresse, Naturtyper i Norge.
* Problemstilling: Er det stor sannsynlighet for å se trua arter i ditt nærområde? Er det mye skog i ditt nærområde? Hvor mange av studentene i gruppa har naturskog innenfor sin grunnkrets? Hvordan overlapper skogen i AR50 med skogen i gammelskog-datasettet? Hvilke naturtyper finner du i ditt nærområde? Fins det inngrepsfri natur i Kristiansand? 
* Løsningsforslag: 
    * Last ned data (shape, geojson, geopackage m.m.) og finn tjenester (WMS, WFS, OGC API) fra GeoNorge. 
    * Kan du bruke data fra OpenStreetMap?
    * Filtrer AR50-data for å vise utvalg av arealtyper. Bruk ferdig SLD-visualisering fra GeoNorge.
    * Legg til naturskog-datasett og arter. Bruk filter og field calculator. Lag gode visualiseringer av datasettene.
    * Visualiser befolkningsutvalget for studenter per grunnkrets. Vis data som labels. 
    * Lage kart på ulike målestokker (zoom-nivå) som viser hele byen, kun et nabolag, senterpunkt på "studentområder"


## **Verktøy, datasett og tips**
* [QGIS](https://qgis.org)
* [QGIS Training Manual](https://docs.qgis.org/latest/en/docs/training_manual/)
* [ColorBrewer2](https://colorbrewer2.org)
* [GeoNorge](https://www.geonorge.no)
* [Natural Earth](https://www.naturalearthdata.com)
* [Nedlasting av OpenStreetMap-data over Norge fra GeoFabrik](https://download.geofabrik.de/europe/norway.html)
* [Nedlasting av utvalg fra OpenStreetMap](https://overpass-turbo.eu/)
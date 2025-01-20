# Oppgave 2: Geografiske IT-utvikling

# UTKAST!!

## **Målsetting og krav til innlevering**
* Gruppen skal vise forståelse og kompetanse på bruk av fullstack geografisk IT-utvikling og geografisk analyse.
* Levere screenshots og/eller video av ferdig løsning med tilhørende beskrivelser i en README.md. Leveres som link til (åpent) github-repo. Kun README.md blir evaluert.
* Minimumskrav til løsningen er: 
    * Omfatte 3 datasett
    * Ha basis brukerinteraksjon
    * Visualisere grunnlagsdata og resultat av analyse
    * Være en fullstack-applikasjon med datalagring og frontend
* Teknologi er valgfri blant det som er forelest. Valg av teknologi må dokumenteres i README.
* Løsningen skal ha en problemstilling innenfor enten klima/miljø eller samfunnsberedskap. Tema velger gruppen selv.

## **Oppgavebeskrivelse**
* Velg dere en tematisk problemstilling. Se eksempler under.
* Utarbeid teknologivalg og arkitektur på `lagring`,(`backend/API`,) `frontend` 
* Velg datasett og/eller tjenester fra åpne datakilder, eksempelvis: [GeoNorge](https://www.geonorge.no), [OpenStreetMap](https://www.openstreetmap.org), [Natural Earth](https://www.naturalearthdata.com).
* Bearbeid data i QGIS, Python eller lignende.
* Last inn data i database/lagringsmiljø
* Implementer tilstrekkelig backend / API
* Implementer frontend og visualisering

## **Eksempler på oppgaver**
(hint: bruk LLMs for å hjelpe til strategier, løsninger og valg av teknologi)
**Er beredskapen god nok i grunnkretsen der du bor?**
* Problemstilling: Bor du i et flomutsatt/skredutsatt område? Hvor lang tid vil det ta for brannbilen å kjøre til huset ditt fra brannstasjonen? 
Hvor ligger ditt nærmeste tilfluktsrom? Er det plass til alle som bor i din grunnkrets i det aktuelle tilfluktsrommet?
* Bruk åpne data og tjenester for å finne data innenfor en avstand fra en adresse eller et punkt i kartet.
* Kan du bruke åpne tjenester for å lage et kjøreavstands-polygon?

**Friluftslivets år - motiverende tur-app**
* Lag en app som viser turstier nær brukeren og interessepunkter
* Kan du "tracke" GPS-sporet når brukeren beveger seg?
* Kan du lage en "stolpejakten"-app?


**Hvordan står det til med naturen i ditt nærområde?**
* Problemstilling: Er det stor sannsynlighet for å se trua arter i ditt nærområde? Er det mye skog i ditt nærområde? Hvor mange av studentene i gruppa har naturskog innenfor sin grunnkrets? Hvordan overlapper skogen i AR50 med skogen i gammelskog-datasettet? Hvilke naturtyper finner du i ditt nærområde? Fins det inngrepsfri natur i Kristiansand? 
* Lag en webapp som henter ut data som er i nærheten av brukeren. Kan brukeren velge "radius"? Kan du la brukeren filtrere på egenskaper til datasettene? 
* La brukeren gjøre arealanalyser (fks: fotballbaner med myr, gammelskog, dyrket mark) på eiendommer eller inntegnede polygon.


## **Verktøy, datasett og tips**
* [Leaflet](https://leafletjs.com)
* [OpenLayers](https://openlayers.org)
* [Maplibre](https://maplibre.org)
* [Supabase](https://supabase.com)
* [Postgis](https://postgis.net)
* [DuckDB](https://duckdb.org)
* [TurfJS](https://turfjs.org)
* [supabase_geojson_sqlapi](https://github.com/alexanno/supabase_geojson_sqlapi)
* [ColorBrewer2](https://colorbrewer2.org)
* [GeoNorge](https://www.geonorge.no)
* [Natural Earth](https://www.naturalearthdata.com)
* [Nedlasting av OpenStreetMap-data over Norge fra GeoFabrik](https://download.geofabrik.de/europe/norway.html)
* [Nedlasting av utvalg fra OpenStreetMap](https://overpass-turbo.eu/)
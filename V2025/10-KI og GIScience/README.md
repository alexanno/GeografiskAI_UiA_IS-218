# Introduksjon til GIScience

[Slides - Forelesning](https://docs.google.com/presentation/d/1N3B_OG7IuypvhuVnCY5rhTQwnyBSdVIY-csuTAt8t1k/edit?usp=sharing)

### Demo i QGIS
* Processing toolbox (søkefunksjon)
* Vector-dropdown
* Filter

[Vektoranalyser med eksempler i PostGIS og GeoPandas](./vektoranalyse.md)

### Øvingstime
Oppgaver - velg ut noen du vil jobbe med i listen under eller fra de enklere buffer-oppgavene nederst
**Oppgaver**
* "Du er allergisk mot Lauvskog og Blandingsskog - men vil allikevel gå tur! Hvilke turstier bør du velge?"
    * [Arealressurskart - treslag](https://kartkatalog.geonorge.no/metadata/arealressurskart-ar50-treslag/04b6aa8e-ac46-4303-baba-0149403a2acb)
        * [Dokumentasjon](https://www.nibio.no/tjenester/nedlasting-av-kartdata/dokumentasjon/ar50)
* “Hvilke 3 turstier mellom 3-6 km som er nærme skog finnes nær meg?”
    * [Arealressurskart (artype 30), GeoNorge](https://kartkatalog.geonorge.no/metadata/arealressurskart-ar50-arealtyper/41f6b000-c394-41c5-8ebb-07a0a3ec914f)
* “Hvilken eiendom har mest kvadratmeter myr i Agder?”
    * [Eiendom, GeoNorge](https://kartkatalog.geonorge.no/metadata/matrikkelen-eiendomskart-teig/74340c24-1c8a-4454-b813-bfe498e80f16)
    * [Arealressurskart (artype 60), GeoNorge](https://kartkatalog.geonorge.no/metadata/arealressurskart-ar50-arealtyper/41f6b000-c394-41c5-8ebb-07a0a3ec914f)
* “Hvilken kommune i Agder har mest bebygd areal?”
    * [Arealressurskart, GeoNorge](https://kartkatalog.geonorge.no/metadata/arealressurskart-ar50-arealtyper/41f6b000-c394-41c5-8ebb-07a0a3ec914f)
    * [Administrative enheter, GeoNorge](https://kartkatalog.geonorge.no/metadata/administrative-enheter-kommuner/041f1e6e-bdbc-4091-b48f-8a5990f3cc5b?search=administrat)
* “Hvor mange kafeer og badeplasser er innenfor 5 minutter el-sykkelavstand?”
    * [OpenStreetMap - overpass turbo - bruk wizard](https://overpass-turbo.eu/)
    * [Overture maps](https://overturemaps.org/)
    * [OpenRouteService - isochrone](https://maps.openrouteservice.org/#/)

**Enklere buffer-oppgaver med tips**
* Lag det geografiske området som dronen til brannvesenet i Kristiansand dekker (500m, 1km, 1.5km).
    * Kan du finne ut hvor mange bygningspunkt dronen dekker? [Matrikkelen - bygningspunkt](https://kartkatalog.geonorge.no/metadata/matrikkelen-bygningspunkt/24d7e9d1-87f6-45a0-b38e-3447f8d7f9a1)
* Velg ut alle turstier i Jegersberg (cirka). Lag en buffer på 10 meter på de utvalgte turstiene. [(Turruter, GeoNorge)](https://kartkatalog.geonorge.no/metadata/turrutebasen/d1422d17-6d95-4ef1-96ab-8af31744dd63)
* Last ned et lite område med bygninger fra OpenStreetMap (overpass-turbo). Lag 8 meter buffer på alle bygningspolygoner. Slå sammen til felles polygoner der de overlapper (dissolve).

**Aktuelle tjenester og biblioteker**
* [Turf.js](https://turfjs.org/)
* [PostGIS](https://postgis.net/)
* [GeoPandas](https://geopandas.org/)
* [OvertureMaps](https://overturemaps.org/)
* [OpenRouteService](https://openrouteservice.org/)
* [Nominatim](https://nominatim.org/)


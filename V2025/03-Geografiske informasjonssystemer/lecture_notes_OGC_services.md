## Innholdsfortegnelse

1. [Introduksjon til OGC- og API-standarder for IT-utviklere](#introduksjon-til-ogc--og-api-standarder-for-it-utviklere)
2. [Ressurser til forelesning](#ressurser-til-forelesning)
    - [Introduksjon til aktører og konsepter](#introduksjon-til-aktører-og-konsepter)
    - [Gridsets og tiles](#gridsets-og-tiles)
    - [OGC-standarder](#ogc-standarder)
        - [Fordeler med OGC-standarder](#fordeler-med-ogc-standarder)
        - [WMS (Web Map Service)](#wms-web-map-service)
        - [WMTS (Web Map Tile Service)](#wmts-web-map-tile-service)
        - [WFS (Web Feature Service)](#wfs-web-feature-service)
        - [WCS (Web Coverage Service)](#wcs-web-coverage-service)
    - [OGC API-standarder](#ogc-api-standarder)
        - [OGC API - Features](#ogc-api---features)
        - [OGC API - Tiles](#ogc-api---tiles)
3. [Forfatter](#forfatter)

# Introduksjon til OGC- og API-standarder for IT-utviklere

## Ressurser til forelesning

### Introduksjon til aktører og konsepter
- **ISO-TC211**: Internasjonal standardisering for geospatiale data og tjenester. ISO/TC 211 er en teknisk komité innenfor International Organization for Standardization (ISO) som fokuserer på standardisering innen geospatiale data og tjenester. Komiteen utvikler standarder som sikrer interoperabilitet og kvalitet i geospatiale data og tjenester på tvers av ulike systemer og applikasjoner. [Mer informasjon](https://committee.iso.org/home/tc211)

- **Open Geospatial Consortium (OGC)**: Utvikler åpne standarder for geospatiale tjenester. OGC er en internasjonal organisasjon som arbeider med å utvikle og fremme åpne standarder for geospatiale tjenester. Disse standardene sikrer at geospatiale data og tjenester kan brukes på tvers av ulike plattformer og applikasjoner, noe som fremmer interoperabilitet og samarbeid. [Mer informasjon](https://www.ogc.org/). Se https://opengeospatial.github.io/e-learning/index.html for god og praktisk introduksjon til standardene. 

- **ESRI og ArcGIS**: Proprietær leverandør av GIS-programvare med stor markedsandel. ESRI er en ledende leverandør av geografiske informasjonssystemer (GIS) og tilbyr en rekke programvareprodukter under merkenavnet ArcGIS. ArcGIS brukes av organisasjoner over hele verden for å samle inn, analysere og visualisere geospatiale data. [Mer informasjon](https://www.esri.com/en-us/arcgis/about-arcgis/overview)

- **SOSI-standardisering**: Norsk standard for geodata, utviklet av Kartverket. SOSI (Samordnet Opplegg for Stedfestet Informasjon) er en norsk standard for utveksling av geodata. Standarden er utviklet av Kartverket og brukes for å sikre at geodata kan utveksles og brukes på tvers av ulike systemer og applikasjoner i Norge. [Mer informasjon](https://www.geonorge.no/Geodataarbeid/standardisering/)

- **Teknologisk rammeverk (Kartverket/Norge Digitalt)**: Rammeverk for geodata i Norge. Dette rammeverket er utviklet av Kartverket og Norge Digitalt for å sikre en helhetlig og effektiv forvaltning av geodata i Norge. Rammeverket inkluderer retningslinjer og standarder for innsamling, lagring, og deling av geodata. [Mer informasjon](https://www.geonorge.no/Geodataarbeid/Norge-digitalt/geografisk-infrastruktur/teknologisk-rammeverk/)

- **Defacto-standardisering**: Standarder etablert av store internasjonale aktører som Google og Mapbox. Defacto-standarder er standarder som har blitt allment akseptert og brukt på grunn av deres utbredelse og popularitet, selv om de ikke nødvendigvis er formelt godkjent av en standardiseringsorganisasjon. Google Maps og Mapbox har vært drivere i utviklingen av defacto-standarder. [Google Maps](https://maps.google.com) | [Mapbox](https://www.mapbox.com/)

- **Cloud Native Geo (CNG)**: Moderne tilnærming til geografiske tjenester i skyen. Cloud Native Geo refererer til bruk av skybaserte teknologier og arkitekturer for å levere geografiske tjenester. Er under rask utvikling. [Cloud Native Geo (cng)](https://cloudnativegeo.org/) og [Cloud-Optimized Geospatial Formats Guide](https://guide.cloudnativegeo.org/)

- **OSGeo (Open Source Geospatial Foundation)**: Støtter og fremmer utviklingen av åpen kildekode geospatiale programvareprosjekter. OSGeo er en ideell organisasjon som støtter og fremmer utviklingen av åpen kildekode programvare for geospatiale applikasjoner. Organisasjonen tilbyr ressurser og støtte til en rekke prosjekter som dekker alt fra GIS-programvare til geospatiale biblioteker og verktøy. [Mer informasjon](https://www.osgeo.org/)

### Gridsets og tiles

- **Gridsets (Discrete Global Grid System)**
Geografiske grids, også kjent som rutenett, er systemer som deler jordens overflate inn i mindre, håndterbare celler eller ruter. Disse rutene kan brukes til å organisere, analysere og visualisere geospatiale data. Et Discrete Global Grid System (DGGS) er en type geografisk grid som deler jordens overflate inn i hierarkiske, regelmessige geometriske celler. DGGS er designet for å støtte effektiv lagring, analyse og visualisering av geospatiale data på ulike skalaer. Ved å bruke DGGS kan man enkelt sammenligne og kombinere data fra forskjellige kilder og oppløsninger.
    - [Introduction to Discrete Global Grid System (DGGS)](https://ecce.esri.ca/blog/2023/06/24/introduction-to-discrete-global-grid-system-dggs/)
    - [SSB rutenett for statistikk](https://www.ssb.no/natur-og-miljo/geodata#Nedlasting_av_rutenettsstatistikk)
    - [Sammenligning mellom gridsets](https://h3geo.org/docs#comparisons)
    - [Blogpost om H3 fra Uber](https://www.uber.com/en-SG/blog/h3/)
    - [H3 Documentation](https://h3geo.org/)
    - [Geohash](https://en.wikipedia.org/wiki/Geohash)
    - [PostGIS Geohash](https://postgis.net/docs/ST_GeoHash.html)
    
- **Tiles - konseptuelt**
Geografiske tiles er en metode for å dele opp kartdata i mindre, håndterbare biter som kan lastes inn dynamisk etter behov. Dette konseptet brukes ofte i slippy maps, som er interaktive kart hvor brukeren kan panorere og zoome. Hver tile representerer en bestemt del av kartet på et gitt zoom-nivå, og ved å kombinere flere tiles kan hele kartet vises. Dette gjør det mulig å laste inn bare de nødvendige delene av kartet, noe som forbedrer ytelsen og brukeropplevelsen. Tiles er vanligvis kvadratiske bilder (f.eks. 256x256 piksler) og identifiseres ved hjelp av koordinater for zoom-nivå, rad og kolonne.
    - [Tiled Web Map](https://en.wikipedia.org/wiki/Tiled_web_map)
    - [Zoom Levels](https://wiki.openstreetmap.org/wiki/Zoom_levels)
    - [Google Maps Coordinates, Tile Bounds, Projection](https://docs.maptiler.com/google-maps-coordinates-tile-bounds-projection/#How_does_a_zoomable_map_work)
    - Eksempel på XYZ scheme fra OpenStreetMap
        ```js
        https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png
        ```
- **Vector Tiles - konseptuelt**
Vector tiles er en metode for å levere geografiske data som vektorgrafikk i stedet for rasterbilder. Dette gjør det mulig å skalere og visualisere kartdata dynamisk på klientsiden, noe som gir bedre ytelse og fleksibilitet. Vector tiles inneholder vektordata som punkter, linjer og polygoner, samt tilhørende attributter, som kan brukes til å tegne kart på ulike zoom-nivåer uten tap av kvalitet. Dette er spesielt nyttig for interaktive kartapplikasjoner som krever rask innlasting og høy detaljrikdom.
    - [Vector Tiles](https://en.wikipedia.org/wiki/Vector_tiles)
    - [Mapbox Vector Tiles](https://docs.mapbox.com/help/glossary/vector-tiles/)
    - [MapTiler Vector Tiles](https://docs.maptiler.com/vector-tiles/)
    - Eksempel på MapTiler Vector Tiles som tiles.json
        ```js
        https://demotiles.maplibre.org/tiles/tiles.json
        ```
    - Eksempel på en vector tile-request
        ```js
        https://demotiles.maplibre.org/tiles/1/1/0.pbf
        ```

- **TileJSON** er en defacto-standard opprinnelig laget av Mapbox [github-spec](https://github.com/mapbox/tilejson-spec). `tiles.json` er en metadatafil som beskriver strukturen og innholdet i et sett med vektorfliser (vector tiles). Denne filen inneholder informasjon om tilgjengelige zoom-nivåer, koordinatsystem, og URL-mønstre for å hente flisene. `tiles.json` brukes ofte i kartapplikasjoner for å konfigurere og optimalisere innlasting av vektorfliser, slik at kartdata kan vises effektivt og dynamisk. Prøv ut standarden her: https://tilejson.io/

    - Eksempel på en `tiles.json`-fil:
        ```json
        {
            "tilejson": "2.2.0",
            "name": "example",
            "description": "An example of tiles.json",
            "version": "1.0.0",
            "attribution": "© Example",
            "scheme": "xyz",
            "tiles": [
                "https://example.com/tiles/{z}/{x}/{y}.pbf"
            ],
            "minzoom": 0,
            "maxzoom": 14,
            "bounds": [-180, -85.0511, 180, 85.0511],
            "center": [0, 0, 2]
        }
        ```

### OGC-standarder

Open Geospatial Consortium (OGC) er en internasjonal organisasjon som utvikler åpne standarder for geospatiale tjenester. Her er en kort introduksjon til noen av de mest brukte OGC-standardene:

#### Fordeler med OGC-standarder

- **Interoperabilitet**: OGC-standarder sikrer at geospatiale data og tjenester kan brukes på tvers av ulike systemer og applikasjoner.
- **Åpenhet**: Som åpne standarder, fremmer de transparens og samarbeid mellom ulike organisasjoner og utviklere.
- **Fleksibilitet**: De støtter et bredt spekter av dataformater og koordinatsystemer, noe som gjør dem anvendelige i mange forskjellige sammenhenger.
- **Skalerbarhet**: Spesielt WMTS er designet for å håndtere store mengder data effektivt, noe som er viktig for moderne web- og mobilapplikasjoner.

Ved å forstå og implementere disse standardene, kan utviklere bygge robuste og skalerbare geospatiale applikasjoner som kan integreres sømløst med andre systemer og tjenester.

OSGeo har flere referanseimplementasjoner av OGC-standarder. GeoServer er en kartserver som støtter og utvider flere OGC-standarder. [GeoServer sin dokumentasjon](https://docs.geoserver.org/) har ofte gode eksempler på bruk av standarderne. OGC har også laget e-learning (https://opengeospatial.github.io/e-learning/) som er en god ressurs for å lære om OGC-standarder.

#### WMS (Web Map Service)

WMS (https://opengeospatial.github.io/e-learning/wms/text/basic-main.html) er en standard for å levere georefererte kartbilder over internett. Det gir en enkel måte å integrere kart fra forskjellige kilder i en enkelt applikasjon. WMS støtter også ulike koordinatsystemer og projeksjoner, noe som gjør det fleksibelt for ulike bruksområder.

En typisk WMS-forespørsel kan se slik ut:

```js
GET /wms?service=WMS&version=1.3.0&request=GetMap&layers=example_layer&styles=&crs=EPSG:4326&bbox=-180,-90,180,90&width=800&height=600&format=image/png
```

- `service`: Tjenestetype, her `WMS`.
- `version`: Versjon av WMS, f.eks. `1.3.0`.
- `request`: Type forespørsel, f.eks. `GetMap`.
- `layers`: Navn på laget som skal vises.
- `crs`: Koordinatsystem, f.eks. `EPSG:4326`.
- `bbox`: Bounding box som definerer området som skal vises.
- `width` og `height`: Dimensjoner på bildet.
- `format`: Format på bildet, f.eks. `image/png`.

Mer informasjon: [OGC eLearning](https://opengeospatial.github.io/e-learning/wms/text/operations.html#getmap) og formell standard på [OGC WMS](https://www.ogc.org/standards/wms)


#### WMTS (Web Map Tile Service)

WMTS er optimalisert for rask levering av kartfliser (tiles) over internett, noe som er ideelt for applikasjoner som krever høy ytelse og skalerbarhet. Ved å bruke forhåndsgenererte fliser, kan WMTS levere kartdata mye raskere enn dynamisk genererte kartbilder.

Eksempel på bruk:
- Nettbaserte karttjenester som Google Maps eller OpenStreetMap.
- Mobilapplikasjoner som krever rask kartinnlasting og zooming.

#### Fordeler og ulemper med WMTS

##### Fordeler
- **Høy ytelse**: Ved å bruke forhåndsgenererte fliser, kan WMTS levere kartdata raskt og effektivt, noe som er ideelt for applikasjoner som krever rask respons.
- **Skalerbarhet**: WMTS er designet for å håndtere store mengder data og mange samtidige brukere, noe som gjør det godt egnet for web- og mobilapplikasjoner.
- **Standardisert**: Som en OGC-standard, sikrer WMTS interoperabilitet mellom ulike systemer og applikasjoner.

##### Ulemper
- **Lagringsbehov**: Forhåndsgenerering av fliser kan kreve betydelig lagringsplass, spesielt for store områder og mange zoom-nivåer.
- **Oppdateringsfrekvens**: Forhåndsgenererte fliser kan bli utdaterte hvis underliggende data endres ofte, noe som krever regelmessig regenerering av fliser.
- **Kompleksitet i oppsett**: Oppsett og administrasjon av en WMTS-tjeneste kan være mer komplekst sammenlignet med enklere tjenester som WMS.


En typisk WMTS-forespørsel kan se slik ut:

```js
GET /wmts?service=WMTS&version=1.0.0&request=GetTile&layer=example_layer&style=default&tilematrixSet=EPSG:3857&tilematrix=10&tilerow=20&tilecol=30&format=image/png
```

- `service`: Tjenestetype, her `WMTS`.
- `version`: Versjon av WMTS, f.eks. `1.0.0`.
- `request`: Type forespørsel, f.eks. `GetTile`.
- `layer`: Navn på laget som skal vises.
- `style`: Stil som skal brukes, f.eks. `default`.
- `tilematrixSet`: Tile matrix set, f.eks. `EPSG:3857`.
- `tilematrix`: Zoom-nivå.
- `tilerow` og `tilecol`: Rad og kolonne for tilen.
- `format`: Format på tilen, f.eks. `image/png`.

Mer informasjon: [OGC WMTS](https://www.ogc.org/standards/wmts)

#### WFS (Web Feature Service)

WFS gir tilgang til vektordata, som er essensielt for analyser og redigering av geospatiale data. I motsetning til WMS, som bare leverer bilder, gir WFS tilgang til de faktiske dataene som kan manipuleres og analyseres.

Eksempel på bruk:
- Hente og analysere eiendomsgrenser for byplanlegging.
- Utføre romlige analyser som å finne alle bygninger innenfor en viss avstand fra en vei.

#### Fordeler og ulemper med WFS

##### Fordeler
- **Direkte tilgang til data**: WFS gir tilgang til de faktiske geospatiale dataene, ikke bare bilder, noe som muliggjør avanserte analyser og redigering.
- **Standardisert format**: Bruk av standardiserte formater som GML (Geography Markup Language) sikrer interoperabilitet mellom ulike systemer.
- **Søkemuligheter**: WFS støtter komplekse spørringer for å hente spesifikke data basert på attributter og geografiske kriterier.

##### Ulemper
- **Kompleksitet**: Implementering og bruk av WFS kan være mer komplekst sammenlignet med enklere tjenester som WMS.
- **Ytelse**: Henting og overføring av store mengder vektordata kan være ressurskrevende og påvirke ytelsen, spesielt over tregere nettverk.
- **Kompatibilitet**: Ikke alle GIS-applikasjoner støtter WFS like godt, noe som kan begrense bruken i visse miljøer.

En typisk WFS-forespørsel kan se slik ut:
```js
GET /wfs?service=WFS&version=2.0.0&request=GetFeature&typeNames=example_feature&outputFormat=application/json
```

- `service`: Tjenestetype, her `WFS`.
- `version`: Versjon av WFS, f.eks. `2.0.0`.
- `request`: Type forespørsel, f.eks. `GetFeature`.
- `typeNames`: Navn på feature-typen som skal hentes.
- `outputFormat`: Format på utdata, f.eks. `application/json`.

Mer informasjon: [OGC WFS](https://www.ogc.org/standards/wfs)

#### WCS (Web Coverage Service)

WCS er designet for å levere rasterdata, som ofte brukes i fjernmåling og miljøovervåking. Rasterdata kan inkludere alt fra satellittbilder til høyde- og temperaturdata.

Eksempel på bruk:
- Analysering av satellittbilder for landbruksovervåking.
- Høydeanalyser for flomrisikovurdering.


En typisk WCS-forespørsel kan se slik ut:

```js
GET /wcs?service=WCS&version=2.0.1&request=GetCoverage&coverageId=example_coverage&format=image/tiff
```

- `service`: Tjenestetype, her `WCS`.
- `version`: Versjon av WCS, f.eks. `2.0.1`.
- `request`: Type forespørsel, f.eks. `GetCoverage`.
- `coverageId`: ID for dekningen som skal hentes.
- `format`: Format på utdata, f.eks. `image/tiff`.

Mer informasjon: [OGC WCS](https://www.ogc.org/standards/wcs)

### OGC API-standarder

De nye OGC API-standardene er designet for å være mer RESTful og enklere å bruke. Her er noen eksempler:

#### OGC API - Features

```js
GET /collections/example_collection/items?bbox=-180,-90,180,90&f=json
```

- `collections`: Samling av features.
- `items`: Henter items fra samlingen.
- `bbox`: Bounding box som definerer området som skal vises.
- `f`: Format på utdata, f.eks. `json`.

Mer informasjon: [OGC API - Features](https://ogcapi.ogc.org/features/)

#### OGC API - Tiles

```js
GET /collections/example_collection/tiles/WebMercatorQuad/10/20/30?f=png
```

- `collections`: Samling av tiles.
- `tiles`: Henter tiles fra samlingen.
- `WebMercatorQuad`: Tile matrix set.
- `10/20/30`: Zoom-nivå, rad og kolonne for flisen.
- `f`: Format på flisen, f.eks. `png`.

Mer informasjon: [OGC API - Tiles](https://ogcapi.ogc.org/tiles/)

For mer informasjon om OGC-standarder, besøk [OGC's offisielle nettside](https://www.ogc.org/).





**Forfatter**

Denne artikkelen er skrevet av Alexander Salveson Nossum (@alexanno), Norkart AS ved hjelp av Github Copilot

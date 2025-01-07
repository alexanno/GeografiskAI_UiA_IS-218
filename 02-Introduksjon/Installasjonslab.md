# Installasjonslab

Du skal installere verktøy og opprette kontoer som det blir bruk for i kurset: 

- [QGIS m/ GDAL/OGR](#qgis-m-gdalogr)
    - [Hva er QGIS, GDAL/OGR og osgeo4w shell?](#hva-er-qgis-gdalogr-og-osgeo4w-shell)
- [Rancher Desktop (eller Docker)](#rancher-desktop-eller-docker)
    - [Hva er Rancher Desktop og containere?](#hva-er-rancher-desktop-og-containere)
- [Github-konto](#github-konto)
- [Visual Studio Code](#visual-studio-code)
- [Postman / Thunderclient](#postman--thunderclient)
    - [Thunderclient](#thunderclient)
    - [Postman](#postman)
- [Google Colab](#google-colab)
- [Anaconda og Python-miljø](#anaconda-og-python-miljø)
    - [Installere Anaconda](#installere-anaconda)
    - [Opprette et Python-miljø](#opprette-et-python-miljø)
- [Supabase-konto](#supabase-konto)

## QGIS m/ GDAL/OGR

* Last ned siste long term release av QGIS fra https://qgis.org/
* Fullfør installasjonen
* Sjekk at 'QGIS desktop' fungerer
* (**KUN for Windows**): Sjekk at 'osgeo4w shell' fungerer
* (**KUN for Mac**): Installer GDAL via Homebrew: https://formulae.brew.sh/formula/gdal 

### Hva er QGIS, GDAL/OGR og osgeo4w shell?

**QGIS** er et gratis og åpen kildekode geografisk informasjonssystem (GIS) som lar brukere lage, redigere, visualisere, analysere og publisere romlige data.

**GDAL/OGR** er et bibliotek for å lese og skrive raster- og vektor romlige dataformater. GDAL håndterer rasterdata, mens OGR håndterer vektordata.

**osgeo4w shell** er en kommandolinjegrensesnitt for OSGeo4W, en samling av åpen kildekode romlige verktøy og biblioteker for Windows, inkludert QGIS og GDAL/OGR.

## Rancher Desktop (eller Docker)

* Last ned Rancher Desktop fra https://rancherdesktop.io/ (du kan også bruke Docker hvis du har det fra før)
* Installer og sjekk at det fungerer

### Hva er Rancher Desktop og containere?

**Rancher Desktop** er et verktøy for å bygge, kjøre og administrere containere på din lokale maskin. Det gir en enkel måte å jobbe med Kubernetes og containerteknologier uten behov for en ekstern server. Rancher er drop-in erstatning for Docker.

**Containere** er en lettvekts, bærbar og konsistent måte å pakke programvare og dens avhengigheter på, slik at den kan kjøre på tvers av ulike miljøer uten endringer. Containere sikrer at applikasjoner kjører på samme måte uansett hvor de distribueres.


## Github-konto

* Opprett en Github-konto
* Lag ditt første repository
* Test ut Github Copilot

## Visual Studio Code

**Visual Studio Code (VSCode)** er en gratis, åpen kildekode-kodeeditor utviklet av Microsoft. Den støtter flere programmeringsspråk og har innebygde funksjoner som debugging, Git-kontroll, syntax highlighting, intelligent kodefullføring, snippets og kode refactoring. VSCode kan utvides med et stort antall extensions for å tilpasse og forbedre utviklingsopplevelsen.

* Installer VSCode og sjekk at det fungerer: https://code.visualstudio.com/
* Koble sammen med Github og Copilot

## Postman / Thunderclient

### Thunderclient
Thunderclient er en lettvektsutvidelse for Visual Studio Code som gir lignende funksjonalitet som Postman, men direkte integrert i koden din. Det er ideelt for utviklere som ønsker å teste API-er uten å forlate IDE-en.

### Postman
Postman er et populært verktøy for API-utvikling som lar deg sende HTTP-forespørsler og se svarene. Det gir en brukervennlig grensesnitt for å lage, teste og dokumentere API-er. Du kan også automatisere tester og integrere dem i CI/CD-pipelines.

Begge verktøyene hjelper utviklere med å sikre at API-ene deres fungerer som forventet ved å simulere forespørsler og analysere svarene.

* Installer Thunderclient som en extension i VSCode: https://www.thunderclient.com/
* Valgfritt: Installer Postman desktop: https://www.postman.com/downloads/

## Google Colab

Google Colab er en gratis skybasert tjeneste fra Google som lar deg skrive og kjøre Python-kode i nettleseren. Det er spesielt nyttig for maskinlæring, dataanalyse og utdanning, da det gir tilgang til GPUer og TPUer uten behov for lokal konfigurasjon.

* Gå til https://colab.research.google.com/
* Logg inn med din Google-konto
* Opprett en ny notebook og test ut Python-kode

## Anaconda og Python-miljø

Anaconda er en gratis og åpen kildekode-distribusjon av Python og R programmeringsspråk for vitenskapelig databehandling (datavitenskap, maskinlæring, big data, etc.). Den forenkler pakkehåndtering og distribusjon.

### Installere Anaconda

1. Last ned Anaconda fra den offisielle nettsiden: https://www.anaconda.com/products/distribution
2. Følg installasjonsinstruksjonene for ditt operativsystem.
3. Etter installasjon, åpne Anaconda Navigator for å administrere ditt Python-miljø og installere nødvendige pakker.

### Opprette et Python-miljø

1. Åpne Anaconda Navigator.
2. Gå til "Environments" og klikk på "Create".
3. Gi miljøet ditt et navn og velg Python-versjonen du ønsker å bruke.
4. Klikk "Create" for å opprette miljøet.

Du kan nå installere pakker og avhengigheter i ditt nye miljø ved å bruke Anaconda Navigator eller kommandolinjeverktøyet `conda`.

## Supabase-konto

Supabase er en åpen kildekode Firebase-alternativ som gir backend-tjenester som database, autentisering, lagring og sanntidsfunksjoner. Det er bygget på toppen av PostgreSQL og støtter PostGIS for geografiske data.

* Gå til https://supabase.com/
* Opprett en konto og logg inn
* Opprett et nytt prosjekt og utforsk funksjonene



(skrevet ved hjelp av Github Copilot)
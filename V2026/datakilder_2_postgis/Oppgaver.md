# Oppgaver til øvingstime i Datakilder del 2: PostGIS

## Opprett en Supabase-konto med PostGIS extension
* Lag en ny konto på https://supabase.com/
* Opprett en ny organisasjon og et prosjekt
* Installer postgis som extension i "database"-panelet OBS!! Velg `public` som schema for extension (det er "feil" i dokumentasjonen). [Dokumentasjon](
https://supabase.com/docs/guides/database/extensions/postgis?queryGroups=language&language=js&queryGroups=database-method&database-method=dashboard)
* Koble til med dbeaver ved å bruke "transaction pooler"
* Koble til med qgis ved å legge til en postgis-server

## Last inn data til PostGIS serveren din
* Last ned ulike datakilder fra GeoNorge (se forslag i screenshot under)
* Pakk ut zip-filene og husk hvor du plasserer de på maskinen din
* Prøv ut ogr2ogr-kommandoer for å laste inn data på ulike måter: [ogr2ogr cheatsheet](./ogr2ogr-cheatsheet.md)
* Ekstraoppgave: Prøv å koble til databasen i QGIS og rediger på datasettene direkte. Kan du lage et nytt temp-layer og laste inn i databasen som ny tabell? 

![alt text](<$ GEONORGE.png>)

## Kjør spørringer mot databasen
* Bruk DBeaver og kjør eksemplene i [PostGIS Workshop](./postgis_workshop.md)
    * Pro tip: Lagre schemadefinition.md og bruk som context i Github Copilot til å hjelpe med SQL-analyser!
* Finn på dine egne spørringer og analyser! 

**Ekstraoppgaver**
* [Advent of GIS - 2024/10](https://github.com/Norkart/AdventOfGIS/blob/2024/10/README.md) - PostGIS
* [Advent of GIS - 2024/11](https://github.com/Norkart/AdventOfGIS/blob/2024/11/README.md) - ST SQL, intersect, area
* [Advent of GIS - 2024/13](https://github.com/Norkart/AdventOfGIS/blob/2024/13/README.md) - Brannkart, PostGIS
* [Advent of GIS - 2024/14](https://github.com/Norkart/AdventOfGIS/blob/2024/14/README.md) - ST SQL, buffer, distance
* [Advent of GIS - 2024/16](https://github.com/Norkart/AdventOfGIS/blob/2024/16/README.md) - PostGIS, KNN
* [Advent of GIS - 2024/18](https://github.com/Norkart/AdventOfGIS/blob/2024/18/README.md) - SQL API

**Pro tip - GeoJSON SQL API med edge function i Supabase** 
Prøv å lage din egen geojson-sql-api som "edge function" på din Supabase konto
* [Supabase GeoJSON SQL API](https://github.com/alexanno/supabase_geojson_sqlapi)

# Flere ressurser
* https://postgis.net/docs/reference.html
* https://github.com/dkakkar/Geospatial-data-management-with-PostGIS
* https://postgis.net/workshops/postgis-intro/

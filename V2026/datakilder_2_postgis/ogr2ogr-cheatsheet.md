# Dataprosessering med ogr2ogr (gdal)
## Hva er ogr2ogr?
ogr2ogr er et kommandolinjeverktøy fra GDAL-biblioteket som gjør det enkelt å konvertere og laste inn geografiske data mellom ulike formater og databaser. Det er særlig nyttig for å importere data fra WFS-servere, geodatabaser og shapefiler direkte til PostGIS.

### Sentrale parametere
* `-s_srs EPSG:XXXX`: Kildekoordinatsystem
* `-t_srs EPSG:XXXX`: Målkoordinatsystem
* `-nln navn`: Navn på det nye laget i databasen
* `-spat xmin ymin xmax ymax`: Bounding box for å filtrere ut ønsket område
* `-spat_srs EPSG:XXXX`: Koordinatsystem for bounding box
* `-overwrite`: Overskriver eksisterende lag
* `-progress`: Viser fremgangen under kjøring
* `--config PG_USE_COPY YES`: Bruker COPY-kommando for raskere import til PostGIS
* `-gt 65536`: Gruppestørrelse for transaksjoner
* `-lco GEOMETRY_NAME=geom`: Navn på geometri-kolonnen
* `-lco SPATIAL_INDEX=GIST`: Opprett GIST-indeks for raskere spørringer

## ogr2ogr - standard innlasting fra WFS til postgis
ogr2ogr kommando for å laste inn alle data fra en wfs server til en postgis server som nytt lag. layer=layer_183 kommer fra GetCapabilities fra WFS-serveren. Du finner den fra QGIS (obs! ikke ta med namespace 'ms:')
* WFS server: https://ogc.dsb.no/wfs.ashx med layer=layer_183
* Postgis: postgresql://postgres.ydfnpvezmrkocdfyaodl:[YOUR-PASSWORD]@aws-1-eu-west-1.pooler.supabase.com:5432/postgres
```sh
ogr2ogr -progress --config CPL_DEBUG ON -s_srs EPSG:25832 -t_srs EPSG:25832 -nln brannstasjoner \
  PG:"postgresql://postgres.ydfnpvezmrkocdfyaodl:[YOUR-PASSWORD]@aws-1-eu-west-1.pooler.supabase.com:5432/postgres?sslmode=require" \
  "WFS:https://ogc.dsb.no/wfs.ashx" \
  "layer_183"
```


## ogr2ogr - standard innlasting fra fildatabase til postgis
ogr2ogr kommando for å laste inn alle data i ett bestemt layer fra en filegeodatabase
* fgdb: Samfunnssikkerhet_42_Agder_25832_Flomsoner_FGDB.gdb layer=flomsoner_flomareal
* Postgis: postgresql://postgres.ydfnpvezmrkocdfyaodl:[YOUR-PASSWORD]@aws-1-eu-west-1.pooler.supabase.com:5432/postgres
```sh
ogr2ogr -progress --config CPL_DEBUG ON -s_srs EPSG:25832 -t_srs EPSG:25832 -nln flomsoner_agder \
  PG:"postgresql://postgres.ydfnpvezmrkocdfyaodl:[YOUR-PASSWORD]@aws-1-eu-west-1.pooler.supabase.com:5432/postgres?sslmode=require" \
  Samfunnssikkerhet_42_Agder_25832_Flomsoner_FGDB.gdb \
  flomsoner_flomareal
```


## ogr2ogr - Kun laste inn over et spesifikt område - med optimalisering for hastighet og overwrite
Område som WKT (Kristiansand++): `POLYGON ((7.538778203625469 58.37092828982031, 7.538778203625469 57.98405659247041, 8.567705602086363 57.98405659247041, 8.567705602086363 58.37092828982031, 7.538778203625469 58.37092828982031))`

* fgdb: Basisdata_42_Agder_25832_N50Kartdata_FGDB.gdb layer=N50_Arealdekke_omrade
* Postgis: postgresql://postgres.ydfnpvezmrkocdfyaodl:[YOUR-PASSWORD]@aws-1-eu-west-1.pooler.supabase.com:5432/postgres

```sh
ogr2ogr -progress --config CPL_DEBUG ON -overwrite -s_srs EPSG:25832 -t_srs EPSG:25832 -nln n50_arealdekke_kristiansand \
  --config PG_USE_COPY YES \
  -gt 65536 \
  -lco GEOMETRY_NAME=geom \
  -lco SPATIAL_INDEX=GIST \
  -spat 7.538778203625469 57.98405659247041 8.567705602086363 58.37092828982031 \
  -spat_srs EPSG:4326 \
  PG:"postgresql://postgres.ydfnpvezmrkocdfyaodl:[YOUR-PASSWORD]@aws-1-eu-west-1.pooler.supabase.com:5432/postgres?sslmode=require" \
  Basisdata_42_Agder_25832_N50Kartdata_FGDB.gdb \
  N50_Arealdekke_omrade
```
* `-spat xmin ymin xmax ymax`: Bounding box for å filtrere features (rektangel)
* `-spat_srs EPSG:4326`: Koordinatsystem for bounding box (lon/lat)

## cheat sheet
Basisdata_42_Agder_25832_MatrikkelenBygning_FGDB.gdb
layer=bygning

```sh
ogr2ogr -progress --config CPL_DEBUG ON -s_srs EPSG:25832 -t_srs EPSG:25832 -nln bygninger_punkt \
    --config PG_USE_COPY YES \
    -gt 65536 \
    -lco GEOMETRY_NAME=geom \
    -lco SPATIAL_INDEX=GIST \
    -spat 7.538778203625469 57.98405659247041 8.567705602086363 58.37092828982031 \
    -spat_srs EPSG:4326 \
    PG:"postgresql://postgres.ydfnpvezmrkocdfyaodl:[YOUR-PASSWORD]@aws-1-eu-west-1.pooler.supabase.com:5432/postgres?sslmode=require" \
    Basisdata_42_Agder_25832_MatrikkelenBygning_FGDB.gdb \
    bygning
```

Samfunnssikkerhet_42_Agder_25832_StormfloHavniva_FGDB.gdb
layer=stormflo_havniva_stormfloovreestimat_klimaarna
```sh
ogr2ogr -progress --config CPL_DEBUG ON -s_srs EPSG:25832 -t_srs EPSG:25832 -nln stormflo_havniva \
  --config PG_USE_COPY YES \
  -gt 65536 \
  -lco GEOMETRY_NAME=geom \
  -lco SPATIAL_INDEX=GIST \
  -spat 7.538778203625469 57.98405659247041 8.567705602086363 58.37092828982031 \
  -spat_srs EPSG:4326 \
  PG:"postgresql://postgres.ydfnpvezmrkocdfyaodl:[YOUR-PASSWORD]@aws-1-eu-west-1.pooler.supabase.com:5432/postgres?sslmode=require" \
  Samfunnssikkerhet_42_Agder_25832_StormfloHavniva_FGDB.gdb \
  stormflo_havniva_stormfloovreestimat_klimaarna
```
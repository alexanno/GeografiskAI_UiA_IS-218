## Romlige databaser

**Supabase og PostGIS-ressurser:**
* [Supabase og spatial SQL-tutorial](./supabase_tutorial.md)
* [Supabase GeoJSON SQL API](https://github.com/alexanno/supabase_geojson_sqlapi)
* [Advent of GIS - 2024/10](https://github.com/Norkart/AdventOfGIS/blob/2024/10/README.md) - PostGIS
* [Advent of GIS - 2024/11](https://github.com/Norkart/AdventOfGIS/blob/2024/11/README.md) - ST SQL, intersect, area
* [Advent of GIS - 2024/13](https://github.com/Norkart/AdventOfGIS/blob/2024/13/README.md) - Brannkart, PostGIS
* [Advent of GIS - 2024/14](https://github.com/Norkart/AdventOfGIS/blob/2024/14/README.md) - ST SQL, buffer, distance
* [Advent of GIS - 2024/16](https://github.com/Norkart/AdventOfGIS/blob/2024/16/README.md) - PostGIS, KNN
* [Advent of GIS - 2024/18](https://github.com/Norkart/AdventOfGIS/blob/2024/18/README.md) - SQL API
* https://postgis.net/workshops/postgis-intro/
* [PostGIS workshop (litt gammel)](https://docs.google.com/presentation/d/1qYXdeCIymLl32uoAHvAPrp1r-hK-_4Z8InG7sHEo6vc/edit#slide=id.gda62f9ff7a_1_67)

**Docker container for lokal kjøring:**
https://hub.docker.com/r/kartoza/postgis/
```
docker pull kartoza/postgis
docker run -e POSTGRES_PASS='passord1234' -e POSTGRES_USER='brukernavn' -p 25432:5432 kartoza/postgis
```


## Cloud Native Geospatial
* [Advent of GIS - 2024/19](https://github.com/Norkart/AdventOfGIS/blob/2024/19/README.md) - FlatGeoBuf
* [Advent of GIS - 2024/20](https://github.com/Norkart/AdventOfGIS/blob/2024/20/README.md) - PMTiles og Maplibre
* [Advent of GIS - 2024/22](https://github.com/Norkart/AdventOfGIS/blob/2024/22/README.md) - COG, snøkart
* [Advent of GIS - 2024/23](https://github.com/Norkart/AdventOfGIS/blob/2024/23/README.md) - COG, rastervisualisering

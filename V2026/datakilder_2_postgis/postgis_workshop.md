# PostGIS

## Queries

### Få skrevet ut schema til alle tabeller i public. Lagre som "markdown" i en fil for å bruke med KI-agenten i VSCode
```sql
SELECT 
    table_name,
    column_name,
    data_type
FROM 
    information_schema.columns
WHERE 
    table_schema = 'public'
ORDER BY 
    table_name, 
    ordinal_position;
```


### Hvilke bygninger er innenfor "stormflo"?
```sql
SELECT 
    b.objectid,
    b.bygningsnummer,
    b.bygningstype,
    b.kommunenavn,
    s.lokalid,
    s.vannstandovernn2000,
    b.geom
FROM bygninger_punkt b
INNER JOIN stormflo_havniva s ON ST_Intersects(b.geom, s.geom);
```

### Lag 100 meter buffer på alle bygninger


### Hvor er de 10 største arealene med dyrket mark?
#### Finn ut hvilke objekttyper som finnes
```sql
SELECT DISTINCT objtype
FROM n50_arealdekke_kristiansand
ORDER BY objtype;
```

### Regn ut areal med `ST_Area()`, sorter og limit. 
```sql
-- Kan du regne ut kvadratkilometer?
SELECT 
    objectid, 
    objtype, 
    navn, 
    ST_Area(geom) as area
FROM n50_arealdekke_kristiansand
WHERE objtype = 'DyrketMark'
ORDER BY ST_Area(geom) DESC
LIMIT 10;
```

## Finn alle flomsoner innenfor et rektangel definert med geojson
Rektangelet kan du lage via geojson.io eller qgis

### Fra WKT
```sql
SELECT 
    objectid,
    flomsoneid,
    gjentaksintervall,
    lokalid,
    ST_Area(shape) as area,
    shape
FROM flomsoner_agder
WHERE ST_Intersects(
    shape,
    ST_Transform(
        ST_SetSRID(
            ST_GeomFromText('POLYGON((8.030984028237299 58.24279493884066, 8.030984028237299 58.17359398982293, 8.164762712541517 58.17359398982293, 8.164762712541517 58.24279493884066, 8.030984028237299 58.24279493884066))'),
            4326
        ),
        25832
    )
);
```

### Fra GeoJSON
```sql
SELECT *
FROM flomsoner_agder
WHERE ST_Intersects(
    shape,
    ST_Transform(
        ST_SetSRID(
            ST_GeomFromGeoJSON('{"type": "Polygon", "coordinates": [[[8.030984028237299, 58.24279493884066], [8.030984028237299, 58.17359398982293], [8.164762712541517, 58.17359398982293], [8.164762712541517, 58.24279493884066], [8.030984028237299, 58.24279493884066]]]}'),
            4326
        ),
        25832
    )
);
```

### Klipp geometrien som overlapper med st_intersection
```sql
SELECT 
    objectid,
    flomsoneid,
    gjentaksintervall,
    lokalid,
    ST_Intersection(
        shape,
        ST_Transform(
            ST_SetSRID(
                ST_GeomFromGeoJSON('{"type": "Polygon", "coordinates": [[[8.030984028237299, 58.24279493884066], [8.030984028237299, 58.17359398982293], [8.164762712541517, 58.17359398982293], [8.164762712541517, 58.24279493884066], [8.030984028237299, 58.24279493884066]]]}'),
                4326
            ),
            25832
        )
    ) as clipped_geom
FROM flomsoner_agder
WHERE ST_Intersects(
    shape,
    ST_Transform(
        ST_SetSRID(
            ST_GeomFromGeoJSON('{"type": "Polygon", "coordinates": [[[8.030984028237299, 58.24279493884066], [8.030984028237299, 58.17359398982293], [8.164762712541517, 58.17359398982293], [8.164762712541517, 58.24279493884066], [8.030984028237299, 58.24279493884066]]]}'),
            4326
        ),
        25832
    )
);
```

### Enklere skrevet med CTE
```sql
WITH bbox AS (
    SELECT 
        ST_Transform(
            ST_SetSRID(
                ST_GeomFromGeoJSON('{"type": "Polygon", "coordinates": [[[8.030984028237299, 58.24279493884066], [8.030984028237299, 58.17359398982293], [8.164762712541517, 58.17359398982293], [8.164762712541517, 58.24279493884066], [8.030984028237299, 58.24279493884066]]]}'),
                4326
            ),
            25832
        ) as geom
)
SELECT 
    objectid,
    flomsoneid,
    gjentaksintervall,
    lokalid,
    ST_Intersection(shape, bbox.geom) as clipped_geom
FROM flomsoner_agder
CROSS JOIN bbox
WHERE ST_Intersects(shape, bbox.geom);
```


## Finn de 1000 nærmeste husene (i luftavstand) fra Brannstasjonen i Kristiansand
### Finn brannstasjonen i Kristiansand (QGIS fungerer også)
```sql
SELECT * 
FROM brannstasjoner b 
WHERE b.brannstasj LIKE 'Kristiansand%';
```

### Alternativ 1: Naiv (beregner alle distanser)
```sql
SELECT 
    b.objectid,
    b.bygningsnummer,
    b.bygningstype,
    b.kommunenavn,
    ST_Distance(b.geom, ST_Transform(s.msgeometry, 25832)) as distance
FROM bygninger_punkt b
CROSS JOIN brannstasjoner s
WHERE s.brannstasj LIKE 'Kristiansand%'
ORDER BY ST_Distance(b.geom, ST_Transform(s.msgeometry, 25832))
LIMIT 1000;
```

### Alternativ 2: Mye raskere - KNN med <->
```sql
SELECT 
    b.objectid,
    b.bygningsnummer,
    b.bygningstype,
    b.kommunenavn,
    ST_Distance(b.geom, ST_Transform(s.msgeometry, 25832)) as distance
FROM bygninger_punkt b
CROSS JOIN brannstasjoner s
WHERE s.brannstasj LIKE 'Kristiansand%'
ORDER BY b.geom <-> ST_Transform(s.msgeometry, 25832)
LIMIT 1000;
```

### Alternativ 3: Bruke CTE. Mest for "lesbarhet"
```sql
WITH brannstasjon AS (
    SELECT 
        ST_Transform(msgeometry, 25832) as geom,
        brannstasj as navn
    FROM brannstasjoner
    WHERE brannstasj = 'Kristiansand'
)
SELECT 
    bs.navn as brannstasjon,    
    b.objectid,
    b.bygningsnummer,
    b.bygningstype,
    b.kommunenavn,
    ST_Distance(b.geom, bs.geom) as distance
FROM bygninger_punkt b
CROSS JOIN brannstasjon bs
ORDER BY b.geom <-> bs.geom
LIMIT 1000;
```

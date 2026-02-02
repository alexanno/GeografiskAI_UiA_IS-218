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
**Konsept: Spatial JOIN med ST_Intersects**
- `ST_Intersects()` sjekker om to geometrier overlapper eller berører hverandre
- `INNER JOIN` returnerer kun rader hvor båte tabeller har matchende geometrier
- Dette er en romlig spørring som kobler sammen data basert på geografisk posisjon

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
**Konsept: Geometriske beregninger og sortering**
- `ST_Area()` beregner arealet av et polygon i samme enheter som koordinatsystemet (m² for UTM)
- `ORDER BY DESC` og `LIMIT` brukes til å finne de største arealene

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

**Konsept: Koordinatsystem-transformasjon (CRS)**
- `ST_SetSRID()` setter koordinatsystemet (SRID) - 4326 = WGS84 (lat/lon), 25832 = UTM32
- `ST_Transform()` konverterer fra ett koordinatsystem til et annet
- Viktig: data må være i samme CRS før romlige operasjoner!
- `ST_GeomFromText/GeoJSON()` konverterer tekst til geometri

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

### Klipp geometrien som overlapper med ST_Intersection
**Konsept: Geometriske operasjoner**
- `ST_Intersection()` returnerer bare delen av geometrien som overlapper
- Brukes når du skal "klippe ut" data innenfor et område
- Resultatet er en ny geometri som er mindre enn den originale

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
**Konsept: Common Table Expressions (CTE)**
- `WITH` gjør spørringen lettere å lese ved å dele den inn i steg
- `CROSS JOIN` med CTE gjør at samme geometri brukes flere ganger
- Best practice: definer komplekse geometrier en gang, bruk flere ganger

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
**Konsept: Tekst-søk**
- `LIKE` med `%` gjøre fleksibelt søk uten å vite det eksakte navnet
- Returnerer ett resultat som basis for neste spørring

```sql
SELECT * 
FROM brannstasjoner b 
WHERE b.brannstasj LIKE 'Kristiansand%';
```

### Alternativ 1: Naiv (beregner alle distanser)
**Konsept: Brute-force avstandsberegning**
- `ST_Distance()` beregner avstanden i meter (samme enhet som CRS)
- `CROSS JOIN` kombinerer hver bygning med brannstasjonen
- **Problem**: Beregner avstanden for ALLE bygninger - veldig treg for store datasett!

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

### Alternativ 2: Mye raskere - KNN (K-Nearest Neighbors) med <->
**Konsept: Spatial indexing og KNN-operator**
- `<->` er PostGIS sin avstandsoperator som bruker spatial index (veldig rask!)
- KNN = "K-Nearest Neighbors" - databasen bruker indekser til å finne nærmeste elementer først
- **Mange ganger raskere** enn alternativ 1, spesielt med stor datasett
- Operator returnerer resultater sortert etter avstand

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

### Alternativ 3: Bruke CTE. Mest for lesbarhet
**Konsept: Best practice for vedlikehold og lesbarhet**
- `WITH` gjør koden lettere å forstå - du ser hva som skjer steg for steg
- Gjenbruk av CTE-resultatet reduserer behovet for å skrive kompleks geometri flere ganger
- Kombinerer fordelen av lesbarhet (CTE) med ytelse (KNN-operator)

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

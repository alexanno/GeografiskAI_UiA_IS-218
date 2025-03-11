### Github Copilot og LLMs

### Example prompts

# 1. Load a shapefile into GeoPandas
"""
Write a Python function that loads a shapefile into a GeoDataFrame using GeoPandas.
Ensure the function can handle different encodings and provide an optional argument for specifying the encoding.
"""

# 2. Convert GeoDataFrame to WGS84
"""
Write a function that takes a GeoDataFrame as input and converts its coordinate reference system (CRS) to WGS84 (EPSG:4326).
Ensure that the function returns a new GeoDataFrame without modifying the original.
"""

# 3. Load a GeoJSON file into DuckDB
"""
Write a DuckDB SQL query that loads a GeoJSON file into a spatial table.
Ensure that the geometry column is correctly recognized, and reproject it to EPSG:4326 if necessary.
"""

# 4. Clip a GeoDataFrame using another GeoDataFrame
"""
Write a function that clips a GeoDataFrame using another GeoDataFrame as a mask.
Ensure the function handles cases where geometries do not overlap and returns an empty GeoDataFrame if necessary.
"""

# 5. Convert a PostGIS table to a GeoDataFrame
"""
Write a Python function that connects to a PostGIS database and loads a specific table into a GeoDataFrame.
Ensure the function allows filtering by a SQL WHERE clause.
"""

# 6. Reproject a shapefile using OGR2OGR
"""
Write an OGR2OGR command to reproject a shapefile from EPSG:25832 to EPSG:4326.
Ensure the command preserves attribute data and handles large datasets efficiently.
"""

# 7. Find the centroid of all polygons in a GeoDataFrame
"""
Write a Python function using GeoPandas that calculates the centroid of all polygons in a GeoDataFrame.
Ensure that the function works for both projected and geographic coordinate systems.
"""

# 8. Calculate the distance between two points using PostGIS
"""
Write a PostGIS SQL query that calculates the distance between two points stored in a spatial table.
Ensure the query accounts for geographic coordinates (using ST_DistanceSphere).
"""

# 9. Convert a CSV file with latitude and longitude to a GeoDataFrame
"""
Write a Python function that loads a CSV file containing latitude and longitude columns into a GeoDataFrame.
Ensure the function allows specifying the column names and sets the correct CRS.
"""

# 10. Merge two spatial datasets in DuckDB
"""
Write a DuckDB SQL query that performs a spatial join between two spatial tables using ST_Intersects.
Ensure the query includes an inner join and a left join version for different use cases.
"""

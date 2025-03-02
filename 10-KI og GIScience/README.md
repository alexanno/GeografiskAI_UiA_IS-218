Forelesning
* Analyser på enkelt-lag
    * Buffer
    * Merge vs Dissolve
* Flerlagsanalyser
    * Concave, convex hull 
    * Centroid, Center of mass
    * Overlay (overlagsanalyser)
        - **Union**: Kombinerer to polygonlag og bevarer alle geometrier og attributter.
        - **Intersect**: Bevarer kun overlappende områder mellom to lag.
        - **Symmetrical Difference**: Fjerner overlappende områder og beholder kun ikke-overlappende deler.
        - **Identity**: Bevarer hele det første laget og legger til overlappende deler fra det andre laget.
        - **Clip**: Begrenser geometrier til et definert område.
        - **Erase**: Fjerner overlappende områder fra et lag.
        - **Split**: Deler et lag inn i flere basert på et annet lags geometri.
    * Spatial joins
* Ruteanalyser
    * a-til-b
    * Distance matrix
    * Isochrones
* Øvingstime
    * 

Aktuelle tjenester og biblioteker
* https://turfjs.org/
* PostGIS
* GeoPandas
* OvertureMaps
* https://openrouteservice.org/
* https://nominatim.org/



Neste forelesning    
* Cluster-analyser
    * DBscan, KNN, Voronoi??
* (Rasteranalyser)

# Australia

## DEM

SRTM-derived 1 Second Digital Elevation Models Version 1.0

DEM-H (Hydrologically enforced version of the smoothed DEM-S.

https://ecat.ga.gov.au/geonetwork/srv/eng/catalog.search#/metadata/72759

## Landuse

AU ABARES Landuse classes

https://www.agriculture.gov.au/abares/aclump/land-use


## Soils

The Australian Soil Resource Information System (ASRIS) data were obtained through TERN AusCover (http://www.auscover.org.au). TERN is Australia’s land-based ecosystem observatory delivering data streams to enable environmental research and management (TERN, http://www.tern.org.au). TERN is a part of Australia’s National Collaborative Research Infrastructure Strategy (NCRIS, https://www.education.gov.au/national-collaborative-research-infrastructure-strategy-ncris). 

http://www.asris.csiro.au

The Soils are parameters based on the ASRIS database. The database queries clay, silt, sand, organic matter, and ksat for a top soil layer and a sub soil layer. It is also provides a top soil depth estimate. ki, and kr are computed from clay, sand, silt, and om as specified by the WEPP user manual. The remaining parameters are pulled from disturbed WEPP soils after identifying the soil texture. For the PeP interface the burn severity is parameterized according to soil texture from the disturbed WEPP values.
 
 ## Climates
 
 
For the climates we have Australian Gridded Climate Data (AGDC) on a 5km grid. The monthly ensembles were obtained and then monthly normals were calculated for tmax, tmin, rain, and radiation (not used). The normals are used to select an equivalent US station and then can be used to spatialize the climates by hillslope.
 

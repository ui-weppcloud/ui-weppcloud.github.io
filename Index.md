## About
The Water Erosion Prediction Project (WEPP) model is a hydrology and erosion model wildly used by academics and land managers to assess the effects of land management changes on runoff and sediment yield. Even for advanced users, data preparation is a lengthy process that involves downloading various maps and datasets, and processing and saving the data in formats that are readable by the model. 

[WEPPcloud](https://wepp1.nkn.uidaho.edu/weppcloud) is an online interface for the WEPP model that facilitates input data preparation and hydrologic simulations from any computer connected to the internet. The user can zoom to a location, identify an area of interest, and delineate a watershed. Then based on a series of options that involve selection of soils, managements, and weather information from national or locally-stored databases, the user can quickly get estimates of runoff and soil erosion for their watershed of interest. Results are displayed in the web browser as text files and as geospatial maps and are also downloadable. Most hydrologic simulations can be completed within a few minutes, depending on the size of the watershed. 

WEPPcloud was mainly developed for forestry applications as a joint effort between University of Idaho and Forest Service Rocky Mountain Research Station. Other contributions to the applicaiton include USDA ARS, Swansea University, and Michigan Technological University.

**Looking for more information?** View the [FAQ](FAQ.md)

## Getting Started

- [QuickStart](QuickStart.md)


## Advanced Topics and Troubleshooting

- [Clearing Locks](AdvancedTopics.md#Clearing-Locks)
- [Combined Watershed Generator](AdvancedTopics.md#WEPPcloud-Utilities)
- [wepppy-win-bootstrap](https://github.com/rogerlew/wepppy-win-bootstrap) for local runs
- [wepppy](https://github.com/rogerlew/wepppy) the opensource project that powers WEPPcloud

## Help / Feedback

For general assistance or questions please contact Mariana Dobre at mdobre@uidaho.edu. 

For technical assistance please contact Roger Lew at rogerlew@uidaho.edu. Providing the url to the run in question and a screenshot of the problem would also be helpful.

For questions regarding the WEPP model please contact Anurag Srivastava at srivanu@idaho.edu.

## Locales

WEPPcloud relies on publically available databases to parameterize the necessary WEPP inputs. The various WEPPcloud interfaces are more-or-less supported in the following locales:

- [Conterminous United States](us-data.md)
- [Europe](eu-data.md)
- [Australia](au-data.md)

WEPPcloud has region specific data for some locations that are used to provide better calibration. These regions include:

- Lake Tahoe
- Portland Municipal Watershed

## Interfaces

WEPPcloud is comprised of numerous interfaces with sometimes subtle distinctions between them. While this helps to provide backwards compatibility the result can be confusing to users. If you are unsure of what interface to use, use the general WEPPcloud Interface or the Disturbed Interface.

### WEPPcloud

Delineates and builds 7778 soils and managements with available data. The soils and landuse are parameterized directly from available datasets. 

### Disturbed

Backfills soils and managements with parameters from the USFS Disturbed database based on landcover type and soil texture.

### WEPP-PEP (Post Fire Erosion Prediction)

Assigns 2006 soils and managements based on soil texture (sand loam, silt loam, clay loam, loam), and burn severity (unburned, low/moderate, high).

### RRED (Rapid Response Erosion Database) 

Obtains soils and managements from the [http://rred.mtri.org/rred](http://rred.mtri.org/rred). These use 2006 soils and 97.3 managements.

## Tools

Specialized tools and reports are available on some interfaces to assist with post-fire risk assessment. These tools include:

### WATAR (Water Erosion Prediction Project cloud model - Wildfire Ash Transport And  Risk estimation tool)

WATAR has been under developed since 2017 (Neris et al. 2017). The model predicts the probability of both ash and soil, and the potential pollutants in them, to be transported from burned hillslopes into stream channels and waterbodies and utilizes WEPP outputs.

### Debris Flow

A empirical Debris Flow model is available for the US. It is parameterized from SSURGO and uses NOAA precipitation interval data.

### RHEM (Rangeland Hydrology and Erosion Model)

This interface provides a watershed scale online interface for RHEM. It parameterizes soils based on cover values obtained from the NLCD 2016 Shrubland database.

### Lake Tahoe-Fire

This interface is for the Lake Tahoe Basin. Soil Burn Severity is estimated from a random forest classification model developed specifically for Lake Tahoe. This interface also incorporates phosphorus soil data.

## The WEPP Model

### Model Background

The WEPP model is a physically-based hydrology and erosion model (Flanagan and Nearing, 1995, Flanagan et al., 2007), initially developed to be applied at hillslope scales or in small agricultural catchments. The advantage of WEPP is its ability to estimate the spatial and temporal distribution of soil loss or deposition along a hillslope, as well as sediment yield at the bottom of a hillslope. WEPP is based on the fundamentals of hydrology, plant science, hydraulics, and erosion mechanics (Flanagan and Nearing, 1995). For the detailed description of model components and processes please refer to the WEPP User Summary (Flanagan and Livingston, 1995) and WEPP Technical Documentation (Flanagan and Nearing, 1995). 

Developments such as the incorporation of baseflow algorithms and channel routing methods have extended the applicability of the model to larger watersheds. The model has been tested for several undisturbed watersheds and for forest management effects on water and sediment yield from watersheds in Pacific Northwest (Brooks et al., 2016; Srivastava et al., 2020).

Following are the brief description of model components and processes:

#### Watershed Delineation

Watershed delineation can be performed by TOPAZ or TauDEM

##### TOPAZ

- Topographic Parameterization (TOPAZ) tool is used to derive topographic features (slope length, width, aspect, slopes) using the Digital Elevation Model (DEM).
- TOPAZ characterizes watersheds as representative hillslopes and channels, and links hillslopes to channel networks.
- A Python watershed abstraction routine (wepppy.watershed_abstraction) parameterizes representative hillslopes by walking the flowpaths for each subcatchment identified by TOPAZ
- The output grids and tables from TOPAZ are included in archived project downloads. Descriptions of these products are found here in the [TOPAZ Manual](https://www.ars.usda.gov/ARSUserFiles/30700510/TOPAZ_User-Manual2.pdf)

##### TauDEM

- [TauDEM](https://hydrology.usu.edu/taudem/taudem5/index.html) (Terrain Analysis Using Digital Elevation Models) is a suite of Digital Elevation Model (DEM) tools for the extraction and analysis of hydrologic information from topography as represented by a DEM.
- TauDEM is similiar to TOPAZ but more modern in its implementation
- TauDEM supports larger catchment areas and defines a binary channel network that eliminates more than 3 channels entering a single junction
- A Python module (wepppy.taudem) provide TOPAZ emulation to delineate subcatchments within each of the TauDEM catchments and parameterize representative hillslopes from the D-Infinity TauDEM slope products

#### Hydrology and Hydraulics

WEPP first executes hydrological and erosion calculations for each hillslope and channel. The flow and sediment yield from each of the hillslopes are fed to those of the associated channel and are routed through the channels to the watershed outlet. 

- WEPP simulates surface hydrology and hydraulics, subsurface hydrology, vegetation growth and residue decomposition, and sediment detachment and transport along each hillslope and channel segment using four major input files: climate, slope, soil, and vegetation.
- Climate: Requires precipitation amount and its characteristics (duration, peak intensity, and time-to-peak intensity). Other variables include maximum and minimum temperatures, dew point temperature, solar radiation, wind speed and wind direction.
- Winter hydrology: Snow accumulation, snowmelt, frost and thaw. These processes are performed internally by the model on an hourly basis.
- Surface hydrology: The surface hydrology component calculates infiltration, rainfall excess, depression storage, and peak discharge. Rainfall excess is calculated at 1 min intervals following the modified Green-Ampt-Mein-Larson equation. 
- Hydraulics: Overland flow and peak discharge are computed using a modified kinematic wave equation.
- Percolation: Uses storage routing techniques to predict flow through soil layers.
-	Plant growth: Follows EPIC’s model approach for vegetation growth. Model estimates biomass accumulation based on heat units and photosynthetic active radiation. Plant growth accounts for water and temperature stress. Plant growth variables include growing degree days, vegetative dry matter, canopy cover and height, root growth, leaf area index.
-	Evapotranspiration: Uses Penman equation for potential evapotranspiration. Other available method is FAO 56 Penman-Monteith. 
-	Subsurface flow: Subsurface lateral flow from hillslopes is estimated using Darcy’s law.
-	WEPP maintains a continuous daily water balance of surface runoff, subsurface lateral flow, soil evaporation, plant transpiration, residue evaporation, total soil-water, deep percolation, snow accumulation and melt, and frost and thaw.

#### Hillslope Erosion

-	WEPP-simulated soil erosion on a hillslope profile is represented in two ways: 1) detachment and delivery of soil particles by raindrop impact and shallow sheet flow on interrill areas, and 2) soil particle detachment, transport, and deposition by concentrated flow in rill areas. 
-	Rill erosion is modeled as a function of the flow’s capacity to detach and transport soil versus the existing sediment load in the flow. WEPP uses a steady-state sediment continuity equation for erosion computations. Soil detachment in rills occurs when the flow hydraulic shear stress exceeds the critical shear stress of the soil, and when sediment load is less than sediment transport capacity. 
-	Deposition occurs when sediment load in the rill flow is greater than the flow sediment transport capacity. The sediment transport capacity is calculated using a modified Yalin equation.

#### Channel Hydrology and Erosion

-	Peak runoff rates are computed using: 1) a modified EPIC; 2) CREAMS; 3) Kinematic Wave; 4) Muskingum-Cunge; and 5) Muskingum-Cunge (variable). The last three routing methods support simulations of perennial channels/streams.
-	The channel erosion routine in WEPP is similar to the simulation of rill erosion on hillslopes with the exception that the flow shear stress is calculated using regression equations that approximate the spatially-varied flow equations, and only entrainment, transport, and deposition by concentrated flow are considered. 
-	Detachment is assumed to occur from the channel bottom until the nonerodible layer is reached, after which the channel starts to widen, and the erosion rate decreases with time until the flow is too shallow to cause detachment.

#### Recent Developments

-	an improved algorithm for frost simulation based on energy balance (Dun et al., 2010) 
-	an enhanced algorithm for percolation and subsurface lateral flow, allowing for saturation-excess runoff (Dun et al., 2009; Boll et al., 2015)
-	a FAO 56 Penman-Monteith method for reference and actual evapotranspiration (ET) developed by Allen et al. (1998) (Wu and Dun, 2004)  
-	the implementation of more appropriate channel routing methods (e.g. kinematic-wave and the Muskingum-Cunge) for perennial streams (Wang et al., 2014)
-	a linear reservoir groundwater baseflow contribution from hillslopes to channel streamflow (Srivastava et al., 2017) 


## Related Work

### Windows WEPP

Several WEPP interfaces are available for different applications. The USDA Agricultural Research Service National Soil Erosion Research Lab (NSERL) is the agency the manages the model development and handles all the updates and releases (Laflen et al., 1991; Flanagan and Nearing, 1995). The WEPP Windows interface can be ran on personal computers for individual hillslopes or small agricultural catchments. For a complete list of model documentation, updates, and other information related to the WEPP model see:
[https://www.ars.usda.gov/midwest-area/west-lafayette-in/national-soil-erosion-research/docs/wepp/](https://www.ars.usda.gov/midwest-area/west-lafayette-in/national-soil-erosion-research/docs/wepp/)

### NSERL WEPP Online

NSERL is also the developer of an online interface for the WEPP model (Frankenberger et al., 2011), which allows the WEPP model to be set up for small watersheds and ran using a web browser: 
[https://milford.nserl.purdue.edu/ol/wepp/verify.php](https://milford.nserl.purdue.edu/ol/wepp/verify.php)

Additionally, researchers at NSERL are working on developing other online interfaces at both hillslope and watershed scales for land managers interested in evaluating the effects of runoff and erosion from various agricultural practices. 

### GeoWEPP

An ArcGIS version of the model (GeoWEPP, Renschler, C.S., 2003) has been developed for users that are familiar with GIS:
[http://geowepp.geog.buffalo.edu](http://geowepp.geog.buffalo.edu)

GeoWEPP guides users through a series of questions that facilitate data preparation and model runs. The model is ArcMap dependent and a user needs to update GeoWEPP with every ArcMap update. 

## Platform Architecture

WEPPcloud is a Python Flask web interface for running WEPP (and other hydrological) models in the cloud (remote servers). WEPPcloud uses the `wepppy` library to acquire and process GIS data from a variety of sources. `wepppy` contains a scientific Python-based hillslope abstraction routine and functionality for running WEPP at the watershed scale. This eliminates the need for TopWEPP (a.k.a. TopWEPP2, prepwepp) and improves the flexibility and reliability of the process. WEPPcloud automates the delineation of hillslopes by running Digital Elevation Models (DEMs) through TOPAZ. The climates can be stochastically generated or observed daily climate input files are created with the assistance of CLIGEN. Additional climate processing functionality is available (dependent on the region) to spatialize climates on monthly gridded daily temperature minimums, maximums, and precipitations. In the US there is support for generating daily observed (historical) climate files from DAYMET or GRIDMET.

![Platform Architecture](https://user-images.githubusercontent.com/3652906/87733873-d9fc7480-c785-11ea-8a03-3c64d0a3ec18.png)

## Change Log
<table class="table">
<thead>
  <tr><th>Date</th><th>Notable Change</th></tr>
</thead>
<tbody>
<tr><td>December 8, 2020</td><td>TauDEM alpha release. Ash Transport gridded alpha release. Fractional zoom for map. Disturbed has ability to remove SBS. Channel shape export has discharge in m^3. Some other miscellaneous changes.</td></tr>
<tr><td>Noveber 19, 2020</td><td>Tillage and surface effects removed from Tahoe/Disturbed WEPP files.</td></tr>
<tr><td>November 18, 2020</td><td>All channel managements set to a default management specific for channels instead
    of assigning all the channels the dominate management of the channels.<td></td></tr>
<tr><td>November 17, 2020</td><td>Disturbed uses the Tahoe 20-yr Old Forest for forest conditions instead of an outdated
    management that would result in increased erosion with Current Conditions.</td></tr>
<tr><td>November 15, 2020</td><td>Forking revised for improved reliability. Forking now provides a console that outputs
    status of the forking process. Once the forking is complete a link to the new run should be provided at the bottom of the page.</td></tr>
<tr><td>October 29, 2020</td><td>Bug fix for properly reloading RRED projects. Link to export preparation
    details. wepp_aa57a1d with extended formatting loss report for larger watersheds. Disturbed interface will always
    use latest version of wepp.
</td></tr>
<tr><td>October 27, 2020</td><td>Write 2006.2 channel soils if hillslope soils are 9x.x or 2006.2.
</td></tr>
<tr><td>October 20, 2020</td><td>Combined Watershed Viewer units support and bug fixes.</td></tr>
<tr><td>October 16, 2020</td><td>WEPPcloud-Disturbed Beta release</td></tr>
<tr><td>October 14, 2020</td><td>Report WEPP channel width in channel table of preparation details.</td></tr>
<tr><td>October 12, 2020</td><td>Cligen 5.3.2 fix for running observed climates.</td></tr>
<tr><td>October 6, 2020</td><td>Ability to export without WEPP results. US Gage Locations as map overlay.
    Simple soil texture classes incorporated in BAER.</td></tr>
<tr><td>October 2, 2020</td><td>User pages bug fixes.</td></tr>
<tr><td>September 28, 2020</td><td>Ability to clear landuse selection. Average Annual Water balance
    Streamflow includes runoff and latqcc. StreamFlow graph is stacked</td></tr>
<tr><td>September 23, 2020</td><td>GRIDMET support for current year.</td></tr>
<tr><td>September 4, 2020</td><td>GHCN climates added to interface.</td></tr>
<tr><td>August 28, 2020</td><td>Adjustment to how field capacity and wilt point are calculated to not
    double correct for rock (EB).</td></tr>
<tr><td>August 27, 2020</td><td>No soil specialization for water. PortlandMod implementation.
    Water restrictive layer set to 1 10000 100 (AS).</td></tr>
<tr><td>July 15, 2020</td><td>No water in channel soils.</td></tr>
<tr><td>July 7, 2020</td><td>Landuse change enabled on general interface.</td></tr>
<tr><td>July 2, 2020</td><td>Use gdal for projection transformations were possible.</td></tr>
<tr><td>June 26, 2020</td><td>PyProj multiple import fix.</td></tr>
<tr><td>June 18, 2020</td><td>Bug fix for soil specialization.</td></tr>
<tr><td>May 11, 2020</td><td>PMETPARA input file preparation</td></tr>
<tr><td>April 1, 2020</td><td>Fixed project forking bug.</td></tr>
<tr><td>March 18, 2020</td><td>AshPost implementation to optimize interface. Ash support added to PowerUser
    Panel.</td></tr>
<tr><td>March 4, 2020</td><td>NaN checking for Loss Summary.</td></tr>
<tr><td>March 1, 2020</td><td>Support for discontinuous temperature adjustment to climate files. Ability to
control whether pmet, frost, baseflow, and tcr WEPP sub-routines are ran.</td></tr>
<tr><td>February 29, 2020</td><td>Portland bedrock attributes updated.</td></tr>
<tr><td>February 28, 2020</td><td>Cligen5.32 integrated into interface. This includes a fix for tpeak
    values when building from observed datasets. Phosphorus added to Loss Summary. Portland bedrock
    attributes updated  (jimf).</td></tr>
<tr><td>February 21, 2020</td><td>Calibration soils for LT.</td></tr>
<tr><td>January 27, 2020</td><td>WEPPcloud-PEP wepp channel type set to OnRock 2. (md)</td></tr>
<tr><td>June 17, 2019</td><td>Hillslope and Watershed ash transport modeling for WEPPcloud-PEP.
    Single Storm climate fully implemented.</td></tr>
<tr><td>May 17, 2019</td><td>Annual climate precip, tmax, tmin in station summary and .cli summary.
    Phosphorus variables removed from freq flood report when not ran. Units fixed for runoff on combined
    watershed viewer. Summary for wepp run is now populated. Mary Ellen's soil texture classification
    incorporated. Soil texture based on surgo data in ERMiT download. ERMiT meta data file contains climate
    station information (state, station description, par). Link to FSWEPP batch processing scripts below the
    ERMiT csv. Units pretty much everywhere rounding to 2 significant digits. MCL and CSA inputs respect the
    units of the project (m and ha or ft and acre). Tab titles now include project name if a project name
    is defined.</td></tr>
<tr><td>March 29, 2019</td><td>Various usability enhancements. 10-min and 30-min peak rainfall intensities
                               added to return period analysis. soil fix for channels and hillslopes with
                               dominate water.</td></tr>
<tr><td>February 14, 2019</td><td>Hazard SEES - FireEarth Data Portals added.</td></tr>
<tr><td>January 14, 2019</td><td>Miscellaneous interface improvements and bug fixes.</td></tr>
<tr><td>December 3, 2018</td><td>Bug fix for building DAYMET Climates with small extents.</td></tr>
<tr><td>November 2, 2018</td><td>Changed default parameters for running TOPAZ and WEPP.</td></tr>
<tr><td>August 27, 2018</td><td>Combined Watershed URL Generator. Ability to reassign landuse to different management.
                                Zack Holden's WRF Precipitation dataset integrated into Debris Flow model
                                over bounds of [-117.386, 34.694, 48.756, -96.980].</td></tr>
<tr><td>August 13, 2018</td><td>Debris flow enhancements (liquid limit from surgo, SBS area based on grid).</td></tr>
<tr><td>July 31, 2018</td><td>Fixed layout bug with screens with 1280px width.</td></tr>
<tr><td>July 30, 2018</td><td>Updated phosphorus maps for Lake Tahoe. New WEPP binary to fix missing chanwb
                              output. Bug fix for hillslope delineation in locations below 1m in elevation.</td></tr>
<tr><td>July 20, 2018</td><td>frost submodule removed from hillslope processing. WEPP bug fix for
                              empty chanwb outputs.</td></tr>
<tr><td>June 14, 2018</td><td>Disturbed WEPP managements added to single landuse selection. Single landuse
                              selection added. Support for 98.4 management files.</td></tr>
<tr><td>June 10, 2018</td><td>Minor map and interface enhancements.</td></tr>
<tr><td>June 8, 2018</td><td>2006.2 WEPP soil support added, county level soil database for NSERL.</td></tr>
<tr><td>June 3, 2018</td><td>Coeur d'Alene added.</td></tr>
<tr><td>May 31, 2018</td><td>Lake Tahoe (LT) Homepage added.</td></tr>
<tr><td>May 18, 2018</td><td>Observed climates for Lake Tahoe added to interface.</td></tr>
<tr><td>May 15, 2018</td><td>WEPP runs hillslopes in parallel.</td></tr>
<tr><td>May 11, 2018</td><td>Debris flow model added.</td></tr>
<tr><td>April 23, 2018</td><td>Soil restrictive layer scaled by 1/100.</td></tr>
<tr><td>April 7, 2018</td><td>Power User Panel added to interface.</td></tr>
<tr><td>April 5, 2018</td><td>Total yearly water balance report.</td></tr>
<tr><td>April 4, 2018</td><td>totalwatsed export added.</td></tr>
<tr><td>April 3, 2018</td><td>Watershed preparation details added.</td></tr>
<tr><td>April 3, 2018</td><td>Watershed preparation details added.</td></tr>
<tr><td>Mar 26, 2018</td><td>Projects can be set READONLY and PUBLIC.</td></tr>
<tr><td>Mar 21, 2018</td><td>Project archive export added.</td></tr>
<tr><td>Mar 20, 2018</td><td>Return Period Analysis implemented.</td></tr>
</tbody>
</table> 


# References

see [References](References.md)


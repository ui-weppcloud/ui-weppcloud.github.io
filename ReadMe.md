# WEPPcloud

## About
The Water Erosion Prediction Project (WEPP) model is a hydrology and erosion model wildly used by academics and land managers to assess the effects of land management changes on runoff and sediment yield. Even for advanced users, data preparation is a lengthy process that involves downloading various maps and datasets, and processing and saving the data in formats that are readable by the model. 

[WEPPcloud](https://wepp1.nkn.uidaho.edu/weppcloud) is an online interface for the WEPP model that facilitates input data preparation and hydrologic simulations from any computer connected to the internet. The user can zoom in to a location, identify an area of interest, and delineate a watershed. Then based on a series of options that involve selection of soils, managements, and weather information from national or locally-stored databases, the user can quickly get estimates of runoff and soil erosion for their watershed of interest. Results are displayed in the web browser as text files and as geospatial maps and are also downloadable. Most hydrologic simulations can be completed within a few minutes, depending on the size of the watershed. 

WEPPcloud was mainly developed for forestry applications as a joint effort between University of Idaho and Forest Service Rocky Mountain Research Station. Other contributions to the applicaiton include USDA ARS, Swansea University, and Michigan Technological University.

## User Accounts
WEPPcloud allows users to create and store model runs. Users can also create accounts to access "PowerUser" features or to find and collaborate on model runs with other users. By default, anonymous runs are always publicly available via the URL to the project. Be aware that any resources, such as soil burn severity maps, that are uploaded to the interface would be potentially publicly available. If logged in the created runs are private by default and are only available to the project owner and collaborators. Private runs can be made publicly available if collaborators wish to share them. It is suggested that the runs also be made "Read Only" to avoid having viewers accidentally alter the model results.

User accounts can be created here:
[https://wepp1.nkn.uidaho.edu/weppcloud/register](https://wepp1.nkn.uidaho.edu/weppcloud/register)

GPDR: We ask for your first and last name to provide polite coorespondances. Your email is used as a unique indentifier for your account. None of your personal identifiable information is shared with third-parties. 

## Locales

WEPPcloud relies on publically available databases to parameterize the necessary WEPP inputs. The various WEPPcloud interfaces are more-or-less supported in the following locales:

- Conterminous United States
- Europe
- Australia

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

Obtains soils and managements from the [http://rred.mtri.org/rred](RRED). These use 2006 soils and 97.3 managements.

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

## Getting Started

See the [QuickStart](QuickStart)

## Help / Feedback

For general assistance or questions please contact Mariana Dobre at mdobre@uidaho.edu. 

For technical assistance please contact Roger Lew at rogerlew@uidaho.edu. Providing the url to the run in question and a screenshot of the problem would also be helpful.

For questions regarding the WEPP model please contact Anurag Srivastava at srivanu@idaho.edu.

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

## References




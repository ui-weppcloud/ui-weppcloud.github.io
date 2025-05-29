# Quick Start Reference Guide


## Web Browser

Modern browsers including Firefox, Chrome, Safari, and Edge should work with WEPPcloud. For best results use a laptop/desktop sized display. Internet Explorer is not supported


## User Accounts (Optional)

WEPPcloud allows users to create and store model runs. Users can also create accounts to save runs and collaborate on model runs with other users. By default, anonymous runs are always publicly available via the URL to the project. Be aware that any resources, such as soil burn severity maps, that are uploaded to the interface would be potentially publicly available. If logged in the created runs are private by default and are only available to the project owner and collaborators. Private runs can be made publicly available if collaborators wish to share them. It is suggested that the runs also be made "Read Only" to avoid having viewers accidentally alter the model results.

User accounts can be created here:
[https://wepp.cloud/weppcloud/register](https://wepp.cloud/weppcloud/register)

GPDR: We ask for your first and last name to provide polite coorespondances. Your email is used as a unique indentifier for your account. None of your personal identifiable information is shared with third-parties. 


## Creating a Project

WEPPcloud projects are also referred to as runs, as in _model runs_. To start a project click on the "Start Disturbed Run (CONUS)" button.
<img width="1184" alt="Start WEPPcloud Run" src="https://github.com/user-attachments/assets/c54b730b-f1dd-4e05-be5e-7cac6d4f9f4d" />
This creates a new project folder on the server.


### RunID and Interface Config

The newly created project has a unique RunID, underlined in red. This RunID is unique for every project and can be used to return to the project as well as for debugging purposes. In the cloud a project folder is created with this RunID.

A large array of functionality is provided by WEPPcloud through the use of interface configurations. Each interface has a configuration file ("config file") that can specify specific boundaries for the interface as well as specific datasets and processing for the interface. The config is specified after the RunID in the URL. In the image below it is underlined in blue. The "0" config is for the US (Most of the config names are more meaningful).

![RunID and Interface Config](https://user-images.githubusercontent.com/3652906/68883157-4ee25080-06c5-11ea-9b69-66f314c5a7ed.png)


## Selecting Map Extent

The first step is to specify the boundary for the catchment you wish to model. The extent of the map is used as the boundary for modeling. The map has controls to zoom in and out. It is also possible to double click on the map to zoom in. The map can be panned by clicking and dragging. The extent can also be specified by holding down shift will drawing a box. This is especially helpful when zoomed out.


## Channel Delineation

The channel delineation is limited in the size of catchment areas that can be delineated. The limit is dependent on the TOPAZ processing parameters for Minimum Channel Length (MCL) and Critical Subcatchment Area (CSA). For this reason, it is suggested that you zoom into a level of 13 or greater. 

When setting the extent it is important that the ridgeline of the catchment you wish to model is within the boundary of the map. TOPAZ will fail if the catchment falls outside of the map when delineating subcatchments.

![Map](https://user-images.githubusercontent.com/3652906/68883858-b77dfd00-06c6-11ea-8630-1c34b6da480a.png)


### TOPAZ

WEPPCloud uses TOPAZ to parameterize topographic data from DEMs to create hillslope profiles called sub-catchments for each watershed. TOPAZ delineates a channel network from the DEM based on the steepest downslope path from each raster cell (pixel) from the 8 cells surrounding it (Garbrecht and Martz 1997). Adjustments can be made to the detail of the channel network by changing values of Mean Source Channel Length (MSCL) and Critical Source Area (CSA). The MSCL is the shortest length that any channel is allowed to be. The CSA defines the minimum drainage area below which a permanent channel forms (Garbrecht and Martz 1997). Setting these to low values will increase the density of channels, which is useful when defining small watersheds. From the defined channel network, the user specifies the exact watershed outlet and TOPAZ generates the sub-catchments that delineate the watershed. Each sub-catchment represents the direct contributing area for each side of the drainage (Garbrecht and Martz 1997) and has homogeneous slope and aspect (Renschler 2002).

<dl>
<dt>Minimum Source Channel Length (MSCL)</dt>
<dd>The shortest length that any channel is allowed to be. The default value is set to 60 m, which means that atleast two 30-m DEM pixel is needed to initiate the headwater channel.</dd>
<dt>Critical Source Area (CSA)</dt>
<dd>The minimum drainage area below which a permanent channel forms. The default value is set to 4 ha.</dd>
</dl>


### Repeatable Delineation

The watershed will delineate differently if the map extent, TOPAZ parameters, or outlet location are changed. To get the same watershed to delineate you can manually set the center location of the map and zoom level as well as specify the longitude and latitude of the outlet.


## Subcatchment Delineation

Subcatchments whether delineated by TOPAZ or TauDEM will always have a TOPAZ Identifier as well as a WEPP Identifier. The TOPAZ identifiers (ids) are assigned in a clockwise fashion starting at the outlet. TOPAZ uses a numbering scheme where all the subcatchments end with "1," "2," or "3" and all the channels end with "4." Subcatchments to the right of a junction end with "2," and subcatchments to the left and with "3." Subcatchments that drain into a channel end with "1." Subcatchments and channels that are closer to the outlet typically have lower numbers.

The WEPP structure file requires sequential numbering and hence the need for having both TOPAZ identifiers and WEPP identifiers.


## Managements

Readily available managements for WEPP use are provided in the drop-down menu. First, the interface determines the dominant landuse for each hillslope based on 2011 National Land Cover Data (NLCD) map. Then readily available managements are assigned to land uses. User might want to refine managements for better representation of croplands and forestland practices. 

Note: The current interface does not have the capability to build/edit managements for simplicity purpose. Future versions will include include this capability.

Two options are provided for management selection.
<dl>
<dtDetermine by hillslope</dt>
<dd>Automatically determines management per hillslope.</dd>
<dt>Single Landuse for watershed</dt>
<dd>Manually select a management from the drop-down list.</dd>
</dl>


### Modifying landuses

Some interfaces allow the user to apply treatments through the map at the top of the screen. First build the managements. The landuse covers will be assigned from the management database. The cover values can be modified from the default values by clicking the gear icon. Below the selected landuse a dialog should appear to allow for setting groud cover, interill, and rill cover values. The values are saved when the selection is made.

![Modifying landuse cover](https://user-images.githubusercontent.com/3652906/70350832-66bc7880-181c-11ea-9c4c-48747164a57f.png)

The landuses can be viewed on the map by selecting the "Dominant Landcover" layer on the layer tab to the right of the map.
![Viewing Landuses](https://user-images.githubusercontent.com/3652906/70351880-bdc34d00-181e-11ea-98d6-0adadd9e153d.png)

## Soils

(US) Two databases for soils are available in WEPPcloud: SSURGO and STATSGO. The SSURGO database is used as default and is queried during the watershed delineation process. Alternatively, when SSURGO database is not available, STATSGO database will be used to build the soil files. 

Three options are provided for determining soils.
<dl>
<dtDetermine by hillslope</dt>
<dd>Automatically creates a soil file for each hillslope from the available soil database. (For WEPP-PEP only soil texture is used to identify the correct soil from the WEPP-PEP soil database.)</dd>
<dt>Single Soil for watershed (MUKEY)</dt>
<dd>Assign one soil for the entire watershed based on the SSURGO/STATSGO MUKEY.</dd>
<dt>Single Soil for Watershed (Database)</dt>
<dd>Select a soil for the entire watershed from a local database.</dd>
</dl>

Most of the time WEPPcloud builds WEPP soil files (7778 format) parameterized from the USDA's SSURGO/STATSGO database (for US Locale; not with WEPP-PEP or RRED). After building a summary table is provided for reviewing the soils within the catchment. The soils file names are taken from the SSURGO/STATSGO MUKEYs.

![Soil Building](https://user-images.githubusercontent.com/3652906/70351636-3970ca00-181e-11ea-99af-70b06c790c54.png)

## Climate

The climate input processing relies heavily on CLIGEN. 

WEPP uses CLIGEN climate files as input. CLIGEN is a climate generator capable of generating stochastic daily climates, single storm events, or observed climates from daily temperature minimum, maximum, and precipitation series. 

CLIGEN uses station parameter or (.par) files. We use the NSERL CLIGEN database of weather stations with monthly parameters for US Locales and a GHCN based database has global coverage for Europe and Australia.  The first step in building a climate is to select a weather station as a basis for the climate files. The recommended method to select a climate station is to select the "Multi-Factor Ranking (Considers Distance, Elevation, and Climate)" radio button. Once selected, WEPPcloud evaluates 2400+ stations to find the best match based on distance, elevation, and monthly climate values from PRISM. After a few seconds the best match should appear in the selection dialog, and summary climate statistics should appear below the selected station.

![Climate Station Selection](https://user-images.githubusercontent.com/3652906/70352648-7342d000-1820-11ea-8650-4189042ec4bd.png)

The selection control lists the 10 best matching stations in descending order. After the station description in parenthesis is an ordinal ranking metric (lower is better) and the distance from the centroid of the catchment. The user can select any station in the list.

![Station Selection](https://user-images.githubusercontent.com/3652906/70352793-cc126880-1820-11ea-9f4a-dacdf452dc4e.png)
CLIGEN is a stochastic weather generator but also supports generating daily timeseries climate files if daily minimum and maximum temperatures and daily precipitations are available. CLIGEN also has the ability to produce single storm climate files **Please note that the WEPP outputs for Single Storm Events are different from the Continuous outputs and not all of post wepp functionality including WATAR**


### “Vanilla” CLIGEN (Stochastic weather generation). 

The daily climate is generated using the CLIGEN (CLImate GENerator) and the nearest parameter (.PAR) file. Values in .PAR files includes monthly statistical values derived using the NCDC-NOAA weather stations from 1974 through 2013.


###	PRISM Modified 

Monthly values of precipitation, maximum and minimum, wet/dry days in “Vanilla” CLIGEN .PAR file is replaced with PRISM normal covering the period 1981-2010


### Observed (DAYMET)

Interpolated 1-km spatial resolution daily observed precipitation, maximum and minimum temperatures are obtained from the data source. This dataset is available from 1980-2016. Other required weather inputs in the climate files are generated using nearest CLIGEN station.


###	Observed (DAYMET) with PRISM Revision 

Interpolated 1-km spatial resolution daily observed precipitation, maximum and minimum temperatures are obtained from the data source. This dataset is available from 1980-present. Other required weather inputs in the climate files are generated using nearest CLIGEN station.


### Observed (GRIDMET) with PRISM Revision

Interpolated 4-km spatial resolution daily observed precipitation, maximum and minimum temperatures are obtained from the data source. This dataset is available from 1980-present. Other required weather inputs in the climate files are generated using nearest CLIGEN station.


### Future (CMIP5) 

Interpolated 4-km spatial resolution daily observed precipitation, maximum and minimum temperatures are obtained from the data source. This dataset is available from 2006-2099. Other required weather inputs in the climate files are generated using nearest CLIGEN station.


### Single Storm 

User-defined storm for event-wise simulation

<dl>
<dt>Storm Amount</dt>
<dd>Enter the precipitation depth in inches or in millimeters.</dd>
<dt>Storm Duration</dt>
<dd>Enter the duration of the storm (in hours).</dd>
<dt>% Duration to Peak Intensity</dt>
<dd>Enter the time (in percent of the storm duration value) at which the peak intensity of the storm occurs. Note that this is not a time value, but a percentage of the total duration value which was entered in the previous field. For instance, if the peak intensity occurs at hour 4 of a 10-hour storm, then you would enter 40 (%) or 0.4 here.</dd>
<dt>Max Intensity</dt>
<dd>Enter the peak rainfall intensity of the storm in inches per hour or millimeters per hour.</dd>
</dl>


## Watershed Preparation Report

Watershed Preparation details describes hillslopes and channels associations with the aforementioned four inputs climate, management, soil, and slope. The table described here might also be useful for referencing variables/values in the output reports with subcatchment delineation map.  


## WEPP Advanced Options


### Flowpath Processing

WEPP is ran for each flowpath in the subcatchments. The plot files are used to produce a gridded soil loss/deposition map. This is only available with the TOPAZ delineation backend.

#### Slope definitions

The flowpath slope definitions are constructed by watershed_abstraction routine in wepppy. For each cell in a hillslope a flowpath is constructed by walking down the slope identified by the slope grid from topaz. A distance array is constructed from the pixel coordinates and the slope points are truncated to 19 by linear interpolation if more than 19 points are defining the slope.

#### Soils, Managements, and Climates

Flowpath runs use the soil, management, and climate of their parent hillslope.

#### Gridded Output

Each flowpath is ran through wepp and a plot file is generated by wepp. This file contains distance downslope, elevation, and soil deposition/loss (loss is positive). The soil dep/loss is interpolated against the normalized distance points from the flowpaths slope file to obtain a estimate at each pixel value. Many flowpaths might run through a particular cell. The dep/loss estimates are aggregated by taking the average of the non-zero values at each cell.

### Baseflow Processing

Daily simulated streamflow at the outlet of a watershed is composed of surface runoff, lateral flow (i.e. shallow subsurface stormflow) and baseflow. Baseflow is assumed to be routed to the stream outlet point from an aquifer network with a volumetric discharge following linear reservoir theory. The single aquifer is assumed to receive all water which vertically percolates below all upland hillslopes. It is assumed that the recharge to the aquifer is limited by the upslope drainage area defined by the surface topography and that there is no lateral groundwater exchange across watershed boundaries.  Following linear reservoir theory the baseflow from an aquifer (Qbase in mm/day) is calculated as a fixed percentage (k, the baseflow coefficient having units of 1/days) of the amount of water stored in the aquifer (S is total water volume in the aquifer in units of mm) using the following equation: 

Q<sub>base</sub> = k * S

The linear coefficient can be best estimated by slope of the ln (time) vs ln (flow) hydrograph during drought flow conditions.  The default parameter for the linear coefficient is k = 0.04 1/day.  

In cases where the groundwater aquifer leaks water to either a deeper more regional aquifer or laterally across the watershed boundary or below the stream gage then users can optionally define a secondary aquifer loss (Qaq) based on second deep seepage linear coefficient (kds in 1/day units) based on the same storage amount S.  

Q<sub>aq</sub> = k<sub>ds</sub> * S

By default, the model assumes there is no other deep aquifer loss and therefore assumes Kds = 0. The amount of groundwater storage in the aquifer on any given day (i) is determined based on the follow equation.

S<sub>i</sub> = S<sub>i-1</sub> - Q<sub>base,i</sub> – Q<sub>aq,i</sub>

where S<sub>i-1</sub> is the groundwater storage volume from the previous day in the simulation.  The model assumes the initial amount of water storage in the aquifer on the first day of the simulation is 200 mm.

Baseflow is simulated both at the watershed outlet and within the stream network if the upslope area above a point in the stream network is greater than user defined critical watershed area.  The default critical area is 1.0 ha.  This value should be assigned a larger magnitude in more arid locations.  


### Pollutant Processing 

This is an optional selection that allows users to estimate a pollutant based on known concentrations provided by the user. The estimates are simplistic and do not account for sorption, desorption, mineralization, or immobilization. They only provide rough estimates of the pollutant being transported by both water (via surface runoff, lateral flow, and baseflow) and sediments. 


### FAO Penman-Monteith

FAO 56 Penman-Monteith method for reference and actual evapotranspiration (ET) developed by Allen et al. (1998) (Wu and Dun, 2004)  


## Run WEPP

Once the user selects all the soil, management, and climate options, all the necessary input files are automatically created for the user. At this stage the user can run the WEPP model, which will wake anywhere between a few seconds, for smaller watersheds and several minutes or even an hour, for larger watersheds. The status bar should indicate the hillslopes being ran. Once successfully completed, the summary bar will provide information of the number of hillslopes ran and elapsed time. If one or more input files are missing, the interface will error, alerting the user of the missing information. 


## WEPP Results


### Watershed Loss Summary

The Watershed Loss Summary output frame provides average annual simulated hydrologic and sediment yield metrics in three accessible tables from the watershed outlet, each hillslope (i.e. subcatchment) in the watershed, and each stream channel in the watershed, respectively.  

The watershed loss results at the outlet include both absolute mass and volume-based metrics as well as normalized mass and volume output per unit upslope watershed area including: 

-	average annual precipitation 
-	water discharge (streamflow from the watershed outlet) 
-	total hillslope sediment loss 
-	total channel sediment loss 
-	sediment discharge at the watershed outlet (net sediment yield delivered to the watershed outlet) 
-	an overall sediment deliver ratio defined as the total sediment loss from the hillslopes divided by the total sediment discharge at the watershed outlet  

The _Average Annual Summary for Subcatchments_ table provides information on:

-	hillslope id (both WEPP and Topaz based ID numbers) 
- landuse ID number 
-	soil MUKEY ID 
-	hillslope length 
-	hillslope area 
-	runoff 
-	soil loss (i.e. detachment or erosion rate mass/hillslope area) 
-	sediment deposition 
-	sediment yield (i.e. mass of sediment delivered to the outlet of the hillslope)

The _Average Annual Summary for Channels_ table provides hydrologic and sediment transport metrics for each channel


### Return Periods Report

Understanding the variability and risk of soil erosion is critical for forest managements. This section reports return period assessment for precipitation depth, runoff, peak discharge, 10-min and 30-min peak intensity, and sediment yield using the Weibull plotting position method based on annual maximum series.


### Sediment Delivery Report

Provides information regarding the delivery of sediment at the outlet, from the channels, and from the hillslopes. This report also provides class particle size fractions.


### Water Balance Report

The Average Annual Report provides major water balance components of each hillslope:
-	precipitation 
-	ET (transpiration + evapotranspiration) 
-	surface runoff 
-	subsurface lateral flow 
-	deep seepage


### Daily Streamflow (Runoff + Subsurface Lateral Flow + Baseflow) Graph

This figure shows the contribution of daily runoff, subsurface lateral flow, and baseflow to streamflow averaged over hillslopes in a watershed.


### Observed Data Model Fit 

TODO @roger_lew

## Export Functionality


### Download project

#### Zip Archive directly from interface

Once the WEPP model runs are completed, the user can download all the input and output files as a zip archive, which contains several folders with all the maps and data used in the analysis. **This can be somewhat hit or miss with large projects. For large project consider using wget.**

#### Using wget

Projects can be acquired using wget. [wepppy-win-bootstrap](https://github.com/rogerlew/wepppy-win-bootstrap) provides a script and instructions on downloading projects with wget.


### Project Directory Structure

Description of all the available files and folders:


<dl>
<dt>climate (dir)</dt>
<dd>contains all the PAR files and .cli files for each hillslope and for watershed.</dd>
<dt>dem (dir)</dt>
<dd>contains the DEM map used in the analysis as well as a topaz sub directory with all the maps created during the watershed delineation.</dd>
<dt>export (dir)</dt>
<dd>channels and subcatchments files in ArcGIS format containing topographic characteristics (such as slope, aspect, or length), input data (soil and management), and output information (runoff, lateral flow, baseflow, sediment, pollutant, etc.). The file also contains the several GeoTIFF maps used in the model run.</dd>
<dt>landuse (dir)</dt>
<dd>contains landuse map (e.g. ascii map with the 2016 National Land Cover Database (NLCD) for US Locale. The NLCD codes are translated into WEPP-equivalent managements based the mapping for the configuration.) </dd>
<dt>observed (dir)</dt>
<dd>files containing the observed data (if) provided by the user</dd>
<dt>watershed (dir)</dt>
<dd>files containing slope information for each channel and hillslope</dd>
<dt>wepp/flowpaths (dir)</dt>
<dd>if the flowpath option is selected, the WEPP model will be run for each map pixel. This folder contains a runs folder with all the input data and an output folder with the runoff and soil loss for each flowpath</dd>
<dt>wepp/output (dir)</dt>
<dd>contains all the WEPP model output files </dd>
<dt>wepp/plots (dir)</dt>
<dd>maps of gridded soil loss when flowpaths are ran</dd>
<dt>wepp/runs (dir)</dt>
<dd>folder containing all the WEPP model input files</dd>
<dt>*.nodb</dt>
<dd>JSON serialized instances of wepppy.nodb classes used by WEPPcloud. These contain metadata related to the project. They are viewable in FireFox/Notepad++ etc.</dd>
</dl>


#### More on NoDB Files

WEPPcloud project runs are designed to be self-contained and to not rely on a centralized database. This is accomplished by storing model run information in JSON (JavaScript Object Notation) files. These are the .nodb files in the project's root folder. The .nodb files are serialized Python class instances that greatly simplifies modeling from a programmatic perspective. Even for non-programmers these files can be informative. Loading the topaz.nodb shows the following:
![topaz.nodb contents](https://user-images.githubusercontent.com/3652906/68886461-1b56f480-06cc-11ea-8291-d215764734c8.png)


### Daily Water Balance Report 

The ['totalwatsed.csv'](https://wepp1.nkn.uidaho.edu/weppcloud/runs/lt_Watershed_10_CurCond.2020.cl532.ki5krcs.chn_cs25/lt/resources/wepp/totalwatsed.csv) file contains all the water balance components and sediment yield combined across the hillslopes in a watershed. The report also has daily streamflow and sediment yield at the outlet of the watershed that can be used to compare results against observed values. Users can open this file in excel and analyze the results as desired. The pivot table in excel can be used to summarize the results by calendar year or water year.

### Arcmap Resources
Quick link to the output results in ESRI's proprietary shapefile. These model outputs are similar to the ones from the export folder from the [Zip Archive](https://wepp1.nkn.uidaho.edu/weppcloud/runs/lt_Watershed_10_CurCond.2020.cl532.ki5krcs.chn_cs25/lt/export/arcmap/).

### ERMiT 

The ERMiToutput files allow users to directly input hillslope parameters directly into Erosion Risk Management Tool (ERMiT) Batch or Disturbed WEPP Batch spreadsheets for further analysis. ERMiT and ERMiT Batch are provided to allow users to compare various post-fire erosion control treatments in a probabilistic output. The ERMiT Batch allows users to examine all of the hillslopes in a watershed at once with various output options to determine which hillslopes have the probability of the highest (or lowest) erosion rates, how erosion mitigation treatments (i.e. mulching, seeding, etc.) will affect the hillslope erosion rates and how will recovery time effect erosion rates for up to 5 years post-fire. Disturbed WEPP and Disturbed WEPP Batch allows for analyzing various forest conditions and management options on hillslope erosion and provide probability of erosion in the first year after disturbance.

#### Download Hillslope Input CSV for ERMiT Batch and Disturbed WEPP Batch 

This link will generate an input CSV file as a zip file. Download to your computer and extract the two files. The first is a Excel spreadsheet CSV file that is the input to ERMiT Batch or Disturbed WEPP. The second is metadata file providing the user with information on WEPPcloud run date, number of hillslopes, watershed outlet, climate station selected and description of all the columns in the CSV file.

#### Download the ERMiT Batch and Disturbed WEPP Batch Processing Spreadsheets

This link connects the user to the ERMiT and Disturbed WEPP Batch home page where you can download ERMiT or Disturbed WEPP Batch spreadsheets. Once downloaded, the user can import the CSV file by following directions in ERMIT Batch or Disturbed WEPP Batch spreadsheets.




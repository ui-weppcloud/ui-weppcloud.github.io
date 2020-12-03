# Quick Start Reference Guide

## Web Browser

Modern browsers including Firefox, Chrome, Safari, and Edge should work with WEPPcloud. For best results use a laptop/desktop sized display. Internet Explorer is not supported

## Channel Delineation

The extent of the map sets the boundary for obtaining DEM and other datasets. Move the map so it encompasses the catchment you wish to delineate.

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

Subcatchments whether delineated by TOPAZ or TauDEM will always have a TOPAZ Identifier as well as a WEPP Identifier. The TOPAZ identifiers (ids) are assigned in a clockwise fashion starting at the outlet. Left subcatchments always end in 1, right subcatchments end in 2, the source subcatchments end in 0, and the channels end in 4.

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

Some interfaces allow the user to apply treatments through the map at the top of the screen. First build the managements. Then, select the management modification tool and either select subcatchments to change on the map or enter TOPAZ IDs.

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

## Climate

The climate input processing relies heavily on CLIGEN. CLIGEN uses station parameter or (.par) files. The most extensive database for CLIGEN coverage is across the US but a GHCN based database has global coverage for Europe and Australia. CLIGEN is a stochastic weather generator but also supports generating daily timeseries climate files if daily minimum and maximum temperatures and daily precipitations are available. CLIGEN also has the ability to produce single storm climate files **Please note that the WEPP outputs for Single Storm Events are different from the Continuous outputs and not all of post wepp functionality including WATAR**

### “Vanilla” CLIGEN (Stochastic weather generation). 

The daily climate is generated using the CLIGEN (CLImate GENerator) and the nearest parameter (.PAR) file. Values in .PAR files includes monthly statistical values derived using the NCDC-NOAA weather stations from 1974 through 2013.

###	PRISM Modified 

Monthly values of precipitation, maximum and minimum, wet/dry days in “Vanilla” CLIGEN .PAR file is replaced with PRISM normal covering the period 1981-2010

### Observed (DAYMET)

Interpolated 1-km spatial resolution daily observed precipitation, maximum and minimum temperatures are obtained from the data source. This dataset is available from 1980-2016. Other required weather inputs in the climate files are generated using nearest CLIGEN station

###	Observed (DAYMET) with PRISM Revision 

Interpolated 1-km spatial resolution daily observed precipitation, maximum and minimum temperatures are obtained from the data source. This dataset is available from 1980-present. Other required weather inputs in the climate files are generated using nearest CLIGEN station

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




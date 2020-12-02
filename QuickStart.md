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
<dt>o	Single Soil for Watershed (Database)</dt>
<dd>Select a soil for the entire watershed from a local database.</dd>
</dl>

## Climate

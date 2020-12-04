# WEPP FAQ:

**_How do you calibrate the WEPP model?_**

The WEPP model is a process-based model where most of the key parameters can be directly measured, estimated, or acquired from common spatially-explicit data sources (e.g. STATSGO, SSURGO). Many of the recent improvements to the web interface have focused on providing the model with the highest resolution spatial weather data using publicly available mapping data sets as often the key issue in hydrologic models is to capture variability in precipitation and temperature across a landscape. The soil parameters are extracted directly from the soil survey and do not rely on statistical decay coefficients or exponents that can only be fixed using historic observed data. We have adopted this approach as the model is often applied as a decision support tool in ungauged basins where calibration is not possible. We do have the ability to calibrate either manually or using an automated approach (e.g. Model-independent parameter estimation package, PEST model) but we have often found reasonable predictions without much calibration, especially for runoff.  

**_How accurate is the WEPP model?_**

The difference in observed soil erosion rates from duplicate hillslope plots side by side to each other are often on the order of 50%. The natural variability and complexity in a landscape can never be fully captured in a model. Annual or monthly predictions (e.g. annual water yield or sediment load) will likely be much more reliable than daily predictions. Sub-watershed and hillslope scale predictions will likely be less accurate than watershed basin predictions. Absolute accuracy will be poorer than the ability for WEPP to predict relative variability across a basin and in-response to treatments. The hillslope version of WEPP has been validated for post fire conditions with field collected hillslope erosion data with acceptable accuracy (Robichaud et al. 2016). The watershed version of WEPP has been validated after the 2011 Wallow Fire in Arizona with acceptable accuracy (Quinn et al., 2018). We often use the 50% variability as a good rule of thumb for explicit model accuracy.

**_What are the most sensitive parameters in the model?_** 

Other than precipitation and temperature inputs, the soil parameters (soil depth, hydraulic conductivity of the lower restrictive layer, effective hydraulic conductivity of the surface soil layer) are often the most sensitive parameters for predicting runoff. The soil surface cover, interrill erodibility, rill erodibility and critical shear are the most sensitive parameters for simulating soil erosion rates. The late summer streamflows and hydrograph shape are often most sensitive to lateral hydraulic conductivity and the baseflow recession coefficient. The baseflow recession coefficient is typically stable across a region and can be fixed using streamflow from the nearest stream gauge station. Soil surface cover is easily measured and therefore only requires knowledge of the recovery or impact to ground cover.

**_How is vegetative recovery and residue decay simulated?_**

Without nitrogen and carbon cycling, vegetative growth and residue decay are based on soil moisture and temperature relationships that drive vegetation growth and decay. Other models such as Regional Hydro-Ecological Simulation System, RHESSYS, can be used to predict the vegetative regrowth as well. With RHESSYS, either direct vegetative characteristic maps (e.g. LAI, canopy cover) can be fed to WEPP or regrowth curves can be extracted if time series outputs are desired rather than the probabilistic outputs described below.

**_How well does WEPP predict stream channel erosion?_**

Stream channel erosion in WEPP is simulated using a somewhat simplistic approach relative to some of the more advanced hydrodynamic stream channel models (e.g. CONCEPTS, CCHE1D, HEC-6) as stream cross-sectional characteristics are empirically assigned to a stream based on the ‘order’ of the stream (e.g. 1st order stream, 2nd order stream). Particle size of the bed, critical shear, bank/bed erodibility and depth to an impermeable layer parameters are defined for each stream based on the dominant soil type along the stream channel and the stream order. The ability to simulate stream channel erosion has only been recently developed and tested for watersheds greater than 1 square mile. Simulation results from forested watersheds in Idaho, Arizona, and Lake Tahoe, California, indicate good agreement between measured and observed sediment load and the response in sediment load to thinning and wildfire disturbances.

**_Is carbon/nitrogen cycling included in the model?_**

No, the WEPP watershed interface does not simulate changes in soil carbon or nitrogen cycling. There are beta versions of the model at the USDA-ARS and University of Idaho, which have some algorithms for this but it is currently under development.

**_How does the model generate probabilistic runoff and erosion output for each year following a disturbance (e.g. post-fire)?_**
 
The model provides the probability of any magnitude erosion event happening on specific years by essentially running the model 100 times under the same vegetative and soil conditions. Using these 100 simulations as 100 different potential realizations, we calculate exceedance probabilities and return periods for specific magnitude events (e.g. 2-yr return period). Each year following a disturbance or management treatment, there could be unique vegetative and soil conditions. For each unique vegetative soil conditions, the model simulates 100 possible weather scenarios that could occur and provides probabilistic outputs.

**_What is the largest size watershed that someone should run with WEPP?_**

Currently the WEPP watershed interface is limited to 1000 hillslope runs. Typically, simulations are for 10-20 square mile watersheds or smaller. Although this upper limit can be extended, there are several reasons for this upper limitation. First, the simulation run time increases with watershed size. Second, the stream channel algorithms require that runoff generated within a day will leave the watershed outlet in the same day (i.e. water storage in the channel is not simulated). Third, the simplistic in stream sediment transport algorithms will not be able to simulate the complex sediment transport dynamics of large rivers. Fourth, when users apply WEPP to large watersheds they tend to delineate large, long, hillslopes where erosion can be dominated by large gully erosion rather than rill erosion which WEPP is best suited to simulation. If the purpose of the model is to provide hillslope erosion rates rather than predict sediment load or peak flows from a watershed, then the model can be run on larger watersheds, and in this case, we recommend users to ignore the watershed outlet outputs. The strength of WEPP is its ability to predict both the spatial variability of runoff and erosion within a landscape. There have been several recent studies (Miller et al. 2011) where WEPP has been used to simulate hillslope erosion for the entire Pacific Northwest region.

**_Can WEPP predict debris flows or landslides?_**

The WEPPcloud watershed interface can predict the probability of occurrence and magnitude of debris flow after wildfire using the Cannon et al (2010) model. We want to emphasize caution when using this tool as there are some empirical parameters in there that might not be appropriate for some watersheds. The USGS provides the most up-to-date post fire debris flow probability information (https://www.usgs.gov/center-news/debris-flow-forecasts-wildfires) for the US. WEPP does not predict landslides, however, Level I Stability Analysis (LISA) and Deterministic Level I Stability Analysis (D-LISA) are available on the Forest Service WEPP website (https://forest.moscowfsl.wsu.edu/engr/slopesw.html).

**_What is the difference between all these WEPP Tools (ERMiT, Disturbed WEPP, FSWEPP, GEOWEPP, QWEPP, WEPPcloud)?_**

All these models are based fundamentally on the same core Water Erosion Prediction Project (WEPP) model (Nearing et al., 1989, Flanagan and Nearing, 1995). We have developed these unique tools to try to provide products that match the objectives, knowledge, skillset, spatial scale, and required application of the end-user.  Some of these tools provide output for a single hillslope (e.g. ERMiT, Disturbed WEPP, WEPP:road). 
In developing these tools we fix most of the input parameters to the model based on expert knowledge and experience from field data for the specific application (e.g. road erosion studies, post-fire runoff/erosion studies).  We allow the user to select the climate, soil type, topographic profile, and some of the broad management characteristics but keep the model inputs simple. Other tools are developed to simulate larger complex catchments and watershed using GIS based tools/interfaces. GEOWEPP operates within ESRI software (ARCGIS), QWEPP operates within QGIS, and WEPPcloud is an online interface which does not require the user to own or download GIS software to their personal computer. These watershed tools require a bit more training and learning to operate.

**_Can WEPP simulate reservoirs and their effect on settling out sediments and modifying peak flows?_**

WEPP was developed with the option to simulate small sediment ponds downstream of agricultural fields. This has not been incorporated into the online watershed interface and to our knowledge the algorithm has seldom been used in model applications. It certainly was not developed to simulate impacts of large reservoirs on sediment and peak flows.

**_Can the WEPP watershed interface simulate the impacts of roads on runoff and sediment delivery to a watershed?_**

WEPP has been applied to large road networks and we are working on getting these networks automatically defined in the WEPP interface. Most often the erosion from road networks is quantified using the online FS-WEPP interface tools (https://forest.moscowfsl.wsu.edu/fswepp/), see the WEPP:Road and WEPP:Road Batch tools after the road segments are manually delineated in a watershed (see Brooks et al., 2016).
  
# References

see [References](References)

# Disturbed Land Soil Table Parameters for WEPPcloud

The disturbed land soil table in WEPPcloud contains parameters that define soil properties for various land use categories and soil textures. These parameters are essential for modeling erosion and hydrology in disturbed lands using the WEPP (Water Erosion Prediction Project) model. The table includes data for combinations of land use (e.g., agriculture crops, forest, bare) and soil texture (clay loam, loam, sand loam, silt loam).

## Table of Parameters

| Parameter   | Description                                                       | Units     |  Notes   |
|-------------|-------------------------------------------------------------------|-----------|----------|
| luse        | Land use category (disturbed class from the land use map)         | -         |          |
| stext       | Soil texture (clay loam, loam, sand loam, silt loam)              | -         |          |
| ki          | Interrill erodibility                                            | kg·s/m⁴   |          |
| kr          | Rill erodibility                                                 | s/m       |          |
| shcrit      | Critical shear stress                                            | Pa        |          |
| avke        | Effective hydraulic conductivity                                 | mm/h      | Determined from field data. Do not change unless you have a good region. |
| ksflag      | Flag to use internal hydraulic conductivity adjustments (0: no, 1: yes) | {0,1} |          |
| ksatadj     | Adjustment factor for saturated hydraulic conductivity            | -         |          |
| ksatfac     | ignore - will be removed                                          | -         |          |
| ksatrec     | ignore - will be removed                                          | -         |          |
| pmet_kcb    | Basal crop coefficient (Kcb)                                     | ratio     |          |
| pmet_rawp   | Parameter for readily available water                            | -         |          |
| rdmax       | Maximum root depth                                               | m         |          |
| xmxlai      | Maximum leaf area index                                          | frac      |          |
| keffflag    | Flag for lower limit of effective conductivity (lkeff; 0: no, 1: yes) | {0,1} |          |
| lkeff       | Lower limit of effective conductivity (-9999 indicates no adjustment) | mm/h  |          |



## Other Calbration Parameters of Interest

#### Rain-snow temperature threshold

Under WEPPP Advanced Options

Units: degrees C
Range: -3 - 1
Use:
  - 0 for CLIGEN
  - 0 for DAYMET
  - -2 for GRIDMET

#### Underlying bedrock conductivity

Units: mm/hr
Default: based on SSURGO values
  - ksat of the last horizon / 100
  - or other rules
Range: 0.001 - 0.1
Use: 
 - 0.001 restricts flow to baseflow (more lateral flow and runoff)
 - 0.1 to allows flow to baseflow (less lateral flow and runoff)

#### Baseflow coefficient

Units: per day
Range: 0.01–0.04
  - 0.01 = longer recession; 100 days
  - 0.04 = shorter recession; 25 days
Use: 
0.02, 0.03, or 0.04
Can be determined from observed streamflow data; slope of streamflow during recession days


 

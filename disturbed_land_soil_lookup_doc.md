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
| avke        | Effective hydraulic conductivity                                 | mm/h      |  |
| ksflag      | Flag to use internal hydraulic conductivity adjustments (0: no, 1: yes) | {0,1} |          |
| ksatadj     | Adjustment factor for saturated hydraulic conductivity            | -         |          |
| ksatfac     | ignore - will be removed                                          | -         |          |
| ksatrec     | ignore - will be removed                                          | -         |          |
| pmet_kcb    | Basal crop coefficient (Kcb)                                     | -          |
| pmet_rawp   | Parameter for readily available water                            | -         |          |
| rdmax       | Maximum root depth                                               | m         |          |
| xmxlai      | Maximum leaf area index                                          | frac      |          |
| keffflag    | Flag for lower limit of effective conductivity (lkeff; 0: no, 1: yes) | {0,1} |          |
| lkeff       | Lower limit of effective conductivity (-9999 indicates no adjustment) | mm/h  |          |



## Additional Notes and Other Parameters of Interest

#### Effective hydraulic conductivity (avke)

Determined from field data. Do not change unless you have a good reason.

Values for disturbed/undisturbed may be less significant west of the Cascades (e.g., in Oregon)

#### Basal crop coefficient (pmet_kcb)

KCB parameter for FAO Penman-Monteith equation approximates net evapotranspiration from meteorological data as a replacement for direct measurement of evapotranspiration.

Units: NA
For forests use default: 0.95 (default; well-watered conditions)
Use mainly for undisturbed conditions: 
1.2 to increase ET (decrease annual water yield; well-watered conditions)
0.65 to reduce ET (increase annual water yield; during drought conditions) 
No need to modify for disturbed conditions, as the reduction in ET is accounted for by a reduction in LAI within the model.

For more information see: [Crop evapotranspiration - Guidelines for computing crop water requirements - FAO Irrigation and drainage paper 56, Chapter 7 - ETc - Dual crop coefficient (Kc = Kcb + Ke)](https://www.fao.org/4/x0490e/x0490e0c.htm#chapter%207%20%20%20etc%20%20%20dual%20crop%20coefficient%20(kc%20=%20kcb%20+%20ke))


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


 

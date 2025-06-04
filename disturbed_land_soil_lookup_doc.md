# Disturbed Land Soil Table Parameters for WEPPcloud

The disturbed land soil table in WEPPcloud contains parameters that define soil properties for various land use categories and soil textures. These parameters are essential for modeling erosion and hydrology in disturbed lands using the WEPP (Water Erosion Prediction Project) model. The table includes data for combinations of land use (e.g., agriculture crops, forest, bare) and soil texture (clay loam, loam, sand loam, silt loam).

## Table of Parameters

| Parameter   | Description                                                       | Units     |
|-------------|-------------------------------------------------------------------|-----------|
| luse        | Land use category (disturbed class from the land use map)         | -         |
| stext       | Soil texture (clay loam, loam, sand loam, silt loam)              | -         |
| ki          | Interrill erodibility                                            | kg·s/m⁴   |
| kr          | Rill erodibility                                                 | s/m       |
| shcrit      | Critical shear stress                                            | Pa        |
| avke        | Effective hydraulic conductivity                                 | mm/h      |
| ksflag      | Flag to use internal hydraulic conductivity adjustments (0: no, 1: yes) | {0,1} |
| ksatadj     | Adjustment factor for saturated hydraulic conductivity            | -         |
| ksatfac     | Factor for saturated hydraulic conductivity                      | -         |
| ksatrec     | Recovery factor for saturated hydraulic conductivity             | -         |
| pmet_kcb    | Basal crop coefficient (Kcb)                                     | ratio     |
| pmet_rawp   | Parameter for readily available water                            | -         |
| rdmax       | Maximum root depth                                               | m         |
| xmxlai      | Maximum leaf area index                                          | frac      |
| keffflag    | Flag for lower limit of effective conductivity (lkeff; 0: no, 1: yes) | {0,1} |
| lkeff       | Lower limit of effective conductivity (-9999 indicates no adjustment) | mm/h  |

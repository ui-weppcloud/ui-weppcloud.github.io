# WEPPcloud Calibration 


## Disturbed Land Soil Lookup Table (PowerUser Panel → Modify Disturbed Parameters)
The disturbed land soil table in WEPPcloud contains parameters that define soil properties for various land use categories and soil textures. These parameters are essential for modeling erosion and hydrology in disturbed lands using the WEPP (Water Erosion Prediction Project) model. The table includes data for combinations of land use (e.g., agriculture crops, forest, bare) and soil texture (clay loam, loam, sand loam, silt loam).

### Table of Parameters

| Parameter     | Description                                                              | Units        |
|---------------|--------------------------------------------------------------------------|--------------|
| luse          | Land use category (disturbed class from the land use map)                | -            |
| stext         | Soil texture (clay loam, loam, sand loam, silt loam)                     | -            |
| ki            | Interrill erodibility                                                   | kg·s/m⁴      |
| kr            | Rill erodibility                                                        | s/m          |
| shcrit        | Critical shear stress (τc)                                               | N/m² or Pa   |
| avke          | Effective hydraulic conductivity                                        | mm/h         |
| ksflag        | Flag to use internal hydraulic conductivity adjustments (0: no, 1: yes) | {0,1}        |
| ksatadj       | Adjustment factor for saturated hydraulic conductivity                   | -            |
| ksatfac       | ignore - will be removed                                                 | -            |
| ksatrec       | ignore - will be removed                                                 | -            |
| pmet_kcb      | Basal crop coefficient (Kcb)                                             | -            |
| pmet_rawp     | Parameter for readily available water                                   | -            |
| rdmax         | Maximum root depth                                                      | m            |
| xmxlai        | Maximum leaf area index                                                 | frac         |
| keffflag      | Flag for lower limit of effective conductivity (lkeff; 0: no, 1: yes)   | {0,1}        |
| lkeff         | Lower limit of effective conductivity (-9999 indicates no adjustment)    | mm/h         |

## Additional Notes and Other Parameters of Interest

### Effective Hydraulic Conductivity (avke)

Determined from field data. Do not change unless you have a good reason.

Values for disturbed/undisturbed may be less significant west of the Cascades (e.g., in Oregon).

### Interrill Erodibility (ki)

Interrill areas are the sheet flow zones between small channels (rills) on a hillslope. Interrill erodibility measures the soil's susceptibility to detachment by raindrop impact and shallow sheet flow. It is influenced by:

- Soil texture
- Surface cover (e.g., vegetation, mulch)
- Soil structure and cohesion

**Units**: kg·s/m⁴  
**Note**: Do not change.

### Rill Erodibility (kr)

Rills are small channels formed by concentrated flow on hillslopes. Rill erodibility is the soil’s susceptibility to detachment by concentrated flow (not raindrop impact). Rill erosion is generally more intense on steeper and/or longer slopes and can cause greater sediment transport than interrill erosion.

**Units**: s/m  
**Note**: Do not change. In West Cascades, divide by 10 or 100.

### Critical Shear Stress (τc)

This is the minimum hydraulic shear stress required to initiate detachment of soil particles in rills. Below this threshold, the flow is not energetic enough to detach soil. It acts as a resistance parameter in rill erosion models.

**Units**: N/m² or Pa  
**Note**: Do not change.

### Basal Crop Coefficient (pmet_kcb)

The Kcb parameter for the FAO Penman-Monteith equation approximates net evapotranspiration from meteorological data as a replacement for direct measurement of evapotranspiration.

**Units**: None  
**Guidelines**:
- For forests, use default: 0.95 (well-watered conditions).
- For undisturbed conditions:
  - Use 1.2 to increase ET (decrease annual water yield; well-watered conditions).
  - Use 0.65 to reduce ET (increase annual water yield; during drought conditions).
- No need to modify for disturbed conditions, as the reduction in ET is accounted for by a reduction in LAI within the model.

For more information, see: [Crop evapotranspiration - Guidelines for computing crop water requirements - FAO Irrigation and drainage paper 56, Chapter 7 - ETc - Dual crop coefficient (Kc = Kcb + Ke)](https://www.fao.org/4/x0490e/x0490e0c.htm#chapter%207%20%20%20etc%20%20%20dual%20crop%20coefficient%20(kc%20=%20kcb%20+%20ke))

### Rain-Snow Temperature Threshold

Found under WEPP Advanced Options - Snow.

**Units**: °C  
**Range**: -3 to 1  
**Guidelines**:
- Use 0 for CLIGEN.
- Use 0 for DAYMET.
- Use -2 for GRIDMET.

### Underlying Bedrock Conductivity (ksat for restrictive layer - kslast)

Found under WEPP Advanced Options - Bedrock

**Units**: mm/h  
**Default**: Based on SSURGO values (ksat of the last horizon / 100, or other rules).  
**Range**: 0.001–0.1  
**Guidelines**:
- Use 0.001 to restrict flow to baseflow (more lateral flow and runoff).
- Use 0.1 to allow flow to baseflow (less lateral flow and runoff).

### Baseflow Coefficient

Found under WEPP Advanced Options - Baseflow Processing.

**Units**: per day  
**Range**: 0.01–0.04  
**Guidelines**:
- 0.01 = longer recession (100 days).
- 0.04 = shorter recession (25 days).
- Suggested values: 0.02, 0.03, or 0.04.
- Can be determined from observed streamflow data; slope of streamflow during recession days.

### Channel Critical Shear Stress (τc)

Found under WEPP Advanced Options - Channel Parameters

**Units**: N/m² or Pa
**Range**: 0.05 (fine silt) and 170 coarse cobble
**Guidelines**:
- This is the minimum shear stress required to initiate the movement of sediment particles on the bed of a channel (such as a river, stream, or canal). 
- In simple terms, it's the threshold force per unit area that water flow must exert on the channel bed to start erosion or sediment transport.
**Examples**:
- Lake Tahoe: 10−180
- Oregon (near Portland)/Washington (near Seattle): 83
- North Idaho (Mika Creek): 35−40
- Oregon (near Eugene): 70
  

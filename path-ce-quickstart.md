# PATH Cost-Effective Reference Manual

This tutorial walks the user through the steps necessary to successfully run PATH.

### Pre-PATH Requirements

Prior to running PATH the user must first successfully configure and run a WEPP scenario for the sub-catchment of the users choosing. Once run the user may proceed configuring PATH.


## PATH Cost-Effective

### Step 1. Define Biophysical Thresholds

The PATH Cost-Effective model objective minimizes the cost of treatment while meeting the user defined sediment discharge and sediment yield thresholds. By inputing sediment discharge and sediment yield threshold values PATH will find the optimal hillslopes to treat that will meat these thresholds. (Ex. User inputs a sediment discharge threshold of 200 tons. Total sediment discharge after treatment of all hillslopes will be \leq 200 tons.) 

### Step 2. Configure Landscape Filters

The user may enter a range of slope angles (in degrees) they wish PATH to consider. Hillslopes that fall outside this range will not be considered for treatment. The user may also choose to filter based on burn severity by selecting the levels they wish PATH to consider. Those not selected will not be considered, unless none are selected in which case all severities will be considered.


### Step 3. Scenario Package and Treatment Costs

PATH provisions a fixed Omni bundle before each run. The solver compares the post-fire SBS baseline, three mulch intensities, and the undisturbed reference scenario. Using the data from these Omni scenarios and the cost values provided by the user here, PATH will find the optimal hillslopes for treatment. Enter the cost in USD/hectare ($/ha) for each quantity of mulch. PATH multiplies by hillslopes area to build the solver cost vector used to perform the optimization. 


### Step 4. Run PATH Cost-Effective

Once the sediment thresholds, filters, and treatment costs have all been entered and or selected, the user may proceed with running PATH. 

### Output

After PATH has successfully completed its run, a link to a final report will be available. This report provides a summary of PATH’s outputs including tables, plots, and maps of the selected hillslopes and treatments. 


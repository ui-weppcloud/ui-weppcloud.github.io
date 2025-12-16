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

The newly created project has a unique RunID, underlined in red. This RunID is unique for every project and can be used to return to the project as well as for debugging purposes. In the cloud a project folder is created with this RunID. The run ids are generated using a package called "Awesome-Codenames" and has a dictionary of 26,000 words. The codenames are used to produce ids that are memorable and easily transcribable.

A large array of functionality is provided by WEPPcloud through the use of interface configurations. Each interface has a configuration file ("config file") that specifies datasets and parameters for specific locations or models. The config is specified after the RunID in the URL. In the image below it is underlined in blue. The "disturbed9002" config is for the US.

<img width="771" alt="RunID and Interface Config" src="https://github.com/user-attachments/assets/e7d8786b-9da5-4edf-8d1d-7fb36957a0a6" />

## Selecting Map Extent

The first step is to specify the boundary for the catchment you wish to model. The extent of the map is used as the boundary for modeling. The map has controls to zoom in and out. It is also possible to double click on the map to zoom in. The map can be panned by clicking and dragging. The extent can also be specified by holding down shift will drawing a box. This is especially helpful when zoomed out.


## Channel Delineation

The channel delineation is limited in the size of catchment areas that can be delineated. The limit is dependent on the TOPAZ processing parameters for Minimum Channel Length (MCL) and Critical Subcatchment Area (CSA). For this reason, it is suggested that you zoom into a level of 13 or greater. 

When setting the extent it is important that the ridgeline of the catchment you wish to model is within the boundary of the map. TOPAZ will fail if the catchment falls outside of the map when delineating subcatchments.

<img width="1428" alt="Map" src="https://github.com/user-attachments/assets/e837613f-c729-4a45-ab8f-dfb343dce87e" />


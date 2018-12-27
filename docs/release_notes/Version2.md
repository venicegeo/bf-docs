# GEOINT Services | Release Notes
------

<img src="../images/logo_inverted.png" alt="Beachfront Logo" width="80%" style="margin-top:0; margin-bottom:0;" />

## Version 2.1

Date and version number of current changes: TBD, v2.1

Beachfront 2.1 builds on Beachfront 2.0 and consists fixes to enhance the 
user experience and to get Sentinel 2 data to correctly produce and display 
coastline data.

The following additions and enhancements were made within the 2.1 release:

Key Fixes:

#### Beachfront User Interface Fixes
* Added an Activation state to the Beachfront coastline detection process to mirror the Planet.com imagery retrieval process. Beachfront will now tell users exactly when their input dataset is awaiting Planet.com activation.
* All GeoServer Web Map Service (WMS) shoreline detection layers now are properly proxied through the Beachfront services component, instead of directing the user directly to GeoServer. This will help prevent many common Cross-Origin Resource Sharing (CORS) errors.
* Improved user functionality by adding an auto-scrolling feature to the Job Creation workflow. This helps users navigate selections throughout the coastline production process
* Enhanced error messages to guide the user to provide more search details when required
* Fixed minor styling issue to keep the style consistent across the entire application
* Fixed bug that caused style abnormalities when user tries to access an invalid url
* Fixed styling issues in the User Tour when user has low screen resolution

#### Single Scene Coastline Detection Job Execution with Sentinel 2 data provided by Planet.com
* Users may now select Sentinel-2 in the search results dataset drop-down and run the detection process on Sentinel-2 imagery pulled from the Amazon Web Services hosted Sentinel-2 catalog.

#### Algorithm efficiency improvements
* Improved various memory inefficiencies with the NDWI algorithm that previously caused algorithms to fail or take longer than needed to process.
* Updated algorithm software dependencies to latest approved versions to improve performance and resolve issues with old dependencies
     * Potrace 1.15
     * Gippy 1.0
     * GDAL 2.1.3

#### Beachfront code update to accommodate image activation time in Planet.com     
 * Allow a greater length of time for Planet.com image activation to take place. Previously, there was a very short timespan allocated to image activation, which sometimes caused failures in activation because the process took longer than expected.
 
#### Coastline Dataset Metadata Fixes
 * Added all relevant metadata for coastline detections, such as creation date, tides information, algorithm and image types, to the detection results. This fixes a bug where previously certain metadata information was being excluded.

#### Metrics Functionality
 * Added several metrics capabilities to Beachfront within L2 & L4 logsearch, including dashboards displaying user-related and jobs-related metrics

#### Features or functionality retired in Beachfront 2.1
 * No capabilities were retired in Beachfront 2.1

#### Improvements from previous version
 * See above
 
------

## Version 2.0

Date and version number of current changes: 01 May 2018, v2.0

Beachfront 2.0 builds on Beachfront 1.0 and Piazza and starts to combine the
two applications into one finding efficiencies.  These release notes contain
the Beachfront 1.0 and Piazza MVP since those versions of the software were not
ever officially delivered and granted ATO through NGA.  Beachfront 2.0 in UC
will enable users to securely login using GEOAxIS, search-activated Planet
provided imagery, execute coastline detection using an NDWI-based algorithm
service, and download tide-coordinated vector outputs after detection job
execution. Piazza capabilities have been absorbed into Beachfront and it will be
ATO’d as one project, referred to as Beachfront_Piazza in this document going
forward.

The following additions and enhancements were made within the 2.0 release:

#### Beachfront User Interface:

-   Users will be able to interact with the Beachfront system through a
    map-driven user interface at <https://beachfront.gs.mil>
-   OSM Basemap Tiles will be the basemap until more become available

#### GeoAxis User Authentication:

-   Users will be able to login using their GeoAxis credentials (PKI,
    Disadvantaged User Account, Austere Account) through an OAuth2-enabled system

#### Searching Planet Data to run Coastline Detection on through Planet:

-   User-controlled search of active AOIs and TOIs of RapidEye, PlanetScope, and
    Copernicus Sentinel-2 imagery can be made using the following filters:
    -   Spatial
    -   Temporal
    -   Cloud Cover
-   Users can choose between searching RapidEye, PlanetScope, or Sentinel-2
    imagery for candidate scenes/tiles

#### Scene/Tile Preview of Planet Data (provided by Planet):

-   Enables users to visually inspect image scenes/tiles provided by Planet DAS,
    e.g., Planet DAS tile server dependency, prior to detection job execution
-   Enables user download to a local machine
    -   Vector outputs will be in GeoJSON, GeoPackage, or Shapefile format
        (user's choice)

#### Single Scene Coastline Detection Job Execution (Register and Execute an Algorithm):

-   Users can execute coastline detection using a NDWI-based Python algorithm
    combined with avectorization component in one detection service
-   Beachfront fetches required Planet scene/tile analytic asset and stages for
    processing
-   Beachfront processes pixels with the algorithm and provides vector output
    of a shoreline detection.

#### Tide Prediction Service:

-   Beachfront calls a Global Tide Prediction Service upon scene selection using
    the centroid of the scene and time of collect in order to predict a tidal
    height, using a 24-hour low and high value, and decorates every output
    feature with this metadata

#### Output Vector Data:

-   Output vector metadata (at feature level) provides the following
    attribution (and JSON types) relevant to the job it was created by:

| Field             | Type                      |
|-------------------|---------------------------|
| id                | text                      |
| job_id            | text                      |
| algorithm_id      | text                      |
| algorithm_name    | text                      |
| algorithm_version | text                      |
| cloud_cover       | number                    |
| created_by        | text                      |
| created_on        | text (ISO-8601 date/time) |
| name              | text                      |
| resolution        | number                    |
| scene_id          | text                      |
| sensor_name       | text                      |
| status            | text                      |
| tide              | number                    |
| tide_min_24h      | number                    |
| tide_max_24h      | number                    |
| time_of_collect   | text (ISO-8601 date/time) |
| data_usage        | text                      |
| classification    | text                      |

#### Jobs List:
-   Jobs List provides user ability to return to view historical jobs and their
    success/failure

#### Performance Enhancements:

-   Non-redundant processing and caching of detections, increasing
    performance and efficiency
-   API micro-service refactored to achieve better maintainability, reliability,
    and configuration integration with the deployment environment
-   Job executor service refactored for better horizontal scaling, increasing
    concurrent user capacity by 3x
-   Decreased processing time by 3x through various performance improvements

#### Bug Fixes:
-   Significant amount of work went into geting the NDWI to correct output
    coastline vectors onto the UI.

#### Features or functionality retired in Beachfront 1.0:

-   Piazza will no longer be refer to as a separate application.  By combining
    the two applications, the architecture was simplified. This has resulted
    in better maintainability and faster development.


#### Improvements from previous version:

-   N/A

## System Requirements:

Data exported from Beachfront 1.x is viewable in Boundless Desktop/QGIS, ArcGIS 10.3 (and later versions) with the Data Interoperability Extension, and GEOINT Viewer as GeoJSON and GeoPackage file formats

Browser requirements for the Beachfront web user interface:

-   **Recommended:** Chrome 55 and later
-   Firefox 45 and later

------

> **Additional Info**
> For more information on the release, please use the Beachfront
> "Ask the Expert" channel.

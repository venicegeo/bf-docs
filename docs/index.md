<img src="userguide/images/logo_inverted.png" alt="Beachfront Logo" width="80%" style="margin-top:0; margin-bottom:0;" />
# Automated Coastline Extraction

## What is Beachfront?

Beachfront is a set of open-source cloud services that enables users to
leverage detection algorithms and operational imagery sources to update global
coastline vectors. Users can exploit third-party imagery data using detection
algorithms to generate coastline vector data. It provides users the ability to
automatically extract large sections of coastline to produce timely, dynamic
data in support of multiple communities using the best-available source imagery.
Although intended for shorelines, Beachfront can be modified to serve other
feature communities of interest to assist in automated feature and object
detection if other algorithms are available.

## Benefits of Beachfront

Previous shoreline extraction efforts used massive, infrequent efforts to digitize
global shorelines. Beachfront drastically reduces the amount of time spent on manual
digitization of features, and allows for the constant update of feature data products on
demand.

-   Users can download only the imagery they need and obtain much more current
    information for the specific sections of coast in which they are interested.
-   This app simplifies the process for the user by preventing the need to both
    obtain large shapefiles and search through large outdated files. Users can
    update coastline vector data as often as new source data is available.
-   Its auto-extraction feature exports immediately to ArcMap or QGIS for editing.

The result is that users have more time to conduct analysis on other tasks.

## What type of data does Beachfront produce?

-   Beachfront extracts shorelines by examining available imagery. The app
    commonly uses imagery that includes PlanetScope and Rapid Eye data
    (3-to-5-meter resolution). Beachfront outputs vector data, most commonly
    for coastlines.

-   Beachfront also captures data on cloud cover, resolution, tide, time of
    collection, and more in the metadata of the output vectors. Users can export
    this data as GeoJSON, GeoPackage, or Shapefile.

## Impact to mission

-   Reduced manual feature extraction time means more available time for other
    tasks
-   On-demand products and tools reflect more current information by pulling
    from multiple or the most recent datasets, rather than from dated,
    mass-produced products
-   Scalable for use globally or in localized areas, depending on the mission
-   Tailored algorithms can be used for additional mission areas and feature
    extraction types using the same architecture.

## How can users access Beachfront?

Beachfront is accessible through GEOINT services:

-   JWICS: <https://home.gs.ic.gov/>
-   NIPRnet: <https://home.gs.mil>

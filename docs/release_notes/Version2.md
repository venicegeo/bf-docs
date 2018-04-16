## GEOINT Services | Release Notes
------

<p>
<img src="../images/logo_inverted.png" alt="Beachfront Logo" width="80%" style="margin-top:0; margin-bottom:0;" />
</p>

### Version 2.0
Date and version number of current changes: 12 April 2018, v2.0

Beachfront 2.0 builds on Beachfront 1.0 and Piazza and starts to combine the two applications into one finding efficiencies.  These release notes contain the Beachfront 1.0 and Piazza MVP since those versions of the software were not ever officially delivered and granted ATO through NGA.  Beachfront 2.0 in UC will enable users to securely login using GEOAxIS, search-activated PlanetDAS provided imagery, execute coastline detection using an NDWI-based algorithm service, and download tide-coordinated vector outputs after detection job execution. Piazza capabilities have been absorbed into Beachfront and it will be ATO’d as one project, referred to as Beachfront_Piazza in this document going forward.

<br/>
The following additions and enhancements were made within the 2.0 release:

<b>Beachfront User Interface:</b>
<ul>
    <li>Users will be able to interact with the Beachfront system through a map-driven user interface at <a target="_blank" href="https://beachfront.gs.mil">https://beachfront.gs.mil</a></li>
    <li>OSM Basemap Tiles will be the basemap until more become available</li>
</ul>

<b>GeoAxis User Authentication:</b>
<ul>
    <li>Users will be able to login using their GeoAxis credentials (PKI, Disadvantaged User Account, Austere Account)</li>
</ul>

<b>Searching Planet Data to run Coastline Detection on through PlanetDAS:</b>
<ul>
    <li>User-controlled search of active AOIs and TOIs of PlanetScope and RapidEye imagery can be made using the following filters:
        <ul>
            <li>Spatial</li>
            <li>Temporal</li>
            <li>Cloud Cover</li>
        </ul
    </li>
    <li>Users can choose between searching PlanetScope or RapidEye imagery for candidate scenes/tiles</li>
</ul>

<b>Scene/Tile Preview of Planet Data (provided by PlanetDAS):</b>
<ul>
    <li>Enables users to visually inspect image scenes/tiles provided by Planet DAS, e.g., Planet DAS tile server dependency, prior to detection job execution</li>
    <li>Enables user download to a local machine (vector outputs will be in GeoJSON format)</li>
</ul>
<b>Single Scene Coastline Detection Job Execution (Register and Execute an Algorithm):</b>
<ul>
    <li>Users can execute coastline detection using a NDWI-based Python algorithm combined with a vectorization component in one detection service</li>
    <li>Users can rename jobs if they choose (job name defaults to image Scene ID)</li>
    <li>Beachfront fetches required Planet scene/tile analytic asset and stages for processing</li>
    <li>Beachfront processes pixels with the algorithm and provides vector output of a shoreline detection.</li>
</ul>

<b>Tide Prediction Service:</b>
<ul>
    <li>Beachfront calls a Global Tide Prediction Service upon scene selection using the centroid of the scene and time of collect in order to predict a tidal height, using a 24-hour low and high value, and decorates every output feature with this metadata</li>
</ul>

<b>Output Vector Data:</b>
<ul>
    <li>Output vector metadata (at feature level) provides the following attribution:
    <table border="1" style="width:50%; font-size:8pt;">
                <colgroup>
                    <col style="width:50%">
                    <col style="width:50%">
                </colgroup>
                <thead>
                    <tr>
                        <th>Field</th>
                        <th>Type</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td>id</id><td>String</td></tr>
                    <tr><td>job_id</id><td>String</td></tr>
                    <tr><td>algorithm_id</id><td>String</td></tr>
                    <tr><td>algorithm_name</id><td>String</td></tr>
                    <tr><td>algorithm_version</id><td>String</td></tr>
                    <tr><td>cloud_cover</id><td>Integer</td></tr>
                    <tr><td>created_by</id><td>String</td></tr>
                    <tr><td>created_on</id><td>DateTime</td></tr>
                    <tr><td>name</id><td>String</td></tr>
                    <tr><td>resolution</id><td>Integer</td></tr>
                    <tr><td>scene_id</id><td>String</td></tr>
                    <tr><td>sensor_name</id><td>String</td></tr>
                    <tr><td>status</id><td>String</td></tr>
                    <tr><td>tide</id><td>Real</td></tr>
                    <tr><td>tide_min_24h</id><td>String</td></tr>
                    <tr><td>tide_max_24h</id><td>String</td></tr>
                    <tr><td>time_of_collect</id><td>DateTime</td></tr>
                    <tr><td>data_usage</id><td>String</td></tr>
                    <tr><td>classification</id><td>String</td></tr>
                </tbody>
        </table>
    </li>
</ul>

<b>Jobs List:</b>
<ul>
    <li>Jobs List provides user ability to return to view historical jobs and their success failure</li>
</ul>

<b>Performance Enhancements:</b>
<ul>
    <li>Non-Redundant processing and caching of detections</li>
    <li>API  micro-service refactored to avoid software entropy</li>
    <li>Increased concurrent user capacity by 3x</li>
    <li>Decreased processing time by 3x</li>
</ul>

<b>Bug Fixes:</b>
<ul>
    <li>Significant amount of work went into geting the NGWI to correct output coastline vectors onto the UI.</li>
</ul>

<b>Features or functionality retired in Beachfront 1.0:</b>
<ul>
    <li>Piazza will no longer be refer to as a separate application.  By combining the two applications, the architecture was simplified.</li>
</ul>

<b>Improvements from previous version:</b>
<ul>
<li>N/A</li>
</ul>

<b>System Requirements:</b>
<ul>
    <li>Data exported from Beachfront 1.x is viewable in Boundless Desktop/QGIS, ArcGIS 10.3 (and later versions) with the Data Interoperability Extension, and GEOINT Viewer as GeoJSON and GeoPackage file formats</li>
</ul>
> <div>__Additional Info?:__<div style="margin-top:3px;">For more information on the release, please use the Beachfront “Ask the Expert” channel.</div></div>




Classification: UNCLASSIFIED

![Beachfront](images/logo_inverted.png)

# Beachfront User's Guide

## Table of Contents

- [Searching for Scenes](#searching-for-scenes)
- [Creating a Job](#creating-a-job)
- [Viewing a Job's Results](#viewing-a-jobs-results)
- [Removing a Job from your Jobs List](#removing-a-job-from-your-jobs-list)



## Searching for Scenes

### 1. Navigate to the _Create Job_ menu

The scene search is a part of the job creation workflow:

[![screenshot](images/0000_navigate_to_create_job.png)](images/0000_navigate_to_create_job.png)


### 2. Draw a bounding box to define the search space

Drawing a bounding box is a 2-click process.  Click once to drop the first corner and again to complete the bounding box:

[![screenshot](images/0001_draw_bbox.png)](images/0001_draw_bbox.png)


### 3. Adjust search criteria, then execute search

> __Note:__ Dates should be entered in `YYYY-MM-DD` format, e.g., `2017-07-04`.

Make any necessary adjustments to the imagery source, cloud cover and date range, then click on the ___Search for imagery___ button to execute a search using the selected filtering criteria:

[![screenshot](images/0002_catalog_search_criteria.png)](images/0002_catalog_search_criteria.png)

After a moment, footprints of the scenes found in the catalog should render on the map.  You can readjust the filtering criteria and re-execute the search as many times as you need:

[![screenshot](images/0003_catalog_search_results.png)](images/0003_catalog_search_results.png)


### 4. Click on a scene's footprint to bring up metadata and a preview

> __Note__: If the full-color preview does not load on the map, please contact the Beachfront team for technical support.

[![screenshot](images/0004_select_scene.png)](images/0004_select_scene.png)



## Creating a Job

> __Note:__ Start from the end of the instructions for [Searching for Scenes](#searching-for-scenes).

### 1. After picking a scene, find a compatible algorithm

Look under the _Select Algorithm_ section to see what algorithms are available.  Some algorithms have strict requirements in order to yield meaningful coastline vector data:

[![screenshot](images/0005_select_algorithm_incompatible.png)](images/0005_select_algorithm_incompatible.png)

### 2. After picking an algorithm, submit the scene for processing

> __Note__: By default, Beachfront will name the job after the scene being processed.  You can optionally give a custom name to a job if desired.

<!---->

> __Note__: Algorithm processing time may vary depending on the size/age of the scene (i.e., bigger scenes require more time to process and older scenes require more time to request from archives) and the Beachfront system load at the time of execution.  If a scene takes longer to process than 2 hours, please contact the Beachfront team for technical support.

To submit the scene for algorithm processing, click the ___Run Algorithm___ button:

[![screenshot](images/0006_select_algorithm_compatible.png)](images/0006_select_algorithm_compatible.png)



## Viewing a Job's Results

### 1. Navigate to the _Jobs_ menu

The ___Jobs___ menu will list the status and details for all jobs you are tracking:

[![screenshot](images/0007_navigate_to_jobs.png)](images/0007_navigate_to_jobs.png)

### 2. Find the job you want to view, then click _View on Map_

> __Note:__ You can also click any visible job frame directly on the map to "select" it in the same way.

Selecting a job from the ___Jobs___ menu will pan and zoom the map to the job's frame:

[![screenshot](images/0008_view_job_on_map.png)](images/0008_view_job_on_map.png)

### 3. Shoreline detections will render for any successful job

> __Note:__ If you select a job that is currently running, shoreline detections automatically appear once it successfully completes.  If this does not happen, please notify the Beachfront team for technical support.

[![screenshot](images/0009_selected_job_frame.png)](images/0009_selected_job_frame.png)

### 4. Click on the job's list item row to view more details

To view extra information about a particular job, expand the job's row in the ___Jobs___ menu:

[![screenshot](images/0010_job_details.png)](images/0010_job_details.png)

### 5. Click "Download" button to download detections as GeoJSON

The GeoJSON file will have the same name as the job, e.g., `20170103_162024_1737916_RapidEye-1.geojson`:

[![screenshot](images/0011_download_job_geojson.png)](images/0011_download_job_geojson.png)




## Removing a Job from your Jobs List

### 1. Navigate to the _Jobs_ menu

The ___Jobs___ menu will list the status and details for all jobs you are tracking:

[![screenshot](images/0007_navigate_to_jobs.png)](images/0007_navigate_to_jobs.png)


### 2. Expand the job's details, then click _Remove this Job_

> __Note:__ The job does not get deleted from the system; it just won't show up in your tracking list anymore unless you visit that job's URL again.

[![screenshot](images/0012_remove_job.png)](images/0012_remove_job.png)


#Tide Prediction#
##Description##

Bf-tideprediction is a Beachfront service that estimates the tide level for a given date/time as well as the 24 hour min/max tides and corresponding times surrounding that date/time.  This service is used by Beachfront to provide contextual information to be used in conjunction with Beachfront’s shoreline extraction services.

###Why are tides important for shoreline extraction?###
![Examples of Beachfront Shoreline extraction at high tide vs low tide](images/image07.png)

###Why create a new tide service instead of using a third-party service?###
* Limited API access
* Most services offer either historic tide data or predict future tides, but don’t offer both
* Cost. Best services require user subscriptions
* Query locations visible to 3rd party
* Inability to migrate to classified environment
* Reliance on 3rd party server availability


##Operation##
Bf-tideprediction works in both individual and batch modes.  

###Individual Query mode:###

####API####
The individual mode has an api endpoint of https://bf-tideprediction.geointservices.io and accepts the following keys:

| Keys | Description
------|-------------------
| lat | decimal degrees between -90 and 90	
| lon | decimal degrees between -180 and 180
| dtg | Date/Time in format : YYYY-MM-DD-HH-MM (Universal Standard Time)

Sample Query:
~~~
 curl -X POST -d 'lat=-33.85&lon=151&dtg=2016-05-31-0-1' "https://bf-tideprediction.geointservices.io/"
~~~

####Web Interface####
The individual query mode also has a web-based form.  Enter coordinates in decimal degrees, and provide the data and time in the format YYY-mm-DD-HH-M in UST.  Select “Calculate” and the results will be returned in the browser as a json file.

![Alt](images/image04.png)

###Batch Queries###


TidePrediction.stage.geointservices.io json collections in the format:


```json
{
  "locations": [
    {
      "dtg": "some_dtg1",
      "lat": "some_lat1",
      "lon": "some_lon1"
    },
    {
      "dtg": "some_dtg2",
      "lat": "some_lat2",
      "lon": "some_lon2"
    }
  ]
}
```


Sample Query:
~~~
curl -X POST -H "Content-Type: application/json"  -d '
{"locations": [{"lat": 73.63008647322661, "lon": -81.5557487110026, "dtg": "2015-12-20-09-36"}]}' "https://tideprediction.stage.geointservices.io/tides"
~~~

##Algorithm##


Beachfront’s Tide Prediction service utilizes the python library Pytides to predict past and future tides.  These predictions are based upon harmonic constituents estimated from historical sea level buoy data. The service accepts a latitude/longitude pair and a date time group and returns the current tide level at that time, as well as the minimum and maximum of the 24 hour period following the time.  According to their documentation, Pytide's tidal prediction is based upon several fundamental assumptions.  The first assumption is that tides anywhere on Earth are caused solely by the gravitational forces of the moon and the sun. Pytides neglects the gravitational forces of other planetary bodies as their effect on the tide is several orders of magnitude weaker than those of the moon and sun.  The second assumption is that for any given location on Earth, there exist constant values such that the tide there obeys this relation.  So if we have many past measurements of the tide at a given location, we can attempt to choose values  which best fit our previous readings.Then, by assumption, we can predict the future tide by allowing t to increase into the future.

![Example showing Tide prediction results compared to actual measurements](images/image09.png)


Beachfront's Tide Prediction service obtains these historic measurements by querying the GLOSS buoy network.  The service takes latitude and longitude coordinates, as well as a date-time group (DTG).  A lookup table hosted by bf-tideprediction calculates the station id for the appropriate sea level monitoring stations.  Utilizing a locally stored database of historic sea level data, constituents are calculated for each appropriate station.  The tides are then predicted for those stations, for a 24 hour  period surrounding the image DTG on a minute by minute basis.  These data points are interpolated to provide sea level height for the image date-time group, and a minimum and maximum tide height for a given time period.  

![Gloss Buoy Locations](images/image08.png)
#######Gloss Buoy Locations ########


![Density Map of Gloss Buoy Locations](images/image11.png)
#######Density Map of Gloss Buoy Locations ########


A lookup table hosted by bf-tideprediction calculates the station id for the appropriate sea level monitoring stations by querying the coordinates against a pre-computed set of voronoi polygons.  In mathematics, a Voronoi diagram is a partitioning of a plane into regions based on distance to points in a specific subset of the plane.  For each initial point (or seed) there is a corresponding polygon consisting of all points closer to that seed than to any other. These regions are called Voronoi cells.  For the Beachfront Tide Prediction service, a one-time calculation of Voronoi polygons was generated for the Gloss Buoy data.  For a given coordinate, the corresponding known point is queried  This is simpler than triangulating between the points of a Delaunay triangle, but may be less accurate as its based on a single known point.


![Voronoi Polygon Example](images/image13.png)

#######Source (https://commons.wikimedia.org/wiki/File:Euclidean_Voronoi_diagram.svg)#######
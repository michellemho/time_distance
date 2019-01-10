# time_distance
A project called "Where Should We Move?" that identifies best location based on minimizing commute to multiple locations

Steps to manually get this running... it's not pretty:

1. Get OpenTripPlanner routing machine (http://www.opentripplanner.org/) running on an OSM extract and GTSF feeds for NYC locally (at localhost:8080)
2. Collect "home" locations (places to minimize distance/time to/from) and place in CARTO table (this process currently relies on having a CARTO account)
3. Run the new_work_location notebook. This notebook does many things:
    - Generates isochrone queries for two situations (with and without L train stops) from "home" locations CARTO table
    - Request queries from OTP machine and saves results to two directories (which need to made manually for now)
    - Merge all the geojsons in each directory together into one big geojson file (requiring geojson-merge)
    - Use CARTO python manager to send the two geojsons to your CARTO account
    - Make rectangle grid table (taking advantage of CARTO PostGIS function CDB_RectangleGrid) over the extent of the isochrones
    - Count the number of overlaps in each grid cell and sum the minimum times in each grid cell
    - Create two new tables of rectangle grids (with and without L train) in CARTO with the above information.
4. Create the map visualization with CARTO VL (code in index.html) and put in a bl.ock [Voila!](http://bl.ocks.org/michellemho/raw/7bda353d62975d8dc24f600db25ac550/)

Oh boy

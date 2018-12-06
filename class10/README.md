# Class 10: Maps, part II

## Housekeeping
  * Show + tell?
  * Any questions?
  * Next two classes: stacked bar, sankey diagrams, chart morphing?
  * Goals for today
  	* Proficience finding shapefiles and converting them to useable json formats
  	* Apply nesting techniques to mapping


# Mapping checklist.

Just like we did with charts, we may benefit from a small checklist when making maps.

** General gameplan for making a map**

1. If you're starting with a Shapefile, you will need to convert to TopoJSON somehow. I prefer [Mapshaper](http://www.mapshaper.org), but there are plenty of options.
2. Navigate to your working directory, create an `index.html` file with D3, queue and topojson loaded and start a local server
3. Load all your data
4. Add an SVG on the page.
5. Format your data, adding fields as necessary
6. Convert topojson back to geoJSON
7. Define a geo path 
8. Create your map in SVG using a data join with your geojson features.
9. Create a way to link your data to the map, preferably using a Javascript map object, also what we've been calling a "lookup function."
10. Style your map accordingly.

## Lab, part I
Today we're going to be working with data that's a little different than states and counties. Specifically, data about droughts.

1. Start by downloading the National Climatic Data Center drought boundaries shapefile from [this page](https://www.ncdc.noaa.gov/monitoring-references/maps/us-climate-divisions.php). (You need to click on the [Current Dataset](ftp://ftp.ncdc.noaa.gov/pub/data/cirs/climdiv/), then [CONUS_CLIMATE_DIVISIONS](ftp://ftp.ncdc.noaa.gov/pub/data/cirs/climdiv/CONUS_CLIMATE_DIVISIONS.shp.zip).) We'll also need some data for the [Palmer Drought Severity Index](https://www.drought.gov/drought/content/products-current-drought-and-monitoring-drought-indicators/palmer-drought-severity-index), which is [found here](views/data/tidy-drought-data.csv). Download both to your local folder.
2. Take a look at the csv and Google around until you know what the numbers represent.
3. Let's explore the shapefile. It's nice if you have the [Mapshaper node module](https://github.com/mbloch/mapshaper#installation) installed, but you don't need to. Check out the awesome console tool in the browser! Or install it locally if you like.
4. Let's simplify our data manually, using your simplification algorithm of choice, then load it in the browser like we did with the US data. We really only care about outputtting `CLIMDIV` field, but you can keep them all.
5. Draw your map!


## Lab, part II
Our goal is to make a map drought severity in the United States as of June 2015. [These breakpoints](http://www.cpc.ncep.noaa.gov/products/analysis_monitoring/regional_monitoring/palmer.gif) may be useful for our color scale's domain, but we can probably do better on the colors – perhaps with [every ColorBrewer scale](http://bl.ocks.org/mbostock/5577023) or the new sequential [color scales](http://bl.ocks.org/pstuffa/d5934843ee3a7d2cc8406de64e6e4ea5)? Or we can use the upshot styling, like this:

<img src="images/Screen Shot 2018-12-06 at 2.56.22 PM.png">

Also, we'll need to create a data object that gives us the drought value given a `CLIMDIV` id and year.

## Lab, part III
Use d3.nest() or a function and generalize your code to a map for every year. (That's a lot of years.) Something like this:
<img src="images/Screen Shot 2018-12-06 at 2.26.00 PM.png">

## Lab, part IV
It could be cool to have a slider input at the top of the page so we could have a user change which year they wanted to look at. How would you do that? Think about the checklist:
 * Create a slider input (type = range)
 * Set the min and max values to the slider to be the min and max year
 * When the slider changes, update the colors of the chart (and maybe text)

### Homework
Publish your map! Choose either the maps we worked on Tuesday or today, but publish one of them and send me your notebook. Also, office hours Sunday @ 8:00.





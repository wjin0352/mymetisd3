# Class 9: Maps, part I
You could have an entire class on maps and D3: using the command-line tools, U.S. Atlas, Mapshaper command line, Gdal, projections, all without getting into optimization, interactivity or design. In this class we'll equip you to make two very common forms of maps – **Choropleth** and **Bubble** – and equip you to alter mapping examples to suit your needs.

## Housekeeping
  
  * Any questions?
  * We're doing Stacked Bar Charts & Sankey Charts!
  * Goals for today
    * Discuss the strength of maps as a visualization form
    * How to get shapefiles and convert them into topojson 
    * Geo projections
    * Interaction on maps

## Mapping and Intent
Just like with charting, mapping is all about what you want to show. There's no such thing as the perfect form, especially with maps. A few examples:
  * [Basic Choropleth](https://beta.observablehq.com/@mbostock/d3-choropleth)
  * [Presidential vote](http://elections.nytimes.com/2012/results/president)
  * [An Extremely Detailed Map of the 2016 Election](https://www.nytimes.com/interactive/2018/upshot/election-2016-voting-precinct-maps.html)
  * [Older Version / Opacities](http://www.nytimes.com/interactive/2014/11/04/upshot/senate-maps.html)
  * [House maps](http://elections.nytimes.com/2014/results/house), and sometimes [maps shouldn't be maps](http://www.ericson.net/content/2011/10/when-maps-shouldnt-be-maps/)
  * [Pushing the envelope](https://www.flickr.com/photos/dukefifa/6307925837/)
  * Sometimes things are [easier by hand](http://farm9.staticflickr.com/8203/8199825791_e7f7919f8d_o.jpg) though
  * Sometimes they [are not](https://beta.observablehq.com/@fil/map-layers-perspective)

## Lab, Part 1: Why to use TopoJSON.

  1. Let's download some data from the Census. How about a [big shapefile](https://www.census.gov/cgi-bin/geo/shapefiles2010/main) of counties? Download and unzip the 2010 counties file `tl_2010_us_county10` to your local project folder. 
  2. If you have a GIS program you like, like ESRI maps, feel free to inspect your shapefile there. Otherwise...
  3. Let's go to Matthew Bloch's amazing [MapShaper.org](http://mapshaper.org/). Drag your `.shp` file to the browser and choose "simplify." See what happens to the file size as you move the slider.
  4. Export the map as both TopoJSON and GeoJSON. Notice any difference?
  5. Let's [look](http://bost.ocks.org/mike/simplify/) at how that difference in file size happens.
  6. In a nutshell, that's all we need to know about TopoJSON: it's really good at reducing file size. It can do hard spatial things too, but for now let's focus on using TopoJSON files someon else has already prepared for us. If you want to do fancier things, [start installing command-line tools](http://bost.ocks.org/mike/map/#installing-tools).

## Lab part II: maps three ways
Our goal: to visualize [Chicago gun traces](views/guns-history.csv) on a map. It should look something like this:

<img src="images/Screen Shot 2018-12-04 at 1.46.46 PM.png">

Make a new `index.html` file like always. Add in a link to TopoJSON this time under your link to d3 (or grab the starter file):
  
  ```
  <script src="https://d3js.org/topojson.v1.min.js"></script>
  ```
Download [us.json](views/us.json) just like we always do and log it in the console.
To convert the TopoJSON back into GeoJSON, log this:

  ```
  topoJSON.feature(us, us.objects.counties)
  ```

What's the difference between them?

Set up and append an SVG just like always (though no margin is necessary this time, as we have no axes).
Let's imagine we wanted to do a data join and add 3,000 lines to our SVG. What would that code look like? Make a variable of the topojson features and do a data join with it, adding one circle for each county.

Obviously, we need some way to tell the computer how to draw the shapes in our data. Luckily for us, they've been pre-projected. We can get into this in a minute. But for now, all we need to do is tell D3 it's a [geo.path()](https://github.com/mbostock/d3/wiki/Geo-Paths#path).  
```
const path = d3.geoPath();
```
Instead of appending circles, append paths -- just like any other path! 
See anything good? Let's make a list of things we need to visualize our data.

We have three goals:
  * Make a map showing the extent of the geography of the origins of guns successfully traced to Chicago.
  * Make a choropleth map
  * Make a bubble map 

Things we may need: loading [more than one](http://bl.ocks.org/mapsam/6090056) data file at once, learning about [color scales](https://github.com/d3/d3-scale/blob/master/README.md#scaleThreshold), some light data formatting, probably finding out the [center of a path](https://github.com/d3/d3-geo/blob/master/README.md#path_centroid)

A bonus, add a little interactivity to your map using `mouseenter` and `mouseleave`.

## It's not that simple, though.
If there's time, we'll talk about different projections.

## Optional reading for Monday
  * Mike's helpful [tutorial series](http://bost.ocks.org/mike/map/).
  * [When Maps Shouldn't Be Maps](http://www.ericson.net/content/2011/10/when-maps-shouldnt-be-maps/) by Matt Ericson, NYT Big Dog

# Helpful links
  * [Sickening Examples](https://beta.observablehq.com/collection/@fil/geo) from Philippe Rivière
  * [Great examples](https://www.jasondavies.com/maps/) from Jason Davies
  * Mike's [US Atlas](https://github.com/mbostock/us-atlas)
  * Matt Bloch's amazing [Mapshapr](http://mapshaper.org/)
  * [QGIS](http://www.qgis.org/en/site/) is excellent, free GIS software 
  * I use [this bl.ock](http://bl.ocks.org/mbostock/3306362) as a starter kit
  * Gregor Aisch's very helpful [color picker](http://gka.github.io/palettes/#colors=lightyellow,orange,deeppink,darkred|steps=7|bez=1|coL=1)
  * [Every ColorBrewer scale](http://bl.ocks.org/mbostock/5577023)
  * [Where 50,000 Guns in Chicago Came From](http://www.nytimes.com/interactive/2013/01/29/us/where-50000-guns-in-chicago-came-from.html) (NYT)

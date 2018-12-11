# Class 11: Stack Layouts

## Housekeeping
  * Show N' Tell? 
  * Questions?
  * Last class Thursday!
  * Goals for Today
  	* Learn about stack layouts
    * Master data manipulation for d3.stack()
    * If there's time, beeswarms 

# Stack Layouts
from the [D3 API](https://github.com/d3/d3-shape/blob/master/README.md#stack)...
>Generates a stack for the given array of data, returning an array representing each series. Any additional arguments are arbitrary; they are simply propagated to accessors along with the this object. The series are determined by the keys accessor; each series i in the returned array corresponds to the ith key. Each series is an array of points, where each point j corresponds to the jth element in the input data. Lastly, each point is represented as an array [y0, y1] where y0 is the lower value (baseline) and y1 is the upper value (topline); the difference between y0 and y1 corresponds to the computed value for this point. The key for each series is available as series.key, and the index as series.index. The input data element for each point is available as point.data.

English:
>Stacks your data and provides the min and max y value.

Here are [some](https://beta.observablehq.com/@mbostock/d3-stacked-bar-chart) [basic](https://beta.observablehq.com/@mbostock/d3-stacked-horizontal-bar-chart) [examples](https://beta.observablehq.com/@mbostock/d3-stacked-normalized-horizontal-bar-chart), and a [streamgraph](https://beta.observablehq.com/@mbostock/streamgraph-transitions)


## Lab, part I:

Let's see what the d3.stack() function does with a simple example. We'll make something that looks like this:

<img src="images/Screen Shot 2016-10-18 at 8.39.28 PM.png">

We already know how to make a bar chart, so what we need to figure out here is:
1. How to use d3.stack() to layer the data
2. How to draw the bars using the output of d3.stack()
3. Also, some of the parameters we can tweak with d3.stack()

## Lab, part II
Now, let's apply what we've learned to a more interesting dataset.

I found this [data]("views/population/UNdata_Export_20161019_010544114") on world polations from a [UN website](http://data.un.org/Data.aspx?q=population&d=PopDiv&f=variableID%3a12). It has population counts for each country, by year, with projections for future years. We're going to need to filter the data somewhat, as there is a lot of information. I've also attached a country lookup file for getting regions names from [here](https://github.com/lukes/ISO-3166-Countries-with-Regional-Codes/blob/master/all/all.csv). The goal will be to make something like this:

<img src="images/Screen Shot 2018-12-11 at 3.42.34 PM.png">

Download the data locally, start up a new index.html file and a local server. You can copy and paste the work we just did from the simple example or use one of the starter files (under views/population/starter.html)
* What do we notice about the data?
* How is it structured?
* What will we need to do to get it into the right format?
* Let's make a checklist for what we want to build out

Also,
* Let's use d3.area() to convert our bar chart to an area chart
* Labels or a legend?
* What sort of interactivity would be good to add?


## Homework for Thursday
* Bring questions, examples, anything you want to discuss one more time with the class.
* I'd like each of you to share some work you've done. Have a link ready for Thursday.





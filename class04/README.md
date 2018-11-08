#Class 4: Continuing our barley charts; Abstracting functions, discussing merits of chart forms; d3.nest()

Mmmmmmm Barley

##Housekeeping

 * Any questions?
 * Projects & Pace
 
 * Goals for today
 	* Review Mondays's class work
 	* Continue our progress on barley charts, judge merits of each.
	* Using functions to draw charts
	* Discussing abstractions and functions
	* Learning about data hierarchies in the DOM and d3.nest()

 * Resources on transforming and nesting data:
	* [Arrays and nesting](https://github.com/mbostock/d3/wiki/Arrays#-nest)
	* [An extremely useful tool by Shan Carter](http://bl.ocks.org/shancarter/raw/4748131/)
	* [More examples of d3.nest](http://bl.ocks.org/phoebebright/raw/3176159/)

 * Resources on d3 selections:
	* [General Update Pattern](https://bl.ocks.org/mbostock/3808218)
	* [Thinking with Joins](https://bost.ocks.org/mike/join/)
	* [Nested selections](https://bost.ocks.org/mike/nest/)

## All the ways we can chart barley yields
No form is perfect -- each comes with its own tradeoffs. Here are some versions of different ways to visualize the data:

  * Lots of [bar charts](http://bl.ocks.org/pstuffa/326c1dc86d98d565b40f4c388b449e88)
  * A [line chart](https://bl.ocks.org/pstuffa/29b92ac24deb4ecefe5e403d9385070b)
  * A [slope graph](http://bl.ocks.org/pstuffa/5ac32bf4e3810a7ae61866ee5de02d41) from a previous cohort.
  * Here's a [dot plot](http://bl.ocks.org/kpq/1f6fc300f11850aba80e) from a previous cohort.
  * Here's a variation using [a scatterpplot and convex hulls](http://bl.ocks.org/pstuffa/2039304ed80b1c08be718fce486360ca)
  * And a VERY silly [network graph version](https://bl.ocks.org/pstuffa/c65d82662507d677249db3d1513b874f)


## Review & Another Way
 1. Let's go over the work we did on Tuesday
 2. Let's try to do the bar chart version, but using a new method, d3.nest()


# Generalizing our charts
How would we do this if we wanted to make not one chart, but N charts? Two ways of thinking about it.

## Lab
 1. Check out [Mister Nester](http://bl.ocks.org/shancarter/raw/4748131/) and try pasting the barley data into it.
 2. Try making your group of six charts either using functions or using d3.nest(). (Note: for you nesters, some of you may need to nest twice.

## Homework for Wednesday
 * Publish to Observable! Have a block for Anscombe quartet and your barley visualization.

## Optional for Wednesday and beyond
 * Explore the extended Barley Yield dataset from this [blog post](http://blog.revolutionanalytics.com/2014/07/theres-no-mistake-in-the-barley-data.html).
 * Extended barley data from [agridat package](http://www.rdocumentation.org/packages/agridat/functions/minnesota.barley.yield)




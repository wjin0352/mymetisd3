# Class 7: Updating elements: Data joins; interactivity; (possibly) responsive charts

## Housekeeping
* Review of last week: hierarchy, nesting
* Any questions?
* Goals for today
  * Understand how to make charts update, using the General Update Pattern
* 3 weeks left!
* The final run through of topics:
  * [Network Graphs](https://beta.observablehq.com/@mbostock/d3-force-directed-graph)
  * [Treemaps](https://beta.observablehq.com/@mbostock/d3-treemap)
  * [Stacked Bar Charts](https://beta.observablehq.com/@mbostock/d3-stacked-bar-chart)
  * [Heatmaps](https://beta.observablehq.com/@leoyuholo/hong-kong-temperature-heatmap)
  * [Pie Charts / Donut Charts](https://beta.observablehq.com/@mbostock/d3-pie-chart)
  * [Bubble Charts](https://beta.observablehq.com/@mbostock/d3-bubble-chart)
  * [Sankey Diagrams](https://beta.observablehq.com/@mbostock/d3-sankey-diagram)
  * [Simple Scrollytelling](https://pudding.cool/2017/03/comeback/) (this might have to be a two session walk through.. we'll see)
* If there's nothing else, lets vote during the break

## What is the General Update Pattern?
 * [Thinking with joins](http://bost.ocks.org/mike/join/)
 * [General Update Pattern](http://bl.ocks.org/mbostock/3808218)
 * [General Update Pattern II](http://bl.ocks.org/mbostock/3808221)
 * [General Update Pattern III](http://bl.ocks.org/mbostock/3808234)

## Lab, part 1 - Updating Charts

Today we will use the general update pattern on a version of our income line chart from last week:
 * What would we need to update? How would we do it?
 * Try to make the chart so it updates for each country for the median income. We'll aim for something like this:

<img src="images/Screen Shot 2016-10-04 at 10.16.01 PM.png">


Let's make a checklist:
  1. Make new data join
  2. Assign an ID (optional)
  3. Get rid of old elements
  4. Update existing elements
  5. Append elements as needed
  6. Update scales as needed
  7. Utilize the `d3.transition` function to make it pop!

Let's do it first with lines, and then increase complexity with to dots.

## Lab, part 2 - Mobile

Designing a visualization that works for both mobile and desktop is hard. Take a look at these examples that I think do a great job. *Note how to view on Mobile with Chrome developer tools*

  - [A 3-D View of a Chart That Predicts The Economic Future: The Yield Curve](http://www.nytimes.com/interactive/2015/03/19/upshot/3d-yield-curve-economic-growth.html)
  - [The Facebook Offering: How It Compares](http://www.nytimes.com/interactive/2012/05/17/business/dealbook/how-the-facebook-offering-compares.html)
  - [Fewer Helmets, More Deaths](http://www.nytimes.com/interactive/2014/03/31/science/motorcycle-helmet-laws.html)
  - [The Tenure Pipeline at Harvard Business School](http://www.nytimes.com/2013/09/08/education/harvard-case-study-gender-equity.html?ref=education)

Our visualization works OK on mobile, but how could we make it better? Let's use `window.on('resize')` to update the charts size when the browser window changes.

Going furtuer, what are some design ideas we could do to make it much better for mobile? Let's sketch something out, then again use `window.on('resize')`, perhaps with some conditionals, to redraw our chart when we switch to mobile.

#### For Thursday

Read [this observable notebook](https://beta.observablehq.com/@mbostock/psr-b1919-21) and try to understand how it works. It's a slight variation of the line charts we have been making, that utilizes this overlap effect to create whats called a Ridgeline Plot. **Extra Credit** if you can fork the notebook and either swap out the data or create an alternate design. 




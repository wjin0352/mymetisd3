#Introduction to D3

### D3
* Documentation https://github.com/mbostock/d3/wiki
* Examples Gallery https://github.com/mbostock/d3/wiki/Gallery

## Observable
* Main Site http://observablehq.com/
* Five Minute Introduction 

### Mike Bostock
* Observable https://beta.observablehq.com/@mbostock
* Bl.ocks http://bl.ocks.org/mbostock

### Paul Buffa
* Observable https://beta.observablehq.com/@pstuffa
* Twitter https://twitter.com/pstuffa

### Kevin Quealy
* Recent work https://www.nytimes.com/by/kevin-quealy
* The Upshot http://www.nytimes.com/section/upshot

### Amanda Cox
* New York Times http://topics.nytimes.com/top/reference/timestopics/people/c/amanda_cox/index.html
* OpenVis Conf Keynote https://www.youtube.com/watch?v=ha9LA3rYD9g

[Resources](https://github.com/thisismetis/nyc18_dataviz11/blob/master/resources.md)

## Class 1: Charting basics, using D3 with the DOM and making a scatterplot

Here's what we'll do today:

"SOFT" (non-technical)
  - Set personal goals for the class
  - Think about long-term class projects
  - Make sure our computers are configured properly
  - Get a sense of who's here
  - Understand the role of visualization in data analysis
  - Learn about charting components and terms

"HARD" (more technical)
  - D3 scales, axes, data joins and DOM selection
  - Create, manipulate and style SVG elements
  - Use D3 and SVG documentation pages and wikis
  - Do our first data join
  - Create and share a bl.ock using git and Github
  - Use D3 in the console for debugging and experimentation
  - Use the Chrome inspector 

---

## Housekeeping and discussion

  1. First, everyone should take a minute write down on a notecard some goals they have for themselves in this class.
  2. 30-second introductions: names, jobs, goals for the class, and a favorite thing to do that involves no computers whatsoever. 
  3. Let's make sure our computers are configured correctly. You should have a [Github account](www.github.com), know how to set up a [local server](https://github.com/mbostock/d3/wiki#using), use a text editor (we enjoy [Sublime text](https://www.sublimetext.com/), but you do you) and use the Chrome Web inspector. 
  4. Two things we should keep in mind as we begin the class: different goals for the class and skill variance.
  5. Expectations about communicating with me. Also, there's a [Slack channel](https://metis-data-viz.slack.com/messages);
  6. How each class will be (loosely) structured: **discussion** of readings or an interactive project, (sometimes) a no-computers **activity** or minimal **lecture**, an in-class **demonstration** and an option for you – a lab session or time to work on your own projects.
  7. Overall class outcomes: technical and non-technical.
  8. Projects!

## Activity
Everyone will be assigned a Roman Numeral, I, II, III or IV.

Copy the data locally from [this Google doc](https://docs.google.com/spreadsheets/d/17xOrBfaXxM_z1xrwNv-mZQokXnwqt-piGzpJDIAjv70/edit?usp=sharing) *for your group only* and do the following calculations:

 1. Calculate the average value and variance (`VAR` in Excel and Google spreadsheets) of both the "x" and "y" columns. 
 2. Calculate the [Pearson's coefficient](https://en.wikipedia.org/wiki/Pearson_product-moment_correlation_coefficient) of x and y (you can use `CORR` in Excel or `CORREL` in Google Spreadsheets). 
 3. Now calculate the slope and y-intercept of the best-fit line to the data (`SLOPE` and `INTERCEPT` in both). 
 4. Plot the data by hand using the graph paper. If possible, use one color for your data, another for your best-fit line and another for everything else.
 5. When we're all done, paste your chart to the wall. How do they look?
 6. Let's talk about our charts and go over some basic ideas and charting terms.


## Why we visualize
This exercise, called [Anscombe's quartet](https://en.wikipedia.org/wiki/Anscombe's_quartet), may have seemed obvious or simple, but it's a classic example of the importance of visualizing data. In one of her [many](http://www.slideshare.net/openjournalism/amanda-cox-visualizing-data-at-the-new-york-times) [amazing](https://vimeo.com/133608685) lectures and talks, Amanda Cox lists several important reasons for visualizing data:

 * To *describe geography*, like how Last Chance Harvey is the [ultimate suburban movie](http://www.nytimes.com/interactive/2010/01/10/nyregion/20100110-netflix-map.html?_r=0), or why presidential voting in the south is really about [snail shells](http://cstl-csm.semo.edu/agathman/cottonvote.htm) [millions](http://www.vigorousnorth.com/2008/11/black-belt-how-soil-types-determined.html) of years old.
 * To *show patterns*, as in [this linechart](http://www.nytimes.com/interactive/2014/07/08/upshot/how-the-year-you-were-born-influences-your-politics.html) of birth years to political views
 * To *reveal outliers*, as with [Steph Curry's crazy three-point shooting](http://www.nytimes.com/interactive/2016/04/16/upshot/stephen-curry-golden-state-warriors-3-pointers.html), or [extremely large Chipotle orders](http://www.nytimes.com/interactive/2015/02/17/upshot/what-do-people-actually-order-at-chipotle.html)
 * To *provide context*, as with this helpful map of the extent of [the moon landing](http://history.nasa.gov/alsj/a11/A11vsFootball.gif), or long-jumping [on a basketball court](http://www.nytimes.com/interactive/2012/08/04/sports/olympics/bob-beamons-long-olympic-shadow.html) or this [outstanding video](https://www.youtube.com/watch?v=2i28MU8-lcw) showing how fast NFL players are.

This exercise is also a good introduction to the nuts and bolts of thinking about charting – translating data to a physical space. We'll need to think about these relationships much more formally using D3.

## Lab part I

We're going to make the chart we drew by hand using D3. We're going to cover a lot of fundamentals right now. If this is all new to you, try to suspend your disbelief a bit. It will all make more sense as we go a long. (We'll also spend time beginning of next class rewiewing/going over any questions.)

  1. Start by making a folder however you like, however you want to organize things. Make a file called `index.html` in this folder and [load D3](http://d3js.org/) on the page. (In my folder structure, it's `/nyc18_dataviz11/class01/class-work.html`, but you're the boss.) 

  ```
  <!DOCTYPE html>
  <meta charset="utf-8">

  <style type="text/css">
    /*css to go here*/
  </style>

  <body></body>

 <script src="https://d3js.org/d3.v4.min.js"></script>
 
  <script>
    //JS to go here
  </script>

  ```
  2. Fire up a local server and open the page in the console. Test and see if your version loaded. 
  3. Make a Javascript object out of your tabular data and make sure you know how to manipulate it. (This is an annoying but useful exercise in getting useful in a text editor.) I'll use the data from the group number II, but you should chart whatever you drew.
  4. Add an SVG element of width 720 and height 400.
  5. Using a data join, add a circle for every element of our array. Give it a radius 5 and a class, 'anscombe-circle'. Inspect it in the browser. To start, I like to put a border around the SVG to make sure I knew it drew:

  ```
  svg {
    border: 1px solid #000;
  }
  ```

  6. Position the circles based on their `x` and `y` attributes. How does SVG interpret these positions?
  7. We need a [scale](https://github.com/mbostock/d3/wiki/Quantitative-Scales#linear-scales). Let's add one. 
  8. Let's label the coordinate positions of each using text. Is another data join really necessary?
  9. Redo the original join, using groups first, then appending circles and text. Note SVG [transformation](http://www.w3.org/TR/SVG/coords.html) documentation, which is not that fun. 
  10. Maybe [axes](https://github.com/mbostock/d3/wiki/SVG-Axes) are in order?  
  11. We might need to move our axes around. We'll go through the math. Also, maybe add some styles?
  12. The margins are a problem, and they will always be. Here's [a great trick](https://bl.ocks.org/mbostock/3019563) we'll use on every chart we make from here on out.
  13. Let's style the chart to match our drawing. Things like [tickSize](https://github.com/mbostock/d3/wiki/SVG-Axes#tickSize) might help.
  14. Let's make this a block before time runs out, using git and Github. Add a thumbnail and check out your own bl.ocks page! 

## If there's time/getting more advanced

 1. Add `p` tags under the chart for the mean of x and y, and the variance of each. Calculate them dynamically.
 2. Load your data dynamically instead of using a variable. (Why would we want to do that?) Here's [a tsv](quartet.tsv) to get you started. You might need to filter your data before plotting your quartet.
 3. So far, after 100 lines of code, our chart isn't really better than what we get with the free tools. (Paste your data into [Chartbuilder](http://quartz.github.io/Chartbuilder/) and feel free to weep.) What makes D3 different is its ability to create **dynamic** visualizations and things that tools aren't designed to create. A scatterplot is simple to make a widget for; [other forms](http://www.nytimes.com/newsgraphics/2013/09/28/eli-manning-milestone/), less so.
 4. To push this further, abstract our chart out by making a function that updates the chart given a group id, including updating the text fields for averages. Fire the function (and update the chart) every three seconds.
 5. If you're really interested in doing stats in Javascript, calculate the Pearson Coefficient and best-fit line and update both in your function. 


## Reading for next week
On Wednesday we'll be talking about charting and *intent*. Read these and be ready to discuss them.
  - [The Power of Visualization’s “Aha!” Moments](https://hbr.org/2013/03/power-of-visualizations-aha-moment/)
  - [Redesigining a Circular Timeline](http://www.thefunctionalart.com/2015/02/redesigning-circular-timeline.html)
  - [Design and Redesign in Data Visualization](https://medium.com/@hint_fm/design-and-redesign-4ab77206cf9)
  - [What are you trying to say?](http://lulupinney.co.uk/2012/08/what-are-you-trying-to-say/)

Also, read through [this code](review.html). Even if you don't understand it, take a few minutes to look through and try to get some general idea of what each section does. 


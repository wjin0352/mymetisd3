[Resources](https://github.com/thisismetis/nyc18_dataviz11/blob/master/resources.md)
[Projects](https://github.com/thisismetis/nyc18_dataviz11/blob/master/projects.md)


## Class 2: Charting basics, using D3 with the DOM and making a scatterplot - Part II!

Here's what we'll do today:

 * Review any questions we had from class 1
 * Continue with our build of Anscombe's Quartet
 * Publish our work
 * Discuss Homework
  * [The Power of Visualization’s “Aha!” Moments](https://hbr.org/2013/03/power-of-visualizations-aha-moment/)
  * [Redesigining a Circular Timeline](http://www.thefunctionalart.com/2015/02/redesigning-circular-timeline.html)
  * [Design and Redesign in Data Visualization](https://medium.com/@hint_fm/design-and-redesign-4ab77206cf9)
  * [What are you trying to say?](http://lulupinney.co.uk/2012/08/what-are-you-trying-to-say/)


## Where we left off

  ```
  <!DOCTYPE html>
  <meta charset="utf-8">

  <style type="text/css">
    svg {
      border: 1px solid #ff00ff;
    }
  </style>

  <body>

  </body>

  <script src="https://d3js.org/d3.v4.min.js"></script>

  <script>
    //JS to go here

    var xScale = d3.scaleLinear()
        .domain([0, 20])
        .range([0, 300]);

    var yScale = d3.scaleLinear()
        .domain([0, 15])
        .range([150, 0]);

    var data = [
      {"x":8, "y":  6.58, "group": "IV"},
      {"x":8, "y":  5.76, "group": "IV"},
      {"x":8, "y":  7.71, "group": "IV"},
      {"x":8, "y":  8.84, "group": "IV"},
      {"x":8, "y":  8.47, "group": "IV"},
      {"x":8, "y":  7.04, "group": "IV"},
      {"x":8, "y":  5.25, "group": "IV"},
      {"x":19, "y": 12.5, "group": "IV"},
      {"x":8, "y":  5.56, "group": "IV"},
      {"x":8, "y":  7.91, "group": "IV"},
      {"x":8, "y":  6.89, "group": "IV"}
    ];

    // d3.select("svg").append("circle")

    var body = d3.select("body");

    body.append("h1")
      .text("Hello 2");

    var svg = body.append("svg");
    
    var circle = svg.selectAll("circle")
      .data(data)
      .enter()
      .append("circle")
      .attr("r", 4)
      .attr("cx", function(d,i) {
        return xScale(d.x);
      })
      .attr("cy", function(d,i) {
        return yScale(d.y);
      });

  </script>
  ```


##Lab

We're going to recreate what we did last Monday, but with a few differences. Let's make a list of things to do. What does our chart need? (Think along the ladder of abstraction)

I have some ideas but I'm sure we can get a good list.


##If there's time/getting more advanced

 1. Add `p` tags under the chart for the mean of x and y, and the variance of each. Calculate them dynamically.
 2. So far, after 100 lines of code, our chart isn't really better than what we get with the free tools. (Paste your data into [Chartbuilder](http://quartz.github.io/Chartbuilder/) and feel free to weep.) What makes D3 different is its ability to create **dynamic** visualizations and things that tools aren't designed to create. A scatterplot is simple to make a widget for; [other forms](http://www.nytimes.com/newsgraphics/2013/09/28/eli-manning-milestone/), less so.
 3. To push this further, abstract our chart out by making a function that updates the chart given a group id, including updating the text fields for averages. Fire the function (and update the chart) every three seconds.
 4. If you're really interested in doing stats in Javascript, calculate the Pearson Coefficient and best-fit line and update both in your function. 


## Observable
Observable is a brand new site, and is functioning as the replacement for bl.ocks. In previous versions of this course, we've taught how to publish on blocks, but given this is the new direction for sharing D3 code, we'll walk through how observable works. Let's walk through Mike's [5-minute introduction](https://beta.observablehq.com/@mbostock/five-minute-introduction).

##### Basics of porting to Observable
```
{
  const svg = DOM.svg(width, height)

  return svg.node();
}
```

## Homework for Monday
 * Publish your Anscombe's Quartet in Observable 

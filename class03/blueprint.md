In detail:

1. **Navigate to your working directory of choice and fire up a local server**
 Make sure you're comfortable using the command line. There are [many ways](https://github.com/mbostock/d3/wiki#using) to set up a server.

2. **Loading data** Many data sets you'll be desiging for change – hourly, weekly, monthly, whatever. You don't want to be copy/pasting or doing manual labor every time your data set changes, so loading it exernally is a good idea. D3 comes with a [wide variety](https://github.com/mbostock/d3/wiki/Requests) of methods that let you load data asynchronously. We'll primarily use d3.tsv for "rectangular" data sets. This 

 ```
 d3.tsv("path/to/file.tsv").then((data) => {

   //your code starts here

 });
 ```

 To clean things up, we can name the callback `ready` and define it below, but the difference is only cosmetic.

 ```
 d3.tsv("path/to/file.tsv").then(ready);

 function ready(data) {

   //your code starts here

 }

 ```

2. **Add an SVG on the page.**
 Most, but not all, of the time, you are going to be charting on an SVG element. There are all sorts of ways to do this, but [this bl.ock](http://bl.ocks.org/mbostock/3019563), which includes handy margin conventions is really useful, and my favorite. Key passage:

 ```
 var margin = {top: 20, right: 10, bottom: 20, left: 10};

 var width = 960 - margin.left - margin.right,
     height = 500 - margin.top - margin.bottom;

 var svg = d3.select("body").append("svg")
     .attr("width", width + margin.left + margin.right)
     .attr("height", height + margin.top + margin.bottom)
   .append("g")
     .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
 ```

 Note a personal preference you're free to ignore: in the beginning, sometimes I like to make sure the SVG rendered without using the inspector, so I make a border around the SVG in CSS:

 ```
 <style type="text/css">
   svg {
     border: 1px solid #f0f;
   }
 </style>
 ```

3. **Format your data** 
 D3.tsv() Usually turns your data into strings, which makes doing math on them a bad idea. Or sometimes you just need to do light formatting, whether adding a leading zero to 4-digit FIPS codes or turning a string into a Date. Do this right when you load your data. 

 ```
 d3.tsv("path/to/file.tsv").then(ready);

 function ready(data) {

   //formatting numbers
   data.forEach(function(d) {
     d.x = +d.x;
     d.y = +d.y;
   });

 }

 ```


4. **Do your data join**
 Before you can style your elements or move them around your canvas, you need to create elements inside your SVG. Usually, this starts with a data join. If you're doing a data join with externally-loaded data, this join should happen inside your `ready` function. Note this pattern will not apply for every kind of data you chart, but it should do for the kinds of things we've worked with so far. Here, we add a `g` element for every row in our data.

 ```
 var margin = {top: 20, right: 10, bottom: 20, left: 10};

 var width = 960 - margin.left - margin.right,
     height = 500 - margin.top - margin.bottom;

 var svg = d3.select("body").append("svg")
     .attr("width", width + margin.left + margin.right)
     .attr("height", height + margin.top + margin.bottom)
   .append("g")
     .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

 d3.tsv("path/to/file.tsv").then(ready);

 function ready(data) {

   svg.selectAll(".circle-group")
       .data(data)
       .enter()
       .append("g")
       .attr("class", "circle-group");
 }
 ```

5. **Position your elements** To do this, you need [scales](https://github.com/mbostock/d3/wiki/Scales), whether they’re linear, time, ordinal or something else. Note that when you’re making your scale dynamic –– to define its domain based on the data you load – you will have to define it in two steps: [range](https://github.com/mbostock/d3/wiki/Quantitative-Scales#linear_range) first, then [domain](https://github.com/mbostock/d3/wiki/Quantitative-Scales#linear_domain). Here, we define them above the `ready` function and update the domain for `xScale` and `yScale` only inside the `ready` function. (Why?)  

 ```
 var margin = {top: 20, right: 10, bottom: 20, left: 10};

 var width = 960 - margin.left - margin.right,
     height = 500 - margin.top - margin.bottom;

 var svg = d3.select("body").append("svg")
     .attr("width", width + margin.left + margin.right)
     .attr("height", height + margin.top + margin.bottom)
   .append("g")
     .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

 var xScale = d3.scaleLinear()
     .range([0,width]);

 // note our trick on yScale's range, since y=0 is at the top of the SVG 
 var yScale = d3.scaleLinear()
     .range([height,0]);

 d3.tsv("path/to/file.tsv").then(ready);

 function ready(data) {

   //update domains based on extrema, which has pluses and minuses
   xScale.domain(d3.extent(data, function(d) { return d.xPos; }));
   yScale.domain(d3.extent(data, function(d) { return d.yPos; }));

   var circleGroup = svg.selectAll(".circle-group")
       .data(data)
     .enter()
       .append("g")
       .attr("class", "circle-group")
       .attr("transform", function(d) { return "translate(" + xScale(d.xPos) + "," + yScale(d.yPos) + ")"; });

   //since the gs are already positioned, we dont need to transform any of their child elements
   circleGroup.append("circle")
       .attr("r", 5);

   //move these just a touch
   circleGroup.append("text")
       .text(function(d) { return d.xPos + "," + d.yPos; })
       .attr("dx", 5)
       .attr("dy", -5);
 }
 ```

6. **Add an axis**
 D3 Axes are helpful, but they seem complicated sometimes. By calling an axis component, d3 will add a `g` element of class `tick` to your SVG. In each, it will add a `line` and `text`. You do this in two steps.

 First, declare the axes as variables.

 ```
 var xAxis = d3.axisBottom(xScale);

 var yAxis = d3.axisRight(yScale);
 ```

 Then add `g` elements to your page and `call` the axes. Note the translation here.

 ```
 svg.append("g")
     .attr("class", "x axis")
     .attr("transform", "translate(0," + height + ")")
     .call(xAxis);

 svg.append("g")
     .attr("class", "y axis")
     .attr("transform", "translate(" + width + ",0)")
     .call(yAxis);
 ```

7. **Add styles** and customize as necessary
 You'll definitely need to style your axes at the very least, but probably more too.

8. **Example: putting it all together.** 
 Also captured here as [a bl.ock](http://bl.ocks.org/kpq/4ec215b40c1d559fcb2a)

 ```
 <!DOCTYPE html>
 <meta charset="utf-8">

 <style type="text/css">

   body {
     font-family: arial, sans;
     font-size: 11px;
   }
   
   svg {
     border: 1px solid #f0f;
   }

   .axis line,
   .axis path {
     fill: none;
     stroke: #000;
     shape-rendering: crispEdges;
   }

 </style>

 <body>

 </body>

 <script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.5/d3.min.js" charset="utf-8"></script>

 <script type="text/javascript">
   
 var margin = {top: 20, right: 50, bottom: 20, left: 10};

 var width = 960 - margin.left - margin.right,
     height = 500 - margin.top - margin.bottom;

 var svg = d3.select("body").append("svg")
     .attr("width", width + margin.left + margin.right)
     .attr("height", height + margin.top + margin.bottom)
   .append("g")
     .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

 var xScale = d3.scaleLinear()
     .range([0,width]);

 var yScale = d3.scaleLinear()
     .range([height,0]);

 var xAxis = d3.axisBottom(xScale);

 var yAxis = d3.svg.axisRight(yScale);

 d3.tsv("quartet.tsv").then(ready);

 function ready(data) {

   data.forEach(function(d) {
     d.xPos = +d.xPos;
     d.yPos = +d.yPos;
   });

   //update domains based on extrema, which has pluses and minuses
   xScale.domain(d3.extent(data, function(d) { return d.xPos; }));
   yScale.domain(d3.extent(data, function(d) { return d.yPos; }));

   svg.append("g")
       .attr("class", "x axis")
       .attr("transform", "translate(0," + height + ")")
       .call(xAxis);

   svg.append("g")
       .attr("class", "y axis")
       .attr("transform", "translate(" + width + ",0)")
       .call(yAxis);

   var circleGroup = svg.selectAll(".circle-group")
       .data(data)
     .enter()
       .append("g")
       .attr("class", "circle-group")
       .attr("transform", function(d) { return "translate(" + xScale(d.xPos) + "," + yScale(d.yPos) + ")"; });

   circleGroup.append("circle")
       .attr("r", 5);

   circleGroup.append("text")
       .text(function(d) { return d.xPos + "," + d.yPos; })
       .attr("dx", 5)
       .attr("dy", -5);

     }
 </script>
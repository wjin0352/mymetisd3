# Class 12: Network Graphs & Sankey Diagrams

## Housekeeping
  * Show N' Tell! Let's see some of your work.
  * Last class! 
  * Goals for Today
  	* Learn what network graphs are
  	* Learn about how to use a force directed layouts
  	* Learn about how Sankey diagrams work
    * Make a sankey diagram with our world population data 
    * How to keep learning after class

# Network Graphs 

What is a Network Graph?

> In mathematics and computer science, graph theory is the study of graphs, which are mathematical structures used to model pairwise relations between objects. A graph in this context is made up of vertices, nodes, or points which are connected by edges, arcs, or lines.

Sounds complicated, but it's not that bad. Essentially, you have two sets of items: nodes and links. The nodes are (usually) the circles in the network graph. The links are the lines. And having two datasets, one for the nodes and one for the links, is how you'll generate a network graph. Here's a look at a very basic network graph:

![simple graph!](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5b/6n-graf.svg/2000px-6n-graf.svg.png)

##### Types of Graphs

There are many different type of layouts for graphs. They type of graph is determined by it's layout. All graph layouts are generally aim for the same goal: readabiliy. Here's a look at few:
 * [Force Directed](https://bl.ocks.org/mbostock/4062045)
  * [Blocks](https://bl.ocks.org/mbostock/afecf1ce04644ad9036ca146d2084895)
  * [Lattice](https://bl.ocks.org/mbostock/1b64ec067fcfc51e7471d944f51f1611)
 * [Arc](https://www.jasondavies.com/primos/)
 * [Hive](https://bost.ocks.org/mike/hive/)
 * [Tree](https://bl.ocks.org/mbostock/4339083)
 * And yes! [Sankey Diagrams](https://beta.observablehq.com/@mbostock/d3-sankey-diagram)

Note the way the data is structed in each example. All `graph = {nodes, links}`

## Lab, part I

Let's first make that image above of a really basic network graph. Let's go through that Force Directed Graph example to get a sense of what that'll look like:
 1. Add you SVG
 2. Define your force simluation
 3. Put your data in the correct format
 4. Input the data into the simulation
 5. Set the positions for all the elements you want using the ticked() function
 6. Start the simulation 

## Lab, part II - Sankey!

Think of sankey diagrams as another form of network graphs. It'ss all about the nodes and links. As always, it's good to checkout [the API](https://github.com/d3/d3-sankey) to learn about the specifics. (Although the docs can be a bit obtuse, still helpful to see what parameters you can set.) Note, d3.sankey() is **not** part of the main D3 library, so you need to include `<script src="https://unpkg.com/d3-sankey@0"></script>` at the top of your page.

Your nodes and links in a Sankey diagram must have some features: 

```
Each node must be an object. The following properties are assigned by the Sankey generator:

node.sourceLinks - the array of outgoing links which have this node as their source
node.targetLinks - the array of incoming links which have this node as their target
node.value - the node’s value; the sum of link.value for the node’s incoming links
node.index - the node’s zero-based index within the array of nodes
node.depth - the node’s zero-based graph depth, derived from the graph topology
node.height - the node’s zero-based graph height, derived from the graph topology
node.x0 - the node’s minimum horizontal position, derived from node.depth
node.x1 - the node’s maximum horizontal position (node.x0 + sankey.nodeWidth)
node.y0 - the node’s minimum vertical position
node.y1 - the node’s maximum vertical position (node.y1 - node.y0 is proportional to node.value)

```
Ok, so basically, you need to supply nodes with some id, and the rest is created by `d3.sankey()`

As for links:

```
Each link must be an object with the following properties:

link.source - the link’s source node
link.target - the link’s target node
link.value - the link’s numeric value
```

So then for links, we're going to make something very similar to the force-directed graph, but we have to add a `value` field. This makes sense, as in a sankey diagram, the size of the rectangles and links are meaningful. Let's try to make this very simple sankey diagram. Let's talk about what the data will look like for it: 

<img src="images/Screen Shot 2018-12-13 at 1.47.46 PM.png">

Similar checklist to force-directed
 1. Add you SVG
 2. Define your Sankey()
 3. Put your data in the correct format
 4. Input the data into the Sankey() funciton
 5. Set the positions for all the elements 


## Lab, part III

Now that we have a simple example of a Sankey diagram done, let's try to up the complexity by creating one with the UN population data we worked with on Tuesday:

<img src="images/Screen Shot 2018-12-13 at 2.22.14 PM.png">

The goal for this will be to figure out how we transform the data to get it in the right format. Let's talk about the data structure and see from our bag of tricks what we might want to use:
 * lookups functions?
 * d3.nest()?
 * forEach()?



# Keep it going! 
So today's the final class, but you should keep learning more D3. How!? You might ask...

  * What should I do?  __Publish Your Work__, even if they are not completed.
    * Observable is great for this
    * Twitter as a distribution channel
  * What should I make? __Something you care about__. Might sound obvious, but work on something that makes you excited. It's really hard to work on things you find boring.
  * What if I don't have any time? __Make it part of your job__. Try to get the time you have to spend at work time you spent making great data viz.
  * You can keep using this repo!
    * Use the examples we've done in class for your own projectss
    * Class-work, starter, and review 
  * Good Ways to Share your Work
      * Screenshots
      * Videos
      * Videos to gifs 
        * [Imagemagik](https://www.imagemagick.org/script/index.php)
              $ ffmpeg -i ~/videos/{YOUR FILE NAME}.mov -vf scale=400:-1 -r 5 ./stage/ffout%3d.png
        * ``` $ convert -delay 8 -loop 0 ./stage/ffout*.png ../gifs/{YOUR GIF NAME}.gif
          ```
      * Storing Data
        * Gists (smaller datasets)
        * S3 Buckets (AWS)
      * Observable
      * Twitter
      * [Heroku](https://github.com/thisismetis/nyc17_dataviz7/tree/master/class13)
      * [gh-pages](https://pages.github.com/)
      * [reveal.js](http://lab.hakim.se/reveal-js/)
  * Frameworks
    * Don't worry about React
    * Check out [Vega](https://vega.github.io/vega/)

## AMA
* Jobs
* D3 Methods
* Trends in the Field


## Keep in touch!
 * p.buffa@gmail.com
 * twitter.com/pstuffa
 * www.linkedin.com/in/paul-buffa/



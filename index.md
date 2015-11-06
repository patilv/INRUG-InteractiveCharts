---
title: "Using JavaScript Visualization libraries from R: rCharts and htmlwidgets"
author: "Vivek H. Patil"
date: "October 28, 2015"
output:
  ioslides_presentation:
    smaller: yes
    theme: spacelab
    widescreen: yes
---


<style>
.title-slide hgroup h1 {color: red;}
h2 {color: red;}
slides > slide:not(.nobackground):after {
  content: '';
}
</style>

## htmlwidgets and rCharts

* `htmlwidgets`: Ramnath Vaidyanathan, Kenton Russell, and RStudio
* `rCharts` (a transition to 2.0 using `htmlwidgets` is underway): Ramnath Vaidyanathan

* Provide the ability, from within R, to create, customize and publish interactive JavaScript (JS) visualizations
* JS is a computer programming language that can create interactivity using web browsers
* There are many pre-written JS libraries that make the process of creating visualizations easier. 


```r
install.packages("htmlwidgets")
devtools::install_github("ramnathv/rCharts")
```

## Challenge in learning

* Different JS libraries developed independently - consistency in calls can at times be a challenge
* Customization for specific needs may require writing JS code

### Learning approach

* Follow examples, questions, and issues presented in different venues
* Stick to few JS libraries which provide many choices of charts and become very familiar with them. Don't forget that few have restrictions for commercial use.


## Few Resources

* `htmlwidgets`
  * [htmlwidgets' site](http://www.htmlwidgets.org/index.html)
  * [Timelyportfolio's challenge - A widget a week](http://www.buildingwidgets.com/)
  * [Ryan Hafen's gallery of htmlwidgets developed by different people](http://hafen.github.io/htmlwidgetsgallery/)
  * [Search GitHub](http://www.github.com) for `htmlwidgets`
* `rCharts` 
    * [rCharts' website](http://rcharts.io/) and its [gallery of submissions from different people](http://rcharts.io/gallery/).
    * [rCharts on GitHub and the issues posted there](https://github.com/ramnathv/rCharts) and on [stackoverflow](http://stackoverflow.com/search?q=rCharts)
    * [A work-in-progress documentation](http://timelyportfolio.github.io/docs/_build/html/)
    * [rCharts-related posts from different bloggers via R-bloggers](http://www.r-bloggers.com/?s=rCharts)


## A sampling of the several htmlwidget packages 
|   |   |
|---|---|
| Interactive tables | [DT](https://rstudio.github.io/DT/), [formattable](http://renkun.me/formattable/), [rpivotTable](https://github.com/smartinsightsfromdata/rpivotTable),  [rhandsontable](http://jrowen.github.io/rhandsontable/), [D3TableFilter](https://github.com/ThomasSiegmund/D3TableFilter),  [sortableR](https://github.com/timelyportfolio/sortableR) |
| Heatmaps  | [d3heatmap](https://github.com/rstudio/d3heatmap)|
|Dimple|[rcdimple](https://github.com/timelyportfolio/rcdimple)|
| Tau Charts|[taucharts](https://github.com/hrbrmstr/taucharts)|
|Metrics Graphics|[metricsgraphics](http://hrbrmstr.github.io/metricsgraphics/)|
| Bokeh | [rbokeh](http://hafen.github.io/rbokeh/)|

## Few more sample packages 
|   |   |
|---|---|
|streamgraph|[streamgraph](http://hrbrmstr.github.io/streamgraph/)|
|Scatterplot matrices|[pairsD3](https://github.com/garthtarr/pairsD3), [scatterMatrixD3](https://github.com/jcizel/scatterMatrixD3)|
|Pan and Zoom graphs|[svgPanZoom](https://github.com/timelyportfolio/svgPanZoom)|
|Parallel Coordinate Charts|[parcoords](https://github.com/timelyportfolio/parcoords)|
|Sequences Sunburst|[sunburstR](http://www.buildingwidgets.com/blog/2015/7/2/week-26-sunburstr)|

## `rCharts`

|Code examples for different libraries for rCharts (Dropped those that have htmlwidgets now)   |   |
|---|---|
|[nvd3](https://github.com/ramnathv/rCharts/blob/master/inst/libraries/nvd3/examples.R)  |
[polychart](https://github.com/ramnathv/rCharts/blob/master/inst/libraries/polycharts/examples.R)    |
[rickshaw](https://github.com/ramnathv/rCharts/blob/master/inst/libraries/rickshaw/examples.R)  |
| [highcharts](https://github.com/ramnathv/rCharts/blob/master/inst/libraries/highcharts/examples.R)  | [timeline](https://github.com/ramnathv/rCharts/blob/master/inst/libraries/timeline/examples.R)  |
| [morris](https://github.com/ramnathv/rCharts/blob/master/inst/libraries/morris/examples.R)  | [uvcharts](http://imaginea.github.io/uvCharts/)  |
 [xcharts](https://github.com/ramnathv/rCharts/blob/master/inst/libraries/xcharts/examples.R)   |


## Example 1: Interactive table


```r
if (!require("DT")) install.packages('DT')
```

```
## Loading required package: DT
```

```r
library(DT)
datatable(iris)
```

<!--html_preserve--><div id="htmlwidget-4070" style="width:100%;height:auto;" class="datatables"></div>
<script type="application/json" data-for="htmlwidget-4070">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60","61","62","63","64","65","66","67","68","69","70","71","72","73","74","75","76","77","78","79","80","81","82","83","84","85","86","87","88","89","90","91","92","93","94","95","96","97","98","99","100","101","102","103","104","105","106","107","108","109","110","111","112","113","114","115","116","117","118","119","120","121","122","123","124","125","126","127","128","129","130","131","132","133","134","135","136","137","138","139","140","141","142","143","144","145","146","147","148","149","150"],[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5,7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7,6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],[3.5,3,3.2,3.1,3.6,3.9,3.4,3.4,2.9,3.1,3.7,3.4,3,3,4,4.4,3.9,3.5,3.8,3.8,3.4,3.7,3.6,3.3,3.4,3,3.4,3.5,3.4,3.2,3.1,3.4,4.1,4.2,3.1,3.2,3.5,3.6,3,3.4,3.5,2.3,3.2,3.5,3.8,3,3.8,3.2,3.7,3.3,3.2,3.2,3.1,2.3,2.8,2.8,3.3,2.4,2.9,2.7,2,3,2.2,2.9,2.9,3.1,3,2.7,2.2,2.5,3.2,2.8,2.5,2.8,2.9,3,2.8,3,2.9,2.6,2.4,2.4,2.7,2.7,3,3.4,3.1,2.3,3,2.5,2.6,3,2.6,2.3,2.7,3,2.9,2.9,2.5,2.8,3.3,2.7,3,2.9,3,3,2.5,2.9,2.5,3.6,3.2,2.7,3,2.5,2.8,3.2,3,3.8,2.6,2.2,3.2,2.8,2.8,2.7,3.3,3.2,2.8,3,2.8,3,2.8,3.8,2.8,2.8,2.6,3,3.4,3.1,3,3.1,3.1,3.1,2.7,3.2,3.3,3,2.5,3,3.4,3],[1.4,1.4,1.3,1.5,1.4,1.7,1.4,1.5,1.4,1.5,1.5,1.6,1.4,1.1,1.2,1.5,1.3,1.4,1.7,1.5,1.7,1.5,1,1.7,1.9,1.6,1.6,1.5,1.4,1.6,1.6,1.5,1.5,1.4,1.5,1.2,1.3,1.4,1.3,1.5,1.3,1.3,1.3,1.6,1.9,1.4,1.6,1.4,1.5,1.4,4.7,4.5,4.9,4,4.6,4.5,4.7,3.3,4.6,3.9,3.5,4.2,4,4.7,3.6,4.4,4.5,4.1,4.5,3.9,4.8,4,4.9,4.7,4.3,4.4,4.8,5,4.5,3.5,3.8,3.7,3.9,5.1,4.5,4.5,4.7,4.4,4.1,4,4.4,4.6,4,3.3,4.2,4.2,4.2,4.3,3,4.1,6,5.1,5.9,5.6,5.8,6.6,4.5,6.3,5.8,6.1,5.1,5.3,5.5,5,5.1,5.3,5.5,6.7,6.9,5,5.7,4.9,6.7,4.9,5.7,6,4.8,4.9,5.6,5.8,6.1,6.4,5.6,5.1,5.6,6.1,5.6,5.5,4.8,5.4,5.6,5.1,5.1,5.9,5.7,5.2,5,5.2,5.4,5.1],[0.2,0.2,0.2,0.2,0.2,0.4,0.3,0.2,0.2,0.1,0.2,0.2,0.1,0.1,0.2,0.4,0.4,0.3,0.3,0.3,0.2,0.4,0.2,0.5,0.2,0.2,0.4,0.2,0.2,0.2,0.2,0.4,0.1,0.2,0.2,0.2,0.2,0.1,0.2,0.2,0.3,0.3,0.2,0.6,0.4,0.3,0.2,0.2,0.2,0.2,1.4,1.5,1.5,1.3,1.5,1.3,1.6,1,1.3,1.4,1,1.5,1,1.4,1.3,1.4,1.5,1,1.5,1.1,1.8,1.3,1.5,1.2,1.3,1.4,1.4,1.7,1.5,1,1.1,1,1.2,1.6,1.5,1.6,1.5,1.3,1.3,1.3,1.2,1.4,1.2,1,1.3,1.2,1.3,1.3,1.1,1.3,2.5,1.9,2.1,1.8,2.2,2.1,1.7,1.8,1.8,2.5,2,1.9,2.1,2,2.4,2.3,1.8,2.2,2.3,1.5,2.3,2,2,1.8,2.1,1.8,1.8,1.8,2.1,1.6,1.9,2,2.2,1.5,1.4,2.3,2.4,1.8,1.8,2.1,2.4,2.3,1.9,2.3,2.5,2.3,1.9,2,2.3,1.8],["setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica"]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> </th>\n      <th>Sepal.Length</th>\n      <th>Sepal.Width</th>\n      <th>Petal.Length</th>\n      <th>Petal.Width</th>\n      <th>Species</th>\n    </tr>\n  </thead>\n</table>","options":{"columnDefs":[{"className":"dt-right","targets":[1,2,3,4]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[]}</script><!--/html_preserve-->

## Example 2: Interactive table


```r
if (!require("formattable")) devtools::install_github("renkun-ken/formattable")
```

```
## Loading required package: formattable
```

```r
library(formattable)
formattable(head(iris), list(
  Sepal.Length = color_tile("lightyellow", "orange"),
  Sepal.Width=color_bar("pink", 0.2)
))
```


|                                                                                           Sepal.Length|                                                                                                             Sepal.Width| Petal.Length| Petal.Width| Species|
|------------------------------------------------------------------------------------------------------:|-----------------------------------------------------------------------------------------------------------------------:|------------:|-----------:|-------:|
| <span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #ffc654">5.1</span>|  <span style="display: block; width: 64.44%; border-radius: 4px; padding-right: 4px; background-color: pink">3.5</span>|          1.4|         0.2|  setosa|
| <span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #ffdd8b">4.9</span>|    <span style="display: block; width: 20.00%; border-radius: 4px; padding-right: 4px; background-color: pink">3</span>|          1.4|         0.2|  setosa|
| <span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #fff3c3">4.7</span>|  <span style="display: block; width: 37.78%; border-radius: 4px; padding-right: 4px; background-color: pink">3.2</span>|          1.3|         0.2|  setosa|
| <span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #ffffe0">4.6</span>|  <span style="display: block; width: 28.89%; border-radius: 4px; padding-right: 4px; background-color: pink">3.1</span>|          1.5|         0.2|  setosa|
|   <span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #ffd270">5</span>|  <span style="display: block; width: 73.33%; border-radius: 4px; padding-right: 4px; background-color: pink">3.6</span>|          1.4|         0.2|  setosa|
| <span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #ffa500">5.4</span>| <span style="display: block; width: 100.00%; border-radius: 4px; padding-right: 4px; background-color: pink">3.9</span>|          1.7|         0.4|  setosa|

## Example 3: Heatmap


```r
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```

## Example 3 continued: Heatmap


```r
if (!require("d3heatmap")) devtools::install_github("rstudio/d3heatmap")
```

```
## Loading required package: d3heatmap
```

```r
library(d3heatmap)
d3heatmap(mtcars,scale="column")
```

<!--html_preserve--><div id="htmlwidget-9811" style="width:504px;height:504px;" class="d3heatmap"></div>
<script type="application/json" data-for="htmlwidget-9811">{"x":{"rows":{"members":32,"height":425.344651694364,"edgePar":{"col":""},"children":[{"members":23,"height":261.849881468371,"edgePar":{"col":""},"children":[{"members":16,"height":141.704447795403,"edgePar":{"col":""},"children":[{"members":12,"height":113.302300506212,"edgePar":{"col":""},"children":[{"members":11,"height":74.3824295717746,"edgePar":{"col":""},"children":[{"members":6,"height":50.1094029998363,"edgePar":{"col":""},"children":[{"members":5,"height":33.180384265406,"edgePar":{"col":""},"children":[{"members":4,"height":20.6939435584424,"edgePar":{"col":""},"children":[{"members":3,"height":13.1357108677072,"edgePar":{"col":""},"children":[{"members":2,"height":8.65359029536296,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Toyota Corona","edgePar":{"col":""}},{"members":1,"height":0,"label":"Porsche 914-2","edgePar":{"col":""}}]},{"members":1,"height":0,"label":"Datsun 710","edgePar":{"col":""}}]},{"members":1,"height":0,"label":"Volvo 142E","edgePar":{"col":""}}]},{"members":1,"height":0,"label":"Merc 230","edgePar":{"col":""}}]},{"members":1,"height":0,"label":"Lotus Europa","edgePar":{"col":""}}]},{"members":5,"height":64.889871320569,"edgePar":{"col":""},"children":[{"members":4,"height":15.6724726830197,"edgePar":{"col":""},"children":[{"members":2,"height":1.52315462117278,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Merc 280","edgePar":{"col":""}},{"members":1,"height":0,"label":"Merc 280C","edgePar":{"col":""}}]},{"members":2,"height":0.61532511731604,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Mazda RX4 Wag","edgePar":{"col":""}},{"members":1,"height":0,"label":"Mazda RX4","edgePar":{"col":""}}]}]},{"members":1,"height":0,"label":"Merc 240D","edgePar":{"col":""}}]}]},{"members":1,"height":0,"label":"Ferrari Dino","edgePar":{"col":""}}]},{"members":4,"height":14.7807070196253,"edgePar":{"col":""},"children":[{"members":3,"height":10.3922856003865,"edgePar":{"col":""},"children":[{"members":2,"height":5.14734154685698,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Fiat 128","edgePar":{"col":""}},{"members":1,"height":0,"label":"Fiat X1-9","edgePar":{"col":""}}]},{"members":1,"height":0,"label":"Toyota Corolla","edgePar":{"col":""}}]},{"members":1,"height":0,"label":"Honda Civic","edgePar":{"col":""}}]}]},{"members":7,"height":103.431069316719,"edgePar":{"col":""},"children":[{"members":5,"height":51.8242520447715,"edgePar":{"col":""},"children":[{"members":3,"height":2.13834047803431,"edgePar":{"col":""},"children":[{"members":2,"height":0.982649479723062,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Merc 450SL","edgePar":{"col":""}},{"members":1,"height":0,"label":"Merc 450SE","edgePar":{"col":""}}]},{"members":1,"height":0,"label":"Merc 450SLC","edgePar":{"col":""}}]},{"members":2,"height":14.0154994559595,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Dodge Challenger","edgePar":{"col":""}},{"members":1,"height":0,"label":"AMC Javelin","edgePar":{"col":""}}]}]},{"members":2,"height":33.5508692137775,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Hornet 4 Drive","edgePar":{"col":""}},{"members":1,"height":0,"label":"Valiant","edgePar":{"col":""}}]}]}]},{"members":9,"height":214.936685793747,"edgePar":{"col":""},"children":[{"members":8,"height":134.811946429091,"edgePar":{"col":""},"children":[{"members":5,"height":101.738968566622,"edgePar":{"col":""},"children":[{"members":3,"height":21.2655989805131,"edgePar":{"col":""},"children":[{"members":2,"height":10.0761202851097,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Duster 360","edgePar":{"col":""}},{"members":1,"height":0,"label":"Camaro Z28","edgePar":{"col":""}}]},{"members":1,"height":0,"label":"Ford Pantera L","edgePar":{"col":""}}]},{"members":2,"height":40.005247468301,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Pontiac Firebird","edgePar":{"col":""}},{"members":1,"height":0,"label":"Hornet Sportabout","edgePar":{"col":""}}]}]},{"members":3,"height":40.8399635773589,"edgePar":{"col":""},"children":[{"members":2,"height":15.6224446230416,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"Cadillac Fleetwood","edgePar":{"col":""}},{"members":1,"height":0,"label":"Lincoln Continental","edgePar":{"col":""}}]},{"members":1,"height":0,"label":"Chrysler Imperial","edgePar":{"col":""}}]}]},{"members":1,"height":0,"label":"Maserati Bora","edgePar":{"col":""}}]}]},"cols":{"members":11,"height":1475.10429122825,"edgePar":{"col":""},"children":[{"members":9,"height":115.849514457334,"edgePar":{"col":""},"children":[{"members":7,"height":34.7850542618522,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"cyl","edgePar":{"col":""}},{"members":6,"height":18.9208879284245,"edgePar":{"col":""},"children":[{"members":2,"height":3.60555127546399,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"am","edgePar":{"col":""}},{"members":1,"height":0,"label":"vs","edgePar":{"col":""}}]},{"members":4,"height":10.6897474245185,"edgePar":{"col":""},"children":[{"members":2,"height":8.59634050046879,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"carb","edgePar":{"col":""}},{"members":1,"height":0,"label":"wt","edgePar":{"col":""}}]},{"members":2,"height":2.98172768709686,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"drat","edgePar":{"col":""}},{"members":1,"height":0,"label":"gear","edgePar":{"col":""}}]}]}]}]},{"members":2,"height":33.2610913831762,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"qsec","edgePar":{"col":""}},{"members":1,"height":0,"label":"mpg","edgePar":{"col":""}}]}]},{"members":2,"height":656.640441946732,"edgePar":{"col":""},"children":[{"members":1,"height":0,"label":"hp","edgePar":{"col":""}},{"members":1,"height":0,"label":"disp","edgePar":{"col":""}}]}]},"matrix":{"data":["4","0","1","1","2.465","3.7","3","20.01","21.5","97","120.1","4","1","0","2","2.14","4.43","5","16.7","26","91","120.3","4","1","1","1","2.32","3.85","4","18.61","22.8","93","108","4","1","1","2","2.78","4.11","4","18.6","21.4","109","121","4","0","1","2","3.15","3.92","4","22.9","22.8","95","140.8","4","1","1","2","1.513","3.77","5","16.9","30.4","113","95.1","6","0","1","4","3.44","3.92","4","18.3","19.2","123","167.6","6","0","1","4","3.44","3.92","4","18.9","17.8","123","167.6","6","1","0","4","2.875","3.9","4","17.02","21","110","160","6","1","0","4","2.62","3.9","4","16.46","21","110","160","4","0","1","2","3.19","3.69","4","20","24.4","62","146.7","6","1","0","6","2.77","3.62","5","15.5","19.7","175","145","4","1","1","1","2.2","4.08","4","19.47","32.4","66","78.7","4","1","1","1","1.935","4.08","4","18.9","27.3","66","79","4","1","1","1","1.835","4.22","4","19.9","33.9","65","71.1","4","1","1","2","1.615","4.93","4","18.52","30.4","52","75.7","8","0","0","3","3.73","3.07","3","17.6","17.3","180","275.8","8","0","0","3","4.07","3.07","3","17.4","16.4","180","275.8","8","0","0","3","3.78","3.07","3","18","15.2","180","275.8","8","0","0","2","3.52","2.76","3","16.87","15.5","150","318","8","0","0","2","3.435","3.15","3","17.3","15.2","150","304","6","0","1","1","3.215","3.08","3","19.44","21.4","110","258","6","0","1","1","3.46","2.76","3","20.22","18.1","105","225","8","0","0","4","3.57","3.21","3","15.84","14.3","245","360","8","0","0","4","3.84","3.73","3","15.41","13.3","245","350","8","1","0","4","3.17","4.22","5","14.5","15.8","264","351","8","0","0","2","3.845","3.08","3","17.05","19.2","175","400","8","0","0","2","3.44","3.15","3","17.02","18.7","175","360","8","0","0","4","5.25","2.93","3","17.98","10.4","205","472","8","0","0","4","5.424","3","3","17.82","10.4","215","460","8","0","0","4","5.345","3.23","3","17.42","14.7","230","440","8","1","0","8","3.57","3.54","5","14.6","15","335","301"],"dim":[32,11],"rows":["Toyota Corona","Porsche 914-2","Datsun 710","Volvo 142E","Merc 230","Lotus Europa","Merc 280","Merc 280C","Mazda RX4 Wag","Mazda RX4","Merc 240D","Ferrari Dino","Fiat 128","Fiat X1-9","Toyota Corolla","Honda Civic","Merc 450SL","Merc 450SE","Merc 450SLC","Dodge Challenger","AMC Javelin","Hornet 4 Drive","Valiant","Duster 360","Camaro Z28","Ford Pantera L","Pontiac Firebird","Hornet Sportabout","Cadillac Fleetwood","Lincoln Continental","Chrysler Imperial","Maserati Bora"],"cols":["cyl","am","vs","carb","wt","drat","gear","qsec","mpg","hp","disp"]},"image":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAALCAYAAAAeEY8BAAAEFElEQVQ4jXXTf0zUdRzH8efne9+7487jjuNAjB8K/uCAGkNl5RBrLiVLaqX/WGvLPzKbM/uxippZlrPF1lois6lzjen6MbRyOibiciVITiBKxR3k8fOEAzm444K7477fT380r1j2/2Pvvfd6vd9CO7NNityFNCXvYH3PXsjKJLrsccy/1nMm9TXWLfJj6W1ATIXRbw/TUPQxlaFaWJCFvHGdQ9bXGQ9G2FPYyGXjVsoCBxGx2YQ1GRTW9+xFpDgYvf8VDCIOgETB5f0Sobe8LWVgIoErzKdAUWnVNpPvDANgVQMk+ZsR/mH028PcXbjCfArScxmMrMZqmGTztkucPPoIrr46MChIT8+cuZEjp4m9c4DPf5xlT/FPVN9ci5DDR6Xsuo5YswHpaaMpeQe5DgvZNi/j0TyshkmSDEHm6V6YDkEkDGk5/2tnNDvZ0R9AGBL27GAplaFaunOryJff4zNVkmQI4wqdQ4mlr4CCQqTfi3CXEtN08vuqGQovJjtwjIhmI6I5kN7fidndSKkj/V5k3wDrpw7RF5zBeucyOdZfsBlHsRhCnJnYQI/yNHrbVeRgF5U5bZy17yS/r5o3morI+vMkTrOXjzrKEFr9Vqk88xyB2SKcvm+QNz1zusNkot39AXmOKXqDydQ1dVPjOobU/u7y31YGp+goryHPMcWMZqfTH2Gj5/17Wn04QGP5AcSdGZ+8OmLm+Hc3OFHwNTIaBaM6p7vYiQY2TW6n7r1iFBHncHOEt/z7EDYzLSs/pXyiFhGPM1u8kfHIUjI6q8GoIorLIDjCaPKTmJRprt1xzLHXxgsRekuVxKgiClcgAz7G0rfcE4/OFJD5234wqugrK1G6LjC2ZPt/LAuymEpdS9KRd1EfckNWNoQmke5yvKFShsOROVaJPPg8wmxG3uxAOOaTfuswdtMgeSlGhLsUqapcHFxCZutuRNkG0DSU9rN0zH+VZKMfx/g5SjOGEvZ8dDO2n2uIbf+Q+BUP+Ib4Vm5FCQ6xJHSUNfe10+zciVRVGPEhPBPTcr7Fj2OgHiaDEAyBzUZd0g5y02wYBImNu3OrMKuCNLMXa+dX6H8MoKQ5qEuvwp1hJ67rBKPxfy7e3kJD/3LaPGO8eWEXlpcrqO5/ioeLMtB0SflELYaDW9S9SeoYA66XcPgvgsWCyFtKSXYYu9VF+22NoHM1C2NtpAUukWLqJT4vB9NED8JhQ7iLKFkQYJ41nZFpExZVSdhuy7McP+/hE1MtxlVu9AceZdXpfUwu30R9cy/WZRUod6OIxnVeuPIEBEPI/ltgsmL7YheLUq00dvjmxDYUXsyLl9eBKxXZ7wUpSe06TCgap9UzRrNzZ+LtWg9dJfTYbkRJOfsbnWhj05T4PqOjsYfFKQp/ARJ3A/QME5f5AAAAAElFTkSuQmCC","theme":null,"options":{"xaxis_height":80,"yaxis_width":120,"xaxis_font_size":null,"yaxis_font_size":null,"brush_color":"#0000FF","show_grid":true,"anim_duration":500}},"evals":[]}</script><!--/html_preserve-->

## Example 4: `rcdimple`: Many graph types available


```r
if (!require("rcdimple")) devtools::install_github("timelyportfolio/rcdimple")
```

```
## Loading required package: rcdimple
## Loading required package: htmlwidgets
## Loading required package: htmltools
```

```r
library(rcdimple) # demo(dimple) for tons of examples
iris%>% dimple(x = "Sepal.Length",
  y = "Sepal.Width",
  groups = "Species",
  type = "bubble")%>% yAxis( overrideMin = 2)%>%
  add_legend()
```

<!--html_preserve--><div id="htmlwidget-2629" style="width:504px;height:504px;" class="dimple"></div>
<script type="application/json" data-for="htmlwidget-2629">{"x":{"options":{"chart":[],"xAxis":{"type":"addCategoryAxis"},"yAxis":{"type":"addMeasureAxis","overrideMin":2},"zAxis":[],"colorAxis":[],"defaultColors":[],"layers":[],"legend":{"x":"45%","y":"0","width":"45%","height":"10%","horizontalAlign":"right"},"x":"Sepal.Length","y":"Sepal.Width","type":"bubble","groups":"Species"},"data":{"Sepal.Length":[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5,7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7,6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],"Sepal.Width":[3.5,3,3.2,3.1,3.6,3.9,3.4,3.4,2.9,3.1,3.7,3.4,3,3,4,4.4,3.9,3.5,3.8,3.8,3.4,3.7,3.6,3.3,3.4,3,3.4,3.5,3.4,3.2,3.1,3.4,4.1,4.2,3.1,3.2,3.5,3.6,3,3.4,3.5,2.3,3.2,3.5,3.8,3,3.8,3.2,3.7,3.3,3.2,3.2,3.1,2.3,2.8,2.8,3.3,2.4,2.9,2.7,2,3,2.2,2.9,2.9,3.1,3,2.7,2.2,2.5,3.2,2.8,2.5,2.8,2.9,3,2.8,3,2.9,2.6,2.4,2.4,2.7,2.7,3,3.4,3.1,2.3,3,2.5,2.6,3,2.6,2.3,2.7,3,2.9,2.9,2.5,2.8,3.3,2.7,3,2.9,3,3,2.5,2.9,2.5,3.6,3.2,2.7,3,2.5,2.8,3.2,3,3.8,2.6,2.2,3.2,2.8,2.8,2.7,3.3,3.2,2.8,3,2.8,3,2.8,3.8,2.8,2.8,2.6,3,3.4,3.1,3,3.1,3.1,3.1,2.7,3.2,3.3,3,2.5,3,3.4,3],"Petal.Length":[1.4,1.4,1.3,1.5,1.4,1.7,1.4,1.5,1.4,1.5,1.5,1.6,1.4,1.1,1.2,1.5,1.3,1.4,1.7,1.5,1.7,1.5,1,1.7,1.9,1.6,1.6,1.5,1.4,1.6,1.6,1.5,1.5,1.4,1.5,1.2,1.3,1.4,1.3,1.5,1.3,1.3,1.3,1.6,1.9,1.4,1.6,1.4,1.5,1.4,4.7,4.5,4.9,4,4.6,4.5,4.7,3.3,4.6,3.9,3.5,4.2,4,4.7,3.6,4.4,4.5,4.1,4.5,3.9,4.8,4,4.9,4.7,4.3,4.4,4.8,5,4.5,3.5,3.8,3.7,3.9,5.1,4.5,4.5,4.7,4.4,4.1,4,4.4,4.6,4,3.3,4.2,4.2,4.2,4.3,3,4.1,6,5.1,5.9,5.6,5.8,6.6,4.5,6.3,5.8,6.1,5.1,5.3,5.5,5,5.1,5.3,5.5,6.7,6.9,5,5.7,4.9,6.7,4.9,5.7,6,4.8,4.9,5.6,5.8,6.1,6.4,5.6,5.1,5.6,6.1,5.6,5.5,4.8,5.4,5.6,5.1,5.1,5.9,5.7,5.2,5,5.2,5.4,5.1],"Petal.Width":[0.2,0.2,0.2,0.2,0.2,0.4,0.3,0.2,0.2,0.1,0.2,0.2,0.1,0.1,0.2,0.4,0.4,0.3,0.3,0.3,0.2,0.4,0.2,0.5,0.2,0.2,0.4,0.2,0.2,0.2,0.2,0.4,0.1,0.2,0.2,0.2,0.2,0.1,0.2,0.2,0.3,0.3,0.2,0.6,0.4,0.3,0.2,0.2,0.2,0.2,1.4,1.5,1.5,1.3,1.5,1.3,1.6,1,1.3,1.4,1,1.5,1,1.4,1.3,1.4,1.5,1,1.5,1.1,1.8,1.3,1.5,1.2,1.3,1.4,1.4,1.7,1.5,1,1.1,1,1.2,1.6,1.5,1.6,1.5,1.3,1.3,1.3,1.2,1.4,1.2,1,1.3,1.2,1.3,1.3,1.1,1.3,2.5,1.9,2.1,1.8,2.2,2.1,1.7,1.8,1.8,2.5,2,1.9,2.1,2,2.4,2.3,1.8,2.2,2.3,1.5,2.3,2,2,1.8,2.1,1.8,1.8,1.8,2.1,1.6,1.9,2,2.2,1.5,1.4,2.3,2.4,1.8,1.8,2.1,2.4,2.3,1.9,2.3,2.5,2.3,1.9,2,2.3,1.8],"Species":["setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica"]}},"evals":[]}</script><!--/html_preserve-->


## Example 4A grouped bar: `rcdimple`: Many graph types available


```r
gearam=mtcars%>%group_by(gear,am)%>%summarise(count=length(gear))
```

```
## Error in function_list[[i]](value): could not find function "group_by"
```

```r
gearam$am<-ifelse(gearam$am==0,yes= "Auto",no= "Manual")
```

```
## Error in ifelse(gearam$am == 0, yes = "Auto", no = "Manual"): object 'gearam' not found
```

```r
gearam%>%dimple(
    x = c("gear","am"), y = "count",
    groups = "am", type = "bar")%>%
   add_legend()
```

```
## Error in eval(expr, envir, enclos): object 'gearam' not found
```



# Example 5: `taucharts`: Many graph types
[https://github.com/hrbrmstr/taucharts](https://github.com/hrbrmstr/taucharts)

```r
if (!require("taucharts")) devtools::install_github("hrbrmstr/taucharts")
```

```
## Loading required package: taucharts
```

```
## Warning in library(package, lib.loc = lib.loc, character.only = TRUE,
## logical.return = TRUE, : there is no package called 'taucharts'
```

```
## Downloading GitHub repo hrbrmstr/taucharts@master
## Installing taucharts
## Installing 1 packages: stringi
```

```
## package 'stringi' successfully unpacked and MD5 sums checked
```

```
## Warning: cannot remove prior installation of package 'stringi'
```

```
## "C:/PROGRA~1/R/R-32~1.2/bin/x64/R" --no-site-file --no-environ --no-save  \
##   --no-restore CMD INSTALL  \
##   "C:/Users/p/AppData/Local/Temp/RtmpCkmmKZ/devtools237858f97a38/hrbrmstr-taucharts-2cc90a4"  \
##   --library="C:/Users/p/Documents/R/win-library/3.2" --install-tests
```

```r
library(taucharts)
iris %>% tauchart()%>% 
  tau_point(x="Sepal.Length",y="Sepal.Width",color="Species")%>%
  tau_tooltip(c("Sepal.Length", "Sepal.Width", "Species"))%>% tau_legend()
```

<!--html_preserve--><div id="tau-c83892102d53e5733e923410a4bd58" style="width:504px;height:504px;" class="taucharts"></div>
<script type="application/json" data-for="tau-c83892102d53e5733e923410a4bd58">{"x":{"datasource":{"Sepal.Length":[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5,7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7,6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],"Sepal.Width":[3.5,3,3.2,3.1,3.6,3.9,3.4,3.4,2.9,3.1,3.7,3.4,3,3,4,4.4,3.9,3.5,3.8,3.8,3.4,3.7,3.6,3.3,3.4,3,3.4,3.5,3.4,3.2,3.1,3.4,4.1,4.2,3.1,3.2,3.5,3.6,3,3.4,3.5,2.3,3.2,3.5,3.8,3,3.8,3.2,3.7,3.3,3.2,3.2,3.1,2.3,2.8,2.8,3.3,2.4,2.9,2.7,2,3,2.2,2.9,2.9,3.1,3,2.7,2.2,2.5,3.2,2.8,2.5,2.8,2.9,3,2.8,3,2.9,2.6,2.4,2.4,2.7,2.7,3,3.4,3.1,2.3,3,2.5,2.6,3,2.6,2.3,2.7,3,2.9,2.9,2.5,2.8,3.3,2.7,3,2.9,3,3,2.5,2.9,2.5,3.6,3.2,2.7,3,2.5,2.8,3.2,3,3.8,2.6,2.2,3.2,2.8,2.8,2.7,3.3,3.2,2.8,3,2.8,3,2.8,3.8,2.8,2.8,2.6,3,3.4,3.1,3,3.1,3.1,3.1,2.7,3.2,3.3,3,2.5,3,3.4,3],"Petal.Length":[1.4,1.4,1.3,1.5,1.4,1.7,1.4,1.5,1.4,1.5,1.5,1.6,1.4,1.1,1.2,1.5,1.3,1.4,1.7,1.5,1.7,1.5,1,1.7,1.9,1.6,1.6,1.5,1.4,1.6,1.6,1.5,1.5,1.4,1.5,1.2,1.3,1.4,1.3,1.5,1.3,1.3,1.3,1.6,1.9,1.4,1.6,1.4,1.5,1.4,4.7,4.5,4.9,4,4.6,4.5,4.7,3.3,4.6,3.9,3.5,4.2,4,4.7,3.6,4.4,4.5,4.1,4.5,3.9,4.8,4,4.9,4.7,4.3,4.4,4.8,5,4.5,3.5,3.8,3.7,3.9,5.1,4.5,4.5,4.7,4.4,4.1,4,4.4,4.6,4,3.3,4.2,4.2,4.2,4.3,3,4.1,6,5.1,5.9,5.6,5.8,6.6,4.5,6.3,5.8,6.1,5.1,5.3,5.5,5,5.1,5.3,5.5,6.7,6.9,5,5.7,4.9,6.7,4.9,5.7,6,4.8,4.9,5.6,5.8,6.1,6.4,5.6,5.1,5.6,6.1,5.6,5.5,4.8,5.4,5.6,5.1,5.1,5.9,5.7,5.2,5,5.2,5.4,5.1],"Petal.Width":[0.2,0.2,0.2,0.2,0.2,0.4,0.3,0.2,0.2,0.1,0.2,0.2,0.1,0.1,0.2,0.4,0.4,0.3,0.3,0.3,0.2,0.4,0.2,0.5,0.2,0.2,0.4,0.2,0.2,0.2,0.2,0.4,0.1,0.2,0.2,0.2,0.2,0.1,0.2,0.2,0.3,0.3,0.2,0.6,0.4,0.3,0.2,0.2,0.2,0.2,1.4,1.5,1.5,1.3,1.5,1.3,1.6,1,1.3,1.4,1,1.5,1,1.4,1.3,1.4,1.5,1,1.5,1.1,1.8,1.3,1.5,1.2,1.3,1.4,1.4,1.7,1.5,1,1.1,1,1.2,1.6,1.5,1.6,1.5,1.3,1.3,1.3,1.2,1.4,1.2,1,1.3,1.2,1.3,1.3,1.1,1.3,2.5,1.9,2.1,1.8,2.2,2.1,1.7,1.8,1.8,2.5,2,1.9,2.1,2,2.4,2.3,1.8,2.2,2.3,1.5,2.3,2,2,1.8,2.1,1.8,1.8,1.8,2.1,1.6,1.9,2,2.2,1.5,1.4,2.3,2.4,1.8,1.8,2.1,2.4,2.3,1.9,2.3,2.5,2.3,1.9,2,2.3,1.8],"Species":["setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica"]},"dimensions":{"Sepal.Length":{"type":"measure"},"Sepal.Width":{"type":"measure"},"Petal.Length":{"type":"measure"},"Petal.Width":{"type":"measure"},"Species":{"type":"category"}},"x":"Sepal.Length","y":"Sepal.Width","padding":null,"guide":{"x":null,"y":null,"padding":null,"color":null},"forCSS":null,"forFonts":"https://fonts.googleapis.com/css?family=Open+Sans:400italic,600italic,400,600&subset=latin,cyrillic-ext","color":"Species","type":"scatterplot","plugins":[{"type":"tooltip","fields":["Sepal.Length","Sepal.Width","Species"]},{"type":"legend"}]},"evals":[]}</script><!--/html_preserve-->

## Example 5A: `taucharts`: Many graph types


```r
gearam$gear=as.factor(gearam$gear)
```

```
## Error in is.factor(x): object 'gearam' not found
```

```r
tauchart(gearam)%>%tau_bar("gear","count","am")%>%
  tau_tooltip(c("gear", "am", "count"))%>% tau_legend()
```

```
## Error in inherits(data, "xts"): object 'gearam' not found
```

## Example 6: `metricsgraphics`: Many graph types available

Scatter and line plots (time-series data), grids/facets of graphs, and connected graphs


```r
if (!require("metricsgraphics")) devtools::install_github("hrbrmstr/metricsgraphics")
```

```
## Loading required package: metricsgraphics
```

```r
library(metricsgraphics)
iris %>% mjs_plot(x=Sepal.Length,y=Sepal.Width) %>%
  mjs_point(color_accessor=Species, color_type="category")%>%
    mjs_labs(x="Sepal.Length", y="Sepal.Width")%>% 
    mjs_axis_y(min_y=2)
```

<!--html_preserve--><div id="mjs-aea7563ecafde9c86e920ab7f893ab" class="metricsgraphics" style="width:504px;height:504px;"></div>
<div id="mjs-aea7563ecafde9c86e920ab7f893ab-legend" class="metricsgraphics-legend"></div>
<script type="application/json" data-for="mjs-aea7563ecafde9c86e920ab7f893ab">{"x":{"orig_posix":false,"data":{"Sepal.Length":[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5,7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7,6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],"Sepal.Width":[3.5,3,3.2,3.1,3.6,3.9,3.4,3.4,2.9,3.1,3.7,3.4,3,3,4,4.4,3.9,3.5,3.8,3.8,3.4,3.7,3.6,3.3,3.4,3,3.4,3.5,3.4,3.2,3.1,3.4,4.1,4.2,3.1,3.2,3.5,3.6,3,3.4,3.5,2.3,3.2,3.5,3.8,3,3.8,3.2,3.7,3.3,3.2,3.2,3.1,2.3,2.8,2.8,3.3,2.4,2.9,2.7,2,3,2.2,2.9,2.9,3.1,3,2.7,2.2,2.5,3.2,2.8,2.5,2.8,2.9,3,2.8,3,2.9,2.6,2.4,2.4,2.7,2.7,3,3.4,3.1,2.3,3,2.5,2.6,3,2.6,2.3,2.7,3,2.9,2.9,2.5,2.8,3.3,2.7,3,2.9,3,3,2.5,2.9,2.5,3.6,3.2,2.7,3,2.5,2.8,3.2,3,3.8,2.6,2.2,3.2,2.8,2.8,2.7,3.3,3.2,2.8,3,2.8,3,2.8,3.8,2.8,2.8,2.6,3,3.4,3.1,3,3.1,3.1,3.1,2.7,3.2,3.3,3,2.5,3,3.4,3],"Petal.Length":[1.4,1.4,1.3,1.5,1.4,1.7,1.4,1.5,1.4,1.5,1.5,1.6,1.4,1.1,1.2,1.5,1.3,1.4,1.7,1.5,1.7,1.5,1,1.7,1.9,1.6,1.6,1.5,1.4,1.6,1.6,1.5,1.5,1.4,1.5,1.2,1.3,1.4,1.3,1.5,1.3,1.3,1.3,1.6,1.9,1.4,1.6,1.4,1.5,1.4,4.7,4.5,4.9,4,4.6,4.5,4.7,3.3,4.6,3.9,3.5,4.2,4,4.7,3.6,4.4,4.5,4.1,4.5,3.9,4.8,4,4.9,4.7,4.3,4.4,4.8,5,4.5,3.5,3.8,3.7,3.9,5.1,4.5,4.5,4.7,4.4,4.1,4,4.4,4.6,4,3.3,4.2,4.2,4.2,4.3,3,4.1,6,5.1,5.9,5.6,5.8,6.6,4.5,6.3,5.8,6.1,5.1,5.3,5.5,5,5.1,5.3,5.5,6.7,6.9,5,5.7,4.9,6.7,4.9,5.7,6,4.8,4.9,5.6,5.8,6.1,6.4,5.6,5.1,5.6,6.1,5.6,5.5,4.8,5.4,5.6,5.1,5.1,5.9,5.7,5.2,5,5.2,5.4,5.1],"Petal.Width":[0.2,0.2,0.2,0.2,0.2,0.4,0.3,0.2,0.2,0.1,0.2,0.2,0.1,0.1,0.2,0.4,0.4,0.3,0.3,0.3,0.2,0.4,0.2,0.5,0.2,0.2,0.4,0.2,0.2,0.2,0.2,0.4,0.1,0.2,0.2,0.2,0.2,0.1,0.2,0.2,0.3,0.3,0.2,0.6,0.4,0.3,0.2,0.2,0.2,0.2,1.4,1.5,1.5,1.3,1.5,1.3,1.6,1,1.3,1.4,1,1.5,1,1.4,1.3,1.4,1.5,1,1.5,1.1,1.8,1.3,1.5,1.2,1.3,1.4,1.4,1.7,1.5,1,1.1,1,1.2,1.6,1.5,1.6,1.5,1.3,1.3,1.3,1.2,1.4,1.2,1,1.3,1.2,1.3,1.3,1.1,1.3,2.5,1.9,2.1,1.8,2.2,2.1,1.7,1.8,1.8,2.5,2,1.9,2.1,2,2.4,2.3,1.8,2.2,2.3,1.5,2.3,2,2,1.8,2.1,1.8,1.8,1.8,2.1,1.6,1.9,2,2.2,1.5,1.4,2.3,2.4,1.8,1.8,2.1,2.4,2.3,1.9,2.3,2.5,2.3,1.9,2,2.3,1.8],"Species":["setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica"]},"x_axis":true,"y_axis":true,"baseline_accessor":null,"predictor_accessor":null,"show_confidence_band":null,"show_secondary_x_label":null,"chart_type":"point","xax_format":"plain","x_label":"Sepal.Length","y_label":"Sepal.Width","markers":null,"baselines":null,"linked":false,"title":null,"description":null,"left":80,"right":10,"bottom":60,"buffer":8,"format":"count","y_scale_type":"linear","yax_count":5,"xax_count":6,"x_rug":false,"y_rug":false,"area":false,"missing_is_hidden":false,"size_accessor":null,"color_accessor":"Species","color_type":"category","color_range":["blue","red"],"size_range":[1,5],"bar_height":20,"min_x":null,"max_x":null,"min_y":2,"bar_margin":1,"binned":false,"bins":null,"least_squares":false,"interpolate":"cardinal","decimals":2,"show_rollover_text":true,"x_accessor":"Sepal.Length","y_accessor":"Sepal.Width","multi_line":null,"geom":"point","yax_units":"","legend":null,"legend_target":null,"y_extended_ticks":false,"x_extended_ticks":false,"target":"#mjs-aea7563ecafde9c86e920ab7f893ab","full_width":true,"full_height":true},"evals":[]}</script><!--/html_preserve-->


## Example 7: `rbokeh`: Many graph types available
[http://hafen.github.io/rbokeh/](http://hafen.github.io/rbokeh/): Bar missing

```r
if (!require("rbokeh")) devtools::install_github("bokeh/rbokeh")
```

```
## Loading required package: rbokeh
```

```
## Warning in library(package, lib.loc = lib.loc, character.only = TRUE,
## logical.return = TRUE, : there is no package called 'rbokeh'
```

```
## Downloading GitHub repo bokeh/rbokeh@master
## Installing rbokeh
## Installing 1 packages: maps
```

```
## package 'maps' successfully unpacked and MD5 sums checked
```

```
## "C:/PROGRA~1/R/R-32~1.2/bin/x64/R" --no-site-file --no-environ --no-save  \
##   --no-restore CMD INSTALL  \
##   "C:/Users/p/AppData/Local/Temp/RtmpCkmmKZ/devtools2378720568d6/bokeh-rbokeh-2bab3a6"  \
##   --library="C:/Users/p/Documents/R/win-library/3.2" --install-tests
```

```r
library(rbokeh)
figure() %>%
  ly_points(Sepal.Length, Sepal.Width, data = iris,
    color = Species,
    hover = list(Sepal.Length, Sepal.Width))
```

```
## xlim not specified explicitly... calculating...
## ylim not specified explicitly... calculating...
```

<!--html_preserve--><div id="htmlwidget-8616" style="width:480px;height:520px;" class="rbokeh"></div>
<script type="application/json" data-for="htmlwidget-8616">{"x":{"elementid":"b6d9f9240ac3f24a49b27332c1cea74b","modeltype":"Plot","modelid":"09a54cccfc70cb26c2bb27be07513fcb","padding":{"type":"figure","y_pad":10,"x_pad":46},"all_models":[{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","attributes":{"title":null,"id":"09a54cccfc70cb26c2bb27be07513fcb","plot_width":470,"plot_height":474,"x_range":{"type":"Range1d","id":"8efff71dd84cd1a3c507c3fa91766f00"},"y_range":{"type":"Range1d","id":"f3a7e027a5ac0097b225125493092e9e"},"left":[{"type":"LinearAxis","id":"c3b3da4f38dd8b9b3760c1be918ad95c"}],"below":[{"type":"LinearAxis","id":"6a3cae24519363c4439d8272a79813b2"}],"right":[],"above":[],"renderers":[{"type":"GlyphRenderer","id":"9b51801e271f030169915f705efeefaf"},{"type":"GlyphRenderer","id":"dc706f4fdaf37516472af80f1da03dfd"},{"type":"GlyphRenderer","id":"16bb55b3473ab8907c3e3cacd4c16dca"},{"type":"GlyphRenderer","id":"b132a0a4b1c64c053ae71b07efd0bd0a"},{"type":"Legend","id":"f2abc4ea683b3dad4ccec9a9e161a8bc"},{"type":"LinearAxis","id":"6a3cae24519363c4439d8272a79813b2"},{"type":"Grid","id":"86817f1699727eeace29f10cd3586e6e"},{"type":"LinearAxis","id":"c3b3da4f38dd8b9b3760c1be918ad95c"},{"type":"Grid","id":"3119553c69516e20e105afed96b7c831"}],"tools":[{"type":"PanTool","id":"bd89e4c771751aff02bb7ae323743e72"},{"type":"WheelZoomTool","id":"2a3d9b20cfb9385fc10ea77cca5e204c"},{"type":"BoxZoomTool","id":"0ce45075359d18622b2e8129346e8737"},{"type":"ResizeTool","id":"60acaecec07406353fe5f0669352577f"},{"type":"ResetTool","id":"a7d402d9a3bb7a517c29ba7f51256feb"},{"type":"PreviewSaveTool","id":"2f3b5ae32d999876740f8d2c1e2408ab"},{"type":"HoverTool","id":"3effe1fec30a54503fde621fc8a2e60f"}],"tool_events":{"type":"ToolEvents","id":"4a6a0db3bc666813371f7494376b85f2"},"extra_y_ranges":{},"extra_x_ranges":{},"tags":[],"doc":null,"min_border":4},"subtype":"Figure"},{"type":"PanTool","id":"bd89e4c771751aff02bb7ae323743e72","attributes":{"id":"bd89e4c771751aff02bb7ae323743e72","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"},"dimensions":["width","height"]}},{"type":"ToolEvents","id":"4a6a0db3bc666813371f7494376b85f2","attributes":{"id":"4a6a0db3bc666813371f7494376b85f2","tags":[],"doc":null},"geometries":[]},{"type":"WheelZoomTool","id":"2a3d9b20cfb9385fc10ea77cca5e204c","attributes":{"id":"2a3d9b20cfb9385fc10ea77cca5e204c","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"},"dimensions":["width","height"]}},{"type":"BoxZoomTool","id":"0ce45075359d18622b2e8129346e8737","attributes":{"id":"0ce45075359d18622b2e8129346e8737","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"}}},{"type":"ResizeTool","id":"60acaecec07406353fe5f0669352577f","attributes":{"id":"60acaecec07406353fe5f0669352577f","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"}}},{"type":"ResetTool","id":"a7d402d9a3bb7a517c29ba7f51256feb","attributes":{"id":"a7d402d9a3bb7a517c29ba7f51256feb","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"}}},{"type":"PreviewSaveTool","id":"2f3b5ae32d999876740f8d2c1e2408ab","attributes":{"id":"2f3b5ae32d999876740f8d2c1e2408ab","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"}}},{"type":"HoverTool","id":"3effe1fec30a54503fde621fc8a2e60f","attributes":{"id":"3effe1fec30a54503fde621fc8a2e60f","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"},"renderers":[{"type":"GlyphRenderer","id":"9b51801e271f030169915f705efeefaf"}],"names":[],"always_active":true,"tooltips":[["Sepal.Length","@hover_Sepal_Length"],["Sepal.Width","@hover_Sepal_Width"]]}},{"type":"ColumnDataSource","id":"217267a296855f08a9dcd6edc511036b","attributes":{"id":"217267a296855f08a9dcd6edc511036b","tags":[],"doc":null,"column_names":["x","y","line_color","fill_color","hover_Sepal_Length","hover_Sepal_Width"],"selected":[],"discrete_ranges":{},"cont_ranges":{},"data":{"x":[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5,7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7,6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],"y":[3.5,3,3.2,3.1,3.6,3.9,3.4,3.4,2.9,3.1,3.7,3.4,3,3,4,4.4,3.9,3.5,3.8,3.8,3.4,3.7,3.6,3.3,3.4,3,3.4,3.5,3.4,3.2,3.1,3.4,4.1,4.2,3.1,3.2,3.5,3.6,3,3.4,3.5,2.3,3.2,3.5,3.8,3,3.8,3.2,3.7,3.3,3.2,3.2,3.1,2.3,2.8,2.8,3.3,2.4,2.9,2.7,2,3,2.2,2.9,2.9,3.1,3,2.7,2.2,2.5,3.2,2.8,2.5,2.8,2.9,3,2.8,3,2.9,2.6,2.4,2.4,2.7,2.7,3,3.4,3.1,2.3,3,2.5,2.6,3,2.6,2.3,2.7,3,2.9,2.9,2.5,2.8,3.3,2.7,3,2.9,3,3,2.5,2.9,2.5,3.6,3.2,2.7,3,2.5,2.8,3.2,3,3.8,2.6,2.2,3.2,2.8,2.8,2.7,3.3,3.2,2.8,3,2.8,3,2.8,3.8,2.8,2.8,2.6,3,3.4,3.1,3,3.1,3.1,3.1,2.7,3.2,3.3,3,2.5,3,3.4,3],"line_color":["#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C"],"fill_color":["#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#1F77B4","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#FF7F0E","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C","#2CA02C"],"hover_Sepal_Length":["5.1","4.9","4.7","4.6","5.0","5.4","4.6","5.0","4.4","4.9","5.4","4.8","4.8","4.3","5.8","5.7","5.4","5.1","5.7","5.1","5.4","5.1","4.6","5.1","4.8","5.0","5.0","5.2","5.2","4.7","4.8","5.4","5.2","5.5","4.9","5.0","5.5","4.9","4.4","5.1","5.0","4.5","4.4","5.0","5.1","4.8","5.1","4.6","5.3","5.0","7.0","6.4","6.9","5.5","6.5","5.7","6.3","4.9","6.6","5.2","5.0","5.9","6.0","6.1","5.6","6.7","5.6","5.8","6.2","5.6","5.9","6.1","6.3","6.1","6.4","6.6","6.8","6.7","6.0","5.7","5.5","5.5","5.8","6.0","5.4","6.0","6.7","6.3","5.6","5.5","5.5","6.1","5.8","5.0","5.6","5.7","5.7","6.2","5.1","5.7","6.3","5.8","7.1","6.3","6.5","7.6","4.9","7.3","6.7","7.2","6.5","6.4","6.8","5.7","5.8","6.4","6.5","7.7","7.7","6.0","6.9","5.6","7.7","6.3","6.7","7.2","6.2","6.1","6.4","7.2","7.4","7.9","6.4","6.3","6.1","7.7","6.3","6.4","6.0","6.9","6.7","6.9","5.8","6.8","6.7","6.7","6.3","6.5","6.2","5.9"],"hover_Sepal_Width":["3.5","3.0","3.2","3.1","3.6","3.9","3.4","3.4","2.9","3.1","3.7","3.4","3.0","3.0","4.0","4.4","3.9","3.5","3.8","3.8","3.4","3.7","3.6","3.3","3.4","3.0","3.4","3.5","3.4","3.2","3.1","3.4","4.1","4.2","3.1","3.2","3.5","3.6","3.0","3.4","3.5","2.3","3.2","3.5","3.8","3.0","3.8","3.2","3.7","3.3","3.2","3.2","3.1","2.3","2.8","2.8","3.3","2.4","2.9","2.7","2.0","3.0","2.2","2.9","2.9","3.1","3.0","2.7","2.2","2.5","3.2","2.8","2.5","2.8","2.9","3.0","2.8","3.0","2.9","2.6","2.4","2.4","2.7","2.7","3.0","3.4","3.1","2.3","3.0","2.5","2.6","3.0","2.6","2.3","2.7","3.0","2.9","2.9","2.5","2.8","3.3","2.7","3.0","2.9","3.0","3.0","2.5","2.9","2.5","3.6","3.2","2.7","3.0","2.5","2.8","3.2","3.0","3.8","2.6","2.2","3.2","2.8","2.8","2.7","3.3","3.2","2.8","3.0","2.8","3.0","2.8","3.8","2.8","2.8","2.6","3.0","3.4","3.1","3.0","3.1","3.1","3.1","2.7","3.2","3.3","3.0","2.5","3.0","3.4","3.0"]}}},{"type":"Circle","id":"39bb18ea1e86b7f0fdd1680957501144","attributes":{"id":"39bb18ea1e86b7f0fdd1680957501144","tags":[],"doc":null,"size":{"units":"screen","value":10},"line_alpha":{"units":"data","value":1},"fill_alpha":{"units":"data","value":0.5},"x":{"units":"data","field":"x"},"y":{"units":"data","field":"y"},"line_color":{"units":"data","field":"line_color"},"fill_color":{"units":"data","field":"fill_color"}}},{"type":"Circle","id":"6801305b9a7ab20f92cb27667dee554f","attributes":{"id":"6801305b9a7ab20f92cb27667dee554f","tags":[],"doc":null,"size":{"units":"screen","value":10},"line_alpha":{"units":"data","value":1},"fill_alpha":{"units":"data","value":0.5},"x":{"units":"data","field":"x"},"y":{"units":"data","field":"y"},"line_color":{"units":"data","value":"#e1e1e1"},"fill_color":{"units":"data","value":"#e1e1e1"}}},{"type":"GlyphRenderer","id":"9b51801e271f030169915f705efeefaf","attributes":{"id":"9b51801e271f030169915f705efeefaf","tags":[],"doc":null,"selection_glyph":null,"nonselection_glyph":{"type":"Circle","id":"6801305b9a7ab20f92cb27667dee554f"},"server_data_source":null,"name":null,"data_source":{"type":"ColumnDataSource","id":"217267a296855f08a9dcd6edc511036b"},"glyph":{"type":"Circle","id":"39bb18ea1e86b7f0fdd1680957501144"}}},{"type":"ColumnDataSource","id":"9aba471665bee64db2d4742603968a15","attributes":{"id":"9aba471665bee64db2d4742603968a15","tags":[],"doc":null,"column_names":["x","y"],"selected":[],"discrete_ranges":{},"cont_ranges":{},"data":{"x":[null,null],"y":[null,null]}}},{"type":"Circle","id":"e62d131490082915e0323ed36804d8b0","attributes":{"id":"e62d131490082915e0323ed36804d8b0","tags":[],"doc":null,"size":{"units":"screen","value":null},"line_alpha":{"units":"data","value":1},"fill_alpha":{"units":"data","value":0.5},"line_color":{"units":"data","value":"#1F77B4"},"fill_color":{"units":"data","value":"#1F77B4"},"x":{"units":"data","field":"x"},"y":{"units":"data","field":"y"}}},{"type":"Circle","id":"b5ac5b1e51248650fa326f0da4a4f13e","attributes":{"id":"b5ac5b1e51248650fa326f0da4a4f13e","tags":[],"doc":null,"size":{"units":"screen","value":null},"line_alpha":{"units":"data","value":1},"fill_alpha":{"units":"data","value":0.5},"line_color":{"units":"data","value":"#e1e1e1"},"fill_color":{"units":"data","value":"#e1e1e1"},"x":{"units":"data","field":"x"},"y":{"units":"data","field":"y"}}},{"type":"GlyphRenderer","id":"dc706f4fdaf37516472af80f1da03dfd","attributes":{"id":"dc706f4fdaf37516472af80f1da03dfd","tags":[],"doc":null,"selection_glyph":null,"nonselection_glyph":{"type":"Circle","id":"b5ac5b1e51248650fa326f0da4a4f13e"},"server_data_source":null,"name":null,"data_source":{"type":"ColumnDataSource","id":"9aba471665bee64db2d4742603968a15"},"glyph":{"type":"Circle","id":"e62d131490082915e0323ed36804d8b0"}}},{"type":"Circle","id":"e1717355dc0537da3ec0a7f0039adfb8","attributes":{"id":"e1717355dc0537da3ec0a7f0039adfb8","tags":[],"doc":null,"size":{"units":"screen","value":null},"line_alpha":{"units":"data","value":1},"fill_alpha":{"units":"data","value":0.5},"line_color":{"units":"data","value":"#FF7F0E"},"fill_color":{"units":"data","value":"#FF7F0E"},"x":{"units":"data","field":"x"},"y":{"units":"data","field":"y"}}},{"type":"Circle","id":"8aaa2ce5349eb645d840a8a6297d2340","attributes":{"id":"8aaa2ce5349eb645d840a8a6297d2340","tags":[],"doc":null,"size":{"units":"screen","value":null},"line_alpha":{"units":"data","value":1},"fill_alpha":{"units":"data","value":0.5},"line_color":{"units":"data","value":"#e1e1e1"},"fill_color":{"units":"data","value":"#e1e1e1"},"x":{"units":"data","field":"x"},"y":{"units":"data","field":"y"}}},{"type":"GlyphRenderer","id":"16bb55b3473ab8907c3e3cacd4c16dca","attributes":{"id":"16bb55b3473ab8907c3e3cacd4c16dca","tags":[],"doc":null,"selection_glyph":null,"nonselection_glyph":{"type":"Circle","id":"8aaa2ce5349eb645d840a8a6297d2340"},"server_data_source":null,"name":null,"data_source":{"type":"ColumnDataSource","id":"9aba471665bee64db2d4742603968a15"},"glyph":{"type":"Circle","id":"e1717355dc0537da3ec0a7f0039adfb8"}}},{"type":"Circle","id":"5a5231f0d114d702b34d99e833a65874","attributes":{"id":"5a5231f0d114d702b34d99e833a65874","tags":[],"doc":null,"size":{"units":"screen","value":null},"line_alpha":{"units":"data","value":1},"fill_alpha":{"units":"data","value":0.5},"line_color":{"units":"data","value":"#2CA02C"},"fill_color":{"units":"data","value":"#2CA02C"},"x":{"units":"data","field":"x"},"y":{"units":"data","field":"y"}}},{"type":"Circle","id":"3da9b110888f8bf86502030a68b541c1","attributes":{"id":"3da9b110888f8bf86502030a68b541c1","tags":[],"doc":null,"size":{"units":"screen","value":null},"line_alpha":{"units":"data","value":1},"fill_alpha":{"units":"data","value":0.5},"line_color":{"units":"data","value":"#e1e1e1"},"fill_color":{"units":"data","value":"#e1e1e1"},"x":{"units":"data","field":"x"},"y":{"units":"data","field":"y"}}},{"type":"GlyphRenderer","id":"b132a0a4b1c64c053ae71b07efd0bd0a","attributes":{"id":"b132a0a4b1c64c053ae71b07efd0bd0a","tags":[],"doc":null,"selection_glyph":null,"nonselection_glyph":{"type":"Circle","id":"3da9b110888f8bf86502030a68b541c1"},"server_data_source":null,"name":null,"data_source":{"type":"ColumnDataSource","id":"9aba471665bee64db2d4742603968a15"},"glyph":{"type":"Circle","id":"5a5231f0d114d702b34d99e833a65874"}}},{"type":"Legend","id":"f2abc4ea683b3dad4ccec9a9e161a8bc","attributes":{"id":"f2abc4ea683b3dad4ccec9a9e161a8bc","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"},"legends":[["setosa",[{"type":"GlyphRenderer","id":"dc706f4fdaf37516472af80f1da03dfd"}]],["versicolor",[{"type":"GlyphRenderer","id":"16bb55b3473ab8907c3e3cacd4c16dca"}]],["virginica",[{"type":"GlyphRenderer","id":"b132a0a4b1c64c053ae71b07efd0bd0a"}]]]}},{"type":"Range1d","id":"8efff71dd84cd1a3c507c3fa91766f00","attributes":{"id":"8efff71dd84cd1a3c507c3fa91766f00","tags":[],"doc":null,"start":4.048,"end":8.152}},{"type":"Range1d","id":"f3a7e027a5ac0097b225125493092e9e","attributes":{"id":"f3a7e027a5ac0097b225125493092e9e","tags":[],"doc":null,"start":1.832,"end":4.568}},{"type":"LinearAxis","id":"6a3cae24519363c4439d8272a79813b2","attributes":{"id":"6a3cae24519363c4439d8272a79813b2","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"},"axis_label":"Sepal.Length","formatter":{"type":"BasicTickFormatter","id":"db78e591c5d2ad67e568a95b79b7649b"},"ticker":{"type":"BasicTicker","id":"1c55f629c2c7e74ae2c26235f4d74688"},"visible":true,"axis_label_text_font_size":"12pt"}},{"type":"BasicTickFormatter","id":"db78e591c5d2ad67e568a95b79b7649b","attributes":{"id":"db78e591c5d2ad67e568a95b79b7649b","tags":[],"doc":null}},{"type":"BasicTicker","id":"1c55f629c2c7e74ae2c26235f4d74688","attributes":{"id":"1c55f629c2c7e74ae2c26235f4d74688","tags":[],"doc":null,"num_minor_ticks":5}},{"type":"Grid","id":"86817f1699727eeace29f10cd3586e6e","attributes":{"id":"86817f1699727eeace29f10cd3586e6e","tags":[],"doc":null,"dimension":0,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"},"ticker":{"type":"BasicTicker","id":"1c55f629c2c7e74ae2c26235f4d74688"}}},{"type":"LinearAxis","id":"c3b3da4f38dd8b9b3760c1be918ad95c","attributes":{"id":"c3b3da4f38dd8b9b3760c1be918ad95c","tags":[],"doc":null,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"},"axis_label":"Sepal.Width","formatter":{"type":"BasicTickFormatter","id":"34b095e28bb92ded6c3a2449687f0fcf"},"ticker":{"type":"BasicTicker","id":"ec4e714e8ab5bd4ccee728538a4dc919"},"visible":true,"axis_label_text_font_size":"12pt"}},{"type":"BasicTickFormatter","id":"34b095e28bb92ded6c3a2449687f0fcf","attributes":{"id":"34b095e28bb92ded6c3a2449687f0fcf","tags":[],"doc":null}},{"type":"BasicTicker","id":"ec4e714e8ab5bd4ccee728538a4dc919","attributes":{"id":"ec4e714e8ab5bd4ccee728538a4dc919","tags":[],"doc":null,"num_minor_ticks":5}},{"type":"Grid","id":"3119553c69516e20e105afed96b7c831","attributes":{"id":"3119553c69516e20e105afed96b7c831","tags":[],"doc":null,"dimension":1,"plot":{"type":"Plot","id":"09a54cccfc70cb26c2bb27be07513fcb","subtype":"Figure"},"ticker":{"type":"BasicTicker","id":"ec4e714e8ab5bd4ccee728538a4dc919"}}}]},"evals":[]}</script><!--/html_preserve-->

## Example 8: `nvd3` from `rCharts`
[More examples](https://github.com/ramnathv/rCharts/blob/master/inst/libraries/nvd3/examples.R)


```r
if (!require("rcharts")) devtools::install_github("ramnathv/rCharts")
```

```
## Loading required package: rcharts
```

```
## Warning in library(package, lib.loc = lib.loc, character.only = TRUE,
## logical.return = TRUE, : there is no package called 'rcharts'
```

```
## Downloading GitHub repo ramnathv/rCharts@master
## Installing rCharts
## "C:/PROGRA~1/R/R-32~1.2/bin/x64/R" --no-site-file --no-environ --no-save  \
##   --no-restore CMD INSTALL  \
##   "C:/Users/p/AppData/Local/Temp/RtmpCkmmKZ/devtools2378624e37f9/ramnathv-rCharts-389e214"  \
##   --library="C:/Users/p/Documents/R/win-library/3.2" --install-tests
```

```r
library(rCharts)
```

```
## 
## Attaching package: 'rCharts'
## 
## The following object is masked from 'package:rcdimple':
## 
##     getLayer
```

```r
n1=nPlot(Sepal.Length~Sepal.Width,data=iris,group="Species",type="scatterChart")
n1$show()
```

```
## <iframe src=' figure/unnamed-chunk-12-1.html ' scrolling='no' frameBorder='0' seamless class='rChart nvd3 ' id=iframe- chart237817c04101 ></iframe> <style>iframe.rChart{ width: 100%; height: 400px;}</style>
```

## Example 8A: `nvd3`


```r
n2=nPlot(data=gearam,count~gear,group="am",type="multiBarChart")
```

```
## Error in eval(i, data, env): object 'gearam' not found
```

```r
n2$show()
```

```
## Error in eval(expr, envir, enclos): object 'n2' not found
```

## Example 9: `highcharts` from `rCharts`

[More examples](https://github.com/ramnathv/rCharts/blob/master/inst/libraries/highcharts/examples.R)

```r
h1=hPlot(Sepal.Length~Sepal.Width,data=iris,group="Species",type="scatter")
h1$chart(zoomType="xy")
h1$show()
```

```
## <iframe src=' figure/unnamed-chunk-14-1.html ' scrolling='no' frameBorder='0' seamless class='rChart highcharts ' id=iframe- chart237812fd6e6b ></iframe> <style>iframe.rChart{ width: 100%; height: 400px;}</style>
```

## Example 10: Scatter plot matrix `pairsD3`


```r
if (!require("pairsD3")) devtools::install_github("garthtarr/pairsD3")
```

```
## Loading required package: pairsD3
```

```
## Warning in library(package, lib.loc = lib.loc, character.only = TRUE,
## logical.return = TRUE, : there is no package called 'pairsD3'
```

```
## Downloading GitHub repo garthtarr/pairsD3@master
## Installing pairsD3
## Skipping 1 packages ahead of CRAN: shiny
## "C:/PROGRA~1/R/R-32~1.2/bin/x64/R" --no-site-file --no-environ --no-save  \
##   --no-restore CMD INSTALL  \
##   "C:/Users/p/AppData/Local/Temp/RtmpCkmmKZ/devtools23784025866/garthtarr-pairsD3-34a89d7"  \
##   --library="C:/Users/p/Documents/R/win-library/3.2" --install-tests
```

```r
library(pairsD3)
pairsD3(iris[,1:4],group=iris[,5])#%>%savePairs(file = 'iris.html')
```

<!--html_preserve--><div id="htmlwidget-2985" style="width:504px;height:504px;" class="pairsD3"></div>
<script type="application/json" data-for="htmlwidget-2985">{"x":{"data":{"Sepal.Length":[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5,7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7,6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],"Sepal.Width":[3.5,3,3.2,3.1,3.6,3.9,3.4,3.4,2.9,3.1,3.7,3.4,3,3,4,4.4,3.9,3.5,3.8,3.8,3.4,3.7,3.6,3.3,3.4,3,3.4,3.5,3.4,3.2,3.1,3.4,4.1,4.2,3.1,3.2,3.5,3.6,3,3.4,3.5,2.3,3.2,3.5,3.8,3,3.8,3.2,3.7,3.3,3.2,3.2,3.1,2.3,2.8,2.8,3.3,2.4,2.9,2.7,2,3,2.2,2.9,2.9,3.1,3,2.7,2.2,2.5,3.2,2.8,2.5,2.8,2.9,3,2.8,3,2.9,2.6,2.4,2.4,2.7,2.7,3,3.4,3.1,2.3,3,2.5,2.6,3,2.6,2.3,2.7,3,2.9,2.9,2.5,2.8,3.3,2.7,3,2.9,3,3,2.5,2.9,2.5,3.6,3.2,2.7,3,2.5,2.8,3.2,3,3.8,2.6,2.2,3.2,2.8,2.8,2.7,3.3,3.2,2.8,3,2.8,3,2.8,3.8,2.8,2.8,2.6,3,3.4,3.1,3,3.1,3.1,3.1,2.7,3.2,3.3,3,2.5,3,3.4,3],"Petal.Length":[1.4,1.4,1.3,1.5,1.4,1.7,1.4,1.5,1.4,1.5,1.5,1.6,1.4,1.1,1.2,1.5,1.3,1.4,1.7,1.5,1.7,1.5,1,1.7,1.9,1.6,1.6,1.5,1.4,1.6,1.6,1.5,1.5,1.4,1.5,1.2,1.3,1.4,1.3,1.5,1.3,1.3,1.3,1.6,1.9,1.4,1.6,1.4,1.5,1.4,4.7,4.5,4.9,4,4.6,4.5,4.7,3.3,4.6,3.9,3.5,4.2,4,4.7,3.6,4.4,4.5,4.1,4.5,3.9,4.8,4,4.9,4.7,4.3,4.4,4.8,5,4.5,3.5,3.8,3.7,3.9,5.1,4.5,4.5,4.7,4.4,4.1,4,4.4,4.6,4,3.3,4.2,4.2,4.2,4.3,3,4.1,6,5.1,5.9,5.6,5.8,6.6,4.5,6.3,5.8,6.1,5.1,5.3,5.5,5,5.1,5.3,5.5,6.7,6.9,5,5.7,4.9,6.7,4.9,5.7,6,4.8,4.9,5.6,5.8,6.1,6.4,5.6,5.1,5.6,6.1,5.6,5.5,4.8,5.4,5.6,5.1,5.1,5.9,5.7,5.2,5,5.2,5.4,5.1],"Petal.Width":[0.2,0.2,0.2,0.2,0.2,0.4,0.3,0.2,0.2,0.1,0.2,0.2,0.1,0.1,0.2,0.4,0.4,0.3,0.3,0.3,0.2,0.4,0.2,0.5,0.2,0.2,0.4,0.2,0.2,0.2,0.2,0.4,0.1,0.2,0.2,0.2,0.2,0.1,0.2,0.2,0.3,0.3,0.2,0.6,0.4,0.3,0.2,0.2,0.2,0.2,1.4,1.5,1.5,1.3,1.5,1.3,1.6,1,1.3,1.4,1,1.5,1,1.4,1.3,1.4,1.5,1,1.5,1.1,1.8,1.3,1.5,1.2,1.3,1.4,1.4,1.7,1.5,1,1.1,1,1.2,1.6,1.5,1.6,1.5,1.3,1.3,1.3,1.2,1.4,1.2,1,1.3,1.2,1.3,1.3,1.1,1.3,2.5,1.9,2.1,1.8,2.2,2.1,1.7,1.8,1.8,2.5,2,1.9,2.1,2,2.4,2.3,1.8,2.2,2.3,1.5,2.3,2,2,1.8,2.1,1.8,1.8,1.8,2.1,1.6,1.9,2,2.2,1.5,1.4,2.3,2.4,1.8,1.8,2.1,2.4,2.3,1.9,2.3,2.5,2.3,1.9,2,2.3,1.8]},"group":["setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica"],"alldata":{"Sepal.Length":[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5,7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7,6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],"Sepal.Width":[3.5,3,3.2,3.1,3.6,3.9,3.4,3.4,2.9,3.1,3.7,3.4,3,3,4,4.4,3.9,3.5,3.8,3.8,3.4,3.7,3.6,3.3,3.4,3,3.4,3.5,3.4,3.2,3.1,3.4,4.1,4.2,3.1,3.2,3.5,3.6,3,3.4,3.5,2.3,3.2,3.5,3.8,3,3.8,3.2,3.7,3.3,3.2,3.2,3.1,2.3,2.8,2.8,3.3,2.4,2.9,2.7,2,3,2.2,2.9,2.9,3.1,3,2.7,2.2,2.5,3.2,2.8,2.5,2.8,2.9,3,2.8,3,2.9,2.6,2.4,2.4,2.7,2.7,3,3.4,3.1,2.3,3,2.5,2.6,3,2.6,2.3,2.7,3,2.9,2.9,2.5,2.8,3.3,2.7,3,2.9,3,3,2.5,2.9,2.5,3.6,3.2,2.7,3,2.5,2.8,3.2,3,3.8,2.6,2.2,3.2,2.8,2.8,2.7,3.3,3.2,2.8,3,2.8,3,2.8,3.8,2.8,2.8,2.6,3,3.4,3.1,3,3.1,3.1,3.1,2.7,3.2,3.3,3,2.5,3,3.4,3],"Petal.Length":[1.4,1.4,1.3,1.5,1.4,1.7,1.4,1.5,1.4,1.5,1.5,1.6,1.4,1.1,1.2,1.5,1.3,1.4,1.7,1.5,1.7,1.5,1,1.7,1.9,1.6,1.6,1.5,1.4,1.6,1.6,1.5,1.5,1.4,1.5,1.2,1.3,1.4,1.3,1.5,1.3,1.3,1.3,1.6,1.9,1.4,1.6,1.4,1.5,1.4,4.7,4.5,4.9,4,4.6,4.5,4.7,3.3,4.6,3.9,3.5,4.2,4,4.7,3.6,4.4,4.5,4.1,4.5,3.9,4.8,4,4.9,4.7,4.3,4.4,4.8,5,4.5,3.5,3.8,3.7,3.9,5.1,4.5,4.5,4.7,4.4,4.1,4,4.4,4.6,4,3.3,4.2,4.2,4.2,4.3,3,4.1,6,5.1,5.9,5.6,5.8,6.6,4.5,6.3,5.8,6.1,5.1,5.3,5.5,5,5.1,5.3,5.5,6.7,6.9,5,5.7,4.9,6.7,4.9,5.7,6,4.8,4.9,5.6,5.8,6.1,6.4,5.6,5.1,5.6,6.1,5.6,5.5,4.8,5.4,5.6,5.1,5.1,5.9,5.7,5.2,5,5.2,5.4,5.1],"Petal.Width":[0.2,0.2,0.2,0.2,0.2,0.4,0.3,0.2,0.2,0.1,0.2,0.2,0.1,0.1,0.2,0.4,0.4,0.3,0.3,0.3,0.2,0.4,0.2,0.5,0.2,0.2,0.4,0.2,0.2,0.2,0.2,0.4,0.1,0.2,0.2,0.2,0.2,0.1,0.2,0.2,0.3,0.3,0.2,0.6,0.4,0.3,0.2,0.2,0.2,0.2,1.4,1.5,1.5,1.3,1.5,1.3,1.6,1,1.3,1.4,1,1.5,1,1.4,1.3,1.4,1.5,1,1.5,1.1,1.8,1.3,1.5,1.2,1.3,1.4,1.4,1.7,1.5,1,1.1,1,1.2,1.6,1.5,1.6,1.5,1.3,1.3,1.3,1.2,1.4,1.2,1,1.3,1.2,1.3,1.3,1.1,1.3,2.5,1.9,2.1,1.8,2.2,2.1,1.7,1.8,1.8,2.5,2,1.9,2.1,2,2.4,2.3,1.8,2.2,2.3,1.5,2.3,2,2,1.8,2.1,1.8,1.8,1.8,2.1,1.6,1.9,2,2.2,1.5,1.4,2.3,2.4,1.8,1.8,2.1,2.4,2.3,1.9,2.3,2.5,2.3,1.9,2,2.3,1.8],"groupval":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2],"group":["setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica"],"tooltip":["1 <br/> setosa","2 <br/> setosa","3 <br/> setosa","4 <br/> setosa","5 <br/> setosa","6 <br/> setosa","7 <br/> setosa","8 <br/> setosa","9 <br/> setosa","10 <br/> setosa","11 <br/> setosa","12 <br/> setosa","13 <br/> setosa","14 <br/> setosa","15 <br/> setosa","16 <br/> setosa","17 <br/> setosa","18 <br/> setosa","19 <br/> setosa","20 <br/> setosa","21 <br/> setosa","22 <br/> setosa","23 <br/> setosa","24 <br/> setosa","25 <br/> setosa","26 <br/> setosa","27 <br/> setosa","28 <br/> setosa","29 <br/> setosa","30 <br/> setosa","31 <br/> setosa","32 <br/> setosa","33 <br/> setosa","34 <br/> setosa","35 <br/> setosa","36 <br/> setosa","37 <br/> setosa","38 <br/> setosa","39 <br/> setosa","40 <br/> setosa","41 <br/> setosa","42 <br/> setosa","43 <br/> setosa","44 <br/> setosa","45 <br/> setosa","46 <br/> setosa","47 <br/> setosa","48 <br/> setosa","49 <br/> setosa","50 <br/> setosa","51 <br/> versicolor","52 <br/> versicolor","53 <br/> versicolor","54 <br/> versicolor","55 <br/> versicolor","56 <br/> versicolor","57 <br/> versicolor","58 <br/> versicolor","59 <br/> versicolor","60 <br/> versicolor","61 <br/> versicolor","62 <br/> versicolor","63 <br/> versicolor","64 <br/> versicolor","65 <br/> versicolor","66 <br/> versicolor","67 <br/> versicolor","68 <br/> versicolor","69 <br/> versicolor","70 <br/> versicolor","71 <br/> versicolor","72 <br/> versicolor","73 <br/> versicolor","74 <br/> versicolor","75 <br/> versicolor","76 <br/> versicolor","77 <br/> versicolor","78 <br/> versicolor","79 <br/> versicolor","80 <br/> versicolor","81 <br/> versicolor","82 <br/> versicolor","83 <br/> versicolor","84 <br/> versicolor","85 <br/> versicolor","86 <br/> versicolor","87 <br/> versicolor","88 <br/> versicolor","89 <br/> versicolor","90 <br/> versicolor","91 <br/> versicolor","92 <br/> versicolor","93 <br/> versicolor","94 <br/> versicolor","95 <br/> versicolor","96 <br/> versicolor","97 <br/> versicolor","98 <br/> versicolor","99 <br/> versicolor","100 <br/> versicolor","101 <br/> virginica","102 <br/> virginica","103 <br/> virginica","104 <br/> virginica","105 <br/> virginica","106 <br/> virginica","107 <br/> virginica","108 <br/> virginica","109 <br/> virginica","110 <br/> virginica","111 <br/> virginica","112 <br/> virginica","113 <br/> virginica","114 <br/> virginica","115 <br/> virginica","116 <br/> virginica","117 <br/> virginica","118 <br/> virginica","119 <br/> virginica","120 <br/> virginica","121 <br/> virginica","122 <br/> virginica","123 <br/> virginica","124 <br/> virginica","125 <br/> virginica","126 <br/> virginica","127 <br/> virginica","128 <br/> virginica","129 <br/> virginica","130 <br/> virginica","131 <br/> virginica","132 <br/> virginica","133 <br/> virginica","134 <br/> virginica","135 <br/> virginica","136 <br/> virginica","137 <br/> virginica","138 <br/> virginica","139 <br/> virginica","140 <br/> virginica","141 <br/> virginica","142 <br/> virginica","143 <br/> virginica","144 <br/> virginica","145 <br/> virginica","146 <br/> virginica","147 <br/> virginica","148 <br/> virginica","149 <br/> virginica","150 <br/> virginica"]},"n":150,"p":4,"labels":["Sepal.Length","Sepal.Width","Petal.Length","Petal.Width"],"settings":{"width":null,"height":null,"col":["#E41A1C","#377EB8","#4DAF4A"],"cex":3,"opacity":0.9},"leftmar":35,"topmar":2},"evals":[]}</script><!--/html_preserve-->

## Example 11: Scatter plot matrix `scatterMatrixD3`


```r
if (!require("scatterMatrixD3")) devtools::install_github("jcizel/scatterMatrixD3")
```

```
## Loading required package: scatterMatrixD3
```

```
## Warning in library(package, lib.loc = lib.loc, character.only = TRUE,
## logical.return = TRUE, : there is no package called 'scatterMatrixD3'
```

```
## Downloading GitHub repo jcizel/scatterMatrixD3@master
## Installing scatterMatrixD3
## "C:/PROGRA~1/R/R-32~1.2/bin/x64/R" --no-site-file --no-environ --no-save  \
##   --no-restore CMD INSTALL  \
##   "C:/Users/p/AppData/Local/Temp/RtmpCkmmKZ/devtools23783415b29/jcizel-scatterMatrixD3-887b87c"  \
##   --library="C:/Users/p/Documents/R/win-library/3.2" --install-tests
```

```r
library(scatterMatrixD3)
scatterMatrix(
   data = iris
)
```

<!--html_preserve--><div id="htmlwidget-581" style="width:504px;height:504px;" class="scatterMatrix"></div>
<script type="application/json" data-for="htmlwidget-581">{"x":{"data":{"Sepal.Length":[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5,7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7,6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],"Sepal.Width":[3.5,3,3.2,3.1,3.6,3.9,3.4,3.4,2.9,3.1,3.7,3.4,3,3,4,4.4,3.9,3.5,3.8,3.8,3.4,3.7,3.6,3.3,3.4,3,3.4,3.5,3.4,3.2,3.1,3.4,4.1,4.2,3.1,3.2,3.5,3.6,3,3.4,3.5,2.3,3.2,3.5,3.8,3,3.8,3.2,3.7,3.3,3.2,3.2,3.1,2.3,2.8,2.8,3.3,2.4,2.9,2.7,2,3,2.2,2.9,2.9,3.1,3,2.7,2.2,2.5,3.2,2.8,2.5,2.8,2.9,3,2.8,3,2.9,2.6,2.4,2.4,2.7,2.7,3,3.4,3.1,2.3,3,2.5,2.6,3,2.6,2.3,2.7,3,2.9,2.9,2.5,2.8,3.3,2.7,3,2.9,3,3,2.5,2.9,2.5,3.6,3.2,2.7,3,2.5,2.8,3.2,3,3.8,2.6,2.2,3.2,2.8,2.8,2.7,3.3,3.2,2.8,3,2.8,3,2.8,3.8,2.8,2.8,2.6,3,3.4,3.1,3,3.1,3.1,3.1,2.7,3.2,3.3,3,2.5,3,3.4,3],"Petal.Length":[1.4,1.4,1.3,1.5,1.4,1.7,1.4,1.5,1.4,1.5,1.5,1.6,1.4,1.1,1.2,1.5,1.3,1.4,1.7,1.5,1.7,1.5,1,1.7,1.9,1.6,1.6,1.5,1.4,1.6,1.6,1.5,1.5,1.4,1.5,1.2,1.3,1.4,1.3,1.5,1.3,1.3,1.3,1.6,1.9,1.4,1.6,1.4,1.5,1.4,4.7,4.5,4.9,4,4.6,4.5,4.7,3.3,4.6,3.9,3.5,4.2,4,4.7,3.6,4.4,4.5,4.1,4.5,3.9,4.8,4,4.9,4.7,4.3,4.4,4.8,5,4.5,3.5,3.8,3.7,3.9,5.1,4.5,4.5,4.7,4.4,4.1,4,4.4,4.6,4,3.3,4.2,4.2,4.2,4.3,3,4.1,6,5.1,5.9,5.6,5.8,6.6,4.5,6.3,5.8,6.1,5.1,5.3,5.5,5,5.1,5.3,5.5,6.7,6.9,5,5.7,4.9,6.7,4.9,5.7,6,4.8,4.9,5.6,5.8,6.1,6.4,5.6,5.1,5.6,6.1,5.6,5.5,4.8,5.4,5.6,5.1,5.1,5.9,5.7,5.2,5,5.2,5.4,5.1],"Petal.Width":[0.2,0.2,0.2,0.2,0.2,0.4,0.3,0.2,0.2,0.1,0.2,0.2,0.1,0.1,0.2,0.4,0.4,0.3,0.3,0.3,0.2,0.4,0.2,0.5,0.2,0.2,0.4,0.2,0.2,0.2,0.2,0.4,0.1,0.2,0.2,0.2,0.2,0.1,0.2,0.2,0.3,0.3,0.2,0.6,0.4,0.3,0.2,0.2,0.2,0.2,1.4,1.5,1.5,1.3,1.5,1.3,1.6,1,1.3,1.4,1,1.5,1,1.4,1.3,1.4,1.5,1,1.5,1.1,1.8,1.3,1.5,1.2,1.3,1.4,1.4,1.7,1.5,1,1.1,1,1.2,1.6,1.5,1.6,1.5,1.3,1.3,1.3,1.2,1.4,1.2,1,1.3,1.2,1.3,1.3,1.1,1.3,2.5,1.9,2.1,1.8,2.2,2.1,1.7,1.8,1.8,2.5,2,1.9,2.1,2,2.4,2.3,1.8,2.2,2.3,1.5,2.3,2,2,1.8,2.1,1.8,1.8,1.8,2.1,1.6,1.9,2,2.2,1.5,1.4,2.3,2.4,1.8,1.8,2.1,2.4,2.3,1.9,2.3,2.5,2.3,1.9,2,2.3,1.8],"Species":["setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","setosa","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","versicolor","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica","virginica"]}},"evals":[]}</script><!--/html_preserve-->


## Sampling of Network data and Graph Diagrams
* mermaid and grViz: [DiagrammeR](http://rich-iannone.github.io/DiagrammeR/index.html) 
* Vivagraph: [vivagRaph](https://github.com/keeganhines/vivagRaph)
* d3Network: [networkD3](http://christophergandrud.github.io/networkD3/)|
* Circle plot: [edgebundleR](https://github.com/garthtarr/edgebundleR)
* sigma: [sigma](https://github.com/jjallaire/sigma), 
* hive: [d3hiveR](http://www.buildingwidgets.com/blog/2015/7/11/week-27-d3hiver)


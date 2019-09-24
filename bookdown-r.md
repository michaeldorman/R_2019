--- 
title: "Introduction to Spatial Data Programming with R"
author: "Michael Dorman"
date: "2019-09-13 11:13:34"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
bibliography: [book.bib, packages.bib]
biblio-style: apalike
link-citations: yes
---

# Preface {-}

## What is R?

* **R** is a **programming language** and **environment**, originally developed for **statistical computing** and **graphics**
* As of September 2018 there are >13,000 R **packages** in the official repository (CRAN)^[https://cran.r-project.org/web/packages/]
* **Advantages** - 
    * A programming language, yet relatively simple
    * Over 100,000 functions from various areas of interest
    
<div class="figure">
<img src="images/lesson_01_r_trend.png" alt="Stack Overflow Trend for the 'r' question tag^[https://insights.stackoverflow.com/trends?tags=r]" width="90%" />
<p class="caption">(\#fig:lesson-01-r-trend)Stack Overflow Trend for the 'r' question tag^[https://insights.stackoverflow.com/trends?tags=r]</p>
</div>

<div class="figure">
<img src="images/lesson_01_ieee_rank_2018.png" alt="IEEE Language Rankings 2018^[http://blog.revolutionanalytics.com/popularity/]" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-1)IEEE Language Rankings 2018^[http://blog.revolutionanalytics.com/popularity/]</p>
</div>

<div class="figure">
<img src="images/lesson_01_rising_tide_of_R.jpg" alt="Proportion of research papers citing R^[https://www.nature.com/news/programming-tools-adventures-with-r-1.16609]" width="50%" />
<p class="caption">(\#fig:unnamed-chunk-2)Proportion of research papers citing R^[https://www.nature.com/news/programming-tools-adventures-with-r-1.16609]</p>
</div>

A brief overview of the capabilities and packages for several domains of R use, are available in "task views":

* https://cran.r-project.org/web/views/
* http://www.maths.lancs.ac.uk/~rowlings/R/TaskViews/

<div class="figure">
<img src="images/lesson_01_cran_task_views.png" alt="CRAN Task Views" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-3)CRAN Task Views</p>
</div>

## R and analysis of spatial data

* Over time, there was an increasing number of **contributed packages** for handling and analyzing spatial data in R
* Today, spatial analysis is a **major functionality in R**
* As of September 2018, there are **~180 packages**^[https://cran.r-project.org/web/views/Spatial.html] specifically addressing spatial analysis in R

<div class="figure">
<img src="images/books.png" alt="Books on Spatial Data Analysis with R" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-4)Books on Spatial Data Analysis with R</p>
</div>

Some history:

* pre-2003: Variable and incomplete approaches (**`MASS`**, **`spatstat`**, **`maptools`**, **`geoR`**, **`splancs`**, **`gstat`**, ...)
* 2003: Consensus that a package defining standard data structures should be useful; **`rgdal`** released on CRAN\footnote{Comprehensive R Archive Network}
* 2005: **`sp`** released on CRAN; **`sp`** support in **`rgdal`**
* 2008: **Applied Spatial Data Analysis with R**, 1st ed.
* 2010: **`raster`** released on CRAN
* 2011: **`rgeos`** released on CRAN
* 2013: **Applied Spatial Data Analysis with R**, 2nd ed.
* 2016: **`sf`** released on CRAN
* 2018: **`stars`** released on CRAN
* 2019: **Geocomputation with R**, (https://geocompr.robinlovelace.net/)
* 2020(?): **Spatial Data Science** (https://keen-swartz-3146c4.netlify.com/)

R as a Geographic Information System (GIS)?

* **General** advantages of Command Line Interface (CLI) software
    * **Automation** - Doing otherwise unfeasible repetitive tasks
    * **Reproducibility** - Precise control of instructions to the computer
* **Strengths** of R as a GIS
    * R capabilities in **data processing** and **visualization**, combined with dedicated **packages for spatial data**
    * A **single environment** encompassing all analysis aspects - acquiring data, computation, statistics, visualization, Web, etc.
* Situations when **other tools** are needed
    * **Interactive editing or georeferencing** (but see [**`mapedit`**](https://cran.r-project.org/package=mapedit))
    * Unique **GIS algorithms** (3D analysis, label placement, network routing, splitting lines at intersections, etc.)
    * Data that **cannot fit in RAM** (but R can connect to spatial databases^[https://cran.r-project.org/web/packages/sf/vignettes/sf2.html]

### Input and output of spatial data

* Reading spatial layers from a file into an R data structure, or writing the R data structure into a file, are handled by external libraries -
    * [**OGR**](http://www.gdal.org/ogr/) is used for reading/writing vector files, with `sf`
    * [**GDAL**](http://www.gdal.org/) is used for reading/writing raster files, with `raster`
    * [**PROJ4**](http://trac.osgeo.org/proj/) is used for handling CRS, in both `sf` and `raster`
    * Working with specialized formats, e.g. **HDF** with `gdalUtils` or **NetCDF** with `ncdf4`

### **`sf`**: Geoprocessing Vector Layers

* [**GEOS**](http://trac.osgeo.org/geos/) is used for geometric operations on **vector layers** with **`sf`** -
    * **Numeric operators** - Area, Length, Distance...
    * **Logical operators** - Contains, Within, Within distance, Crosses, Overlaps, Equals, Intersects, Disjoint, Touches...
    * **Geometry generating operators** - Centroid, Buffer, Intersection, Union, Difference, Convex-Hull, Simplification...

<div class="figure">
<img src="index_files/figure-html/unnamed-chunk-5-1.png" alt="Buffer function" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-5)Buffer function</p>
</div>

### **`raster`**: Geoprocessing Rasters

* Geometric operations on **rasters** can be done with package `raster` -
    * **Accessing cell values** - As vector, As matrix, Extract to points / lines / polygons, random / regular sampling, Frequency table, Histogram...
    * **Raster algebra** - Arithmetic (`+`, `-`, ...), Math (`sqrt`, `log10`, ...), logical (`!`, `==`, `>`, ...), summary (`mean`, `max`, ...), Mask, Overlay...
    * **Changing resolution and extent** - Crop, Mosaic, (Dis)aggregation, Reprojection, Resampling, Shift, Rotation...
    * **Focal operators** - Distance, Direction, Focal Filter, Slope, Aspect, Flow direction...
    * **Transformations** - Vector layers <-> Raster...

### **`geosphere`**: Geometric calculations on longitude/latitude

* Package `geosphere` implements **spherical trigonometry** functions for distance- and direction-related calculations on **geographic coordinates (lon-lat)**

<div class="figure">
<img src="index_files/figure-html/unnamed-chunk-6-1.png" alt="Points on Great Circle" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-6)Points on Great Circle</p>
</div>

<div class="figure">
<img src="images/facebook_map.png" alt="Visualizing Facebook Friends with `geosphere`^[http://paulbutler.org/archives/visualizing-facebook-friends/]" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-7)Visualizing Facebook Friends with `geosphere`^[http://paulbutler.org/archives/visualizing-facebook-friends/]</p>
</div>

### **`gstat`**: Geostatistical Modelling

* Univariate and multivariate geostatistics - 
    * Variogram modelling 
    * Ordinary and universal point or block (co)kriging
    * Cross-validation

<div class="figure">
<img src="index_files/figure-html/unnamed-chunk-8-1.png" alt="Predicted Zinc concentration, using Ordinary Kriging" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-8)Predicted Zinc concentration, using Ordinary Kriging</p>
</div>

### **`spdep`**: Spatial dependence modelling

* Modelling with spatial weights - 
    * Building neighbor lists and spatial weights
    * Tests for spatial autocorrelation for areal data (e.g. Moran's I)
    * Spatial regression models (e.g. SAR, CAR)

<div class="figure">
<img src="index_files/figure-html/unnamed-chunk-9-1.png" alt="Neighbours list based on regions with contiguous boundaries" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-9)Neighbours list based on regions with contiguous boundaries</p>
</div>

### **`spatstat`**: Spatial point pattern analysis

* Techniques for statistical analysis of spatial point patterns, such as - 
    * Kernel density estimation
    * Detection of clustering using Ripley's K-function 
    * Spatial logistic regression
    
<div class="figure">
<img src="index_files/figure-html/unnamed-chunk-10-1.png" alt="Distance map for the Biological Cells point pattern dataset" width="40%" />
<p class="caption">(\#fig:unnamed-chunk-10)Distance map for the Biological Cells point pattern dataset</p>
</div>

### **`osmdata`**: Access to OpenStreetMap data

* Accessing **OpenStreetMap (OSM)** data using the **Overpass API**^[http://wiki.openstreetmap.org/wiki/Overpass_API]


```r
library(sf)
library(osmdata)
q = opq(bbox = "Beer-Sheva, Israel")
q = add_osm_feature(q, key = "highway")
dat = osmdata_sf(q)
lines = dat$osm_lines
pol = dat$osm_polygons
pol = st_cast(pol, "MULTILINESTRING")
pol = st_cast(pol, "LINESTRING")
lines = rbind(lines, pol)
lines = lines[, c("osm_id", "highway")]
lines = st_transform(lines, 32636)
plot(lines)
```

<div class="figure">
<img src="index_files/figure-html/unnamed-chunk-11-1.png" alt="Beer-Sheva road network" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-11)Beer-Sheva road network</p>
</div>

### **`ggplot2`**, **`ggmap`**: Visualization

<div class="figure">
<img src="images/bike_ggplot.png" alt="London cycle hire journeys with `ggplot2`^[http://spatial.ly/2012/02/great-maps-ggplot2/]" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-12)London cycle hire journeys with `ggplot2`^[http://spatial.ly/2012/02/great-maps-ggplot2/]</p>
</div>

<div class="figure">
<img src="images/ggmap_small_multiples.png" alt="Crime density by day with `ggplot2`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-13)Crime density by day with `ggplot2`</p>
</div>

http://spatial.ly/2012/02/great-maps-ggplot2/

### **`leaflet`**, **`mapview`**: Web mapping

* Packages `leaflet` and `mapview` provide methods to produce **interactive maps** using the [Leaflet JavaScript library](http://leafletjs.com/)

<img src="images/leaflet_logo.png" width="30%" />

* Package [`leaflet`](https://rstudio.github.io/leaflet/) gives more low-level control
* Package [`mapview`](https://r-spatial.github.io/mapview/) is a wrapper around `leaflet`, automating addition of useful features - 
    * Commonly used **basemaps**
    * **Color scales** and **legends**
    * **Labels**
    * **Popups**

* **Function `mapview`** produces an interactive map given a spatial object
    * `zcol="..."` specifies the **attribute** used for symbology 
    * `legend=TRUE` adds a **legend**


```r
library(sf)
library(mapview)
states = st_read("USA_2_GADM_fips.shp")
mapview(states, zcol = "NAME_1", legend = TRUE)
```

<div class="figure">
<img src="images/mapview.png" alt="Intractive map made with `mapview`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-16)Intractive map made with `mapview`</p>
</div>

## Books

* **Hierarchical Modeling and Analysis for Spatial Data** (1st ed 2003, 2nd ed. 2014)
* **Model-based Geostatistics** (2007)
* **Applied Spatial Data Analysis with R** (1st ed. 2008, 2nd ed. 2013)
* **A Practical Guide for Geostatistical Mapping** (2009)
* **Spatial Data Analysis in Ecology and Agriculture using R** (2012)
* **Displaying Time Series, Spatial, and Space-Time Data with R** (1st ed. 2014, 2nd ed. 2018)
* **Learning R for Geospatial Analysis** (2014)
* **An Introduction to R for Spatial Analysis and Mapping** (2015)
* **Spatial Point Patterns: Methodology and Applications with R** (2015)
* **Geocomputation with R** (2019) (https://geocompr.robinlovelace.net/)
* **Spatial Data Science** (2020?) (https://www.r-spatial.org/book/)

## Online courses and tutorials

* Courses
    * https://mgimond.github.io/Spatial/index.html
    * http://adamwilson.us/SpatialDataScience/
    * http://geog.uoregon.edu/bartlein/courses/geog490/index.html
    * https://zia207.github.io/geospatial-data-science.github.io/index.html
    * http://132.72.155.230:3838/r/ (This course)
    * Another list here: https://geocompr.github.io/guestbook/
* Tutorials
    * https://datacarpentry.org/lessons/#geospatial-curriculum
    * http://rspatial.org/
    * http://www.nickeubank.com/gis-in-r/
    * https://www.neonscience.org/resources/data-tutorials





<!--chapter:end:index.Rmd-->

# The R environment {#the-r-environment}



## Programming

### Why is programming necessary?

* Is this a **Microsoft Excel** spreadsheet?
* The file has an Excel **icon**, and it opens in Excel on **double-click**...

<div class="figure" style="text-align: center">
<img src="images/lesson_01_csv_icon.png" alt="CSV file" width="50%" />
<p class="caption">(\#fig:unnamed-chunk-2)CSV file</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_01_csv_excel.png" alt="CSV file opened in Excel" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-3)CSV file opened in Excel</p>
</div>

* However, this is in fact a **plain-text** file in the **Comma Separated Values** (CSV) format, and can be opened in various other software, such as Notepad

<div class="figure" style="text-align: center">
<img src="images/lesson_01_csv_notepad.png" alt="CSV file opened in Notepad" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-4)CSV file opened in Notepad</p>
</div>

* The graphical interface **"protects"** us from the little details - 
    * Hiding the `.csv` file **extension**
    * Displaying an Excel **icon**
    * Automatically **opening** the file in Excel
* Is this a **bad** thing?
    * We can be unaware of the fact that the file can be opened in software **other** than Excel
    * In general - the "ordinary" interaction with the computer is **limited** to clicking on links, selecting from menus and filling dialog boxes
    * The latter approach suggests there are **"boundaries"** set by the computer interface for the user who wishes to accomplish a given task
    * Of course the opposite is true - the user has full **control**, and can tell the computer exactly what he wants to do

* Question: how can we **change** the value of a particular raster **cell**, such as the `[120, 120]` cell?

<div class="figure" style="text-align: center">
<img src="images/lesson_01_rainfall_raster_qgis.png" alt="The `rainfall.tif` raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-5)The `rainfall.tif` raster</p>
</div>

* In **ArcGIS** - 
    * Open the raster with "Add Data"
    * Convert the raster to points
    * Calculate row and column indices
    * Locate the point we want to change and edit its attribute
    * Convert the points to back to a raster, using the same extent and resolution and setting a snap raster
    * Export the raster

<div class="figure" style="text-align: center">
<img src="images/lesson_01_arcgis_raster_to_points.png" alt="Raster to points in ArcGIS" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-6)Raster to points in ArcGIS</p>
</div>

https://support.esri.com/en/technical-article/000010981

* In **R** - 
    * Loading the `raster` package
    * Reading the `rainfall.tif` raster
    * Assigning a new value to the `[120, 120]` cell
    * Writing the raster to disk


```r
library(stars)
r = read_stars("data/rainfall.tif")
r[[1]][120, 120] = 1000
writeRaster(r, "rainfall2.tif")
```

* In **Python**:


```python
import gdalnumeric
r = gdalnumeric.LoadFile("rainfall.tif")
r[119, 119] = 1000
gdalnumeric.SaveArray(
    r, 
    "rainfall2.tif", 
    format = "GTiff", 
    prototype = "rainfall.tif"
)
```

### What is programming

* A **computer program** is a sequence of text instructions that can be "understood" by a computer and executed
* A **programming language** is a machine-readable artificial language designed to express computations that can be performed by a computer
* **Programming** is the preferred way for giving instructions to the computer because that way - 
    * We break free from the **limitations** of the graphical interface, and are able to perform tasks that are unfeasible or even impossible
    * We can keep the code for **editing** and **re-use** in the future, and as a reminder to ourselves of what we did in the past
    * Sharing a **precise** record of our analysis with others, making our results reproducible

### Computer hardware

* The **Central Processing Unit (CPU)** performs (simple) calculations very fast
* The **Random Access Memory (RAM)** is a short-term fast memory
* **Mass Storage** (e.g. hard drive) is long-term and high-capacity memory, but slow
* A **Keyboard** is an example of an input device
* A **Screen** is an example of an output device

<div class="figure" style="text-align: center">
<img src="images/lesson_01_computer_components.png" alt="Components of a computing environment" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-9)Components of a computing environment</p>
</div>

### Abstraction and execution models

* Programming languages differ in their level of **abstraction** and **execution models**
* **Abstraction** is the presentation of data and instructions which hide implementation details
    * **Low-level** programming languages provide little or no abstraction 
        * **Advantage**: efficient memory use and therefore fast
        * **Disadvantage**: difficult to use because of the many technical details the programmer needs to know
    * **High-level** programming languages provide more abstraction and automatically handle various aspects such as memory use
        * **Advantage**: more "understandable" and easier to use
        * **Disadvantage**: Less efficient and therefore slower

* **Abstraction** lets the programmer focus on the task at hand, ignoring the small technical details

<div class="figure" style="text-align: center">
<img src="images/lesson_01_abstraction.png" alt="Increasing abstraction from Assembly to C++ to R" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-10)Increasing abstraction from Assembly to C++ to R</p>
</div>

* **Execution models** are systems for execution of programs written in a given programming language
    * **Compiled** - before being executed, the code needs to be compiled into **executable** machine code
    * **Interpreted** - the code is executed directly, using an **interpreter**
        * **Advantage**: easier to develop and use
        * **Disadvantage**: lower efficiency

* In **compiled** execution models, the code is first translated to an executable file

<div class="figure" style="text-align: center">
<img src="images/lesson_01_compiled1.png" alt="Compilation of C++ code" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-11)Compilation of C++ code</p>
</div>

* The executable file can then be run

<div class="figure" style="text-align: center">
<img src="images/lesson_01_compiled2.png" alt="Running an executable file" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-12)Running an executable file</p>
</div>

* In **interpreted** execution models, the code can be run directly using the interpreter

<div class="figure" style="text-align: center">
<img src="images/lesson_01_interpreted.png" alt="Running R code" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-13)Running R code</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_01_programming_languages_matrix.jpg" alt="Programming languages classification based on abstraction level and execution model" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-14)Programming languages classification based on abstraction level and execution model</p>
</div>

### Object-oriented programming

* The interaction with the computer takes places through **objects**
* Each object belongs to a **class**: an abstract structure with certain properties
* Objects are in fact **instances** of a class
* The class comprises a template which sets the **properties** and **methods** each object of that class should have, while an object contains specific **values** for that particular instance
* For example - 
    * All cars we see in the parking lot are **instances** of the "car" class
    * The "car" class has certain **properties** (manufacturer, color, year) and **methods** (start, drive, stop)
    * Each "car" object has specific **values** for the properties (Suzuki, brown, 2011)

<div class="figure" style="text-align: center">
<img src="images/lesson_01_js_object.png" alt="An object" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-15)An object</p>
</div>

https://www.w3schools.com/js/js\_objects.asp


```r
library(stars)
## Loading required package: abind
## Loading required package: sf
## Linking to GEOS 3.7.1, GDAL 2.4.2, PROJ 5.2.0
r = read_stars("data/rainfall.tif")
r
## stars object with 2 dimensions and 1 attribute
## attribute(s):
##  rainfall.tif   
##  Min.   :179.9  
##  1st Qu.:388.7  
##  Median :507.3  
##  Mean   :491.2  
##  3rd Qu.:586.1  
##  Max.   :957.5  
##  NA's   :21250  
## dimension(s):
##   from  to  offset delta                       refsys point values    
## x    1 155  615965  1000 +proj=utm +zone=36 +datum... FALSE   NULL [x]
## y    1 236 3692430 -1000 +proj=utm +zone=36 +datum... FALSE   NULL [y]
```

### Inheritance

* One of the implications of object-oriented programming is **inheritance**
* Inheritance makes it possible for one class to **"extend"** another class, by adding new properties and/or new methods
* For example - 
    * A "taxi" class is an **extension** of the "car" class
    * A "taxi" has **new** properties (taxi company name), and new methods (switching the taximeter on and off)


```r
str(r)
## List of 1
##  $ rainfall.tif: num [1:155, 1:236] NA NA NA NA NA NA NA NA NA NA ...
##  - attr(*, "dimensions")=List of 2
##   ..$ x:List of 7
##   .. ..$ from  : num 1
##   .. ..$ to    : num 155
##   .. ..$ offset: num 615965
##   .. ..$ delta : num 1000
##   .. ..$ refsys: chr "+proj=utm +zone=36 +datum=WGS84 +units=m +no_defs "
##   .. ..$ point : logi FALSE
##   .. ..$ values: NULL
##   .. ..- attr(*, "class")= chr "dimension"
##   ..$ y:List of 7
##   .. ..$ from  : num 1
##   .. ..$ to    : num 236
##   .. ..$ offset: num 3692430
##   .. ..$ delta : num -1000
##   .. ..$ refsys: chr "+proj=utm +zone=36 +datum=WGS84 +units=m +no_defs "
##   .. ..$ point : logi FALSE
##   .. ..$ values: NULL
##   .. ..- attr(*, "class")= chr "dimension"
##   ..- attr(*, "raster")=List of 3
##   .. ..$ affine     : num [1:2] 0 0
##   .. ..$ dimensions : chr [1:2] "x" "y"
##   .. ..$ curvilinear: logi FALSE
##   .. ..- attr(*, "class")= chr "stars_raster"
##   ..- attr(*, "class")= chr "dimensions"
##  - attr(*, "class")= chr "stars"
```

## The R environment

### Installing R and RStudio

R can be downloaded from the [R-project website](https://www.r-project.org/). The current version is [3.6.1](https://cloud.r-project.org/bin/windows/base/R-3.6.1-win.exe). 

RStudio can be downloaded from the company [website](https://www.rstudio.com/). The current version is [1.2.1335](https://download1.rstudio.org/desktop/windows/RStudio-1.2.1335.exe).

### Starting R

* Start → All Programs → R → R x64 3.61

<div class="figure" style="text-align: center">
<img src="images/lesson_01_rgui.png" alt="RGui" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-18)RGui</p>
</div>

* Start → All Programs → RStudio → RStudio

<div class="figure" style="text-align: center">
<img src="images/lesson_01_rstudio.png" alt="RStudio" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-19)RStudio</p>
</div>

### RStudio - Interface components

* In this lesson we will only work with the **console**, i.e. the command line
* In the following lessons we will also work with other RStudio panels

<div class="figure" style="text-align: center">
<img src="images/lesson_01_rstudio_console.png" alt="RStudio console" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-20)RStudio console</p>
</div>

## Basic R expressions

### Console input and output

* We can type expressions at the command line and press **Enter**
* For example, let's type the expression `1+3+5+7` - 


```r
1 + 3 + 5 + 7
## [1] 16
```

* The expression `1+3+5+7` was sent to the processor, and the result 16 was printed in the console
* (Later on we will discuss the `[1]` part)
* Note: the value 16 is not kept in in the RAM or Mass Storage, just printed on screen

<div class="figure" style="text-align: center">
<img src="images/lesson_01_in_memory.png" alt="In memory" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-22)In memory</p>
</div>

* The input and output appears like this in the slides - 


```r
1 + 3 + 5 + 7
## [1] 16
```

* And here is how it appears in RStudio - 

<div class="figure" style="text-align: center">
<img src="images/lesson_01_console_screenshot.png" alt="RStudio console input and output" width="25%" />
<p class="caption">(\#fig:unnamed-chunk-24)RStudio console input and output</p>
</div>

* We can type a number, the number itself is returned - 


```r
600
## [1] 600
```

* We can type text inside single `'` or double `"` quotes - 


```r
"Hello"
## [1] "Hello"
```

* Both of these are constant values, `numeric` or `text`, the simplest type of expressions in R

### Arithmetic operators

* Through interactive use of the command line we can experiment with basic operators in R
* For example, R includes the standard **arithmetic operators**

| Operator | Meaning |
|---|---|
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `^` | Exponent |

Table: Arithmetic operators

For example:


```r
5 + 3
## [1] 8
4 - 5
## [1] -1
1 * 10
## [1] 10
1 / 10
## [1] 0.1
10 ^ 2
## [1] 100
```

Note: We can use the **up** ↑ and **down** ↓ keys to scroll through the executed expressions history

* Note that very large or very small numbers are formatted in **exponential** notation - 


```r
1 / 1000000 # 1*10^-6
## [1] 1e-06
```


```r
7 * 100000  # 7*10^5
## [1] 7e+05
```

* **Infinity** is treated as a special numeric value `Inf` or `-Inf` -


```r
1 / 0
## [1] Inf
```


```r
-1 / 0
## [1] -Inf
```


```r
Inf + 1
## [1] Inf
```


```r
-1 * Inf
## [1] -Inf
```

* We can control operator precedence with **brackets**, just like in math
* This is recommended for clarity even where not strictly required


```r
2 * 3 + 1
## [1] 7
```


```r
2 * (3 + 1)
## [1] 8
```

### Spaces and comments

* The interpreter ignores everything to the right of **number sign** `#` -


```r
1 * 2 # * 3
## [1] 2
```

* It is therefore used for **code comments** -


```r
# Multiplication example
5 * 5
## [1] 25
```

* The interpreter ignores **spaces**, so the following expressions are treated exactly the same way:


```r
1 + 1
## [1] 2
```


```r
1+1
## [1] 2
```


```r
1+           1
## [1] 2
```

* We can type **Enter** in the middle of an expression and keep typing on the next line
* The interpreter displays the `+` symbol, which means that the expression is **incomplete** - 


```r
5 * 
2
## [1] 10
```

<div class="figure" style="text-align: center">
<img src="images/lesson_01_console_next_line.png" alt="Incomplete expression" width="20%" />
<p class="caption">(\#fig:unnamed-chunk-42)Incomplete expression</p>
</div>

* We can exit from this state by pressing **Esc**
* We can browse previous expressions using the up and down arrows
* The console can be cleared with **Ctrl+L**

### Conditional operators

* **Conditions** are expression that use **conditional operators** and have a yes/no result, i.e. the condition can be either true or false
* The result of a condition is a **logical** value, `TRUE` or `FALSE`
    * `TRUE` means the expression is true
    * `FALSE` means the expression is false
    * (`NA` means it is unknown)

| Operator | Meaning |
|---|---|
| `==` | Equal |
| `>` | Greater than |
| `>=` | Greater than or equal |
| `<` | Less than |
| `<=` | Less than or equal |
| `!=` | Not equal |
| `&` | And |
| `|` | Or |
| `!` | Not |

Table: Conditional operators

* For example, we can use **conditional operators** to compare numeric values -


```r
1 < 2
## [1] TRUE
1 > 2
## [1] FALSE
2 > 2
## [1] FALSE
2 >= 2
## [1] TRUE
2 != 2
## [1] FALSE
```

* **"Equal"** `==` and **"not equal"** `!=` are opposites of each other: a pair of values can be either equal or not


```r
1 == 1
## [1] TRUE
1 == 2
## [1] FALSE
```


```r
1 != 1
## [1] FALSE
1 != 2
## [1] TRUE
```

* The **"and"** `&` and **"or"** `|` operators are used to create more complex conditions
* **"And"** `&` returns `TRUE` when **both** sides are `TRUE`


```r
(1 < 10) & (10 < 100)
## [1] TRUE
(1 < 10) & (10 > 100)
## [1] FALSE
```

* **"Or"** `|` returns `TRUE` when **at least one** of the sides is `TRUE` - 


```r
(1 < 10) | (10 < 100)
## [1] TRUE
(1 < 10) | (10 > 100)
## [1] TRUE
```

* The last conditional operator is **"not"** `!`, which reverses `TRUE` to `FALSE` and `FALSE` to `TRUE` -


```r
1 == 1
## [1] TRUE
!(1 == 1)
## [1] FALSE
```


```r
(1 == 1) & (2 == 2)
## [1] TRUE
(1 == 1) & !(2 == 2)
## [1] FALSE
```

* Question: run the following expression and explain their result - 


```r
FALSE == FALSE
## [1] TRUE
```


```r
!(TRUE == TRUE)
## [1] FALSE
```


```r
!(!(1 == 1))
## [1] TRUE
```

### Special values

| Value | Meaning |
|---|---|
| `Inf` | Infinity |
| `NA` | Not Available |
| `NaN` | Not a Number |
| `NULL` | Empty object |

Table: Special values in R

* For example - 


```r
1/0
## [1] Inf
```


```r
NA + 3
## [1] NA
```


```r
0/0
## [1] NaN
```


```r
NULL
## NULL
```

### Functions

* In math, a **function** is a relation that associates each element x of a set X, to a single element y of another set Y
* For example, the function $y=2x$

<div class="figure" style="text-align: center">
<img src="images/lesson_01_programming_function.png" alt="A function" width="40%" />
<p class="caption">(\#fig:unnamed-chunk-57)A function</p>
</div>

* The concept of functions in programming is similar - 
    * A function is a code piece that "knows" how to do a certain **task**
    * Executing the function is known as a **function call**
    * The function accepts zero or more objects as **input** (e.g. `2`) and returns a single object as output (e.g. `4`), possibly also doing other things known as **side effects**
    * The number and type of inputs the function needs are determined in the function definition; these are known as the function **parameters** (e.g. a single number)
    * The objects the function received in practice, as part of a particular function call, are known as **arguments** (e.g. `2`)

* A function is basically a set of pre-defined **instructions** 
* There are thousands of **built-in** functions in R 
* Later on we will learn to **define** our own functions

<div class="figure" style="text-align: center">
<img src="images/Chambers2014a.png" alt="From Chambers 2014, Statistical Science (https://arxiv.org/pdf/1409.3531.pdf)" width="75%" />
<p class="caption">(\#fig:unnamed-chunk-58)From Chambers 2014, Statistical Science (https://arxiv.org/pdf/1409.3531.pdf)</p>
</div>


```r
`+`(5, 5)
## [1] 10
```

* A **function call** is composed of the function name, followed by the arguments inside brackets `()` and separated by commas `,` -


```r
sqrt(4)
## [1] 2
```

* The `sqrt` function received a single argument `4` and returned its square root `2`

### Error messages

* Consider the following expressions - 


```r
sqrt(16)
## [1] 4
```


```r
sqrt("a")
## Error in sqrt("a"): non-numeric argument to mathematical function
```


```r
sqrt(a)
## Error in eval(expr, envir, enclos): object 'a' not found
```

* In the previous slide we got two **error messages**, because the last two expressions were illegal, i.e. not in agreement with the syntax rules of R
* The **first error** was occurred because we tried to run a mathematical operation `sqrt` on a text value `"a"`
* The **second error** occurred because we tried to use a non-existing object `a`. And text without quotes is treated as a name of an object, i.e. a label for an actual object stored in RAM. Since we don't have an object named `a` we got an error.

### Pre-loaded objects

* When starting R, a default set of **objects** is loaded into the RAM, such as `TRUE`, `FALSE`, `sqrt` and `pi`
* Type `pi` and see what happens - 


```r
pi
## [1] 3.141593
```

### Decimal places

* Is the value of PI stored in memory really equal to `3.141593`? 


```r
pi == 3.141593
## [1] FALSE
```

* If not, what is the difference?


```r
pi - 3.141593
## [1] -3.464102e-07
```

* The reason is that by default R prints only the first 7 digits


```r
options()$digits
## [1] 7
```

### Case-sensitivity

* R is **case-sensitive**, it distinguishes between lower-case and upper-case letters
* For example, `TRUE` is a logical value, but `True` and `true` are undefined - 


```r
TRUE
## [1] TRUE
```


```r
True
## Error in eval(expr, envir, enclos): object 'True' not found
```


```r
true
## Error in eval(expr, envir, enclos): object 'true' not found
```

### Classes

* R is an object-oriented language, where each object belongs to a **class**
* The `class` functions accepts an object and returns the **class name** -  


```r
class(TRUE)
## [1] "logical"
class(1)
## [1] "numeric"
class(pi)
## [1] "numeric"
class("a")
## [1] "character"
class(sqrt)
## [1] "function"
```

* Question: explain the returned value of the following expressions - 


```r
class(1 < 2)
## [1] "logical"
```


```r
class("logical")
## [1] "character"
```


```r
class(1) == class(2)
## [1] TRUE
```

* Question: explain the returned value of the following expressions - 


```r
class(class)
## [1] "function"
```


```r
class(class(sqrt))
## [1] "character"
```


```r
class(class(1))
## [1] "character"
```

### Using help files

* Every built-in object is associated with a **help document**, which can be accessed using the `help` function or the `?` operator - 


```r
# help(class)
# ?class
# ?TRUE
# ?pi
```



<!--chapter:end:01-lesson_01.Rmd-->

# Vectors {#vectors}



## Contents

* Using R code files
* Vector types
* Operations with vectors
* Functions with more than one argument
* Subsetting
* Missing values

## Aims

* Learning how to work with R code files
* Getting to know the simplest data structure in R, the vector
* Learning about subsetting, one of the fundamental operations with data

## Editing code

### Using code files

* Computer code is stored as **plain text**
* When writing computer code, we must use a **plain text editor**, such as **Notepad++** or **RStudio**
* A **word processor**, such as **Microsoft Word**, is not a good choice for writing code, because - 
    * Documents created with a Word Processor contain elements **other than** plain text (such as formatting), which are not processed, leading to confusion
    * Word processors can automatically **correct** "mistakes" thereby introducing unintended changes in our code, such as capitalizing: `max(1)` → `Max(1)`

* Any plain text file can be used to store **R code** 
* Conventionally, R code files have the `*.R` file **extension**
* **Complete** code files can be executed with `source`
* Selected **parts** of code can be executed by marking the section and pressing **Ctrl+Enter**
* Executing **one expression** can be done by standing inside it with the marker and pressing **Ctrl+Enter**

<div class="figure" style="text-align: center">
<img src="images/lesson_02_source.png" alt="Methods of executing R code" width="100%" />
<p class="caption">(\#fig:executing-r-code)Methods of executing R code</p>
</div>

For example, we can run the file `volcano.R` which draws a 3D image of a volcano (Figure \@ref(fig:image-volcano-3d)). 


```r
source("data/volcano.R")
```

<div class="figure" style="text-align: center">
<img src="02-lesson_02_files/figure-html/image-volcano-3d-1.png" alt="3D image of the `volcano` dataset" width="672" />
<p class="caption">(\#fig:image-volcano-3d)3D image of the `volcano` dataset</p>
</div>

### RStudio keyboard stortcuts

RStudio has numerous keyboard shortcuts for making it easier to edit and execute code files. Some useful RStudio keyboard shortcuts are given in Table \@ref(tab:rstudio-shortcuts). 

| Shortcut | Action | 
|---|---|
| **Alt+Shift+K** | List of all shortcuts |
| **Ctrl+1** | Moving cursor to the code editor | 
| **Ctrl+2** | Moving cursor to the console |
| **Ctrl+Enter** | Sending the current selection or line |
| **Ctrl+Shift+P** | Re-sending last selection
| **Ctrl+Alt+B** | Sending from top to current line |
| **Ctrl+Shift+C** | Turn comment on or off |
| **Tab** | Auto-complete |
| **Ctrl+D** | Delete line |
| **Ctrl+Shift+D** | Duplicate line |
| **Ctrl+F** | Find and replace menu |
| **Ctrl+S** | Save | 

Table: (\#tab:rstudio-shortcuts) RStudio keyboard shortcuts

## Assignment

* So far we have been using R by **typing** expressions into the command line and observing the result on screen
* That way R functions as a **"calculator"** - the results are not kept in computer memory

<img src="images/lesson_02_print.png" width="100%" style="display: block; margin: auto;" />

* Storing objects in the temporary computer memory (RAM) is called **assignment**
* Assignment is done using the **assignment operator** 

* In an **assignment expression** we are storing an object, under a certain name, in the RAM
* This is an essential operation in programming, because it make **automation** possible - reaching the goal step by step, while storing intermediate products
* An assignment expression consists of - 
    * The **expression** whose result we want to store
    * The assignment **operator**, `=` or `<-`
    * The **name** which will be assigned to the object
* For example - 


```r
rateEstimate = (6617747987 - 6617746521) / 10
```

<img src="images/lesson_02_assignment1.png" width="100%" style="display: block; margin: auto;" />

* When we type an **object name** in the console, R **accesses** an object stored under that name in the RAM, and **calls** the `print` function on the object - 


```r
rateEstimate
## [1] 146.6
```


```r
print(rateEstimate)
## [1] 146.6
```

<img src="images/lesson_02_assignment2.png" width="100%" style="display: block; margin: auto;" />

* What happens when we assign a new value to an **existing object**? The old object gets deleted, and its name is now pointing on the new value


```r
x = 55
x
## [1] 55
```


```r
x = "Hello"
x
## [1] "Hello"
```

* Note the difference between the `==` and `=` operators!
* `=` is an **assignment** operator - 


```r
one = 1
two = 2
one = two
one
## [1] 2
two
## [1] 2
```

* `==` is a logical operator for **comparison** - 


```r
one = 1
two = 2
one == two
## [1] FALSE
```

* Which user defined objects are currently **in memory**? The `ls` function returns a character vector with their names - 


```r
ls()
```

* Question: why do we write `ls()` and not `ls`?

## Vectors

### What is a vector?

* A vector is an **ordered** collection of values of the **same type**, such as - 
    * **Numbers** - `interger` or `numeric`
    * **Text** - `character`
    * **Logical** - `logical`
* Recall that these are the same three types of constant values we saw in **Lesson 01**; in fact a constant value is a vector of length 1
* We can create an **empty vector** using the `vector` function, specifying - 
    * `mode` - Type
    * `length` - Number of elements


```r
v = vector(mode = "numeric", length = 10)
v
##  [1] 0 0 0 0 0 0 0 0 0 0
```

### The `c` function

* Vectors can also be created with the `c` function, which **combines** the given vectors in the given order - 


```r
x = c(1, 2, 3)
x
## [1] 1 2 3
```


```r
c(x, 5)
## [1] 1 2 3 5
```

* Another example, with `character` values - 


```r
y = c("cat", "dog", "mouse", "apple")
y
## [1] "cat"   "dog"   "mouse" "apple"
```

### Vector subsetting

* We can access individual vector **elements** using the `[` operator and an index; in other words, to get a subset with an individual vector element -


```r
y[2]
## [1] "dog"
```


```r
y[3]
## [1] "mouse"
```

* Note: the index starts at `1`!

* Another example - 


```r
counts = c(2, 0, 3, 1, 3, 2, 9, 0, 2, 1, 11, 2)
counts[4]
## [1] 1
```

* Components of an expression for accessing a vector element - 

<img src="images/lesson_02_subset1.png" width="50%" style="display: block; margin: auto;" />

* We can also **assign** new values into a vector subset - 


```r
x = c(1, 2, 3)
x
## [1] 1 2 3
```


```r
x[2] = 300
x
## [1]   1 300   3
```

* Note: in this example we made an assignment into a subset with a single element; the same way, we can make an assignment into a subset of any length (see below)

### Calling functions on a vector

* There are various functions for calculating vector **properties** - 


```r
x = c(1, 6, 3, -8, 2)
```


```r
length(x)  # Number of elements
## [1] 5
min(x)     # Minimum
## [1] -8
max(x)     # Maximum
## [1] 6
range(x)   # Minimum, maximum
## [1] -8  6
mean(x)    # Average
## [1] 0.8
sum(x)     # Sum
## [1] 4
```

* Other functions operate on **each** vector element, returning a vector of results having the same length as the input - 


```r
sqrt(x)
## [1] 1.000000 2.449490 1.732051      NaN 1.414214
```


```r
abs(x)
## [1] 1 6 3 8 2
```

* Question: why does the result of the first expression contain `NaN`?

### The recycling rule

* Binary operations applied on two vectors are done **element-by-element**, and a vector of the results is returned - 


```r
c(1, 2, 3) * c(10, 20, 30)
## [1] 10 40 90
```

* What happens when the input vector lengths do not match? The shorter vector gets **"recycled"**

* For example, when one of the vectors is of length 3 and the other vector is of length 6, then the sorter (of length 3) is repeated 2 times until it matches the longer vector - 


```r
c(1, 2, 3)          + c(1, 2, 3, 4, 5, 6)
## [1] 2 4 6 5 7 9
```


```r
c(1, 2, 3, 1, 2, 3) + c(1, 2, 3, 4, 5, 6)
## [1] 2 4 6 5 7 9
```

<img src="images/lesson_02_recycle.png" width="50%" style="display: block; margin: auto;" />

* When one of the vectors is of length 1 and the other is of length 4, the shorter vector (of length 1) is replicated 4 times - 


```r
2             * c(1, 2, 3, 4)
## [1] 2 4 6 8
```


```r
c(2, 2, 2, 2) * c(1, 2, 3, 4)
## [1] 2 4 6 8
```

* When one of the vectors is of length 2 and the other is of length 4, the shorter vector (of length 2) is replicated 2 times - 


```r
c(10, 100)          + c(1, 2, 3, 4)
## [1]  11 102  13 104
```


```r
c(10, 100, 10, 100) + c(1, 2, 3, 4)
## [1]  11 102  13 104
```

* When longer vector length is not a multiple of the shorter one recycling is **"incomplete"** and we get a warning message -


```r
c(1, 2)    * c(1, 2, 3)
## Warning in c(1, 2) * c(1, 2, 3): longer object length is not a multiple of
## shorter object length
## [1] 1 4 3
```


```r
c(1, 2, 1) * c(1, 2, 3)
## [1] 1 4 3
```

* The recycling rule applies to many operators and functions, such as all arithmetic operators -


```r
x = c(1, 2, 3)
y = c(4, 5, 6)
```


```r
x + y
## [1] 5 7 9
```


```r
x - y
## [1] -3 -3 -3
```


```r
x * y
## [1]  4 10 18
```


```r
x / y
## [1] 0.25 0.40 0.50
```

### Consecutive and repetitive vectors

* Other than the `vector` and `c` functions, there are three commonly used methods for creating **consecutive** or **repetitive** vectors - 
    * The `:` operator
    * The `seq` function
    * The `rep` function

#### Consecutive vectors

* The `:` operator is used to create a vector of consecutive vectors in steps of `1` or `-1` - 


```r
1:10   # Steps of 1
##  [1]  1  2  3  4  5  6  7  8  9 10
```


```r
55:43  # Steps of -1
##  [1] 55 54 53 52 51 50 49 48 47 46 45 44 43
```

* The `seq` function creates a vector of consecutive values in any step size - 
    * `from` - Where to start
    * `to` - When to end
    * `by` - Step size
* For example - 


```r
seq(from = 100, to = 150, by = 10)
## [1] 100 110 120 130 140 150
```


```r
seq(from = 100, to = 80, by = -5)
## [1] 100  95  90  85  80
```

#### Repetitive vectors

* The `rep` function **replicates** its argument to create a repetitive vector - 
    * `x` - What to replicate
    * `times` - How many time to repeat `x`
    * `each` - How many times to repeat each element of `x`


```r
rep(x = 22, times = 10)
##  [1] 22 22 22 22 22 22 22 22 22 22
```


```r
rep(x = 22, each = 10)
##  [1] 22 22 22 22 22 22 22 22 22 22
```

* The `x` argument can be a vector of **length >1**
* Note the difference between the `times` and the `each` **parameters** - 


```r
rep(x = c(18, 0, 9), times = 3)
## [1] 18  0  9 18  0  9 18  0  9
```


```r
rep(x = c(18, 0, 9), each = 3)
## [1] 18 18 18  0  0  0  9  9  9
```

### Function calls

* Using the `seq` function we will demonstrate three properties of function calls
* **First**, we can omit parameter names as long as the arguments are passed in the default order - 


```r
seq(from = 5, to = 10, by = 1)
## [1]  5  6  7  8  9 10
```


```r
seq(5, 10, 1)
## [1]  5  6  7  8  9 10
```

* **Second**, we can use any argument order as long as parameter names are specified - 


```r
seq(to = 10, by = 1, from = 5)
## [1]  5  6  7  8  9 10
```


```r
seq(by = 1, from = 5, to = 10)
## [1]  5  6  7  8  9 10
```


```r
seq(from = 5, by = 1, to = 10)
## [1]  5  6  7  8  9 10
```

* **Third**, we can omit parameters that have a default value in the function definition - 


```r
seq(5, 10, 1)
## [1]  5  6  7  8  9 10
```


```r
seq(5, 10)
## [1]  5  6  7  8  9 10
```

* To find out what are the parameters of a particular function, their order or their default values, we can look into the documentation - 


```r
# ?seq
```

### Vector subsetting

* So far we created vector subsets using a `numeric` index which consists of a **single** value, such as - 


```r
x = c(43, 85, 10)
x[3]
## [1] 10
```

* We can also use a vector of **length >1** as an index - 


```r
x[1:2]
## [1] 43 85
```

* Note that the vector does not need to be consecutive, and can include repetitions - 


```r
x[c(1, 1, 3, 2)]
## [1] 43 43 10 85
```

* Another example - 


```r
counts = c(2, 0, 3, 1, 3)
counts[1:3]
## [1] 2 0 3
```

<img src="images/lesson_02_subset2.png" width="50%" style="display: block; margin: auto;" />

* Another example - 


```r
counts = c(2, 0, 3, 1, 3, 2, 9, 0, 2, 1, 11, 2)
counts[c(1:3, 7:9)]
## [1] 2 0 3 9 0 2
```

<embed src="images/lesson_02_subset3.pdf" width="75%" style="display: block; margin: auto;" type="application/pdf" />

* For the next examples, let's create a vector of all **even** numbers between 1 and 100 -


```r
x = seq(2, 100, 2)
x
##  [1]   2   4   6   8  10  12  14  16  18  20  22  24  26  28  30  32  34
## [18]  36  38  40  42  44  46  48  50  52  54  56  58  60  62  64  66  68
## [35]  70  72  74  76  78  80  82  84  86  88  90  92  94  96  98 100
```

* Question: what is the meaning of the numbers in square brackets when printing the vector?

* How many **elements** does `x` have?


```r
length(x)
## [1] 50
```

* What is the value of the **last** element in `x`?


```r
x[50]
## [1] 100
```


```r
x[length(x)]
## [1] 100
```

* Question: which of the last two expressions is preferable and why?

* How can we get the **entire** vector using subsetting with a `numeric` index?


```r
x[1:length(x)]
##  [1]   2   4   6   8  10  12  14  16  18  20  22  24  26  28  30  32  34
## [18]  36  38  40  42  44  46  48  50  52  54  56  58  60  62  64  66  68
## [35]  70  72  74  76  78  80  82  84  86  88  90  92  94  96  98 100
```

* How can we get the entire vector **except for** the last element?


```r
x[1:(length(x)-1)]
##  [1]  2  4  6  8 10 12 14 16 18 20 22 24 26 28 30 32 34 36 38 40 42 44 46
## [24] 48 50 52 54 56 58 60 62 64 66 68 70 72 74 76 78 80 82 84 86 88 90 92
## [47] 94 96 98
```

* Question: how can we get a reversed vector using a `numeric` index?

* When requesting an index **beyond** vector length we get `NA` -


```r
x[55]
## [1] NA
```


```r
x[1:80]
##  [1]   2   4   6   8  10  12  14  16  18  20  22  24  26  28  30  32  34
## [18]  36  38  40  42  44  46  48  50  52  54  56  58  60  62  64  66  68
## [35]  70  72  74  76  78  80  82  84  86  88  90  92  94  96  98 100  NA
## [52]  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA
## [69]  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA  NA
```

* Reminder: `NA` is a special value meaning *Not Available*

### The recycling rule

* Earlier, we saw the recycling rule with **arithmetic operators**
* The rule also applies to **assignment** - 


```r
counts = c(2, 0, 3, 1, 3, 2, 9, 0, 2, 1, 11, 2)
counts[c(1:3, 7:9)]
## [1] 2 0 3 9 0 2
```


```r
counts[c(1:3, 7:9)] = NA
counts
##  [1] NA NA NA  1  3  2 NA NA NA  1 11  2
```


```r
counts[c(1:3, 7:9)] = c(NA, 99)
counts
##  [1] NA 99 NA  1  3  2 99 NA 99  1 11  2
```

### Logical vectors

* The third common type of vectors are `logical` vectors
* A **logical vector** is composed of logical values: `TRUE` and `FALSE`
* For example - 


```r
c(TRUE, FALSE, FALSE)
## [1]  TRUE FALSE FALSE
```


```r
rep(TRUE, 7)
## [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE
```

* Usually, we will not be creating `logical` vectors **"manually"**, but through applying a **logical operator** on another vector -


```r
x = 1:5
x
## [1] 1 2 3 4 5
```


```r
x >= 3
## [1] FALSE FALSE  TRUE  TRUE  TRUE
```

* Note how the recycling rule applies to logical operators as well

* When arithmetic operations are applied to a `logical` vector, the `logical` vector is **converted** to a numeric one, where `TRUE` becomes `1` and `FALSE` becomes `0`
* For example - 


```r
sum(x >= 3)
## [1] 3
```


```r
mean(x >= 3)
## [1] 0.6
```

* Question: what is the meaning of the values `3` and `0.6` in the above example?

* We can use a `logical` vector as an **index** for subsetting - 


```r
counts = c(2, 0, 3, 1, 3)
```


```r
counts < 3
## [1]  TRUE  TRUE FALSE  TRUE FALSE
```


```r
counts[counts < 3]
## [1] 2 0 1
```

* The logical vector `counts<3` specifies whether **to include** each of the elements of `counts` in the resulting subset

<img src="images/lesson_02_subset_logical.png" width="50%" style="display: block; margin: auto;" />

* Using a `logical` index - 


```r
x = 1:5
```


```r
x[x >= 3]
## [1] 3 4 5
```


```r
x[x != 2]
## [1] 1 3 4 5
```


```r
x[x > 4 | x < 2]
## [1] 1 5
```


```r
x[x > 4 & x < 2]
## integer(0)
```

* Question: what happened in the last expression?

* The next example is slightly more complex: we select the elements of `z` whose square is larger than 8 - 


```r
z = c(5, 2, -3, 8)
z[z^2 > 8]
## [1]  5 -3  8
```

* `z^2` gives a vector of squared `z` values (`2` is recycled)


```r
z^2
## [1] 25  4  9 64
```

* Each of the squares is compared to 8 (`8` is recycled)


```r
z^2 > 8
## [1]  TRUE FALSE  TRUE  TRUE
```

* Finally, the latter `logical` vector is used for subsetting `z`

### Missing values

* The `is.na` function is used to detect **missing** (`NA`) values in a vector - 
    * Accepts a vector of **any type**
    * Returns a **logical** vector with `TRUE` in place of `NA` values and `FALSE` in place of non-`NA` values
* For example -


```r
x = c(28, 58, NA, 31, 39, NA, 9)
x
## [1] 28 58 NA 31 39 NA  9
```


```r
is.na(x)
## [1] FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE
```

* Many functions that **summarize** vector properties, such as `mean`, have the `na.rm` parameter
* The `na.rm` parameter can be used to **exclude** `NA` values from the calculation
* The default is `na.rm=FALSE`, meaning that `NA` values are **not** excluded
* For example - 


```r
x = c(28, 58, NA, 31, 39, NA, 9)
```


```r
mean(x)
## [1] NA
mean(x, na.rm = TRUE)
## [1] 33
```

* Question 1: why do we get `NA` in the first expression? 
* Question 2: what will be the result of `length(x)`?


```r
x = c(28, 58, NA, 31, 39, NA, 9)
x
## [1] 28 58 NA 31 39 NA  9
```

* Question: how can we replace the `NA` values in the above vector with the mean of its non-`NA` values?

### The `any` and `all` functions

* Sometimes we want to figure out whether - 
    * A `logical` vector contains **at least one** `TRUE` value
    * A `logical` vector is **entirely** composed of `TRUE` values
* We can use the `any` and `all` functions, respectively, for that

* The `any` function returns `TRUE` if **at least one** of the input vector values is `TRUE`, otherwise it returns `FALSE` - 


```r
x = 1:7
x
## [1] 1 2 3 4 5 6 7
```


```r
x > 5
## [1] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
any(x > 5)
## [1] TRUE
```


```r
x > 88
## [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
any(x > 88)
## [1] FALSE
```

* The `all` function returns `TRUE` if **all** of the input vector values are `TRUE`, otherwise it returns `FALSE` - 


```r
x = 1:7
x
## [1] 1 2 3 4 5 6 7
```


```r
x > 5
## [1] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
all(x > 5)
## [1] FALSE
```


```r
x > 0
## [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE
all(x > 0)
## [1] TRUE
```

### The `which` function

* The `which` function **converts** a `logical` vector to a `numeric` one with the indices of `TRUE` values
* That way we can find out the **index** of values that satisfy a given criterion
* For example - 


```r
x = c(2, 6, 2, 3, 0, 1)
x
## [1] 2 6 2 3 0 1
```


```r
x > 2.3
## [1] FALSE  TRUE FALSE  TRUE FALSE FALSE
```


```r
which(x > 2.3)
## [1] 2 4
```

### The `which.min` and `which.max` functions

* Related functions `which.min` and `which.max` return the **index** of the (first) **minimal** or **maximal** value in a vector
* For example - 


```r
x = c(2, 6, 2, 3, 0, 1, 6)
x
## [1] 2 6 2 3 0 1 6
```


```r
which.min(x)
## [1] 5
```


```r
which.max(x)
## [1] 2
```

* Question: how can we get **all** indices of the minimal or maximal value?

## The `order` function

* The `order` function returns **ordered** vector **indices**, based on the order of vector **values**
* In other words, `order` gives the index of the smallest value, the index of the second smallest value, and so on


```r
x = c(2, 6, 2, 3, 0, 1, 6)
x
## [1] 2 6 2 3 0 1 6
```


```r
order(x)
## [1] 5 6 1 3 4 2 7
```

* We can also get the **reverse** order with `decreasing=TRUE` - 


```r
order(x, decreasing = TRUE)
## [1] 2 7 4 1 3 6 5
```

* Question: how can we *sort* a vector using `order`?

### The `paste` and `paste0` functions

* The `paste` function is used to **"paste"** text values
* Its `sep` parameter determines the separating character(s), with default `sep=" "`


```r
paste("There are", "5", "books.")
## [1] "There are 5 books."
paste("There are", "5", "books.", sep = "_")
## [1] "There are_5_books."
```

* Non-character vectors are converted to `character` before pasting - 


```r
paste("There are", 80, "books.")
## [1] "There are 80 books."
```

* The recycling rule applies in `paste` too - 


```r
paste("image", 1:5, ".tif", sep = "")
## [1] "image1.tif" "image2.tif" "image3.tif" "image4.tif" "image5.tif"
```

* The `paste0` function is a shortcut for `paste` with `sep=""` - 


```r
paste0("image", 1:5, ".tif")
## [1] "image1.tif" "image2.tif" "image3.tif" "image4.tif" "image5.tif"
```

## Exercise 1 - Submission date **2018-11-25**







<!--chapter:end:02-lesson_02.Rmd-->

# Time series and function definitions {#time-series-and-function-definitions}



## Contents

* Dates
* Graphical functions
* Function definition

## Aims

* Working with data which represent time (date)
* Learn how to visualize our data with graphical functions
* Learn to define custom functions

## Working with dates

* In R, there are several special classes for representing **times** and **time-series** (time+data)
    * **Times**
        * `Date` 
        * `POSIXct` 
        * `POSIXlt`
    * **Time series** (time+data) 
        * `ts` 
        * `zoo` (package `zoo`)
        * `xts` (package `xts`)
* The simplest data structure for representing times is `Date`, used to represent **dates** (without time of day)

* For example, we can get the **current** date as a `Date` object with `Sys.Date` - 


```r
x = Sys.Date()
x
## [1] "2019-09-13"
```


```r
class(x)
## [1] "Date"
```

* We can convert `character` values in the **standard** date format `YYYY-MM-DD` to `Date`, using `as.Date` -


```r
as.Date("2014-10-20")
## [1] "2014-10-20"
```

* When the `character` values is in a **non-standard** format, we need to specify the format definition with `format`, using the various component symbols 
* Full list of format symbols in `?strptime`

| Symbol | Meaning |
|:---:|---|
| `%d` | day (`"15"`) |
| `%m` | month, numeric (`"08"`) |
| `%b` | month, 3-letter (`"Aug"`) |
| `%B` | month, full (`"August"`) |
| `%y` | Year, 2-digit (`14`) |
| `%Y` | Year, 4-digit (`2014`) |

Table: Common `Date` format components

* For example - 


```r
Sys.setlocale("LC_TIME", "C")
## [1] "C"
```


```r
as.Date("07/Aug/12")
## Error in charToDate(x): character string is not in a standard unambiguous format
as.Date("07/Aug/12", format = "%d/%b/%y")
## [1] "2012-08-07"
```


```r
as.Date("2012-August-07")
## Error in charToDate(x): character string is not in a standard unambiguous format
as.Date("2012-August-07", format = "%Y-%B-%d")
## [1] "2012-08-07"
```

* The opposite conversion, with `format`, lets us **extract** specific date components out of a `Date` object - 


```r
d = as.Date("1955-11-30")
d
## [1] "1955-11-30"
```


```r
format(d, "%d")
## [1] "30"
```


```r
format(d, "%B")
## [1] "November"
```


```r
as.numeric(format(d, "%Y"))
## [1] 1955
```


```r
format(d, "%m/%Y")
## [1] "11/1955"
```

* `Date` objects act like **numeric** vectors with respect to certain **operations** that make sense on dates
* **Logical** operators -


```r
Sys.Date() > as.Date("2013-01-01")
## [1] TRUE
```

* **Subtraction** -


```r
as.Date("2013-01-01") - as.Date("2012-01-01")
## Time difference of 366 days
```


```r
as.Date("2014-01-01") - as.Date("2013-01-01")
## Time difference of 365 days
```

* Creating **sequences** with the `seq` function - 


```r
seq(
  from = as.Date("2018-10-14"), 
  to = as.Date("2019-01-11"), 
  by = 7
)
##  [1] "2018-10-14" "2018-10-21" "2018-10-28" "2018-11-04" "2018-11-11"
##  [6] "2018-11-18" "2018-11-25" "2018-12-02" "2018-12-09" "2018-12-16"
## [11] "2018-12-23" "2018-12-30" "2019-01-06"
```

## Time series

* Let's define two `numeric` vectors: **water level** in Lake Kinneret, in **May** and in **November**, in each year during **1991-2011** -


```r
may = c(
  -211.92,-208.80,-208.84,-209.12,-209.01,-209.60,
  -210.24,-210.46,-211.76,-211.92,-213.13,-213.18,
  -209.74,-208.92,-209.73,-210.68,-211.10,-212.18,
  -213.26,-212.65,-212.37
)
nov = c(
  -212.79,-209.52,-209.72,-210.94,-210.85,-211.40,
  -212.01,-212.25,-213.00,-213.71,-214.78,-214.34,
  -210.93,-210.69,-211.64,-212.03,-212.60,-214.23,
  -214.33,-213.89,-213.68
)
```

* Question 1: what is the average water level in May? in November?
* Question 2: was the water level ever below `-213` (red line) in May? in November?
* Question 3: in which year or years was the water level below `-213` in May? in November?

* Question 2: was the water level ever below `-213` (red line) in May? in November?


```r
any(may < -213)
## [1] TRUE
```


```r
any(nov < -213)
## [1] TRUE
```

* Note: make sure there is a space between `<` and `-`, otherwise the combination is interpreted as an assignment operator `<-`

* Question 3: in which year or years was the water level below `-213` in May? in November?


```r
year = 1991:2011
year
##  [1] 1991 1992 1993 1994 1995 1996 1997 1998 1999 2000 2001 2002 2003 2004
## [15] 2005 2006 2007 2008 2009 2010 2011
```


```r
year[nov < -213]
## [1] 2000 2001 2002 2008 2009 2010 2011
```


```r
year[may < -213]
## [1] 2001 2002 2009
```

* Note: we created a logical vector `nov < -213` and used it to subset the corresponding `year` vector

## Tables


```r
data.frame(year, may, nov)
```


```
##    year     may     nov
## 1  1991 -211.92 -212.79
## 2  1992 -208.80 -209.52
## 3  1993 -208.84 -209.72
## 4  1994 -209.12 -210.94
## 5  1995 -209.01 -210.85
## 6  1996 -209.60 -211.40
## 7  1997 -210.24 -212.01
## 8  1998 -210.46 -212.25
## 9  1999 -211.76 -213.00
## 10 2000 -211.92 -213.71
## 11 2001 -213.13 -214.78
## 12 2002 -213.18 -214.34
## 13 2003 -209.74 -210.93
## 14 2004 -208.92 -210.69
## 15 2005 -209.73 -211.64
## 16 2006 -210.68 -212.03
## 17 2007 -211.10 -212.60
## 18 2008 -212.18 -214.23
## 19 2009 -213.26 -214.33
## 20 2010 -212.65 -213.89
## 21 2011 -212.37 -213.68
```

## Generic functions

* Some of the functions we learned about are **generic functions**
* Generic functions are functions that can accept arguments of different classes. What the function does depends on the class, according to the **method** defined for that class
* Advantages - 
    * Easier to remember function names
    * Possible to run the same code on different types of objects
* For example, `mean`, `print` and `plot` (below) are examples of generic functions
* When the `print` function gets a **vector** it prints the values, but when it gets a **raster** `RasterLayer` object its prints a summary of its properties

## Graphical functions

* The **graphical function** `plot`, given a vector, displays its values in a two dimensional plot where - 
    * Vector **indices** are on the x-axis 
    * Vector **values** are on the y-axis
* For example - 


```r
plot(nov, type = "b")
```

<div class="figure" style="text-align: center">
<img src="03-lesson_03_files/figure-html/unnamed-chunk-25-1.png" alt="Plot of the `nov` vector" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-25)Plot of the `nov` vector</p>
</div>

* Note: `type="b"` means **both** points and lines; Other useful options include - 
    * `type="p"` for points
    * `type="l"` for lines
    * `type="o"` for overplotted lines and points

* If we pass **two** vectors to `plot`, the first appears on the x-axis and the second - on the y-axis
* For example, we can put the years of water level measurement on the x-axis as follows - 


```r
plot(year, nov, type = "b")
```

<div class="figure" style="text-align: center">
<img src="03-lesson_03_files/figure-html/unnamed-chunk-26-1.png" alt="\texttt{nov} as function of \texttt{year}" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-26)\texttt{nov} as function of \texttt{year}</p>
</div>

* We can add a **horizontal line** displaying the red line using `abline` with the `h` parameter - 


```r
plot(year, nov, type = "b")
abline(h = -213)
```

* Note that `abline` draws in an **existing** graphical device, which is initiated with `plot`

<div class="figure" style="text-align: center">
<img src="03-lesson_03_files/figure-html/unnamed-chunk-28-1.png" alt="Adding a horizontal line with \texttt{abline}" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-28)Adding a horizontal line with \texttt{abline}</p>
</div>

* **Additional** "layers" can be added to an existing plot using functions such as `points` and `lines`
* We can also use **graphical parameters** to specify different style for each layer, such as `col` to determine point / line color
* In addition, we will set the y-axis **limit** with `ylim` to make sure both time series are within the displayed range
* `ylim` accepts a vector of length two: the minimum and the maximum -


```r
plot(year, nov, ylim = range(c(nov, may)), type = "b", col = "red")
lines(year, may, type = "b", col = "blue")
abline(h = -213)
```

<div class="figure" style="text-align: center">
<img src="03-lesson_03_files/figure-html/unnamed-chunk-29-1.png" alt="Adding a second series with \texttt{lines}" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-29)Adding a second series with \texttt{lines}</p>
</div>

* Finally, we can set the axis **labels** using the `xlab` and `ylab` parameters of the `plot` function - 


```r
plot(
  year, nov,
  xlab = "Year",
  ylab = "Water level (m)",
  ylim = range(c(nov, may)),
  type = "b", col = "red"
)
lines(year, may, type = "b", col = "blue")
abline(h = -213)
```

<div class="figure" style="text-align: center">
<img src="03-lesson_03_files/figure-html/unnamed-chunk-30-1.png" alt="Setting axis labels" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-30)Setting axis labels</p>
</div>

## Consecutive differences

* The `diff` function can be used to create a vector of **differences** between consecutive elements - 


```r
d_nov = c(NA, diff(nov))
d_nov
##  [1]    NA  3.27 -0.20 -1.22  0.09 -0.55 -0.61 -0.24 -0.75 -0.71 -1.07
## [12]  0.44  3.41  0.24 -0.95 -0.39 -0.57 -1.63 -0.10  0.44  0.21
```

* Note: we add `NA` to match the input vector `nov`

* Now we can find out which year had the biggest water level **increase** or **decrease** - 


```r
year[which.max(d_nov)]
## [1] 2003
```


```r
year[which.min(d_nov)]
## [1] 2008
```

* Note: `which.min` and `which.max` ignore `NA` values 

## Defining custom functions

* In **Lesson 01** we learned that a function call is an instruction to execute a certain function, as in - 


```r
f(arg1, arg2, ...)
```

* A **function** is an object containing code, which is loaded into the RAM and can be executed with specific parameters
* So far we met function defined in the **default** R packages (e.g. `seq`)
* Later on we will use functions from **external** packages (e.g. `left_join`)
* Now we learn how to define our own **custom** functions


```r
add_five = function(x) {
  x_plus_five = x + 5
  return(x_plus_five)
}
```

* Function name (`add_five`)
* Assignment operator (`=`)
* Function keyword (`function`)
* Parameter(s) (`(x)`)
* Brackets (`{`)
* Code (`x_plus_five = x + 5`)
* Returned value (`return(x_plus_five)`)
* Brackets (`}`)

* The idea is that the code inside the function gets **executed** each time the function is called - 


```r
# Function definition
add_five = function(x) {
  x_plus_five = x + 5
  return(x_plus_five)
}
```


```r
# Function call, with argument 5
add_five(5)
## [1] 10
```


```r
# Function call, with argument 7
add_five(7)
## [1] 12
```

* When we make a function call, the values we pass as function arguments are assigned to **local variables** which the function code can use
* The local variables are **not accessible** in the global environment - 


```r
x_plus_five
## Error in eval(expr, envir, enclos): object 'x_plus_five' not found
```

* Every function **returns** a value
* We can **assign** the returned value to a variable to keep it in memory for later use - 


```r
result = add_five(3)
result
## [1] 8
```

* We can **omit** the `return` expression -


```r
return(x_plus_five)
```

* In which case, the returned value is the **last expression** in the function body
* We can also omit the `{` and `}` parentheses in case the code consists of a **single expression**
* Therefore we could define the `add_five` function using **shorter** code - 


```r
add_five = function(x) x + 5
```

* **Default** parameter values can be given in the function definition
* In case there is a default value, we can **skip** that parameter in function calls - 


```r
add_five = function(x) x + 5
add_five()
## Error in add_five(): argument "x" is missing, with no default
```


```r
add_five = function(x = 1) x + 5
add_five()
## [1] 6
```

* There are **no restrictions** for the classes of objects a function can accept, as long as we did not set such restrictions ourselves
* However, we get an **error** if one of the expressions in the function code is illegal given the arguments - 


```r
add_five(1:3)
## [1] 6 7 8
```


```r
add_five("one")
## Error in x + 5: non-numeric argument to binary operator
```

* As another example, let's define a function named `first_last` which accepts a vector and returns the **difference** between the **last** and the **first** elements - 


```r
first_last = function(x) {
  x[length(x)] - x[1]
}
```


```r
first_last(1:3)
## [1] 2
```


```r
first_last(nov)
## [1] -0.89
```

* Question: write a function named `modify` that accepts three arguments - 
    * `x`
    * `index`
    * `value`
* The function assigns `value` into the element at `index` index of vector `x`
* The function returns the modified vector `x`
* For example - 




```r
v = 1:10
v
##  [1]  1  2  3  4  5  6  7  8  9 10
```


```r
modify(x = v, index = 3, value = 99)
##  [1]  1  2 99  4  5  6  7  8  9 10
```
















<!--chapter:end:03-lesson_03.Rmd-->

# Tables, conditionals and loops {#tables-conditionals-and-loops}



## Contents

* `data.frame` object
* Conditionals
* Loops
* The `apply` function
* Using R packages
* Joining tables

## Aims

* Learn to work with `data.frame`, the data structure used to represent tables in R
* Learn several automation methods for controlling code execution and automation in R - 
    * Conditionals
    * Loops
    * The `apply` function
* Install and use packages beyond "base R"
* Join between tables

## Preparation


```r
library(dplyr)
```

## Tables

### What is a table?

* A **table** in R is represented using the `data.frame` class
* A `data.frame` is basically a collection of **vectors** comprising columns, all of the **same size** but possibly of **different types**
* Conventionally - 
    * Each row represents an **observation**, with values possibly of a **different** type for each variable
    * Each column represents a **variable**, with values of the **same** type

<div class="figure" style="text-align: center">
<img src="images/lesson_04_table_in_excel.png" alt="\texttt{rainfall.csv} opened in Excel" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-3)\texttt{rainfall.csv} opened in Excel</p>
</div>

### Creating a `data.frame`

* A `data.frame` can be **created** with the `data.frame` function, given one or more vectors which become columns
* The `stringAsFactors=FALSE` argument *prevents* the conversion of **text columns** to `factor`, which is what we usually want


```r
d = data.frame(
  num = c(3, 7, 1),
  word = c("three", "seven", "one"),
  stringsAsFactors = FALSE
)
d
##   num  word
## 1   3 three
## 2   7 seven
## 3   1   one
```

## Interactive view of a `data.frame`

* The `View` function opens an **interactive view** of a `data.frame`
* When using RStudio, the view also has **sort** and **filter** buttons
* Note: sorting or filtering the view have no effect on the object

<div class="figure" style="text-align: center">
<img src="images/lesson_04_table_view.png" alt="Table view in Rstudio" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-5)Table view in Rstudio</p>
</div>

## `data.frame` properties

* We can get the number of **rows** and number of **columns** in a `data.frame` with `nrow` and `ncol`, respectively - 


```r
nrow(d)
## [1] 3
```


```r
ncol(d)
## [1] 2
```

* Or **both** of them as a vector of length 2 with `dim` - 


```r
dim(d)
## [1] 3 2
```

* `data.frame`s have row and column **names**, which we can get with `rownames` and `colnames`, respectively - 


```r
rownames(d)
## [1] "1" "2" "3"
```


```r
colnames(d)
## [1] "num"  "word"
```

* We can also **set** row or column names by assigning new values to these properties - 


```r
colnames(d)[1] = "Number"
d
##   Number  word
## 1      3 three
## 2      7 seven
## 3      1   one
```


```r
colnames(d)[1] = "num"
d
##   num  word
## 1   3 three
## 2   7 seven
## 3   1   one
```

* `str` gives a summary of the object **structure** - 


```r
str(d)
## 'data.frame':	3 obs. of  2 variables:
##  $ num : num  3 7 1
##  $ word: chr  "three" "seven" "one"
```

## `data.frame` subsetting

* A `data.frame` **subset** can be obtained with the `[` operator
* A `data.frame` is a two-dimensional object, therefore the index is composed of **two vectors** -
    * The first vector refers to **rows**
    * The second vector refers to **columns**
* Each of these vectors can be one of the following **types** - 
    * `numeric` - Specifying the **indices** of rows/columns to retain
    * `character` - Specifying the **names** of rows/columns to retain
    * `logical` - Specifying **whether** to retain each row/column
* The rows or column index can be **omitted**, in which case we get all rows or all columns, respectively


```r
d[1, 1]        # Row 1, column 1
## [1] 3

d[c(1, 3), 2]  # Rows 1 & 3, column 2
## [1] "three" "one"

d[2, ]         # Row 2
##   num  word
## 2   7 seven

d[, 2:1]       # Columns 2 & 1
##    word num
## 1 three   3
## 2 seven   7
## 3   one   1
```

* A subset with a **single column** can be returned as - 
    * A vector (`drop=TRUE`, the default)
    * A `data.frame` (`drop=FALSE`)
* For example - 


```r
d[1:2, 1]
## [1] 3 7
```


```r
d[1:2, 1, drop = FALSE]
##   num
## 1   3
## 2   7
```

* Question: why do you think this applies to a single column, rather than a single row?

* We can also use a `character` index to specify the **names** of rows and/or columns to retain in the subset - 


```r
d[, "num"]
## [1] 3 7 1
```

* The `$` operator is a shortcut for getting a **single column** from a `data.frame` -


```r
d$num
## [1] 3 7 1
```


```r
d$word
## [1] "three" "seven" "one"
```

Summary of subset operators in R:

| Syntax | Objects | Returns |
|---|---|---|
| `x[i]` | **vector**, **table**, **matrix**, **array**, **list** | Subset `i` | 
| `x[[i]]` | vectors, **lists** | Single element `i` | 
| `x$i` | **tables**, lists | Single element `i` | 
| `x@n` | S4 objects | Slot `n` | 

Table: Subset operators in R

* The third option for a `data.frame` index is a `logical` vector, specifying **whether** to retain each row or column
* Most commonly it is used to filter `data.frame` **rows** based on the values of one or more **columns** - 


```r
d[d$num == 1, ]
##   num word
## 3   1  one
```


```r
d[d$word == "seven" | d$word == "three", ]
##   num  word
## 1   3 three
## 2   7 seven
```

* Let's go back to the Kinneret example from **Lesson 03** - 


```r
may = c(
  -211.92,-208.80,-208.84,-209.12,-209.01,-209.60,
  -210.24,-210.46,-211.76,-211.92,-213.13,-213.18,
  -209.74,-208.92,-209.73,-210.68,-211.10,-212.18,
  -213.26,-212.65,-212.37
)
nov = c(
  -212.79,-209.52,-209.72,-210.94,-210.85,-211.40,
  -212.01,-212.25,-213.00,-213.71,-214.78,-214.34,
  -210.93,-210.69,-211.64,-212.03,-212.60,-214.23,
  -214.33,-213.89,-213.68
)
```

* Using these vectors we will construct the following `data.frame` - 


```r
kineret = data.frame(year = 1991:2011, may, nov)
```


```r
head(kineret)
##   year     may     nov
## 1 1991 -211.92 -212.79
## 2 1992 -208.80 -209.52
## 3 1993 -208.84 -209.72
## 4 1994 -209.12 -210.94
## 5 1995 -209.01 -210.85
## 6 1996 -209.60 -211.40
```

* Using a **logical index** we can get a subset of years when the Kinneret level in May was less than `-213` - 


```r
kineret[kineret$may < -213, "year"]  # Method 1
## [1] 2001 2002 2009
```


```r
kineret$year[kineret$may < -213]     # Method 2
## [1] 2001 2002 2009
```

* Similarly, we can get a subset with **all data** for those years - 


```r
kineret[kineret$may < -213, ]
##    year     may     nov
## 11 2001 -213.13 -214.78
## 12 2002 -213.18 -214.34
## 19 2009 -213.26 -214.33
```

## Creating new columns

* Assignment into a column which does not exist adds a **new column** - 


```r
kineret$d_nov = c(NA, diff(kineret$nov))
```


```r
head(kineret)
##   year     may     nov d_nov
## 1 1991 -211.92 -212.79    NA
## 2 1992 -208.80 -209.52  3.27
## 3 1993 -208.84 -209.72 -0.20
## 4 1994 -209.12 -210.94 -1.22
## 5 1995 -209.01 -210.85  0.09
## 6 1996 -209.60 -211.40 -0.55
```

## Flow control

* The default is to let the computer execute **all** expressions in the same **order** they are given in the code
* Flow control commands are a way to **modify** the sequence of code execution
* We learn two flow control operators, from two categories - 
    * `if` and `else` - A **conditional**, conditioning the execution of code
    * `for` - A **loop**, executing code more than once

### Conditionals

* The purpose of the **conditional** is to condition the execution of code
* An `if`-`else` conditional in R contains the following components - 
    * The `if` keyword
    * A condition
    * Code to be executed if the condition is `TRUE`
    * The `else` keyword (optional)
    * Code to be executed if the condition is `FALSE` (optional)
* The condition needs to be evaluated to a **single logical value** (`TRUE` or `FALSE`); If it is `TRUE` then the code section after `if` is executed

* Conditional with `if` - 


```r
if(condition) {
  expressions
}
```

* Conditional with `if` and `else` - 


```r
if(condition) {
  trueExpressions
} else {
  falseExpressions
}
```

* For example - 


```r
x = 3
x > 2
## [1] TRUE

if(x > 2) print("x is large!")
## [1] "x is large!"
```


```r
x = 0
x > 2
## [1] FALSE

if(x > 2) print("x is large!")
```

* Now also with `else`
* The first code section is executed when the condition is `TRUE` - 


```r
x = 3
if(x > 2) print("x is large!") else print("x is small!")
## [1] "x is large!"
```

* The second code section is executed when the condition is `FALSE` - 


```r
x = 1
if(x > 2) print("x is large!") else print("x is small!")
## [1] "x is small!"
```

* We can use a conditional to write our own version of the `abs` function - 


```r
abs2 = function(x) {
  if(x >= 0) return(x) else return(-x)
}
```

* For example - 


```r
abs2(-3)
## [1] 3
```


```r
abs2(24)
## [1] 24
```

* Question 1: what happens when the argument of `abs2` is of length >1?
* Question 2: write a function `is_myname` that checks if the given text is your name, returning `TRUE` or `FALSE`




```r
is_myname("Michael")
## [1] TRUE
is_myname("Yossi")
## [1] FALSE
```

### Loops

* A **loop** is used to execute a given code section more than once
* The number of **times** the code is executed is determined in different ways in different types of loops
* In a `for` loop, the number of times the code is executed is determined in advance based on the length of a **vector** passed to the loop
* The code is executed once for **each element** of the vector
* In each "round", the current element is assigned to a **variable** which we can use in the loop code

* A `for` loop is composed of the following parts - 
    * The `for` keyword
    * The variable name `symbol` getting the current vector value
    * The `in` keyword
    * The vector `sequence`
    * A code section `expressions`


```r
for(symbol in sequence) {
  expressions
}
```

* Note: the constant keywords are just `for` and `in`

* For example - 


```r
for(i in 1:5) print(i)
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
```

* The expression `print(i)` is executed 5 times, according to the length of the vector `1:5`
* Each time, `i` gets the next value of `1:5` and the code section prints `i` on screen

* The vector defining the `for` loop does not necessarily need to be numeric -


```r
for(b in c("Test", "One", "Two")) print(b)
## [1] "Test"
## [1] "One"
## [1] "Two"
```

* The expression `print(b)` is executed 3 times, according to the length of the vector `c("Test", "One", "Two")`
* Each time, `b` gets the next value of the vector and the code section prints `b` on screen

* In case the vector is numeric, it does not necessarily need to be composed of consecutive - 


```r
for(i in c(1,15,3)) print(i)
## [1] 1
## [1] 15
## [1] 3
```

* The expression `print(i)` is executed 3 times, according to the length of the vector `c(1,15,3)`
* Each time, `i` gets the next value of the vector and the code section prints `i` on screen

* The code section does not have to use the current value of the vector - 


```r
for(i in 1:5) print("A")
## [1] "A"
## [1] "A"
## [1] "A"
## [1] "A"
## [1] "A"
```

* The expression `print("A")` is executed 5 times, according to the length of the vector `1:5`
* Each time, the code section prints `"A"` on screen

* The following `for` loop prints each of the numbers from 1 to 10 multiplied by 5 - 


```r
for(i in 1:10) print(i * 5)
## [1] 5
## [1] 10
## [1] 15
## [1] 20
## [1] 25
## [1] 30
## [1] 35
## [1] 40
## [1] 45
## [1] 50
```

* Question: How can we prints a multiplication table for 1-10, using a `for` loop?


```
##  [1]  1  2  3  4  5  6  7  8  9 10
##  [1]  2  4  6  8 10 12 14 16 18 20
##  [1]  3  6  9 12 15 18 21 24 27 30
##  [1]  4  8 12 16 20 24 28 32 36 40
##  [1]  5 10 15 20 25 30 35 40 45 50
##  [1]  6 12 18 24 30 36 42 48 54 60
##  [1]  7 14 21 28 35 42 49 56 63 70
##  [1]  8 16 24 32 40 48 56 64 72 80
##  [1]  9 18 27 36 45 54 63 72 81 90
##  [1]  10  20  30  40  50  60  70  80  90 100
```

* As another example of using a `for` loop, we can write a function named `x_in_y` 
* The function accepts **two vectors** `x` and `y`
* For each **element** in `x` the function checks if it is **found** in `y`
* It returns a `logical` vector of the same length as `x`

* For example - 




```r
x_in_y(c(1, 2, 3, 4, 5), c(2, 1, 5))
## [1]  TRUE  TRUE FALSE FALSE  TRUE
```

* We can use a `for` **loop** to check if each element in `x` is contained in `y` - 


```r
x = c(1, 2, 3, 4, 5)
y = c(2, 1, 5)
```


```r
for(i in x) print(any(i == y))
## [1] TRUE
## [1] TRUE
## [1] FALSE
## [1] FALSE
## [1] TRUE
```

* In a function, we can **"collect"** the results into a vector instead of printing them on screen - 


```r
# Version 1
x_in_y = function(x, y) {
  result = NULL
  for(i in x) result = c(result, any(i == y))
  result
}
```


```r
# Version 2
x_in_y = function(x, y) {
  result = rep(NA, length(x))
  for(i in 1:length(x)) result[i] = any(x[i] == y)
  result
}
```

* In fact, we don't need to write a function such as `x_in_y` ourselves; we can use the `%in%` **operator**
* The `%in%` operator, with an expression `x %in% y`, returns a `logical` vector indicating the **presence** of each element of `x` in `y` -


```r
1:5 %in% c(1, 2, 5)
## [1]  TRUE  TRUE FALSE FALSE  TRUE
```


```r
1:5 %in% c(1, 2, 3, 5)
## [1]  TRUE  TRUE  TRUE FALSE  TRUE
```


```r
c("a", "B", "c", "ee") %in% letters
## [1]  TRUE FALSE  TRUE FALSE
```


```r
c("a", "B", "c", "ee") %in% LETTERS
## [1] FALSE  TRUE FALSE FALSE
```

## Reading table from a file

### Using `read.csv`

* The table `rainfall.csv` contains average **monthly rainfall** data (based on the period 1980-2010) for September-May, in 169 meteorological stations in Israel
* The table also contains station **name**, station **number**, **elevation** and **X-Y** coordinates

<div class="figure" style="text-align: center">
<img src="images/lesson_04_table_in_excel.png" alt="\texttt{rainfall.csv} opened in Excel" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-58)\texttt{rainfall.csv} opened in Excel</p>
</div>

* In addition to creating a table with `data.frame`, we can read an existing table **from disk**, such as from a Comma-Separated Values (CSV) file
* We can read a CSV file with `read.csv` - 


```r
# Windows
read.csv("C:\\Data2\\rainfall.csv")
read.csv("C:/Data2/rainfall.csv")

# Mac / Linux
read.csv("~/Dropbox/Data2/rainfall.csv")
```

<img src="images/lesson_04_import.png" width="40%" style="display: block; margin: auto;" />

* Note: the separating character on Windows is `/` or `\\`, not the familiar `\`
* In case the file path uses the **incorrect separator** `\` we get an error - 


```r
read.csv("C:\Data2\rainfall.csv")
## Error: '\D' is an unrecognized escape in character string starting ""C:\D"
```

* In case the file **does not exist** we get a different error - 


```r
read.csv("C:\\Data2\\rainfall.csv")
## Warning in file(file, "rt"): cannot open file 'C:\Data2\rainfall.csv': No
## such file or directory
## Error in file(file, "rt"): cannot open the connection
```

* The `stringsAsFactors` parameter of `read.csv` (and several other functions) determines whether **text columns** are converted to `factor` (default is `TRUE`)
* Usually, we want to **avoid** the conversion with `stringsAsFactors=FALSE`


```r
read.csv(
  "~/Dropbox/Data2/rainfall.csv", 
  stringsAsFactors = FALSE
)
```

### The working directory

* R always points to a certain directory, knows as the **working directory**
* We can **get** the current working directory with `getwd` - 


```r
getwd()
## [1] "/home/michael/Dropbox/Courses/R_2019"
```

* We can **set** a new working directory with `setwd` - 


```r
setwd("~/Dropbox/Data2")
```

* When **reading a file** from the working directory, we can specify just the **file name** instead of the full path - 


```r
read.csv("rainfall.csv")
```

### Example: the `rainfall.csv` dataset structure

* Let's **read** the `rainfall.csv` file - 


```r
rainfall = read.csv(
  "rainfall.csv", 
  stringsAsFactors = FALSE
)
```



* We can also use the `head` or `tail` function which return a subset of the **first** or **last** several rows, respectively - 


```r
head(rainfall)
##      num altitude sep oct nov dec jan feb mar apr may              name
## 1 110050       30 1.2  33  90 117 135 102  61  20 6.7 Kfar Rosh Hanikra
## 2 110351       35 2.3  34  86 121 144 106  62  23 4.5              Saar
## 3 110502       20 2.7  29  89 131 158 109  62  24 3.8             Evron
## 4 111001       10 2.9  32  91 137 152 113  61  21 4.8       Kfar Masrik
## 5 111650       25 1.0  27  78 128 136 108  59  21 4.7     Kfar Hamakabi
## 6 120202        5 1.5  27  80 127 136  95  49  19 2.7        Haifa Port
##      x_utm   y_utm
## 1 696533.1 3660837
## 2 697119.1 3656748
## 3 696509.3 3652434
## 4 696541.7 3641332
## 5 697875.3 3630156
## 6 687006.2 3633330
```

* We can also use the `head` or `tail` function which return a subset of the **first** or **last** several rows, respectively - 


```r
tail(rainfall)
##        num altitude sep oct nov dec jan feb mar apr may        name
## 164 321800     -180 0.2  12  37  55  65  59  36  11 5.0 Sde Eliyahu
## 165 321850     -220 0.2  13  33  53  64  56  35  11 4.7   Tirat Zvi
## 166 330370     -375 0.1   6  10  20  22  19  11   6 1.3       Kalya
## 167 337000     -390 0.0   5   3  10   7   7   7   3 0.5        Sdom
## 168 345005       80 0.4   2   2   6   5   4   5   2 0.4     Yotveta
## 169 347702       11 0.0   4   2   5   4   3   3   2 1.0       Eilat
##        x_utm   y_utm
## 164 736189.3 3591636
## 165 737522.4 3590062
## 166 733547.8 3515345
## 167 728245.6 3435503
## 168 700626.3 3307819
## 169 689139.3 3270290
```

* We can check the table **structure** with `str` - 


```r
str(rainfall)
## 'data.frame':	169 obs. of  14 variables:
##  $ num     : int  110050 110351 110502 111001 111650 120202 120630 120750 120870 121051 ...
##  $ altitude: int  30 35 20 10 25 5 450 30 210 20 ...
##  $ sep     : num  1.2 2.3 2.7 2.9 1 1.5 1.9 1.6 1.1 1.8 ...
##  $ oct     : int  33 34 29 32 27 27 36 31 32 32 ...
##  $ nov     : int  90 86 89 91 78 80 93 91 93 85 ...
##  $ dec     : int  117 121 131 137 128 127 161 163 147 147 ...
##  $ jan     : int  135 144 158 152 136 136 166 170 147 142 ...
##  $ feb     : int  102 106 109 113 108 95 128 146 109 102 ...
##  $ mar     : int  61 62 62 61 59 49 71 76 61 56 ...
##  $ apr     : int  20 23 24 21 21 19 21 22 16 13 ...
##  $ may     : num  6.7 4.5 3.8 4.8 4.7 2.7 4.9 4.9 4.3 4.5 ...
##  $ name    : chr  "Kfar Rosh Hanikra" "Saar" "Evron" "Kfar Masrik" ...
##  $ x_utm   : num  696533 697119 696509 696542 697875 ...
##  $ y_utm   : num  3660837 3656748 3652434 3641332 3630156 ...
```

* Question: create a plot of rainfall in January (`jan`) as function of elevation (`altitude`) based on the `rainfall` table

<div class="figure" style="text-align: center">
<img src="04-lesson_04_files/figure-html/unnamed-chunk-72-1.png" alt="Rainfall in January as function of elevation" width="65%" />
<p class="caption">(\#fig:unnamed-chunk-72)Rainfall in January as function of elevation</p>
</div>

* We can get specific information from the table trough **subsetting** and **summarizing**
* What is the elevation of the lowest and highest stations?


```r
min(rainfall$altitude)
## [1] -390
```


```r
max(rainfall$altitude)
## [1] 955
```

* What is the name of the lowest and highest station?


```r
rainfall$name[which.min(rainfall$altitude)]
## [1] "Sdom"
```


```r
rainfall$name[which.max(rainfall$altitude)]
## [1] "Rosh Tzurim"
```

* How much rainfall does the `"Haifa University"` station receive in April?


```r
rainfall$apr[rainfall$name == "Haifa University"]
## [1] 21
```

* We can create a **new column** through assignment - 


```r
rainfall$sep_oct = rainfall$sep + rainfall$oct
```

* To accomodate more complex calculations, we can also create a new column inside a `for` **loop** going over table **rows** - 


```r
m = c(
  "sep", "oct", "nov", "dec", "jan",
  "feb", "mar", "apr", "may"
)
for(i in 1:nrow(rainfall)) {
  rainfall$annual[i] = sum(rainfall[i, m])
}
```


```r
head(rainfall)
##      num altitude sep oct nov dec jan feb mar apr may              name
## 1 110050       30 1.2  33  90 117 135 102  61  20 6.7 Kfar Rosh Hanikra
## 2 110351       35 2.3  34  86 121 144 106  62  23 4.5              Saar
## 3 110502       20 2.7  29  89 131 158 109  62  24 3.8             Evron
## 4 111001       10 2.9  32  91 137 152 113  61  21 4.8       Kfar Masrik
## 5 111650       25 1.0  27  78 128 136 108  59  21 4.7     Kfar Hamakabi
## 6 120202        5 1.5  27  80 127 136  95  49  19 2.7        Haifa Port
##      x_utm   y_utm sep_oct annual
## 1 696533.1 3660837    34.2  565.9
## 2 697119.1 3656748    36.3  582.8
## 3 696509.3 3652434    31.7  608.5
## 4 696541.7 3641332    34.9  614.7
## 5 697875.3 3630156    28.0  562.7
## 6 687006.2 3633330    28.5  537.2
```

## The `apply` function

* The `apply` function can **replace** `for` loops, in situations when we are interested in applying the **same function** on all subsets of certain **dimension** of a `data.frame`, a `matrix` or an `array`
* In case of a table, there are two **dimensions** we can work on - 
    * **Rows** = Dimension `1`
    * **Columns** = Dimension `2`
* The `apply` function needs three arguments - 
    * `X` - The **object** we are working on: `data.frame`, `matrix` or `array`
    * `MARGIN` - The **dimension** we are working on
    * `FUN` - The **function** applied on that dimension

<div class="figure" style="text-align: center">
<img src="images/lesson_04_apply.png" alt="The `apply` function, operating on columns (left) or rows (rigth)" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-81)The `apply` function, operating on columns (left) or rows (rigth)</p>
</div>

* For example, the `apply` function can replace a `for` loop for calculating **average** annual rainfall **per station**
* The `sum` function is applied on the **rows** dimension - 


```r
rainfall$annual = apply(
  X = rainfall[, m], 
  MARGIN = 1, 
  FUN = sum
)
```

* As another example, we can calculate **average** monthly rainfall **per month**
* This time, the `mean` function is applied on the **columns** dimension - 


```r
avg_rain = apply(rainfall[, m], 2, mean)
```

* The result `avg_rain` is a **named** `numeric` vector
* Element names correspond to **column** names of `X` - 


```r
avg_rain
##        sep        oct        nov        dec        jan        feb 
##   1.025444  21.532544  64.852071 105.798817 123.053254 103.130178 
##        mar        apr        may 
##  58.366864  16.769231   3.968639
```

* We can quickly visualize the values with `barplot` - 


```r
barplot(avg_rain)
```

<div class="figure" style="text-align: center">
<img src="04-lesson_04_files/figure-html/unnamed-chunk-86-1.png" alt="Average rainfall per month, among 169 stations in Israel" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-86)Average rainfall per month, among 169 stations in Israel</p>
</div>

* As another example, let's use `apply` to find the station **name** with the **highest** rainfall **per month**
* The following applies `which.max` on the columns, returning the row **indices** where the maximal rainfall values are located per column - 


```r
max_st = apply(rainfall[, m], 2, which.max)
max_st
## sep oct nov dec jan feb mar apr may 
##  71  23  77  77  77  66  66  66  77
```

* We can get the corresponding station **names** by subsetting the `name` column using `max_st` - 


```r
rainfall$name[max_st]
## [1] "Eilon"      "Maabarot"   "Horashim"   "Horashim"   "Horashim"  
## [6] "Golan Farm" "Golan Farm" "Golan Farm" "Horashim"
```

* It is convenient to **combine** the names and values in a table - 


```r
data.frame(
  month = m,
  name = rainfall$name[max_st],
  stringsAsFactors = FALSE
)
##   month       name
## 1   sep      Eilon
## 2   oct   Maabarot
## 3   nov   Horashim
## 4   dec   Horashim
## 5   jan   Horashim
## 6   feb Golan Farm
## 7   mar Golan Farm
## 8   apr Golan Farm
## 9   may   Horashim
```

## Joining tables

* The `dates.csv` table contains the **dates** when each image in the raster `modis_south.tif`, which we will work with in **Lesson 05**, was taken - 


```r
dates = read.csv("data/dates.csv", stringsAsFactors = FALSE)
```


```r
head(dates)
##   day month year
## 1  18     2 2000
## 2   5     3 2000
## 3  21     3 2000
## 4   6     4 2000
## 5  22     4 2000
## 6   8     5 2000
```

* For further analysis of the images we would like to be able to group them **by season**
* How can we calculate a new `season` **column**, specifying the season each date belongs to?

| season | months | 
|---|---|
| `"winter"` | `12`, `1`, `2` |
| `"spring"` | `3`, `4`, `5` |
| `"summer"` | `6`, `7`, `8` |
| `"fall"` | `9`, `10`, `11` |

Table: Months and seasons

* One way is to **assign** each season name into a **subset** of a new `season` column - 


```r
dates$season[dates$month %in% c(12, 1:2)] = "winter"
dates$season[dates$month %in% 3:5] = "spring"
dates$season[dates$month %in% 6:8] = "summer"
dates$season[dates$month %in% 9:11] = "fall"
```


```r
head(dates)
##   day month year season
## 1  18     2 2000 winter
## 2   5     3 2000 spring
## 3  21     3 2000 spring
## 4   6     4 2000 spring
## 5  22     4 2000 spring
## 6   8     5 2000 spring
```

* This method of classification may be inconvenient when we have many categories or complex criteria
* Another option is to use a **table join**

## Using R packages

* All object definitions (including functions) in R are contained in **packages**
* To use a particular object, we need to -
    * **Install** the package with `install.packages` (once)
    * **Load** the package using the `library` function (in each new R session)
    * Loading a package basically means the code we downloaded is **executed**, loading all objects the package defined into the **RAM**
* All function calls we used until now did require this. Why? Because several packages are **installed** along with R and **loaded** on R start-up
* There are several more packages which are installed by default but **not loaded** on start-up (total of ~30)

<div class="figure" style="text-align: center">
<img src="images/lesson_04_r_packages_a.svg" alt="Packages included with R" width="30%" />
<p class="caption">(\#fig:unnamed-chunk-94)Packages included with R</p>
</div>

R in a Nutshell, 2010

<embed src="images/lesson_04_r_packages_a.pdf" width="100%" style="display: block; margin: auto;" type="application/pdf" />

* **Most** of the ~13,000 R packages (Sep 2018) are *not* installed by default
* To use one of these packages we first need to **install** it on the computer
* This is a **one-time** operation using the `install.packages` function
* After the package is installed, each time we want to use it we need to **load** it using `library`

* In the next example we use a package called `dplyr`
* This package is not installed with R, we need to **install** it ourselves -


```r
install.packages("dplyr")
```

* Note: if the package is already installed then `install.packages` **overwrites** the old installation
* Once the package is already installed, we need to use the `library` function to **load** it into memory - 


```r
library(dplyr)
```

* Note: package name can be passed to `library` **without** quotes

## Example: season classification

* The `left_join` function from `dplyr` does a **left join** between tables
* The first two parameters are the **tables** that need to be joined, `x` and `y`
* The third `by` parameter is the common **column name(s)** by which the tables need to be joined

<div class="figure" style="text-align: center">
<img src="images/lesson_04_join_types.png" alt="Join types" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-98)Join types</p>
</div>

http://r4ds.had.co.nz/relational-data.html

* Next we prepare a table `tab` with the **classification** of months into seasons - 


```r
tab = data.frame(
  month = c(12, 1:11),
  season = rep(c("winter","spring","summer","fall"), each = 3),
  stringsAsFactors = FALSE
)
```

* Next we prepare a table `tab` with the classification of months into seasons - 


```r
tab
```


```
##    month season
## 1     12 winter
## 2      1 winter
## 3      2 winter
## 4      3 spring
## 5      4 spring
## 6      5 spring
## 7      6 summer
## 8      7 summer
## 9      8 summer
## 10     9   fall
## 11    10   fall
## 12    11   fall
```

* Now we can **join** the `dates` and `tab` tables 
* Before that, we **remove** the `season` column we manually created in the previous example -


```r
dates$season = NULL
dates = left_join(dates, tab, by = "month")
```


```r
head(dates)
##   day month year season
## 1  18     2 2000 winter
## 2   5     3 2000 spring
## 3  21     3 2000 spring
## 4   6     4 2000 spring
## 5  22     4 2000 spring
## 6   8     5 2000 spring
```

* To get a **date** column we can paste the `year`, `month` and `day` columns and apply `as.Date` - 


```r
dates$date = as.Date(
  paste(dates$year, dates$month, dates$day, sep = "-")
)
```


```r
head(dates)
##   day month year season       date
## 1  18     2 2000 winter 2000-02-18
## 2   5     3 2000 spring 2000-03-05
## 3  21     3 2000 spring 2000-03-21
## 4   6     4 2000 spring 2000-04-06
## 5  22     4 2000 spring 2000-04-22
## 6   8     5 2000 spring 2000-05-08
```

## Writing tables to file

* Using `write.csv` we can **write** the contents of a `data.frame` to a **CSV file** -


```r
write.csv(dates, "data/dates2.csv", row.names = FALSE)
```

* The `row.names` parameter determines whether the **row names** are saved
* Note: like in `read.csv`, we can either give a **full** file path or just the **file name**; if the specify just the file name then the file is written to the **working directory**

<embed src="images/lesson_04_export.pdf" width="40%" style="display: block; margin: auto;" type="application/pdf" />

## Exercise 2 - Submission date **2018-12-09**



























<!--chapter:end:04-lesson_04.Rmd-->

# Matrices and rasters {#matrices-and-rasters}



## Contents

* `matrix` and `array` objects
* Rasters
* Raster properties
* Reading and writing rasters

## Aims

* We start working with spatial data (rasters)
* Introducing the basic `matrix` and `array` data structures, and their analogous spatial data structures - single band rasters and multi-band rasters, respectively
* Learn about accessing the values and properties of rasters
* Learn to read and write raster data

## Matrices

* A `matrix` is a **two-dimensional** collection of values of the **same type** (like a vector), where the number of values in all rows is equal
* It is important to know how to work with matrices because - 
    * It is a **commonly** used structure with many uses in data processing
    * Many R function **accept** a `matrix` as an argument (e.g. `focal`)
    * Many R functions **return** a `matrix` (e.g. `extract`)

### Creating a `matrix`

* A `matrix` can be **created** with the `matrix` function
* The `matrix` function accepts the following parameters - 
    * `data` - A vector of the **values** to fill into the matrix
    * `nrow` - The number of **rows**
    * `ncol` - The number of **columns**
    * `byrow` - Whether the matrix is filled **by row** (`TRUE`) or **by column** (`FALSE`, the default)
* For example - 


```r
matrix(1:6, ncol = 3)
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

* The `nrow` and `ncol` parameters determine the number of **rows** and number of **columns**, respectively - 


```r
matrix(1:6, nrow = 3)
##      [,1] [,2]
## [1,]    1    4
## [2,]    2    5
## [3,]    3    6
```


```r
matrix(1:6, nrow = 2)
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

* The `nrow` and `ncol` parameters determine the number of **rows** and number of **columns**, respectively - 


```r
matrix(1:6, ncol = 3)
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
matrix(1:6, ncol = 2)
##      [,1] [,2]
## [1,]    1    4
## [2,]    2    5
## [3,]    3    6
```

* Question 1: create a `matrix` with 3 rows and 4 columns which contains the numbers 12-1 in decreasing order


```
##      [,1] [,2] [,3] [,4]
## [1,]   12    9    6    3
## [2,]   11    8    5    2
## [3,]   10    7    4    1
```

* Question 2: what do you think will happen when we try to create a matrix with less or more `data` values than matrix size `nrow*ncol`?


```r
matrix(12:1, ncol = 4, nrow = 2)
matrix(12:1, ncol = 4, nrow = 4)
```

* Question 3: create a 3×3 matrix where all values are 1/9

### Matrix properties

* The `length` function returns the number of **values** in a `matrix` - 


```r
x = matrix(1:6, ncol = 3)
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
length(x)
## [1] 6
```

* The `nrow` and `ncol` functions return the number of **rows** and **columns** in a `matrix`, respectively - 


```r
x = matrix(1:6, ncol = 3)
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
nrow(x)
## [1] 2
```


```r
ncol(x)
## [1] 3
```

* For example, the built-in `matrix` named `volcano` contains **elevation** data
* Let's check its **dimensions** - 


```r
nrow(volcano)
## [1] 87
```


```r
ncol(volcano)
## [1] 61
```


```r
length(volcano)
## [1] 5307
```

* The `dim` function gives both **dimensions** of the `matrix` as a vector of length 2, i.e. number of rows and columns, respectively - 


```r
x = matrix(1:6, ncol = 3)
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
dim(x)
## [1] 2 3
```

* The `rownames` and `colnames` functions return the **row names** and **column names**, respectively
* The row and column names can also be **modified** by assignment to these properties


```r
x = matrix(1:6, ncol = 3)
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
rownames(x) = c("A", "B")
x
##   [,1] [,2] [,3]
## A    1    3    5
## B    2    4    6
```

### Matrix to vector conversion

* The `as.vector` function converts a `matrix` to a **vector**


```r
x = matrix(1:6, ncol = 3, byrow = TRUE)
x
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    4    5    6
```


```r
as.vector(x)
## [1] 1 4 2 5 3 6
```

* Note: `matrix` values are always arranged by column!

### Matrix to `data.frame` conversion

* The `as.data.frame` function converts a `matrix` to a **table** - 


```r
x = matrix(1:6, ncol = 3)
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
as.data.frame(x)
##   V1 V2 V3
## 1  1  3  5
## 2  2  4  6
```

### Transposing a matrix

* The `t` function **transposes** a `matrix`: it flips the rows and columns - 


```r
x = matrix(1:6, ncol = 3)
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
t(x)
##      [,1] [,2]
## [1,]    1    2
## [2,]    3    4
## [3,]    5    6
```

* Question: what will be the result of `t(t(x))`?

### Image with contours

* Using the `image` and `contour` functions we can graphically **display** `matrix` values
* The **color scale** can be set with `col` and the x/y **aspect ratio** can be set with `asp` -


```r
image(
  volcano,
  col = terrain.colors(30),
  asp = ncol(volcano) / nrow(volcano)
)
contour(
  volcano,
  add = TRUE
)
```

<div class="figure" style="text-align: center">
<img src="05-lesson_05_files/figure-html/unnamed-chunk-27-1.png" alt="Volcano image with contours" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-27)Volcano image with contours</p>
</div>

### Matrix subsetting

* Similarly to what we learned about `data.frame`, `matrix` **indices** are two-dimensional
* The first value refers to **rows** and the second value refers to **columns**


```r
x = matrix(1:6, ncol = 3)
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
x[2, 1]
## [1] 2
x[1, 3]
## [1] 5
x[4, 4]
## Error in x[4, 4]: subscript out of bounds
```

* Another example - 


```r
volcano[20, 40]  # Row 20, column 40
## [1] 190
```


```r
volcano[81, 61]  # Row 81, column 61
## [1] 95
```


```r
volcano[1, 5]    # Row 1, column 5
## [1] 101
```

* **Complete** rows or columns can be accessed by leaving a blank space instead of the row or column index
* By default, a subset that comes from a single row or a single column is **simplified** to a vector - 


```r
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
x[2, ]
## [1] 2 4 6
```


```r
x[ ,2]
## [1] 3 4
```

* To **"suppress"** the simplification of individual rows/columns to a vector, we can use the `drop=FALSE` argument - 


```r
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
x[2, , drop = FALSE]
##      [,1] [,2] [,3]
## [1,]    2    4    6
```


```r
x[, 2, drop = FALSE]
##      [,1]
## [1,]    3
## [2,]    4
```

* When referring to an elevation matrix such as `volcano`, a row or column is actually an elevation **profile**
* For example - 


```r
r30 = volcano[30, ]
r70 = volcano[70, ]
```

* Plot - 


```r
plot(
  r30,
  type = "o", 
  col = "blue", 
  ylim = range(c(r30, r70)),
  xlab = "Column",
  ylab = "Elevation (m)"
)
lines(
  r70, 
  type = "o", 
  col = "red"
)
```

<div class="figure" style="text-align: center">
<img src="05-lesson_05_files/figure-html/unnamed-chunk-40-1.png" alt="Rows 30 (blue) and 70 (red) from the `volcano` matrix" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-40)Rows 30 (blue) and 70 (red) from the `volcano` matrix</p>
</div>

<div class="figure" style="text-align: center">
<img src="05-lesson_05_files/figure-html/unnamed-chunk-41-1.png" alt="Rows 30 and 70 in the `volcano` matrix" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-41)Rows 30 and 70 in the `volcano` matrix</p>
</div>

* We can also use vectors of **length >1** when subsetting - 


```r
x = matrix(1:6, ncol = 3)
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
x[, 1:2]
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```

* We can also use vectors of **length >1** when subsetting - 


```r
x = matrix(1:6, ncol = 3)
x
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


```r
x[2, c(1,3)]
## [1] 2 6
```


```r
x[2, c(1,3), drop = FALSE]
##      [,1] [,2]
## [1,]    2    6
```

* We can **assign** new values to subsets of a `matrix` - 


```r
m = matrix(NA, ncol = 3, nrow = 3)
```


```r
m[2:3, 1:2] = 1
m
##      [,1] [,2] [,3]
## [1,]   NA   NA   NA
## [2,]    1    1   NA
## [3,]    1    1   NA
```


```r
m[1:2, 2:3] = 100
m
##      [,1] [,2] [,3]
## [1,]   NA  100  100
## [2,]    1  100  100
## [3,]    1    1   NA
```

### Summarizing rows and columns

* How can we calculate the row or column **means** of a matrix?
* One way is to use a `for` **loop** -


```r
result = rep(NA, nrow(volcano))
for(i in 1:nrow(volcano)) {
  result[i] = mean(volcano[i, ])
}
```

* Plot - 


```r
plot(result, xlab = "Row", ylab = "Elevation (m)")
```

* Question: what changes do we need to make in the code to calculate *column* means?

<div class="figure" style="text-align: center">
<img src="05-lesson_05_files/figure-html/unnamed-chunk-52-1.png" alt="Row means of the `volcano` matrix" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-52)Row means of the `volcano` matrix</p>
</div>

* A **shorter** way to do the same with `apply` - 


```r
result = apply(volcano, 1, mean)
```

* For the special cases of `mean` there are further **shortcuts** `rowMeans` and `colMeans` - 


```r
result = rowMeans(volcano)
```

* Note: in both cases we can use `na.rm` to determine whether `NA` values are included in the calculation (default is `FALSE`)

* Question 1: does the `volcano` matrix contains `NA`s? How can we make sure?
* Question 2: how can we check whether the above two expressions give exactly the same result?

## Arrays

* An **array** is a data structure that contains values of the **same type** and can have any number of **dimensions**
* We may consider a vector (1 dimension) and a `matrix` (2 dimensions) as **special cases** of an array

* An `array` object can be **created** with the `array` function, specifying the values and the required dimensions - 


```r
y = array(1:24, c(2, 3, 4))
```

<div class="figure" style="text-align: center">
<img src="images/lesson_05_array.png" alt="An `array` with 2 rows, 3 columns and 4 &quot;layers&quot;" width="25%" />
<p class="caption">(\#fig:unnamed-chunk-56)An `array` with 2 rows, 3 columns and 4 "layers"</p>
</div>


```
## , , 1
## 
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
## 
## , , 2
## 
##      [,1] [,2] [,3]
## [1,]    7    9   11
## [2,]    8   10   12
## 
## , , 3
## 
##      [,1] [,2] [,3]
## [1,]   13   15   17
## [2,]   14   16   18
## 
## , , 4
## 
##      [,1] [,2] [,3]
## [1,]   19   21   23
## [2,]   20   22   24
```

* Arrays subsetting - 


```r
y[1, , ]  # 1st dimension
##      [,1] [,2] [,3] [,4]
## [1,]    1    7   13   19
## [2,]    3    9   15   21
## [3,]    5   11   17   23
```

<div class="figure" style="text-align: center">
<img src="images/lesson_05_array_subset1.png" alt="`array` subsetting" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-59)`array` subsetting</p>
</div>

* Arrays subsetting - 


```r
y[, 1, ]  # 2nd dimension
##      [,1] [,2] [,3] [,4]
## [1,]    1    7   13   19
## [2,]    2    8   14   20
```

* Arrays subsetting - 


```r
y[, , 1]  # 3rd dimension
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

* Arrays subsetting - 


```r
y[1, 1, ]  # Dimensions 1 & 2
## [1]  1  7 13 19
```

<div class="figure" style="text-align: center">
<img src="images/lesson_05_array_subset2.png" alt="`array` subsetting" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-63)`array` subsetting</p>
</div>

* Arrays subsetting - 


```r
y[1, , 1]  # Dimensions 1 & 3
## [1] 1 3 5
```

* Arrays subsetting - 


```r
y[, 1, 1]  # Dimensions 2 & 3
## [1] 1 2
```

* Arrays subsetting - 


```r
y[1, 1, 1]  # Dimensions 1 & 2 & 3
## [1] 1
```

* When using `apply` on a 3-dimensional `array`, we can apply a function - 
    * On **one** of the dimensions
    * On a combinations of any **two** dimensions - 


```r
apply(y, 1, mean)    # Row means
## [1] 12 13
```


```r
apply(y, 2, mean)    # Column means
## [1] 10.5 12.5 14.5
```


```r
apply(y, 3, mean)    # 'Layer' means
## [1]  3.5  9.5 15.5 21.5
```


```r
apply(y, 1:2, mean)  # Row/Column combination means
##      [,1] [,2] [,3]
## [1,]   10   12   14
## [2,]   11   13   15
```

## Basic data structures in R

* We can classify the basic **data structures** in R based on - 
    * **Dimensions** - `1`, `2` or `n` (note there is no `0`)
    * **Homogeneity** - homogeneous (values of the same type) or heterogeneous (values of different types)
* Most of the data structures in R are **combinations** of the basic five ones

| | homogeneous | heterogeneous |
|---|---|---|
| one-dimensional | vector | `list` |
| two-dimensional | `matrix` | `data.frame` |
| n-dimensional | `array` | |

Table: Five basic data structures in R

## Rasters

### Raster properties

* **Non-spatial** properties
    * Values
    * Dimensions (rows, columns, layers)
* **Spatial** properties
    * Extent 
    * (Resolution)
    * Coordinate Reference System (CRS)

<div class="figure" style="text-align: center">
<img src="images/lesson_05_raster_esri.png" alt="Raster cells" width="45%" />
<p class="caption">(\#fig:unnamed-chunk-71)Raster cells</p>
</div>

http://desktop.arcgis.com/en/arcmap/10.3/manage-data/raster-and-images/what-is-raster-data.htm

### Raster file formats

* "Simple" rasters
    * **GeoTIFF** (`.tif`)
    * **Erdas Imagine Image** (`.img`)
* "Complex" rasters (>3D and / or metadata)
    * **HDF** (`.hdf`)
    * **NetCDF** (`.nc`)

<div class="figure" style="text-align: center">
<img src="images/HDF_structure.png" alt="Structure of an HDF file" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-72)Structure of an HDF file</p>
</div>

http://matthewrocklin.com/blog/work/2018/02/06/hdf-in-the-cloud

### The `stars` class

* The `stars` package contains the `stars` class for representing rasters, and functions for working with rasters in R

<div class="figure" style="text-align: center">
<img src="images/lesson_05_raster_single_band_vs_multi_band.png" alt="Single-band and multi-band raster" width="60%" />
<p class="caption">(\#fig:unnamed-chunk-73)Single-band and multi-band raster</p>
</div>

https://datacarpentry.org/organization-geospatial/

### Reading raster from file

The most common an useful method for creating a raster object in R (and elsewhere) is reading from a file, such as a GeoTIFF file. We can use the `read_stars` function to read a GeoTIFF file and create a `stars` object in R. The first parameter (`.x`) is the file path to the file we want to read, or just the file name (when the file is located in the working directory).

The file `MOD13A3_2000_2019.tif` is a multi-band raster with monthly NDVI values in Israel, for the period 2000-02-01 to 2019-06-01 from the MODIS instrument on the Terra satellite. Uncertain values were replaced with `NA`. Let's try reading this file to create a `stars` object in the R environment. First, we have to loads the `stars` package:


```r
library(stars)
## Loading required package: abind
## Loading required package: sf
## Linking to GEOS 3.7.1, GDAL 2.4.2, PROJ 5.2.0
```

Then we can use the `read_stars` function to read the file:


```r
r = read_stars("data/MOD13A3_2000_2019.tif")
```

Note: GeoTIFF files can come with both `*.tif` and `*.tiff` file extension, so if one of them does not work you should try the other. 

### The `mapview` function

* The `mapview` function from package `mapview` lets us visually examine spatial objects - vector layers or rasters - in an interactive map on top of various background layers, such as OpenStreetMap, satellite images, etc.
* For example - 


```r
library(mapview)
mapview(as(r[, , , 1], "Raster"), layer.name = "a", legend = TRUE)
```

<!--html_preserve--><div id="htmlwidget-687fed04324859704d6a" style="width:672px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-687fed04324859704d6a">{"x":{"options":{"minZoom":1,"maxZoom":100,"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}},"preferCanvas":false,"bounceAtZoomLimits":false,"maxBounds":[[[-90,-370]],[[90,370]]]},"calls":[{"method":"addProviderTiles","args":["CartoDB.Positron",1,"CartoDB.Positron",{"errorTileUrl":"","noWrap":false,"detectRetina":false}]},{"method":"addProviderTiles","args":["CartoDB.DarkMatter",2,"CartoDB.DarkMatter",{"errorTileUrl":"","noWrap":false,"detectRetina":false}]},{"method":"addProviderTiles","args":["OpenStreetMap",3,"OpenStreetMap",{"errorTileUrl":"","noWrap":false,"detectRetina":false}]},{"method":"addProviderTiles","args":["Esri.WorldImagery",4,"Esri.WorldImagery",{"errorTileUrl":"","noWrap":false,"detectRetina":false}]},{"method":"addProviderTiles","args":["OpenTopoMap",5,"OpenTopoMap",{"errorTileUrl":"","noWrap":false,"detectRetina":false}]},{"method":"addRasterImage","args":["data:image/png;base64,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",[[33.321179153764,34.2240641156389],[29.4793360167309,35.9001512493189]],0.8,null,"layer","layer"]},{"method":"addControl","args":["","topright","imageValues","info legend"]},{"method":"addLegend","args":[{"colors":["#000004 , #090620 5.6534805055037%, #4B0C6B 22.1575816432595%, #8E2469 38.6616827810153%, #CD4347 55.1657839187711%, #F67E14 71.6698850565269%, #F8CD37 88.1739861942827%, #FCFFA4 "],"labels":["-0.2","0.0","0.2","0.4","0.6","0.8"],"na_color":"#BEBEBE","na_label":"NA","opacity":1,"position":"topright","type":"numeric","title":"layer","extra":{"p_1":0.056534805055037,"p_n":0.881739861942827},"layerId":null,"className":"info legend","group":"layer"}]},{"method":"addLayersControl","args":[["CartoDB.Positron","CartoDB.DarkMatter","OpenStreetMap","Esri.WorldImagery","OpenTopoMap"],"layer",{"collapsed":true,"autoZIndex":true,"position":"topleft"}]},{"method":"addScaleBar","args":[{"maxWidth":100,"metric":true,"imperial":true,"updateWhenIdle":true,"position":"bottomleft"}]},{"method":"addHomeButton","args":[33.5733479343278,29.4708333306883,36.4325553976643,33.3374999970083,"Zoom to layer","<strong> layer <\/strong>","bottomright"]}],"limits":{"lat":[29.4793360167309,33.321179153764],"lng":[34.2240641156389,35.9001512493189]}},"evals":[],"jsHooks":{"render":[{"code":"function(el, x, data) {\n  return (function(el, x, data) {\n        var map = this;\n        map.on(\"mousemove\", function (e) {\n          rasterPicker.pick(e, x, null, \"Layer \");\n        });\n      }).call(this.getMap(), el, x, data);\n}","data":null},{"code":"function(el, x, data) {\n  return (\n      function(el, x, data) {\n      // get the leaflet map\n      var map = this; //HTMLWidgets.find('#' + el.id);\n      // we need a new div element because we have to handle\n      // the mouseover output separately\n      // debugger;\n      function addElement () {\n      // generate new div Element\n      var newDiv = $(document.createElement('div'));\n      // append at end of leaflet htmlwidget container\n      $(el).append(newDiv);\n      //provide ID and style\n      newDiv.addClass('lnlt');\n      newDiv.css({\n      'position': 'relative',\n      'bottomleft':  '0px',\n      'background-color': 'rgba(255, 255, 255, 0.7)',\n      'box-shadow': '0 0 2px #bbb',\n      'background-clip': 'padding-box',\n      'margin': '0',\n      'padding-left': '5px',\n      'color': '#333',\n      'font': '9px/1.5 \"Helvetica Neue\", Arial, Helvetica, sans-serif',\n      'z-index': '700',\n      });\n      return newDiv;\n      }\n\n\n      // check for already existing lnlt class to not duplicate\n      var lnlt = $(el).find('.lnlt');\n\n      if(!lnlt.length) {\n      lnlt = addElement();\n\n      // grab the special div we generated in the beginning\n      // and put the mousmove output there\n\n      map.on('mousemove', function (e) {\n      if (e.originalEvent.ctrlKey) {\n      if (document.querySelector('.lnlt') === null) lnlt = addElement();\n      lnlt.text(\n                           ' lon: ' + (e.latlng.lng).toFixed(5) +\n                           ' | lat: ' + (e.latlng.lat).toFixed(5) +\n                           ' | zoom: ' + map.getZoom() +\n                           ' | x: ' + L.CRS.EPSG3857.project(e.latlng).x.toFixed(0) +\n                           ' | y: ' + L.CRS.EPSG3857.project(e.latlng).y.toFixed(0) +\n                           ' | epsg: 3857 ' +\n                           ' | proj4: +proj=merc +a=6378137 +b=6378137 +lat_ts=0.0 +lon_0=0.0 +x_0=0.0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +no_defs ');\n      } else {\n      if (document.querySelector('.lnlt') === null) lnlt = addElement();\n      lnlt.text(\n                      ' lon: ' + (e.latlng.lng).toFixed(5) +\n                      ' | lat: ' + (e.latlng.lat).toFixed(5) +\n                      ' | zoom: ' + map.getZoom() + ' ');\n      }\n      });\n\n      // remove the lnlt div when mouse leaves map\n      map.on('mouseout', function (e) {\n      var strip = document.querySelector('.lnlt');\n      strip.remove();\n      });\n\n      };\n\n      //$(el).keypress(67, function(e) {\n      map.on('preclick', function(e) {\n      if (e.originalEvent.ctrlKey) {\n      if (document.querySelector('.lnlt') === null) lnlt = addElement();\n      lnlt.text(\n                      ' lon: ' + (e.latlng.lng).toFixed(5) +\n                      ' | lat: ' + (e.latlng.lat).toFixed(5) +\n                      ' | zoom: ' + map.getZoom() + ' ');\n      var txt = document.querySelector('.lnlt').textContent;\n      console.log(txt);\n      //txt.innerText.focus();\n      //txt.select();\n      setClipboardText('\"' + txt + '\"');\n      }\n      });\n\n      //map.on('click', function (e) {\n      //  var txt = document.querySelector('.lnlt').textContent;\n      //  console.log(txt);\n      //  //txt.innerText.focus();\n      //  //txt.select();\n      //  setClipboardText(txt);\n      //});\n\n      function setClipboardText(text){\n      var id = 'mycustom-clipboard-textarea-hidden-id';\n      var existsTextarea = document.getElementById(id);\n\n      if(!existsTextarea){\n      console.log('Creating textarea');\n      var textarea = document.createElement('textarea');\n      textarea.id = id;\n      // Place in top-left corner of screen regardless of scroll position.\n      textarea.style.position = 'fixed';\n      textarea.style.top = 0;\n      textarea.style.left = 0;\n\n      // Ensure it has a small width and height. Setting to 1px / 1em\n      // doesn't work as this gives a negative w/h on some browsers.\n      textarea.style.width = '1px';\n      textarea.style.height = '1px';\n\n      // We don't need padding, reducing the size if it does flash render.\n      textarea.style.padding = 0;\n\n      // Clean up any borders.\n      textarea.style.border = 'none';\n      textarea.style.outline = 'none';\n      textarea.style.boxShadow = 'none';\n\n      // Avoid flash of white box if rendered for any reason.\n      textarea.style.background = 'transparent';\n      document.querySelector('body').appendChild(textarea);\n      console.log('The textarea now exists :)');\n      existsTextarea = document.getElementById(id);\n      }else{\n      console.log('The textarea already exists :3')\n      }\n\n      existsTextarea.value = text;\n      existsTextarea.select();\n\n      try {\n      var status = document.execCommand('copy');\n      if(!status){\n      console.error('Cannot copy text');\n      }else{\n      console.log('The text is now on the clipboard');\n      }\n      } catch (err) {\n      console.log('Unable to copy.');\n      }\n      }\n\n\n      }\n      ).call(this.getMap(), el, x, data);\n}","data":null}]}}</script><!--/html_preserve-->

We can also produce a static image of the raster using `plot`:

<div class="figure" style="text-align: center">
<img src="05-lesson_05_files/figure-html/unnamed-chunk-77-1.png" alt="Raster plot" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-77)Raster plot</p>
</div>

We can also plot subsets of the raster: 


```r
plot(r[, , , 1:3])
```

<img src="05-lesson_05_files/figure-html/unnamed-chunk-78-1.png" width="672" style="display: block; margin: auto;" />

More details on this later on. 

https://r-spatial.github.io/mapview/index.html

<div class="figure" style="text-align: center">
<img src="images/lesson_05_modis_image.png" alt="Layer 1 out of 280 of the `modis_south.tif` raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-79)Layer 1 out of 280 of the `modis_south.tif` raster</p>
</div>

### Raster properties

* The `print` method for raster objects gives a **summary** of their properties - 


```r
r
## stars object with 3 dimensions and 1 attribute
## attribute(s), summary of first 1e+05 cells:
##  MOD13A3_2000_2019.tif 
##  Min.   :-0.19         
##  1st Qu.: 0.11         
##  Median : 0.35         
##  Mean   : 0.34         
##  3rd Qu.: 0.51         
##  Max.   : 0.87         
##  NA's   :56391         
## dimension(s):
##      from  to  offset    delta                       refsys point values
## x       1 145 3250139  926.625 +proj=sinu +lon_0=0 +x_0=... FALSE   NULL
## y       1 464 3706965 -926.625 +proj=sinu +lon_0=0 +x_0=... FALSE   NULL
## band    1 233      NA       NA                           NA    NA   NULL
##         
## x    [x]
## y    [y]
## band
```

* The `class` function returns the class name, which is `stars` in this case -


```r
class(r)
## [1] "stars"
```

* As we've seen in **Lesson 01**, a class is a "template" with pre-defined properties that each object of that class has
* For example, every `RasterLayer` **object** has row number, column number, resolution, Coordinate Reference System (CRS), etc.
* When we read the `modis_south.tif` file with `raster`, the information regarding all of the properties was **transferred** from the file and into the `RasterLayer` "template"
* Now, the `RasterLayer` object named `r` is in the **RAM**, filled with the specific values from `modis_south.tif`

* We can display the **structure** of the `RasterLayer` "template" with the specific values with `str` - 


```r
str(r)
```


```
## List of 1
##  $ MOD13A3_2000_2019.tif: num [1:145, 1:464, 1:233] NA NA NA NA NA NA NA NA NA NA ...
##  - attr(*, "dimensions")=List of 3
##   ..$ x   :List of 7
##   .. ..$ from  : num 1
##   .. ..$ to    : num 145
##   .. ..$ offset: num 3250139
##   .. ..$ delta : num 927
##   .. ..$ refsys: chr "+proj=sinu +lon_0=0 +x_0=0 +y_0=0 +a=6371007.181 +b=6371007.181 +units=m +no_defs "
##   .. ..$ point : logi FALSE
##   .. ..$ values: NULL
##   .. ..- attr(*, "class")= chr "dimension"
##   ..$ y   :List of 7
##   .. ..$ from  : num 1
##   .. ..$ to    : num 464
##   .. ..$ offset: num 3706965
##   .. ..$ delta : num -927
##   .. ..$ refsys: chr "+proj=sinu +lon_0=0 +x_0=0 +y_0=0 +a=6371007.181 +b=6371007.181 +units=m +no_defs "
##   .. ..$ point : logi FALSE
##   .. ..$ values: NULL
##   .. ..- attr(*, "class")= chr "dimension"
##   ..$ band:List of 7
##   .. ..$ from  : num 1
##   .. ..$ to    : Named int 233
##   .. .. ..- attr(*, "names")= chr "band"
##   .. ..$ offset: num NA
##   .. ..$ delta : num NA
##   .. ..$ refsys: chr NA
##   .. ..$ point : logi NA
##   .. ..$ values: NULL
##   .. ..- attr(*, "class")= chr "dimension"
##   ..- attr(*, "raster")=List of 3
##   .. ..$ affine     : num [1:2] 0 0
##   .. ..$ dimensions : chr [1:2] "x" "y"
##   .. ..$ curvilinear: logi FALSE
##   .. ..- attr(*, "class")= chr "stars_raster"
##   ..- attr(*, "class")= chr "dimensions"
##  - attr(*, "class")= chr "stars"
```

* You can see that the object is composed of "slots", which themselves can be composed of other slots, and so on, like a **tree**
* The **terminal nodes** are simpler objects, such as `character` or `numeric` vectors
* The `str` output shows both the **class names** and the **values** of the various branches
* For example, the `file` slot contains the `name` slot, which contains a `character` vector of length 1 with the value of - 


```r
# r@file@name
```

* In 99.9% of the cases we do not need to look for the property values by directly accessing object **components**
* Instead, we are using **accessor** functions and methods defined for the class
* For example, the following functions return various properties related to raster **dimensions** - 


```r
nrow(r)
##   x 
## 145
ncol(r)
##   y 
## 464
dim(r)
##    x    y band 
##  145  464  233
names(r)
## [1] "MOD13A3_2000_2019.tif"
```

* Raster layers have associated **layer names**
* These are not part of a GeoTIFF file, and therefore automatically give **default** values based on file name - 


```r
names(r)
## [1] "MOD13A3_2000_2019.tif"
```

* We can change the layer names through **assignment** - 


```r
names(r) = "NDVI"
names(r)
## [1] "NDVI"
```

* The **spatial** properties, determining raster placement in geographical space, include - 
    * Resolution
    * Extent
    * Coordinate Reference System (CRS)


```r
st_dimensions(r)[["x"]]$delta
## [1] 926.6254
st_dimensions(r)[["y"]]$delta
## [1] -926.6254
```


```r
st_bbox(r)
##    xmin    ymin    xmax    ymax 
## 3250139 3277011 3384499 3706965
```


```r
st_crs(r)
## Coordinate Reference System:
##   No EPSG code
##   proj4string: "+proj=sinu +lon_0=0 +x_0=0 +y_0=0 +a=6371007.181 +b=6371007.181 +units=m +no_defs"
```

* A **histogram** can give a first impression of the raster values distribution - 


```r
hist(r$NDVI)
```

<div class="figure" style="text-align: center">
<img src="05-lesson_05_files/figure-html/unnamed-chunk-91-1.png" alt="Distribution of NDVI values" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-91)Distribution of NDVI values</p>
</div>

* **Raster values** can be accessed in several ways
* The simplest is to use the `[` operator
* For example, the **complete vector** of raster values is given by - 


```r
# r[]
```



* We can also get a **subset** of values, using an index -


```r
as.data.frame(r[, 100, 200, 1:5])
##         x       y band   NDVI
## 1 3342338 3522103    1 0.1341
## 2 3342338 3522103    2 0.1618
## 3 3342338 3522103    3 0.1517
## 4 3342338 3522103    4 0.1233
## 5 3342338 3522103    5 0.1140
```


```r
as.data.frame(r[, 1:2, 1:2, 1])
##         x       y band NDVI
## 1 3250602 3706502    1   NA
## 2 3251529 3706502    1   NA
## 3 3250602 3705575    1   NA
## 4 3251529 3705575    1   NA
```

* The ordering of raster values is from the **top-left** corner and to the **right**

<div class="figure" style="text-align: center">
<img src="images/lesson_05_raster_index.pdf" alt="Raster cell indices" width="65%" />
<p class="caption">(\#fig:unnamed-chunk-96)Raster cell indices</p>
</div>

http://rpubs.com/etiennebr/visualraster


```r
dates = read.csv("data/MOD13A3_2000_2019_dates.csv", stringsAsFactors = FALSE)
dates$date = as.Date(dates$date)
r = st_set_dimensions(r, "band", values = dates$date, point = FALSE, names = "time")
```

* Question: find out the mean, minimum and maximum values of the raster `r` (excluding `NA`s)


```
## [1] 0.2339101
## [1] -0.2
## [1] 1
```

*  Question: what is the meaning of the following plot?


```r
x = r[,,,1][[1]]
x = as.numeric(x)
y = r[,,,2][[1]]
y = as.numeric(y)
plot(x, y, xlab = "Band 1", ylab = "Band 2")
```

<div class="figure" style="text-align: center">
<img src="05-lesson_05_files/figure-html/unnamed-chunk-99-1.png" alt="Raster plot" width="50%" />
<p class="caption">(\#fig:unnamed-chunk-99)Raster plot</p>
</div>

### The NetCDF format


```r
u = read_stars("data/MOD13A3.A2000032.h20v05.006.2015138123528.hdf")
## "1 km monthly NDVI", "1 km monthly EVI", "1 km monthly VI Quality", "1 km monthly red reflectance", "1 km monthly NIR reflectance", "1 km monthly blue reflectance", "1 km monthly MIR reflectance", "1 km monthly view zenith angle", "1 km monthly sun zenith angle", "1 km monthly relative azimuth angle", "1 km monthly pixel reliability",
u
## stars object with 2 dimensions and 11 attributes
## attribute(s), summary of first 1e+05 cells:
##  "1 km monthly NDVI"  "1 km monthly EVI"  "1 km monthly VI Quality" 
##  Min.   :-19500000    Min.   :-16080000   Min.   : 2057             
##  1st Qu.: -3240000    1st Qu.: -5060000   1st Qu.: 2112             
##  Median :   900000    Median :  1110000   Median :18445             
##  Mean   : 13490078    Mean   :  5565859   Mean   :13012             
##  3rd Qu.: 28717500    3rd Qu.: 16100000   3rd Qu.:18445             
##  Max.   : 80240000    Max.   : 44680000   Max.   :63487             
##  NA's   :3586         NA's   :3586        NA's   :903               
##  "1 km monthly red reflectance"  "1 km monthly NIR reflectance" 
##  Min.   :   310000               Min.   :   620000              
##  1st Qu.: 10750000               1st Qu.: 20850000              
##  Median : 49850000               Median : 51310000              
##  Mean   : 48990840               Mean   : 50985185              
##  3rd Qu.: 86110000               3rd Qu.: 80460000              
##  Max.   :139410000               Max.   :125490000              
##  NA's   :3586                    NA's   :3586                   
##  "1 km monthly blue reflectance"  "1 km monthly MIR reflectance" 
##  Min.   :   20000                 Min.   :  480000               
##  1st Qu.: 5505000                 1st Qu.: 5490000               
##  Median :46940000                 Median :10070000               
##  Mean   :45332125                 Mean   :12577754               
##  3rd Qu.:83490000                 3rd Qu.:16730000               
##  Max.   :99990000                 Max.   :49840000               
##  NA's   :4089                     NA's   :3586                   
##  "1 km monthly view zenith angle" [°] "1 km monthly sun zenith angle" [°]
##  Min.   :   300                       Min.   :457800                     
##  1st Qu.:150700                       1st Qu.:483700                     
##  Median :257250                       Median :495000                     
##  Mean   :268523                       Mean   :496581                     
##  3rd Qu.:379400                       3rd Qu.:507500                     
##  Max.   :600000                       Max.   :540100                     
##  NA's   :3586                         NA's   :3586                       
##  "1 km monthly relative azimuth angle" [°]
##  Min.   :-1798800                         
##  1st Qu.: -560100                         
##  Median : 1132900                         
##  Mean   :  356068                         
##  3rd Qu.: 1175100                         
##  Max.   : 1799000                         
##  NA's   :3586                             
##  "1 km monthly pixel reliability" 
##  Min.   :0.000                    
##  1st Qu.:1.000                    
##  Median :2.000                    
##  Mean   :1.564                    
##  3rd Qu.:2.000                    
##  Max.   :3.000                    
##  NA's   :3586                     
## dimension(s):
##   from   to  offset    delta                       refsys point values    
## x    1 1200 2223901  926.625 +proj=sinu +lon_0=0 +x_0=...    NA   NULL [x]
## y    1 1200 4447802 -926.625 +proj=sinu +lon_0=0 +x_0=...    NA   NULL [y]
```

### Converting a `matrix` to raster

Creating a sample matrtix:


```r
v = c(171, 189, 204, 208, 208, 209, 207, 200, 191, 173, 
155, 140, 167, 185, 199, 207, 210, 206, 198, 183, 166, 152, 115, 
140, 166, 183, 203, 211, 208, 197, 184, 168, 153, 64, 86, 108, 
141, 167, 207, 211, 203, 188, 174, 155, 44, 60, 86, 115, 139, 
162, 185, 204, 198, 191, 175, 31, 43, 62, 91, 112, 140, 167, 
188, 196, 191, 177, 16, 27, 41, 64, 93, 117, 141, 161, 181, 186, 
179, 6, 14, 20, 34, 64, 91, 112, 139, 158, 173, 183, 4, 4, 5, 
15, 39, 69, 87, 113, 135, 163, 166, 2, 5, 5, 7, 8, 27, 63, 88, 
109, 120, 121, 0, 0, 4, 5, 3, 2, 6, 11, 69, 95, 109, 1, -2, 5, 
7, 4, 1, 1, 1, 10, 26, 32, 2, 5, 6, 6, 5, 5, 3, 2, 4, 5, 15)
m = matrix(v, nrow = 11, ncol = 13)
```

Creating a `stars` object from a `matrix`:


```r
d = st_dimensions(x = 1:ncol(m), y = 1:nrow(m))
s = st_as_stars(t(m))
s = st_set_dimensions(s, 1, offset = 689164, delta = 90)
s = st_set_dimensions(s, 2, offset = 3629999, delta = -90)
s = st_set_crs(s, 32636)
plot(s, text_values = TRUE)
```

<img src="05-lesson_05_files/figure-html/unnamed-chunk-102-1.png" width="672" style="display: block; margin: auto;" />

Another example:


```r
d = st_dimensions(x = 1:ncol(volcano), y = 1:nrow(volcano))
volcano = st_as_stars(t(volcano))
volcano = st_set_dimensions(volcano, 1, offset = 0, delta = 1)
volcano = st_set_dimensions(volcano, 2, offset = nrow(volcano), delta = -1)
plot(volcano)
```

<img src="05-lesson_05_files/figure-html/unnamed-chunk-103-1.png" width="672" style="display: block; margin: auto;" />

### Using `stars_proxy` objects

...

### Writing raster to file

Writing a `stars` raster object to a file on disk is done using `write_stars`. We need to specify: 

* `obj` - The `stars` object to write
* `dsn` - The file name to write

The function can automatically detect the required file format based on the file extension. For example, the following expression writes the `stars` object named `s` to a GeoTIFF file named `dem.tif`:


```r
write_stars(s, "data/dem.tif")
```
















<!--chapter:end:05-lesson_05.Rmd-->

# Raster algebra {#raster-algebra}



## Contents

* Raster algebra
* Classification
* Raster subsetting
* Transforming rasters to other data structures

## Aims

* Calculating new rasters based on one or more overlapping rasters with **raster algebra**
* Converting continuous rasters to categorical ones using raster **classification**
* Learning methods of raster **subsetting** and methods of **transforming** rasters to other data structures

## Preparation


```r
library(stars)
## Loading required package: abind
## Loading required package: sf
## Linking to GEOS 3.7.1, GDAL 2.4.2, PROJ 5.2.0
```

## Raster algebra

<div class="figure" style="text-align: center">
<img src="images/lesson_06_raster_algebra.pdf" alt="Raster algebra" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-3)Raster algebra</p>
</div>

http://rpubs.com/etiennebr/visualraster

* Often we have one or more overlapping rasters, and we want to apply the same operation on all pairs, triplets, etc. of **overlapping pixels**
* In **raster algebra**, we can use different operators - 
    * Arithmetic: `+`, `-`, `*`, `/`
    * Logical: `<`, `<=`, `>`, `>=`, `==`, `!=`, `!`
    * Certain functions: `abs`, `round`, `ceiling`, `floor`, `trunc`, `sqrt`, `log`, `log10`, `exp`, `cos`, `sin`, `max`, `min`, `range`, `prod`, `sum`, `any`, `all`
* On each pair (triplet, etc.) of overlapping rasters, to get a **new raster** where each pixel value is the result of the given **operation** on the **overlapping pixels** in the input rasters
* The operation can also include rasters and `numeric` values, as long as the first argument is a raster

https://cran.r-project.org/web/packages/raster/vignettes/Raster.pdf

* For example, let's take the first **two** layers from `modis_south.tif` - 


```r
r = read_stars("data/MOD13A3_2000_2019.tif")
names(r) = "NDVI"
x = r[, , , 1]
y = r[, , , 2]
```

* Here are several examples of **raster algebra** operations - 


```r
x + y
x > 0.5
x < y
is.na(x)
```

* A **logical** raster algebra operation produces a `logical` raster, a raster with pixel values `TRUE` and `FALSE`
* For example - 

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-6-1.png" alt="Logical raster algebra operation" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-61)Logical raster algebra operation</p>
</div><div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-6-2.png" alt="Logical raster algebra operation" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-62)Logical raster algebra operation</p>
</div>

* A **logical raster** can be used to get a subset of raster values, and possibly **assign** new values into the subset
* For example, we can use the logical raster `is.na(r)` to **replace** all `NA` values in the raster `r` with a **new value** - 


```r
x[is.na(x)] = mean(x$NDVI, na.rm = TRUE)
```

* Question: what is the meaning of the expression `mean(r[], na.rm = TRUE)`?

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-8-1.png" alt="Assignmnent to raster subset using logical raster (before)" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-8)Assignmnent to raster subset using logical raster (before)</p>
</div>


```r
s = r
s[is.na(s)] = mean(s[[1]][], na.rm = TRUE)
```


```r
plot(s)
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-10-1.png" alt="Assignmnent to raster subset using logical raster (after)" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-10)Assignmnent to raster subset using logical raster (after)</p>
</div>

* In operations where a `numeric` representation is **required**, such as - 
    * An arithmetic operation 
    * Saving to a file
* logical raster values `TRUE` and `FALSE` **become** `1` and `0`, respectively


```r
(is.na(x))$NDVI[1:2, 1:2, 1]
##      [,1] [,2]
## [1,] TRUE TRUE
## [2,] TRUE TRUE
(is.na(x)*2)$NDVI[1:2, 1:2, 1]
##      [,1] [,2]
## [1,]    2    2
## [2,]    2    2
```

* How can we calculate the **proportion** of `NA` values in `r`?


```r
# r = read_stars("data/modis_south.tif")
```


```r
# Method 1
# length(r[,,,1][is.na(r)]) / ncell(r)
```


```r
# Method 2
# mean(is.na(r[]))
```


```r
# Method 3
# mean(is.na(r)[])
```

* Question: How does each one of these methods works?

## Landsat

* For the following example, let's read the file `landsat_04_10_2000.tif`
* This is a part of a **Landsat-5** satellite image with **bands 1-5** and **7**, after radiometric and atmospheric corrections
* The raster values represent spectral **reflectance**, therefore all values are in the range 0-1


```r
l = read_stars("data/landsat_04_10_2000.tif")
```

* We can assign meaningful **layer names** - 


```r
# names(l) = c(
#   "Blue", "Green", "Red", 
#   "NIR", "SWIR1", "SWIR2"
# )
```

https://landsat.usgs.gov/what-are-band-designations-landsat-satellites

* Plot - 


```r
plot(l)
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-19-1.png" alt="Logical raster algebra operation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-19)Logical raster algebra operation</p>
</div>

## True color and false color images

<div class="figure" style="text-align: center">
<img src="images/lesson_06_plot_rgb.jpg" alt="RGB image" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-20)RGB image</p>
</div>

https://datacarpentry.org/organization-geospatial/01-spatial-data-structures-formats/index.html

<div class="figure" style="text-align: center">
<img src="images/lesson_06_linear_image_stretch.jpg" alt="Image stretch" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-21)Image stretch</p>
</div>

https://datacarpentry.org/organization-geospatial/01-spatial-data-structures-formats/index.html

* **True color** and **false color** images can be produced with the `plotRGB` function - 


```r
# True color image
plot(l, rgb = c(3, 2, 1))
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-22-1.png" alt="True color (left) and false color (right) images" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-221)True color (left) and false color (right) images</p>
</div>

```r
# False color image
plot(l, rgb = c(4, 3, 2))
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-22-2.png" alt="True color (left) and false color (right) images" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-222)True color (left) and false color (right) images</p>
</div>

## Raster algebra

* **NDVI** can be calculated using raster algebra, as the difference between NIR and Red reflectance, divided by their sum -

$$NDVI=\frac{NIR-Red}{NIR + Red}$$

* Therefore - 


```r
ndvi = (l[,,,4] - l[,,,3]) / (l[,,,4] + l[,,,3])
```

* Plot - 


```r
plot(ndvi)
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-24-1.png" alt="NDVI image" width="60%" />
<p class="caption">(\#fig:unnamed-chunk-24)NDVI image</p>
</div>

## Classification

<div class="figure" style="text-align: center">
<img src="images/lesson_06_reclassify.pdf" alt="Raster classification" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-25)Raster classification</p>
</div>

http://rpubs.com/etiennebr/visualraster

* The `reclassify` function can be used to **reclassify** a raster, i.e. to convert a **continuous** raster to a **categorical** one


```r
l_rec = ndvi
l_rec[ndvi <= 0.2] = 0
l_rec[ndvi > 0.2] = 1
```

* Question: can we do the above reclassification with a single expression?


```r
plot(ndvi, main = "Original NDVI image")
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-27-1.png" alt="Original and reclassified NDVI images" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-271)Original and reclassified NDVI images</p>
</div>

```r
plot(l_rec, main = "Reclassified NDVI image")
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-27-2.png" alt="Original and reclassified NDVI images" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-272)Original and reclassified NDVI images</p>
</div>

## Raster subsetting

* In **Lesson 05**, we have already seen that we can access a subset of pixel values using a **one-dimensional** index `r[i]`, as in - 


```r
# r[8] 
```


```r
# r[2:5]
```

* We can also use a **two-dimensional** index `r[i, j]`, the same way as with a `matrix` - 


```r
# r[7, 15:17]
```


```r
# r[1, ]
```


```r
# r[, 5:7]
```

* (In the last two expressions the output is omitted to save space)

<div class="figure" style="text-align: center">
<img src="images/lesson_06_raster_index2.pdf" alt="Raster subsetting" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-33)Raster subsetting</p>
</div>

http://rpubs.com/etiennebr/visualraster




```r
# r[170, 172:182]
```



* We can also subset raster **layers** using the `[[` operator


```r
# r = brick("data/modis_south.tif")
```

* Subset with **one** layer - 


```r
# r[[3]]
```



* Subset with **several** layers -


```r
# r[[5:7]]
```



* When accessing the **layers** dimension only (with `[[`), the returned object is always a **raster**
* When accessing the **row** / **column** dimensions (with `[`), the returned object type depends on number of layers and the `drop` parameter - 
    * When using `drop=FALSE` the returned object is a **raster**
    * When using `drop=TRUE` (the default), the returned object is simplified to - 
        * A **vector** when the input is a single-band raster
        * A **matrix** when the input is a multi-band raster
* In case a `matrix` is returned, its - 
    * **Rows** represent raster cells
    * **Columns** represent raster bands

* Accessing the **layers** dimension only always returns a **raster** - 


```r
# plot(r[[2]], main = "Layer 2")
# plot(r[[1]], main = "Layer 1")
# plot(r[[3]], main = "Layer 3")
```

* Subsetting rows and/or columns from a single-band raster returns a **vector** with `drop=TRUE` -


```r
# r[[2]][1:2, 1:2, drop = TRUE]
```


```r
# r[[2]][1:2, 1:2]
```

* Or a **raster** with `drop=FALSE` - 


```r
# r[[2]][1:2, 1:2, drop = FALSE]
```



* Subset of a multi-band raster returns a **matrix** with `drop=TRUE` -


```r
# r[[1:3]][1:2, 1:2, drop = TRUE]
```


```r
# r[[1:3]][1:2, 1:2]
```

* Or a **raster** with `drop=FALSE` - 


```r
# r[[1:3]][1:2, 1:2, drop = FALSE]
```



* We can access a **"slice"** of a single pixel through all of the raster layers - 


```r
v = r[[1]][50, 200, ]
class(v)
## [1] "numeric"
```

* The result is a 1×280 `matrix`; it is more convenient to convert it to a **vector** - 


```r
# v = v[1, ]
# class(v)
```

* Plot - 


```r
plot(v, type = "o")
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-53-1.png" alt="Single pixel values across all layers" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-53)Single pixel values across all layers</p>
</div>

* Using the `dates2.csv` table we can display **dates** on the x-axis - 


```r
dates = read.csv("data/MOD13A3_2000_2019_dates.csv", stringsAsFactors = FALSE)
dates$date = as.Date(dates$date)
plot(dates$date, v, type = "o", xlab = "Time", ylab = "NDVI")
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-54-1.png" alt="Single pixel values across all layers" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-54)Single pixel values across all layers</p>
</div>

* We can improve the interpretability of the time series if we mark **seasons** with different color - 


```r
# cols = c("blue", "purple", "red", "yellow")
# seasons = c("winter", "spring", "summer", "fall")
```

* We can use a `for` **loop** to mark the portion of the NDVI time series from each season - 


```r
# plot(dates$date, v, type = "l", xlab = "Time", ylab = "NDVI", col = "grey")
# for(i in 1:4) {
  # tmp = v
  # tmp[dates$season != seasons[i]] = NA
  # lines(dates$date, tmp, col = cols[i], type = "o")
# }
```

* Another **subsetting** example - 


```r
# plot(r[, 1:10, drop = FALSE])
```

* Question 1: how many rows / columns / layers does the result have?
* Question 2: what would the result be if we omit the `drop=FALSE` part?



## Raster coversion

* R has various methods for **accessing** object components and for **transforming** objects to different data structures
* In other words, there are - 
    * Methods for **getting** a particular component from object A as an object B (of a different class)
    * Methods for **converting** an entire object, keeping all or most of its data, from class A to class B 
* We already saw several examples of accessing raster **properties**, such as - 


```r
# r[[1]][1]
```


```r
# proj4string(r)
```

* There are also several methods for **transforming** a raster **to** and **from** the simpler data structures `matrix` and `array`

| Conversion | Function |
|---|---|
| raster → `matrix` | `as.matrix` |
| raster → `array` | `as.array` |
| `matrix` → raster | `raster` |
| `array` → raster | `brick` |

Table: Raster conversion methods

* For example, the following expression converts a **single-band** raster to a `matrix` - 


```r
# x = r[[2]][1:5, 1:5, drop = FALSE]
```


```r
# as.matrix(x)
```

* For example, the following expression converts a **multi-band** raster to an `array` - 


```r
# x = r[[1:2]][1:2, 1:5, drop = FALSE]
```


```r
# as.array(x)
```

* When converting an object to a different class, some of its properties get **"lost"** - in case when the destination class has no such property
* If we convert a raster to a simpler object such as a `matrix` and then back to a raster, the "lost" properties get **arbitrary** or `NA` values

<div class="figure" style="text-align: center">
<img src="images/lesson_06_raster_conversion1.pdf" alt="Raster conversion to `matrix` and vector" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-65)Raster conversion to `matrix` and vector</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_06_raster_conversion2.pdf" alt="raster → `matrix` → raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-66)raster → `matrix` → raster</p>
</div>

## Summarizing layer values

* The `cellStats` function can be used to apply a function on the values of **each layer** in a raster, to get a **vector** of summaries - 


```r
x = st_apply(r, 3, mean, na.rm = TRUE)
plot(x[[1]], type = "o")
```

<img src="06-lesson_06_files/figure-html/unnamed-chunk-67-1.png" width="672" style="display: block; margin: auto;" />

* Note: the default of `cellStats` is `na.rm=TRUE`, i.e. **ignoring** `NA` values


```r
# cellStats(r[[1:6]], mean, na.rm = FALSE)
```

* **Other** possible values for the `stat` parameter: `sum`, `mean`, `min`, `max`, `sd`, `'skew'`, `'rms'`, and other functions


```r
# cellStats(r[[1:6]], min)
```


```r
# cellStats(r[[1:6]], max)
```

* Applying `cellStats` on a single-band raster is equivalent to calling a function on the **vector** of raster values - 


```r
# cellStats(r[[1]], mean)
```


```r
# mean(r[[1]][], na.rm = TRUE)
```

* Remember that applying a function on a raster is a **raster algebra** operation - 


```r
# mean(r[[1]], na.rm = TRUE)
```



* Applying `cellStats` on a multi-band raster is equivalent to applying the function on the **layers dimension** of a raster - 


```r
# cellStats(r[[1:3]], mean)
```


```r
# apply(as.array(r[[1:3]]), 3, mean, na.rm = TRUE)
```

## Raster overlay

* The `overlay` function makes it possible to apply any **custom**, user-defined, raster algebra function
* The `fun` parameter determines the **function** which calculates each pixel value given the respective pixel values of the input raster
* The `fun` function needs to - 
    * Accept a **vector** of **any length**
    * And return - 
        * A **vector** of **length 1**, in which case `overlay` returns a single-band raster, or
        * A **vector** of (fixed) **length n**, in which case `overlay` returns a multi-band raster with n layers

* For example, the following code section uses a **custom function** `f` to create a new raster `s` where each pixel value is the **average** of the first 10 layers in `r` (excluding `NA`s)


```r
s = st_apply(r, 1:2, mean, na.rm = TRUE)
```

* Plot - 


```r
plot(s)
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-78-1.png" alt="Result of `overlay` with `mean` function and `na.rm=TRUE`" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-78)Result of `overlay` with `mean` function and `na.rm=TRUE`</p>
</div>

* In the following example we use `fun=range`, which is a function that returns a vector of **length 2** - 


```r
f = function(x) if(!all(is.na(x))) range(x, na.rm = TRUE) else c(NA, NA)
s = st_apply(r, 1:2, f)
```

* Plot - 


```r
plot(s)
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-80-1.png" alt="Result of applying the `range` function with `na.rm=TRUE` on each pixel" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-80)Result of applying the `range` function with `na.rm=TRUE` on each pixel</p>
</div>

* Question: what do you think the result `s` will be?

* As another example, we can calculate the **difference** between the **maximum** and **minimum** in the first 23 layers of `r` - 


```r
f = function(x) if(!all(is.na(x))) diff(range(x, na.rm = TRUE)) else NA
```


```r
s = st_apply(r, 1:2, f)
```

* Plot - 


```r
plot(s)
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-83-1.png" alt="Result of `overlay` with `max`/`min` difference" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-83)Result of `overlay` with `max`/`min` difference</p>
</div>

* Another useful case for `overlay` is calculating the **proportion** of `NA` values per pixel - 


```r
f = function(x) if(all(is.na(x))) NA else mean(is.na(x))
s = st_apply(r, 1:2, f)
```

* Plot - 


```r
plot(s)
```

<div class="figure" style="text-align: center">
<img src="06-lesson_06_files/figure-html/unnamed-chunk-85-1.png" alt="Result of `overlay`" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-85)Result of `overlay`</p>
</div>

## Exercise 3 - Submission date **2018-12-23**






<!--chapter:end:06-lesson_06.Rmd-->

# Vector layers {#vector-layers}



## Contents

* Data structures for vector layers
* Creating layers from scratch
* Extracting layer components
* Creating point layer from table
* Subsetting based on attributes
* Input and output
* Reprojection

## Aims

* Become familiar with data structures for vector layers: points, lines and polygons
* Examine spatial and non-spatial properties of vector layers
* Create subsets of vector layers based on their attributes
* Learn to transform a layer from one Coordinate Reference System (CRS) to another

## Preparation


```r
library(sf)
library(raster)
library(mapview)

setwd("~/Dropbox/Data2")
```

## Vector layers

<div class="figure" style="text-align: center">
<img src="images/vector_layers.png" alt="Geometry (left) and attributes (right) of vector layers" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-3)Geometry (left) and attributes (right) of vector layers</p>
</div>

https://www.neonscience.org/dc-shapefile-attributes-r

## Vector file formats

* Binary
    * **ESRI Shapefile** (`.shp`, `.shx`, `.dbf`, `.prj`, ...)
    * **GeoPackage (GPKG)** (`.gpkg`)
* Plain Text
    * **GeoJSON** (`.json` or `.geojson`)
    * **GPS Exchange Format (GPX)** (`.gpx`)
    * **Keyhole Markup Language (KML)** (`.kml`)
* Spatial Databases
    * **PostGIS / PostgreSQL**

## Vector data structures (`sp`)

<div class="figure" style="text-align: center">
<img src="images/lesson_07_paper2.png" alt="Pebesma &amp; Bivand, 2005, R News" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-4)Pebesma & Bivand, 2005, R News</p>
</div>

https://journal.r-project.org/archive/r-news.html

<div class="figure" style="text-align: center">
<img src="images/cran_graph.png" alt="The network structure of CRAN; `sp` ecosystem shown in green" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-5)The network structure of CRAN; `sp` ecosystem shown in green</p>
</div>

blog.revolutionanalytics.com/2015/07/the-network-structure-of-cran.html

* Package `sp` has **6 main classes** for vector layers
    * One for each **geometry type** (points, lines, polygons)
    * One for **geometry only** and one for **geometry with attributes**

| class | geometry | attributes |
|---|---|---|
| `SpatialPoints` | Points | - | 
| `SpatialPointsDataFrame` | Points | `data.frame` | 
| `SpatialLines` | Lines | - |
| `SpatialLinesDataFrame` | Lines | `data.frame` | 
| `SpatialPolygons` | Polygons | - |
| `SpatialPolygonsDataFrame` | Polygons | `data.frame` | 

Table: Spatial data structures in package `sp`

## Vector data structures (`sf`)

<div class="figure" style="text-align: center">
<img src="images/lesson_07_paper1.png" alt="Pebesma, 2018, The R Journal" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-6)Pebesma, 2018, The R Journal</p>
</div>

https://journal.r-project.org/archive/2018-1/

* Package `sf` defines a **hierarchical class system**
    * Class `sfg` is for a **single geometry**
    * Class `sfc` is a **set of geometries** with a CRS
    * Class `sf` is a **layer with attributes**

| class | hierarchy | data |
|---|---|---|
| `sfg` | geometry | coords, type, dimension | 
| `sfc` | geometry column | set of `sfg` + CRS | 
| `sf` | layer | `sfc` + attributes | 

Table: Spatial data structures in package `sf`

## Vector layers in R: package `sf`

* `sf` is a relative new (2016-) R package for **handling vector layers in R** 
* In the long-term, `sf` aims to replace `rgdal` (2003-), `sp` (2005-), and `rgeos` (2011-)
* The main innovation in `sf` is a complete implementation of the **Simple Features** (https://cran.r-project.org/web/packages/sf/vignettes/sf1.html) standard 
* Since 2003, Simple Features been widely implemented in **spatial databases** (such as **PostGIS**), commercial GIS (e.g., **ESRI ArcGIS**) and forms the vector data basis for libraries such as GDAL
* When working with spatial databases, Simple Features are commonly specified as (**Well Known Text (WKT)**)[https://en.wikipedia.org/wiki/Well-known_text]
* A subset of simple features forms the [**GeoJSON**](https://en.wikipedia.org/wiki/GeoJSON) standard

<div class="figure" style="text-align: center">
<img src="images/sf_deps.png" alt="`sf` package dependencies" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-7)`sf` package dependencies</p>
</div>

https://github.com/edzer/rstudio_conf

* The `sf` class extends the `data.frame` class to include a **geometry** column 
* This is similar to the way that **spatial databases** are structured

<div class="figure" style="text-align: center">
<img src="images/sf.png" alt="Structure of an `sf` object" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-8)Structure of an `sf` object</p>
</div>

https://cran.r-project.org/web/packages/sf/vignettes/sf1.html

<img src="07-lesson_07_files/figure-html/unnamed-chunk-9-1.png" width="100%" style="display: block; margin: auto;" />

<img src="images/sf.png" width="80%" style="display: block; margin: auto;" />

* The `sf` class is actually a hierarchical structure composed of three classes - 
    * `sf` - Vector **layer** object, a table (`data.frame`) with one or more attribute columns and one geometry column
    * `sfc` - Geometric part of the vector layer, the **geometry column**
    * `sfg` - **Geometry** of an individual simple feature

<img src="images/sf.png" width="100%" style="display: block; margin: auto;" />

## Creating layers from scratch

* Let's create a sample **object** for each of these classes to learn more about them 
* Objects of class `sfg`, i.e. a **single geometry**, can be created using the appropriate function for each geometry type - 
    * `st_point`
    * `st_multipoint`
    * `st_linestring`
    * `st_multilinestring`
    * `st_polygon`
    * `st_multipolygon`
    * `st_geometrycollection`
* From **coordinates** passed as - 
    * `numeric` vectors - `POINT`
    * `matrix` objects - `MULTIPOINT` or `LINESTRING`
    * `list` objects - All other geometries

### Geometry (`sfg`)

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-12-1.png" alt="Simple feature geometry (`sfg`) types in package `sf`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-12)Simple feature geometry (`sfg`) types in package `sf`</p>
</div>

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-13-1.png" alt="Intersection between two polygons may yield a `GEOMETRYCOLLECTION`" width="65%" />
<p class="caption">(\#fig:unnamed-chunk-13)Intersection between two polygons may yield a `GEOMETRYCOLLECTION`</p>
</div>

* For example, we can create a **point geometry** object named `pnt1`, representing a `POINT` geometry, using the `st_point` function - 


```r
pnt1 = st_point(c(34.812831, 31.260284))
```

* Printing the object in the console gives the **WKT** representation -


```r
pnt1
## POINT (34.81283 31.26028)
```

* Note the **class** definition of an `sfg` (geometry) object is actually composed of three parts:
    * `XY` - The **dimensions** type (`XY`, `XYZ`, `XYM` or `XYZM`)
    * `POINT` - The **geometry** type (`POINT`, `MULTIPOLYGON`, etc.)
    * `sfg` - The general **class** (`sfg` = Simple Feature Geometry)
* For example, the `pnt1` object has geometry `POINT` and dimensions `XY` -


```r
class(pnt1)
## [1] "XY"    "POINT" "sfg"
```

* Creating a `POLYGON` with `st_polygon` 
* Note: we learn about `list` in **Leasson 10**


```r
a = st_polygon(
  list(
    cbind(
      c(0,0,7.5,7.5,0),
      c(0,-1,-1,0,0)
    )
  )
)
```


```r
a
## POLYGON ((0 0, 0 -1, 7.5 -1, 7.5 0, 0 0))
```


```r
class(a)
## [1] "XY"      "POLYGON" "sfg"
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-20-1.png" alt="An `sfg` object of type `POLYGON`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-20)An `sfg` object of type `POLYGON`</p>
</div>

* Another `POLYGON` - 


```r
b = st_polygon(
  list(
    cbind(
      c(0,1,2,3,4,5,6,7,7,0),
      c(1,0,0.5,0,0,0.5,-0.5,-0.5,1,1)
    )
  )
)
```


```r
b
## POLYGON ((0 1, 1 0, 2 0.5, 3 0, 4 0, 5 0.5, 6 -0.5, 7 -0.5, 7 1, 0 1))
```


```r
class(b)
## [1] "XY"      "POLYGON" "sfg"
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-24-1.png" alt="Another `sfg` object of type `POLYGON`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-24)Another `sfg` object of type `POLYGON`</p>
</div>

* The `c` function combines `sfg` geometries:


```r
ab = c(a, b)
```


```r
ab
## MULTIPOLYGON (((0 0, 0 -1, 7.5 -1, 7.5 0, 0 0)), ((0 1, 1 0, 2 0.5, 3 0, 4 0, 5 0.5, 6 -0.5, 7 -0.5, 7 1, 0 1)))
```


```r
class(ab)
## [1] "XY"           "MULTIPOLYGON" "sfg"
```

* Question: what type of geometry is `c(a, b, pnt1)`?

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-28-1.png" alt="An `sfg` object of type `MULTIPOLYGON`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-28)An `sfg` object of type `MULTIPOLYGON`</p>
</div>

* A new geometry can be calculated applying various functions on an existing one(s) 
* Note: we learn about `st_intersection` in **Lesson 08**


```r
i = st_intersection(a, b)
```


```r
i
## GEOMETRYCOLLECTION (POINT (1 0), LINESTRING (4 0, 3 0), POLYGON ((5.5 0, 7 0, 7 -0.5, 6 -0.5, 5.5 0)))
```


```r
class(i)
## [1] "XY"                 "GEOMETRYCOLLECTION" "sfg"
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-32-1.png" alt="An `sfg` object of type `GEOMETRYCOLLECTION`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-32)An `sfg` object of type `GEOMETRYCOLLECTION`</p>
</div>

### Geometry column (`sfc`)

* Let's create a **second** object named `pnt2`, representing a different point -


```r
pnt2 = st_point(c(34.798443, 31.243288))
```

* Geometry objects (`sfg`) can be **collected** into a geometry column (`sfc`) object 
* This is done with **function** `st_sfc`

* **Geometry column** objects contain a **Coordinate Reference System** (CRS) definition, specified with the `crs` parameter of function `st_sfc`
* Two types of CRS definitions are accepted - 
    * An **EPSG** code (`4326`)
    * A **PROJ.4** definition (`"+proj=longlat +datum=WGS84"`)
* Let's combine the two `POINT` geometries `pnt1` and `pnt2` into a geometry column (`sfc`) object named `geom` - 


```r
geom = st_sfc(pnt1, pnt2, crs = 4326)
```

* Here is a **summary** of the resulting geometry column - 


```r
geom
```


```
## Geometry set for 2 features 
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 34.79844 ymin: 31.24329 xmax: 34.81283 ymax: 31.26028
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
## POINT (34.81283 31.26028)
## POINT (34.79844 31.24329)
```

### Layer (`sf`)

* A geometry column (`sfc`) can be combined with non-spatial columns, or **attributes**, resulting in a **layer** (`sf`) object
* In our case the two points in the `sfc` geometry column `geom` represent the location of the two **railway stations** in Beer-Sheva
* Let's create a `data.frame` with -
    * A `town` column specifying **town name**
    * A `station` column specifying **station name**
* Note: the **order** of attributes must match the order of the geometries!

* Creating the **attribute table** - 


```r
dat = data.frame(
  town = c("Beer-Sheva", "Beer-Sheva"),
  station = c("North", "Center"),
  stringsAsFactors = FALSE
)
```


```r
dat
##         town station
## 1 Beer-Sheva   North
## 2 Beer-Sheva  Center
```

* And combining the **attribute table** with the **geometry column** - 


```r
layer = st_sf(dat, geom)
layer
```




```
## Simple feature collection with 2 features and 2 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 34.79844 ymin: 31.24329 xmax: 34.81283 ymax: 31.26028
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
##         town station                      geom
## 1 Beer-Sheva   North POINT (34.81283 31.26028)
## 2 Beer-Sheva  Center POINT (34.79844 31.24329)
```

## Extracting layer components

* In the last few slides we - 
    * Started from raw **coordinates**
    * Convered them to **geometry** objects (`sfg`) 
    * Combined the geometries to a **geometry column** (`sfc`)
    * Added attributes to the geometry column to get a **layer** (`sf`)
    * In short: coordinates → `sfg` → `sfc` → `sf`
* Sometimes we are interested in the opposite process
* We may need to extract the simpler components (**geometry**, **attributes**, **coordinates**) from an existing layer
    * `sf` → `sfg`
    * `sf` → attributes (`data.frame`)
    * `sf` → coordinates (`matrix`)

* The **geometry column** (`sfc`) component can be extracted from an `sf` layer object using function `st_geometry` -


```r
st_geometry(layer)
```


```
## Geometry set for 2 features 
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 34.79844 ymin: 31.24329 xmax: 34.81283 ymax: 31.26028
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
## POINT (34.81283 31.26028)
## POINT (34.79844 31.24329)
```

* The non-spatial columns of an `sf` layer, i.e. the **attribute table**, can be extracted from an `sf` object using function `st_set_geometry` and `NULL` - 


```r
st_set_geometry(layer, NULL)
##         town station
## 1 Beer-Sheva   North
## 2 Beer-Sheva  Center
```

<div class="figure" style="text-align: center">
<img src="images/lesson_05_arcgis_attribute_table.png" alt="Attribute table in ArcGIS" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-45)Attribute table in ArcGIS</p>
</div>

* The **coordinates** (`matrix` object) of `sf`, `sfc` or `sfg` objects can be obtained with function `st_coordinates` - 


```r
st_coordinates(layer)
##          X        Y
## 1 34.81283 31.26028
## 2 34.79844 31.24329
```

## Interactive mapping with `mapview`

* Function `mapview` is useful for **inspecting** spatial data - 


```r
mapview(layer)
```

<div class="figure" style="text-align: center">
<img src="images/leaflet2.png" alt="Intractive map of `layer`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-48)Intractive map of `layer`</p>
</div>

## Creating point layer from table

* A common way of creating a point layer is to transform a **table** which has **X** and **Y** coordinate **columns**
* Function `st_as_sf` can **convert** a table (`data.frame`) into a point layer (`sf`)
* In `st_as_sf` we specify -
    * `x` - The `data.frame` to be converted
    * `coords` - Columns names with the coordinates (X, Y)
    * `crs` - The CRS (`NA` if left unspecified)
* Let's take the `rainfall.csv` table as an example - 


```r
rainfall = read.csv(
  "data/rainfall.csv", 
  stringsAsFactors = FALSE
)
```


```r
head(rainfall)
##      num altitude sep oct nov dec jan feb mar apr may              name
## 1 110050       30 1.2  33  90 117 135 102  61  20 6.7 Kfar Rosh Hanikra
## 2 110351       35 2.3  34  86 121 144 106  62  23 4.5              Saar
## 3 110502       20 2.7  29  89 131 158 109  62  24 3.8             Evron
## 4 111001       10 2.9  32  91 137 152 113  61  21 4.8       Kfar Masrik
## 5 111650       25 1.0  27  78 128 136 108  59  21 4.7     Kfar Hamakabi
## 6 120202        5 1.5  27  80 127 136  95  49  19 2.7        Haifa Port
##      x_utm   y_utm
## 1 696533.1 3660837
## 2 697119.1 3656748
## 3 696509.3 3652434
## 4 696541.7 3641332
## 5 697875.3 3630156
## 6 687006.2 3633330
```

* The table can be converted to an `sf` layer using `st_as_sf` - 


```r
rainfall = st_as_sf(
  x = rainfall, 
  coords = c("x_utm", "y_utm"), 
  crs = 32636
)
```

* Note 1: The order of `coords` column names corresponds to X-Y!
* Note 2: `32636` is the EPSG code of the UTM zone 36N projection (see below)

<div class="figure" style="text-align: center">
<img src="images/lesson_05_arcgis_display_xy_data1.png" alt="Displaying XY data from CSV in ArcGIS: step 1" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-52)Displaying XY data from CSV in ArcGIS: step 1</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_05_arcgis_display_xy_data2.png" alt="Displaying XY data from CSV in ArcGIS: step 2" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-53)Displaying XY data from CSV in ArcGIS: step 2</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_05_arcgis_display_xy_data3.png" alt="Displaying XY data from CSV in ArcGIS: step 3" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-54)Displaying XY data from CSV in ArcGIS: step 3</p>
</div>


```r
rainfall
```




```
## Simple feature collection with 169 features and 12 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 629301.4 ymin: 3270290 xmax: 761589.2 ymax: 3681163
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +datum=WGS84 +units=m +no_defs
## First 10 features:
##       num altitude sep oct nov dec jan feb mar apr may              name                 geometry
## 1  110050       30 1.2  33  90 117 135 102  61  20 6.7 Kfar Rosh Hanikra POINT (696533.1 3660837)
## 2  110351       35 2.3  34  86 121 144 106  62  23 4.5              Saar POINT (697119.1 3656748)
## 3  110502       20 2.7  29  89 131 158 109  62  24 3.8             Evron POINT (696509.3 3652434)
## 4  111001       10 2.9  32  91 137 152 113  61  21 4.8       Kfar Masrik POINT (696541.7 3641332)
## 5  111650       25 1.0  27  78 128 136 108  59  21 4.7     Kfar Hamakabi POINT (697875.3 3630156)
## 6  120202        5 1.5  27  80 127 136  95  49  19 2.7        Haifa Port POINT (687006.2 3633330)
## 7  120630      450 1.9  36  93 161 166 128  71  21 4.9  Haifa University POINT (689553.7 3626282)
## 8  120750       30 1.6  31  91 163 170 146  76  22 4.9             Yagur POINT (694694.5 3624388)
## 9  120870      210 1.1  32  93 147 147 109  61  16 4.3        Nir Etzyon POINT (686489.5 3619716)
## 10 121051       20 1.8  32  85 147 142 102  56  13 4.5         En Carmel POINT (683148.4 3616846)
```



## `sf` layer properties

* Number of **rows** / **features** - 


```r
nrow(rainfall)
## [1] 169
```

* Number of **columns** (including geometry column) - 


```r
ncol(rainfall)
## [1] 13
```

* **Both** - 


```r
dim(rainfall)
## [1] 169  13
```

* Question 1: what is the result of `st_geometry(rainfall)`?
* Question 2: and `st_set_geometry(rainfall, NULL)`?

* **Bounding box** coordinates -


```r
st_bbox(rainfall)
##      xmin      ymin      xmax      ymax 
##  629301.4 3270290.2  761589.2 3681162.7
```

* **Coordinate Reference System** (CRS) -


```r
st_crs(rainfall)
## Coordinate Reference System:
##   EPSG: 32636 
##   proj4string: "+proj=utm +zone=36 +datum=WGS84 +units=m +no_defs"
```

## Interactive mapping with `mapview`


```r
mapview(rainfall, zcol = "jan", legend = TRUE)
```

<div class="figure" style="text-align: center">
<img src="images/mapview_rainfall_pnt.png" alt="Intractive map of `rainfall`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-65)Intractive map of `rainfall`</p>
</div>

## Coordinates

* Question: what is the difference between the following two plots? (see next slide)


```r
plot(st_geometry(rainfall))
```


```r
opar = par(mfrow = c(1, 2))
plot(st_geometry(rainfall))
plot(
  st_coordinates(rainfall)[, 1], 
  st_coordinates(rainfall)[, 2]
)
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-67-1.png" alt="Two plots" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-67)Two plots</p>
</div>

```r
par(opar)
```

## Subsetting based on attributes

* **Subsetting** (filtering) of features in an `sf` vector layer is exactly the same as filtering rows in a `data.frame`
* Remember: an `sf` layer *is* a `data.frame`
* For example, the following expressions filters the `rainfall` layer -


```r
plot(st_geometry(
  rainfall[1:10, ]
))
```


```r
plot(st_geometry(
  rainfall[rainfall$jan > 100, ]
))
```

* Note that the geometry column **"sticks"** to the subset, by default, even if we do not select it - 


```r
rainfall[1:2, c("jan", "feb")]
```


```
## Simple feature collection with 2 features and 2 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 696533.1 ymin: 3656748 xmax: 697119.1 ymax: 3660837
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +datum=WGS84 +units=m +no_defs
##   jan feb                 geometry
## 1 135 102 POINT (696533.1 3660837)
## 2 144 106 POINT (697119.1 3656748)
```

* Only when we use `[` with `drop=TRUE`, the geometry column is **"dropped"** and we get - 
    * A `data.frame` when the subset includes **>1 columns**
    * A vector when the subset includes a **single column**


```r
rainfall[1:2, c("jan", "feb"), drop = TRUE]
##   jan feb
## 1 135 102
## 2 144 106
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-73-1.png" alt="Subsets of the `rainfall` layer" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-73)Subsets of the `rainfall` layer</p>
</div>

## Reading vector layers

* In addition to creating from scratch and transforming a table to point layer, often we want to **read** existing vector layers from a **file** (or from a spatial database)
* This can be done with the `st_read` function
* For complete list of **available drivers** see -


```r
View(st_drivers(what = "vector"))
```

* In our next example we will read a **Shapefile**
* In case the Shapefile is located in the **working directory** we only need to specify the **name** of the `.shp` file
* We can also specify `stringsAsFactors=FALSE` to avoid conversion of `character` to `factor`


```r
rainfall = st_read(
  "data/rainfall_pnt.shp", 
  stringsAsFactors = FALSE
)
## Reading layer `rainfall_pnt' from data source `/home/michael/Dropbox/Courses/R_2019/data/rainfall_pnt.shp' using driver `ESRI Shapefile'
## Simple feature collection with 169 features and 12 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 629301.4 ymin: 3270290 xmax: 761589.2 ymax: 3681163
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
```

## Writing vector layers

* **Writing** an `sf` object to a **file** can be done with `st_write`
* Before writing the `rainfall` layer back to disk, let's calculate a new column called `annual` - 


```r
m = c(
  "sep", "oct", "nov", "dec", "jan",
  "feb", "mar", "apr", "may"
)
rainfall$annual = apply(
  X = st_set_geometry(rainfall[, m], NULL),
  MARGIN = 1,
  FUN = sum
)
```

* **Writing** with `st_write` - 


```r
st_write(
  rainfall, 
  "data/rainfall_pnt2.shp", 
  delete_dsn = TRUE
)
## Deleting source `data/rainfall_pnt2.shp' using driver `ESRI Shapefile'
## Writing layer `rainfall_pnt2' to data source `data/rainfall_pnt2.shp' using driver `ESRI Shapefile'
## features:       169
## fields:         13
## geometry type:  Point
```

* Note: the format is automatically determined based on the `.shp` file extension

## Reading vector layers

* As another example, let's read a **Shapefile** of **US county** boundaries - 


```r
county = st_read(
  "data/USA_2_GADM_fips.shp", 
  stringsAsFactors = FALSE
)
## Reading layer `USA_2_GADM_fips' from data source `/home/michael/Dropbox/Courses/R_2019/data/USA_2_GADM_fips.shp' using driver `ESRI Shapefile'
## Simple feature collection with 3103 features and 4 fields
## geometry type:  MULTIPOLYGON
## dimension:      XY
## bbox:           xmin: -124.7628 ymin: 24.52042 xmax: -66.94889 ymax: 49.3833
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
```

* And a **GeoJSON** file with the location of **three airports** - 


```r
airports = st_read(
  "data/airports.geojson", 
  stringsAsFactors = FALSE
)
## Reading layer `airports' from data source `/home/michael/Dropbox/Courses/R_2019/data/airports.geojson' using driver `GeoJSON'
## Simple feature collection with 3 features and 1 field
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: -106.7947 ymin: 35.04807 xmax: -106.0892 ymax: 35.61621
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
```

## Basic plotting


```r
head(st_set_geometry(county, NULL))
##        NAME_1     NAME_2 TYPE_2  FIPS
## 1 Connecticut Litchfield County 09005
## 2 Connecticut   Hartford County 09003
## 3 Connecticut    Tolland County 09013
## 4 Connecticut    Windham County 09015
## 5  California   Siskiyou County 06093
## 6  California  Del Norte County 06015
```


```r
head(st_set_geometry(airports, NULL))
##                        name
## 1 Albuquerque International
## 2           Double Eagle II
## 3        Santa Fe Municipal
```

## Basic plotting

* When plotting an `sf` object we get **multiple** small maps, one for each attribute 
* This can be useful to quickly examine the types of spatial variation in our data


```r
plot(county)
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-82-1.png" alt="Plot of `sf` object" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-82)Plot of `sf` object</p>
</div>

* Plotting a single attribute also shows the **legend**:


```r
plot(county[, "TYPE_2"], key.width = lcm(5), key.pos = 4)
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-83-1.png" alt="Plot of `sf` object, single attribute with legend" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-83)Plot of `sf` object, single attribute with legend</p>
</div>

* Plotting an `sfc` or an `sfg` object shows just the **geometry** - 


```r
plot(st_geometry(county))
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-85-1.png" alt="Plot of `sfc` object" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-85)Plot of `sfc` object</p>
</div>

* When we are plotting an `sfc` **geometry column**, the plot only displays the geometric shape
* We can use basic **graphical parameters** to control the appearance, such as - 
    * `col` - Fill color
    * `border` - Outline color
    * `pch` - Point shape
    * `cex` - Point size

* For example, to draw county outline in **grey** - 


```r
plot(st_geometry(county), border = "grey")
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-86-1.png" alt="Basic plot of `sfc` object" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-86)Basic plot of `sfc` object</p>
</div>

* **Additional** vector layers can be drawn in an **existing** graphical window with `add=TRUE`
* For example, the following expressions draw **both** `airports` and `county`
* Note that the second expression uses `add=TRUE`


```r
plot(st_geometry(county), border = "grey")
plot(st_geometry(airports), col = "red", add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-87-1.png" alt="Using `add=TRUE` in `plot`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-87)Using `add=TRUE` in `plot`</p>
</div>

* We can also use `add=TRUE` to combine `sfc` geometries with **rasters** in the same plot
* For example, `modis_average.tif` contains average NDVI based on MODIS for Israel - 


```r
modis_avg = raster("data/modis_average.tif")
```

* Plot - 


```r
plot(modis_avg)
plot(st_geometry(rainfall), add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-89-1.png" alt="`sfc` layer on top of a raster" width="45%" />
<p class="caption">(\#fig:unnamed-chunk-89)`sfc` layer on top of a raster</p>
</div>

## Coordinate Reference Systems (CRS)

* A **Coordinate Reference System (CRS)** defines how the coordinates in the data relate to the surface of the Earth
    * **Geographic** - longitude and latitude, in degrees
    * **Projected** - implying flat surface, w/ units (e.g. meters)



<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-91-1.png" alt="US counties in WGS84 and US Atlas projections" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-91)US counties in WGS84 and US Atlas projections</p>
</div>



## Reprojection

* **Reprojection** is an important part of spatial analysis workflow since as we often need to -
    * Transform several layers into the same projection
    * Switch between un-projected and projected data
* A vector layer can be **reprojected** with `st_transform`
* `st_transform` has **two parameters** - 
    * `x` - The **layer** to be reprojected 
    * `crs` - The **target CRS**
* Question: why don't we need to specify the *origin* CRS?
* The CRS can be **specified** in one of two ways - 
    * A **PROJ.4** definition (`"+proj=longlat +datum=WGS84"`)
    * An **EPSG** code (`4326`)

<div class="figure" style="text-align: center">
<img src="images/lesson_07_projections.jpg" alt="Map of the US using different projections" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-93)Map of the US using different projections</p>
</div>

https://datacarpentry.org/r-raster-vector-geospatial/09-vector-when-data-dont-line-up-crs/index.html

* Where can we find **EPSG codes** and **PROJ.4** definitions?
    * Internet, such as http://spatialreference.org
    * The `make_EPSG` function from package `rgdal` in R
* During the course we will use just **three** projections: WGS84, UTM 36N and US National Atlas

| Projection | Area | Units | EPSG code |
|---|---|---|---|
| WGS84 | World | degrees | `4326` |
| UTM 36N | Israel | m | `32636` |
| US National Atlas | USA | m | `2163` |

Table: Projections used in this course

* In the following code section we are **reprojecting** both the `county` and `airports` layers 
* The **target** CRS is the US National Atlas Equal Area projection (EPSG=`2163`)


```r
county = st_transform(county, 2163)
airports = st_transform(airports, 2163)
```

* Plot - 


```r
plot(st_geometry(county), border = "grey")
plot(st_geometry(airports), col = "red", add = TRUE)
```

* Airport coordinates in **WGS84** - 


```r
st_coordinates(st_transform(airports, 4326))
##           X        Y
## 1 -106.6169 35.04807
## 2 -106.7947 35.15559
## 3 -106.0892 35.61621
```

* Airport coordinates in **US atlas** - 


```r
st_coordinates(st_transform(airports, 2163))
##           X        Y
## 1 -603868.2 -1081605
## 2 -619184.5 -1068431
## 3 -551689.8 -1022366
```

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-98-1.png" alt="Reprojected `county` and `airport` layers" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-98)Reprojected `county` and `airport` layers</p>
</div>

## Subsetting

* Question: create a subset of `county` with the counties of New-Mexico, Arizona and Texas only, and plot the result

<div class="figure" style="text-align: center">
<img src="07-lesson_07_files/figure-html/unnamed-chunk-99-1.png" alt="Subset of three states from the `county` layer" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-99)Subset of three states from the `county` layer</p>
</div>

## Conversion between `sp` and `sf`

* Since `sf` is new, the majority of the R-Spatial ecosystem **only works with `sp`**
* **"Migration" document** (https://github.com/r-spatial/sf/wiki/migrating) between `sp` and `sf`

* **Conversion** `sf` $\rightarrow$ `sp` using `as(..., "Spatial")` -


```r
airports_sp = as(airports, "Spatial")
class(airports_sp)
## [1] "SpatialPointsDataFrame"
## attr(,"package")
## [1] "sp"
```

* **Conversion** `sp` $\rightarrow$ `sf` using `st_as_sf` -


```r
airports_sf = st_as_sf(airports_sp)
class(airports_sf)
## [1] "sf"         "data.frame"
```




















<!--chapter:end:07-lesson_07.Rmd-->

# Geometric operations with vector layers {#geometric-operations-with-vector-layers}



## Contents

* Join -
    * By attribute
    * By location
* Spatial operators -
    * Area
    * Distance
    * Centroid
    * Union
    * Buffer
    * Intersection
    * Aggregation
    * Convex hull

## Aim

* Learn to join by location and by attributes
* Learn to make geometric calculations between vector layers

## Preparation


```r
library(sf)
## Linking to GEOS 3.7.1, GDAL 2.4.2, PROJ 5.2.0
library(units)
## udunits system database from /usr/share/xml/udunits
library(dplyr)
## 
## Attaching package: 'dplyr'
## The following objects are masked from 'package:stats':
## 
##     filter, lag
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

## US counties and three airports

* Let's load the US **counties** and three **airports** layers (see **Lesson 07**) - 


```r
airports = st_read(
  "data/airports.geojson", 
  stringsAsFactors = FALSE
)
## Reading layer `airports' from data source `/home/michael/Dropbox/Courses/R_2019/data/airports.geojson' using driver `GeoJSON'
## Simple feature collection with 3 features and 1 field
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: -106.7947 ymin: 35.04807 xmax: -106.0892 ymax: 35.61621
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
county = st_read(
  "data/USA_2_GADM_fips.shp", 
  stringsAsFactors = FALSE
)
## Reading layer `USA_2_GADM_fips' from data source `/home/michael/Dropbox/Courses/R_2019/data/USA_2_GADM_fips.shp' using driver `ESRI Shapefile'
## Simple feature collection with 3103 features and 4 fields
## geometry type:  MULTIPOLYGON
## dimension:      XY
## bbox:           xmin: -124.7628 ymin: 24.52042 xmax: -66.94889 ymax: 49.3833
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
```

* And **transform** them to the US National Atlas projection - 


```r
airports = st_transform(airports, 2163)
county = st_transform(county, 2163)
```

## Join by location

* Join by spatial location, or **spatial join**, is one of the most common operations in spatial analysis
* In a spatial join we are "attaching" attributes from one layer to another based on their **spatial relations**
* In ArcGIS this is done using "Join data from another layer based on spatial location"

<div class="figure" style="text-align: center">
<img src="images/lesson_08_arcgis_join_by_location1.png" alt="Join by location in ArcGIS: step 1" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-5)Join by location in ArcGIS: step 1</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_08_arcgis_join_by_location2.png" alt="Join by location in ArcGIS: step 2" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-6)Join by location in ArcGIS: step 2</p>
</div>

* For simplicity, we will create a subset of the counties of New-Mexico only - 


```r
nm = county[county$NAME_1 == "New Mexico", ]
```

* Plot:


```r
plot(st_geometry(nm))
plot(
  st_geometry(airports),
  col = "red",
  pch = 16, 
  cex = 2,
  add = TRUE
)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-8-1.png" alt="The `nm` and `airports` layers" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-8)The `nm` and `airports` layers</p>
</div>

* Note: `pch` = point shape, `cex` = point size (see `?points`)

* Given two layers `x` and `y`, a function call of the form `st_join(x, y)` returns the `x` layer along with **matching attributes** from `y`
* Note: the default is join by **intersection**, other options possible (see `join` parameter in `?st_join`)
* For example, here is how we join the `airports` layer with the matching **county attributes** - 


```r
st_join(airports, nm)
## Simple feature collection with 3 features and 5 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: -619184.5 ymin: -1081605 xmax: -551689.8 ymax: -1022366
## epsg (SRID):    2163
## proj4string:    +proj=laea +lat_0=45 +lon_0=-100 +x_0=0 +y_0=0 +a=6370997 +b=6370997 +units=m +no_defs
##                        name     NAME_1     NAME_2 TYPE_2  FIPS
## 1 Albuquerque International New Mexico Bernalillo County 35001
## 2           Double Eagle II New Mexico Bernalillo County 35001
## 3        Santa Fe Municipal New Mexico   Santa Fe County 35049
##                     geometry
## 1 POINT (-603868.2 -1081605)
## 2 POINT (-619184.5 -1068431)
## 3 POINT (-551689.8 -1022366)
```

* Question: what do you think happens in the following case? How many features does the result have, and why?


```r
st_join(nm, airports)
## Simple feature collection with 34 features and 5 fields
## geometry type:  MULTIPOLYGON
## dimension:      XY
## bbox:           xmin: -863763.9 ymin: -1478601 xmax: -267074.1 ymax: -845634.3
## epsg (SRID):    2163
## proj4string:    +proj=laea +lat_0=45 +lon_0=-100 +x_0=0 +y_0=0 +a=6370997 +b=6370997 +units=m +no_defs
## First 10 features:
##          NAME_1     NAME_2 TYPE_2  FIPS               name
## 1800 New Mexico      Union County 35059               <NA>
## 1801 New Mexico   San Juan County 35045               <NA>
## 1802 New Mexico Rio Arriba County 35039               <NA>
## 1803 New Mexico       Taos County 35055               <NA>
## 1804 New Mexico     Colfax County 35007               <NA>
## 1826 New Mexico       Mora County 35033               <NA>
## 1832 New Mexico    Harding County 35021               <NA>
## 1833 New Mexico   Sandoval County 35043               <NA>
## 1839 New Mexico   Santa Fe County 35049 Santa Fe Municipal
## 1840 New Mexico   McKinley County 35031               <NA>
##                            geometry
## 1800 MULTIPOLYGON (((-267074.1 -...
## 1801 MULTIPOLYGON (((-659007.8 -...
## 1802 MULTIPOLYGON (((-534193 -87...
## 1803 MULTIPOLYGON (((-534193 -87...
## 1804 MULTIPOLYGON (((-464330.7 -...
## 1826 MULTIPOLYGON (((-398962.1 -...
## 1832 MULTIPOLYGON (((-360535.7 -...
## 1833 MULTIPOLYGON (((-563991.5 -...
## 1839 MULTIPOLYGON (((-563252.1 -...
## 1840 MULTIPOLYGON (((-814213.5 -...
```

## Subsetting by location

* We can create **subsets** based on intersection with **another layer** using the `[` operator
* An expression of the form `x[y, ]` returns a subset of `x` features that **intersect** `y`
* For example - 


```r
nm1 = nm[airports, ]
```

* Plot - 


```r
plot(st_geometry(nm))
plot(st_geometry(nm1), col = "lightblue", add = TRUE)
plot(st_geometry(airports), col = "red", pch = 16, cex = 2, add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-12-1.png" alt="Subset of the `nm` layer based on intersection with `airports`" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-12)Subset of the `nm` layer based on intersection with `airports`</p>
</div>

* Question 1: what will be the result of `airports[nm, ]`?
* Question 2: what will be the result of `nm[nm[20, ], ]`?

## Geometric calculations

**Geometric operations** on vector layers can conceptually be divided into **three groups** according to their output -

* **Numeric** values: Functions that summarize geometrical properties of - 
    * A **single layer** (e.g. area, length)
    * A **pair of layers** (e.g. distance)
* **Logical** values: Functions that evaluate whether a certain condition holds true, regarding -
    * A **single layer** (e.g. geometry is valid) 
    * A **pair of layers** (e.g. feature A intersects feature B)
* **Spatial** layers: Functions that create a new layer based on - 
    * A **single layer** (e.g. centroids) 
    * A **pair of layers** (e.g. intersection area)

### Numeric

* There are several functions to calculate **numeric geometric properties** of vector layers in package `sf` - 
    * `st_length`
    * `st_area`
    * `st_distance`
    * `st_bbox`
    * `st_dimension`

* For example, we can calculate the **area** of each feature in the `states` layer (i.e. each state) using `st_area` -


```r
county$area = st_area(county)
county$area[1:3]
## Units: [m^2]
## [1] 2451875694 1941109814 1077788608
```

* The **result** is an object of class `units` -


```r
class(county$area)
## [1] "units"
```

* **CRS units** (e.g. meters) are used by default

* We can convert measurements an **ordinary** `numeric` vector with `as.numeric` - 


```r
as.numeric(county$area[1:3])
## [1] 2451875694 1941109814 1077788608
```

* We can convert measurements to **different units** with `set_units` from package `units` (see `?valid_udunits`) - 


```r
county$area = set_units(county$area, "km^2")
county$area[1:3]
## Units: [km^2]
## [1] 2451.876 1941.110 1077.789
```

* Inspecting the new `"area"` column -


```r
plot(county[, "area"])
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-17-1.png" alt="Calculated `area` attribute" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-17)Calculated `area` attribute</p>
</div>

* An example of a numeric operator on a **pair** of geometries is **geographical distance**
* Distances can be calculated using function `st_distance` -


```r
d = st_distance(airports, nm)
```

* The result is a **matrix** of `units` values - 


```r
d[, 1:4]
## Units: [m]
##          [,1]     [,2]      [,3]      [,4]
## [1,] 266778.9 140470.5 103328.22 140913.62
## [2,] 275925.0 120879.9  93753.25 141511.80
## [3,] 197540.4 145580.9  34956.53  62231.01
```

* In the **distance matrix** - 
    * **rows** refer to features of `x`
    * **columns** refer to features of `y`


```r
dim(d)
## [1]  3 33
```

* Just like areas, distances can always be converted to different **units** with `set_units` - 


```r
d = set_units(d, "km")
```


```r
d[, 1:4]
## Units: [km]
##          [,1]     [,2]      [,3]      [,4]
## [1,] 266.7789 140.4705 103.32822 140.91362
## [2,] 275.9250 120.8799  93.75325 141.51180
## [3,] 197.5404 145.5809  34.95653  62.23101
```

* To work with the distance `matrix`, it can be convenient to set row and column **names** -


```r
rownames(d) = airports$name
colnames(d) = nm$NAME_2
```


```r
d[1:3, 1:2]
## Units: [km]
##                              Union San Juan
## Albuquerque International 266.7789 140.4705
## Double Eagle II           275.9250 120.8799
## Santa Fe Municipal        197.5404 145.5809
```

* When row and column names are set, it is more convenient to find out the distance between a **specific** airport and a **specific** county - 


```r
d["Santa Fe Municipal", "Santa Fe", drop = FALSE]
## Units: [km]
##                    Santa Fe
## Santa Fe Municipal        0
```

### Logical

* Given two layers, `x` and `y`, the following **logical geometric functions** check whether each feature in `x` maintains the specified **relation** with each feature in `y` -
    * `st_intersects`
    * `st_disjoint`
    * `st_touches`
    * `st_crosses`
    * `st_within`
    * `st_contains`
    * `st_overlaps`
    * `st_covers`
    * `st_covered_by`
    * `st_equals`
    * `st_equals_exact`

* When specifying `sparse=FALSE` the functions return a **logical** `matrix`
* Each **element** `i,j` in the matrix is `TRUE` when `f(x[i], y[j])` is `TRUE`
* For example, this creates a matrix of **intersection** relations between counties - 


```r
int = st_intersects(nm, nm, sparse = FALSE)
```


```r
int[1:4, 1:4]
##       [,1]  [,2]  [,3]  [,4]
## [1,]  TRUE FALSE FALSE FALSE
## [2,] FALSE  TRUE  TRUE FALSE
## [3,] FALSE  TRUE  TRUE  TRUE
## [4,] FALSE FALSE  TRUE  TRUE
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-28-1.png" alt="Intersection between counties in New Mexico (`nm`)" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-28)Intersection between counties in New Mexico (`nm`)</p>
</div>

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-29-1.png" alt="Using `st_touches` instead of `st_intersects`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-29)Using `st_touches` instead of `st_intersects`</p>
</div>

* Question: How can we calculate `airports` count per county in `nm`, using `st_intersects`?

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-30-1.png" alt="Airport count per county in New Mexico" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-30)Airport count per county in New Mexico</p>
</div>

### Spatial

* `sf` provides common **geometry-generating** functions applicable to **individual** geometries, such as - 
    * `st_centroid`
    * `st_buffer`
    * `st_sample`
    * `st_convex_hull`
    * `st_voronoi`

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-31-1.png" alt="Geometry-generating operations on individual layers" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-31)Geometry-generating operations on individual layers</p>
</div>

* For example, the following expression uses `st_centroid` to create a layer of **state centroids** - 


```r
ctr = st_centroid(nm)
```

* Plot:


```r
opar = par(mar = rep(0, 4))
plot(
  st_geometry(nm), 
  border = "grey"
)
plot(
  st_geometry(ctr), 
  col = "red", pch = 3, 
  add = TRUE
)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-33-1.png" alt="Centroids of New Mexico counties" width="65%" />
<p class="caption">(\#fig:unnamed-chunk-33)Centroids of New Mexico counties</p>
</div>

```r
par(opar)
```

* What is the distance between the **centroids** of California and New Jersey?


```r
ca = county[county$NAME_1 == "California", ]
nj = county[county$NAME_1 == "New Jersey", ]

ca_ctr = st_centroid(st_union(ca))
nj_ctr = st_centroid(st_union(nj))

d = st_distance(ca_ctr, nj_ctr)

set_units(d, "km")
## Units: [km]
##         [,1]
## [1,] 3846.64
```

* Note: we are using `st_union` to combine the counties into a single geometry and to "dissolve" the borders

* Plot:


```r
opar = par(mar = rep(0, 4))
plot(
  st_geometry(county), 
  border = "grey"
)
plot(
  c(ca_ctr, nj_ctr), 
  col = "red", pch = 16, cex = 2, 
  add = TRUE
)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-35-1.png" alt="California and New Jersey centroids" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-35)California and New Jersey centroids</p>
</div>

```r
par(opar)
```

* How can we draw the corresponding **line**?
* First, we can **combine** the points into a single `sfc` object - 


```r
p = c(ca_ctr, nj_ctr)
p
## Geometry set for 2 features 
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: -1707694 ymin: -667480.7 xmax: 2111204 ymax: -206332.8
## epsg (SRID):    2163
## proj4string:    +proj=laea +lat_0=45 +lon_0=-100 +x_0=0 +y_0=0 +a=6370997 +b=6370997 +units=m +no_defs
## POINT (-1707694 -667480.7)
## POINT (2111204 -206332.8)
```

* Second, we can use `st_combine` to **transform** the points into a single `MULTIPOINT` geoemtry
* `st_combine` is similar to `st_union`, but only combines and **does not dissolve**
* Question: compare the results of `st_union(nm)` and `st_combine(nm)`


```r
p = st_combine(p)
p
```


```
## Geometry set for 1 feature 
## geometry type:  MULTIPOINT
## dimension:      XY
## bbox:           xmin: -1707694 ymin: -667480.7 xmax: 2111204 ymax: -206332.8
## epsg (SRID):    2163
## proj4string:    +proj=laea +lat_0=45 +lon_0=-100 +x_0=0 +y_0=0 +a=6370997 +b=6370997 +units=m +no_defs
## MULTIPOINT (-1707694 -667480.7, 2111204 -206332.8)
```

* The `st_cast` function can be used to convert between different **geometry types**
* The `st_cast` function accepts - 
    * The **input layer**
    * The destination **geometry type**
* Finally, we can use `st_cast` to **convert** a `MULTIPOINT` geometry to a `LINESTRING` geometry


```r
l = st_cast(p, "LINESTRING")
```

* Note: Meaningless `st_cast` operations will fail: for example, try `st_cast(l, "POLYGON")`

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-40-1.png" alt="California and New Jersey centroids, with a line" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-40)California and New Jersey centroids, with a line</p>
</div>

* Another example is the **buffer** function `st_buffer`
* For example, here is how we can calculate 100 km buffers around the `airports` -


```r
# Method 1 - 'dist' is 'numeric'
airports_100 = st_buffer(
  airports, 
  dist = 100 * 10^3
)
# Method 2 - 'dist' is 'units'
airports_100 = st_buffer(
  airports, 
  dist = set_units(100, "km")
)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-42-1.png" alt="`airports` buffered by 100 km" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-42)`airports` buffered by 100 km</p>
</div>

* Other **geometry-generating** functions work on **pairs** of input geometries -
    * `st_intersection`
    * `st_difference`
    * `st_sym_difference`
    * `st_union`

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-43-1.png" alt="Geometry-generating operations on pairs of layers" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-43)Geometry-generating operations on pairs of layers</p>
</div>

* How can we calculate the area that is within 100 km range of **all** three airports at the same time?
* We can find the area of **intersection** of the three airports, using `st_intersection` - 


```r
inter1 = st_intersection(
  airports_100[1, ], airports_100[2, ]
)
inter2 = st_intersection(
  inter1, airports_100[3, ]
)
```

* Plot:


```r
plot(st_geometry(nm))
plot(st_geometry(airports_100), add = TRUE)
plot(inter2, col = "lightblue", add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-45-1.png" alt="Intersection of three `airports` buffers" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-45)Intersection of three `airports` buffers</p>
</div>

* How can we calculate the area that is at within 100 km range of **at least one** of the three airports? 
* We can **"dissolve"** the buffers, using `st_union` - 


```r
airports_100u = st_union(airports_100)
```

* Plot:


```r
opar = par(mar = rep(0, 4))
plot(st_geometry(nm))
plot(st_geometry(airports_100u), add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-47-1.png" alt="`airports` buffered by 100 km, after `st_union`" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-47)`airports` buffered by 100 km, after `st_union`</p>
</div>

```r
par(opar)
```

* We don't have to dissolve **all** features - we can also dissolve by **attribute** or by **location**
* To demonstrate aggregation/dissolving **by attribute**, let's take a subset with all counties of Arizona and Utah - 


```r
s = county[county$NAME_1 %in% c("Arizona", "Utah"), ]
```

* Plot:


```r
plot(s[, "NAME_1"])
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-49-1.png" alt="Subset of two states from `county`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-49)Subset of two states from `county`</p>
</div>

* As shown before, dissolving **all** features into a single feature is done with `st_union` - 


```r
s1 = st_union(s)
```

* Plot - 


```r
plot(s1)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-51-1.png" alt="Union of all counties in `s`" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-51)Union of all counties in `s`</p>
</div>

* Aggregating/dissolving **by attributes** can be done with `aggregate` (or using `dplyr` functions) - 


```r
# Method 1
s2 = aggregate(
  x = s[, "area"], 
  by = st_set_geometry(s[, "NAME_1"], NULL), 
  FUN = sum
)
# (Method 2 - 'dplyr')
s2 = s %>% 
  group_by(NAME_1) %>% 
  summarize(area = sum(area))
```

* Using **Method 1** the unit of measurement is lost, so we need to **reconstruct** it - 


```r
s2$area = set_units(as.numeric(s2$area), "km^2")
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-54-1.png" alt="Union by state name of `s`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-54)Union by state name of `s`</p>
</div>

* The **Convex Hull** of a set X of points is the smallest convex set that contains X

<div class="figure" style="text-align: center">
<img src="images/lesson_08_convex_hull.png" alt="Convex Hull: elastic-band analogy" width="40%" />
<p class="caption">(\#fig:unnamed-chunk-55)Convex Hull: elastic-band analogy</p>
</div>

https://en.wikipedia.org/wiki/Convex_hull

* For example - 


```r
h = st_convex_hull(nm1)
```

* Plot - 


```r
plot(st_geometry(nm1))
plot(st_geometry(h), add = TRUE, border = "red")
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-57-1.png" alt="Convex hull polygons for two counties in New Mexico" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-57)Convex hull polygons for two counties in New Mexico</p>
</div>

* Question: How can we calculate the convex hull of all polygons in `nm1`?

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-58-1.png" alt="Convex Hull of multiple polygons" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-58)Convex Hull of multiple polygons</p>
</div>

* Suppose we build a **tunnel** 10 km wide between the centroids of `"Harding"` and `"Sierra"` counties in New Mexico
* **Which** counties does the tunnel go through?


```r
w = nm[nm$NAME_2 %in% c("Harding", "Sierra"), ]
w_ctr = st_centroid(w)
w_ctr_buf = st_buffer(w_ctr, dist = 5000)
w_ctr_buf_u = st_union(w_ctr_buf)
w_ctr_buf_u_ch = st_convex_hull(w_ctr_buf_u)
nm_w = nm[w_ctr_buf_u_ch, ]
nm_w$NAME_2
## [1] "Harding"    "San Miguel" "Guadalupe"  "Torrance"   "Socorro"   
## [6] "Lincoln"    "Sierra"
```

* Note: we can use `text` with `st_coordinates` to add labels (see next slide)


```r
opar = par(mar = rep(0, 4))
plot(
  st_geometry(nm_w), 
  border = NA, 
  col = "lightblue"
)
plot(
  st_geometry(nm), 
  add = TRUE
)
plot(
  st_geometry(w_ctr_buf_u_ch), 
  add = TRUE
)
text(
  st_coordinates(st_centroid(nm_w)),
  nm_w$NAME_2
)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-60-1.png" alt="Tunnel between &quot;Sierra&quot; and &quot;Harding&quot; county centroids" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-60)Tunnel between "Sierra" and "Harding" county centroids</p>
</div>

```r
par(opar)
```

* How is the area of the "tunnel" **divided** between the various counties that it crosses?
* We can use the fact that `st_intersection(x, y)` returns all (non-empty) geometries resulting from applying the operation to all geometry pairs in `x` and `y` -


```r
int = st_intersection(w_ctr_buf_u_ch, nm_w)
area = st_area(int)
area
## Units: [m^2]
## [1]  199064581  872145769  813577715  702562404 1119738156  108077571
## [7]  575538789
prop = area / sum(area)
prop
## Units: [1]
## [1] 0.04533773 0.19863456 0.18529546 0.16001130 0.25502469 0.02461508
## [7] 0.13108118
```

* Plot - 


```r
opar = par(mar = rep(0, 4))
plot(
  st_geometry(nm_w),
  border = "darkgrey"
)
plot(
  int,
  col = rainbow(7),
  border = "grey",
  add = TRUE
)
text(
  st_coordinates(st_centroid(int)),
  paste0(round(prop, 2)*100, "%"),
  cex = 2
)
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-62-1.png" alt="Proportion of tunnel area within each county" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-62)Proportion of tunnel area within each county</p>
</div>

```r
par(opar)
```

## Join by attributes

* We can join a **vector layer** and a **table** exactly the same way as **two tables**, e.g. using the `left_join` function from `dplyr`
* This is analogous to **"Join attributes from a table"** in ArcGIS
* In the next example we will join county-level **demographic data** (from `CO-EST2012-Alldata.csv`) with the `county` layer
* The join will be based on the common **Federal Information Processing Standards** (FIPS) code of each county

<div class="figure" style="text-align: center">
<img src="images/lesson_08_arcgis_join_by_attributes.png" alt="Join by attributes in ArcGIS" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-63)Join by attributes in ArcGIS</p>
</div>

* Let's **read** the `CO-EST2012-Alldata.csv` file - 


```r
dat = read.csv(
  "data/CO-EST2012-Alldata.csv", 
  stringsAsFactors = FALSE
)
```

* And **subset** the columns we are interested in - 


```r
dat = dat[, c("STATE", "COUNTY", "CENSUS2010POP")]
```


```r
head(dat)
##   STATE COUNTY CENSUS2010POP
## 1     1      0       4779736
## 2     1      1         54571
## 3     1      3        182265
## 4     1      5         27457
## 5     1      7         22915
## 6     1      9         57322
```

* Records where `COUNTY` code is `0` are states **sums**, which we will remove - 


```r
dat = dat[dat$COUNTY != 0, ]
```


```r
head(dat)
##   STATE COUNTY CENSUS2010POP
## 2     1      1         54571
## 3     1      3        182265
## 4     1      5         27457
## 5     1      7         22915
## 6     1      9         57322
## 7     1     11         10914
```

* To get the county FIPS code we need to **standardize** -
    * The state code to a **two-digit** code 
    * the county code to **three-digit** code
* The `formatC` function can be used to change between various numeric **formats**, using different "scenarios"
* The **"add leading zeros"** scenario is specified using `width=n`, where `n` is the required number of digits, and `flag="0"` - 


```r
dat$STATE = formatC(dat$STATE, width = 2, flag = "0")
dat$COUNTY = formatC(dat$COUNTY, width = 3, flag = "0")
dat$FIPS = paste0(dat$STATE, dat$COUNTY)
```

* Now we have a column named `FIPS` with exactly the **same format** as in the `county` layer - 


```r
head(dat)
##   STATE COUNTY CENSUS2010POP  FIPS
## 2    01    001         54571 01001
## 3    01    003        182265 01003
## 4    01    005         27457 01005
## 5    01    007         22915 01007
## 6    01    009         57322 01009
## 7    01    011         10914 01011
```

* Now we can **join** the `county` layer with the `dat` table, based on the common column named `FIPS` -


```r
county = left_join(
  county,
  dat[, c("FIPS", "CENSUS2010POP")],
  by = "FIPS"
)
```

* Note: we are using a `left_join`, therefore the `county` layer remains as is; features that do not have a matching `FIPS` value in `dat` will have `NA` in the new `CENSUS2010POP` column

* Plot with **linear** breaks - 


```r
plot(county[, "CENSUS2010POP"])
```

* Plot with **quantile** breaks - 


```r
plot(county[, "CENSUS2010POP"], breaks = "quantile")
```

* Note: the number of color categories can be controlled with `nbreaks`

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-74-1.png" alt="Population size per county in the US, linear breaks" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-74)Population size per county in the US, linear breaks</p>
</div>

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-75-1.png" alt="Population size per county in the US, quantile breaks" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-75)Population size per county in the US, quantile breaks</p>
</div>

* Now that we know the **amount** and **area size** we can calculate population **density** per county - 


```r
county$density = county$CENSUS2010POP / county$area
```

* Note: the measurement units for the new column are **automatically** determined based on the inputs
* Plot:


```r
plot(county[, "density"], breaks = "quantile")
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-77-1.png" alt="Population density in the US, quantile breaks" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-77)Population density in the US, quantile breaks</p>
</div>

* Question 1: how many features in `county` did not have a matching FIPS code in `dat`? What are their names?



* Question 2: how many features in `dat` do not have a matching FIPS code in `county`?



* We can calculate the **average population density** in the US, by dividing the total population by the total area - 


```r
sum(county$CENSUS2010POP, na.rm = TRUE) / 
  sum(county$area)
## 39.2295 [1/km^2]
```

* According to **Wikipedia** the correct value is **40.015**
* Note: simply averaging the `density` column gives an overestimation, because all counties get equal weight while in reality the smaller counties are more dense - 


```r
mean(county$density, na.rm = TRUE)
## 93.87977 [1/km^2]
```

## Main data structures in the course

| Category | Class | Lesson |
|---|---|:-:|
| Vector | `numeric`, `character`, `logical` | 02 |
| Date | `Date` | 03 |
| Table | `data.frame` | 04 |
| Matrix | `matrix` | 05 |
| Array | `array` | 05 |
| Raster |  `RasterLayer`, `RasterStack`, `RasterBrick` | 05 |
| Vector layer | `sfg`, `sfc`, `sf` | 07 | 
| Units | `units` | 07 | 
| List | `list` | 10 | 

Table: Main data structures in the course

## `ggplot2`


```r
library(ggplot2)
## Registered S3 methods overwritten by 'ggplot2':
##   method         from 
##   [.quosures     rlang
##   c.quosures     rlang
##   print.quosures rlang

state = st_read("data/state.shp", stringsAsFactors = FALSE)
## Reading layer `state' from data source `/home/michael/Dropbox/Courses/R_2019/data/state.shp' using driver `ESRI Shapefile'
## Simple feature collection with 51 features and 10 fields
## geometry type:  MULTIPOLYGON
## dimension:      XY
## bbox:           xmin: -179.1506 ymin: 18.90986 xmax: 179.7734 ymax: 72.6875
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
state = state[!(state$NAME_1 %in% c("Alaska", "Hawaii")), ]

county$density = as.numeric(county$density)
```


```r
ggplot() +
  geom_sf(
    data = county,
    aes(fill = density),
    colour = NA
  ) +
  geom_sf(
    data = state,
    colour = "white", size = 0.25, fill = NA
  ) +
  scale_fill_distiller(
    name = expression(paste("Density (", km^-2, ")")),
    palette = "Spectral",
    trans = "log10", 
    labels = as.character, breaks = 10^(-1:5)
  ) +
  theme_bw() +
  theme(
    axis.text.y = element_text(angle = 90, hjust = 0.5),
    panel.border = element_blank()
  )
```

<div class="figure" style="text-align: center">
<img src="08-lesson_08_files/figure-html/unnamed-chunk-83-1.png" alt="Population density in the US, using `ggplot2`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-83)Population density in the US, using `ggplot2`</p>
</div>

## Exercise 4 - Submission date **2019-01-13**




























<!--chapter:end:08-lesson_08.Rmd-->

# Geometric operations with rasters {#geometric-operations-with-rasters}



## Contents

* Working with the geometric component of rasters
* Resampling and reprojection
* Topographic calculations
* Filters
* Segmentation

## Aims

* We will make changes in the geometric component of rasters - 
    * Mosaic
    * Clip
    * Aggregation / Disaggregation
    * Resampling and reprojection
* And create new rasters based on the relation between neighboring cells - 
    * Topographic calculations
    * Filtering
    * Segmentation

## Preparation


```r
library(stars)
library(raster)
library(sf)
library(nngeo)
```

## Geometric component of rasters

* In the next few examples, we will process a **Digital Elevation Model (DEM)** raster of **Haifa**, by - 
    * Mosaicking
    * Cropping 
    * Reprojecting
* **Haifa** is located in the following coordinates, which we get from a GeoJSON file named `haifa.geojson` - 


```r
haifa = st_read("data/haifa.geojson", stringsAsFactors = FALSE)
## Reading layer `haifa' from data source `/home/michael/Dropbox/Courses/R_2019/data/haifa.geojson' using driver `GeoJSON'
## Simple feature collection with 1 feature and 1 field
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 34.98957 ymin: 32.79405 xmax: 34.98957 ymax: 32.79405
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
```


```r
st_coordinates(haifa)
##          X        Y
## 1 34.98957 32.79405
```

* We start with two $5\times5$ degree tiles of elevation data from the **Shuttle Radar Topography Mission** (SRTM) dataset 
* The tiles are included as two `.tif` **files** in the course materials  - 


```r
dem1 = read_stars("data/srtm_43_06.tif")
dem2 = read_stars("data/srtm_44_06.tif")
```

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-6-1.png" alt="Two elevation tiles from the SRTM dataset" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-61)Two elevation tiles from the SRTM dataset</p>
</div><div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-6-2.png" alt="Two elevation tiles from the SRTM dataset" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-62)Two elevation tiles from the SRTM dataset</p>
</div>

* The tiles have the same **resolution** and aligned **extents** - 


```r
st_bbox(dem1)
## xmin ymin xmax ymax 
##   30   30   35   35
```


```r
st_bbox(dem2)
## xmin ymin xmax ymax 
##   35   30   40   35
```

* Rasters can be **mosaicked** using either the `merge` or the `mosaic` function
* The difference between them is in handling of **overlapping** cells - 
    * `merge` assigns the value from the **first** raster
    * `mosaic` calculates the value based on **all** layers, using the specified function (e.g. `mean`)
* In our case the tiles **do not overlap**, so it does not matter which function we choose - 


```r
dem = c(dem1, dem2, along = "x")
dem = st_set_crs(dem, 4326)
```

* Plot - 


```r
plot(dem, reset = FALSE)
plot(st_geometry(haifa), col = "red", pch = 16, add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-10-1.png" alt="Merged raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-10)Merged raster</p>
</div>

## Creating `Extent` objects

* The `crop` function can **crop** a raster given - 
    * The input raster
    * An `Extent` object
* An `Extent` object specifies the coordinates of a **bounding box**
* It can be **created** with the `extent` function - 


```r
st_bbox(haifa)
##     xmin     ymin     xmax     ymax 
## 34.98957 32.79405 34.98957 32.79405
```

* Adding a numeric value to an `Extent` object **increases** its size both vertically and horizontally, while keeping the **rectangular** shape
* For example, adding `0.25` to a **"point" extent** creates an $0.25\times0.25$ extent centered around that point - 


```r
haifa_ext = st_buffer(haifa, 0.25, endCapStyle = "SQUARE")
## Warning in st_buffer.sfc(st_geometry(x), dist, nQuadSegs, endCapStyle =
## endCapStyle, : st_buffer does not correctly buffer longitude/latitude data
## dist is assumed to be in decimal degrees (arc_degrees).
haifa_ext
## Simple feature collection with 1 feature and 1 field
## geometry type:  POLYGON
## dimension:      XY
## bbox:           xmin: 34.73957 ymin: 32.54405 xmax: 35.23957 ymax: 33.04405
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
##    name                       geometry
## 1 Haifa POLYGON ((35.23957 33.04405...
```

* Plot - 


```r
plot(dem, reset = FALSE)
plot(st_geometry(haifa_ext), border = "red", add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-13-1.png" alt="An $0.25\times0.25$ degrees \texttt{Extent} object" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-13)An $0.25\times0.25$ degrees \texttt{Extent} object</p>
</div>

## Cropping a raster with an `Extent` object

* The `crop` function **cuts** out a **rectangular** subset of a raster based on an `Extent` - 


```r
dem = dem[haifa_ext]
## although coordinates are longitude/latitude, st_intersects assumes that they are planar
```

* Plot - 


```r
plot(dem)
```

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-15-1.png" alt="Cropped raster" width="62%" />
<p class="caption">(\#fig:unnamed-chunk-15)Cropped raster</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_09_crop.pdf" alt="Cropping a raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-16)Cropping a raster</p>
</div>

http://rpubs.com/etiennebr/visualraster

## Raster aggregation and disaggregation

<div class="figure" style="text-align: center">
<img src="images/lesson_09_raster_resolutions.png" alt="Raster resolutions" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-17)Raster resolutions</p>
</div>

https://datacarpentry.org/organization-geospatial/01-spatial-data-structures-formats/index.html

* In **aggregation**, we create a raster with a lower resolution by dissolving (rectangular) groups of pixels in the original raster, into individual, larger, pixels in the new raster
* **Disaggregation** is the opposite, splitting each raster cell into multiple smaller cells

<div class="figure" style="text-align: center">
<img src="images/lesson_09_aggregation_disaggregation.pdf" alt="Raster aggregation and disaggregation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-18)Raster aggregation and disaggregation</p>
</div>

http://rpubs.com/etiennebr/visualraster

* The `aggregate` function can be used for **aggregation**, given - 
    * `x` - The input raster
    * `fact` - The aggregation factor
    * `fun` - Function applied on values (default is `mean`)
* To calculate the new pixel values, a function `fun` is being applied on the "old" values. The default is `fun=mean`, i.e. the new values are **averages** of the old ones
* The rectangular **neighborhood** size where pixels are dissolved is determined by the aggregation factor `fact`, which can be - 
    * A **single** value, in which case it refers to both x and y, such as: `fact=8`
    * A **pair** of values, in which case the first refers to x and the second one to y, such as: `fact=c(5,10)`

* For example - 


```r
dem = as(dem, "Raster")
dem_agg8 = aggregate(dem, fact = 8)
dem_agg16 = aggregate(dem, fact = 16)
dem = st_as_stars(dem)
dem_agg8 = st_as_stars(dem_agg8)
dem_agg16 = st_as_stars(dem_agg16)
```

* Plot - 


```r
plot(dem_agg8)
plot(dem_agg16)
```

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-21-1.png" alt="Raster aggregation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-211)Raster aggregation</p>
</div><div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-21-2.png" alt="Raster aggregation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-212)Raster aggregation</p>
</div>

* The `disaggregate` function does the **opposite** from `aggregate`
* `disaggregate` **splits** each cell in the "old" raster into several new cells
* Each new cell gets the **same value** as the original larger pixel
* For example - 


```r
# dem_agg8_dis8 = disaggregate(dem_agg8, fact = 8)
```

## Raster resampling

* Raster **resampling** is the process of transferring raster values from the original grid to a new grid

<div class="figure" style="text-align: center">
<img src="images/lesson_09_raster_resampling.png" alt="Raster resampling" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-23)Raster resampling</p>
</div>

https://www.safe.com/transformers/raster-resampler/

* To demonstrate resampling, we will recreate the `ndvi`, `l_rec` and `r` rasters from **Lesson 06** - 


```r
l = read_stars("data/landsat_04_10_2000.tif")
ndvi = (l[,,,4] - l[,,,3]) / (l[,,,4] + l[,,,3])
names(ndvi) = "NDVI"
l_rec = ndvi
l_rec[l_rec < 0.2] = 0
l_rec[l_rec >= 0.2] = 1
```


```r
r = read_stars("data/modis_south.tif")
```

* In the next example we **resample** the `r` raster values into the `ndvi` grid - 


```r
plot(r[, , , 15], reset = FALSE)
plot(ndvi, add = TRUE, reset = FALSE)
plot(st_as_sfc(st_bbox(ndvi)), add = TRUE, border = "red")
```

<img src="09-lesson_09_files/figure-html/unnamed-chunk-26-1.png" width="672" style="display: block; margin: auto;" />

* The `resample` function accepts three arguments - 
    * `x` - The raster we are **resampling**
    * `y` - The raster which defines the **new grid**
    * `method` - The resampling **method**, can be -
        * `"ngb"` - Nearest neighbor 
        * `"bilinear"` - Bilinear, i.e. weighted average of nearest 4 pixels (the default)


```r
r_resample_ngb = st_warp(r[, , , 15], ndvi, use_gdal = TRUE)
r_resample_bil = st_warp(r[, , , 15], ndvi, use_gdal = TRUE, method = "bilinear")
```

* We will **stack** the two layers -


```r
resample_results = c(
  r_resample_ngb, 
  r_resample_bil,
  along = 3
)
# names(resample_results) = c("Nearest", "Bilinear")
```

* Plot:


```r
plot(resample_results)
```

<img src="09-lesson_09_files/figure-html/unnamed-chunk-29-1.png" width="672" style="display: block; margin: auto;" />

## Raster reprojection

* Raster **reprojection** is conceptually related to resampling; the difference in that in reprojection we resample into a grid which is in a **different CRS**
* The `projectRaster` function does raster reprojection -
    * `from` - The raster we want to **reproject**
    * `crs` - The **destination CRS**
    * `method` - The resampling **method**, can be either `"ngb"` or `"bilinear"`
    * `res` - The new grid **resolution** (optional)
* Another option is to specify - 
    * `from` - The raster we want to **reproject**
    * `to` - The raster which defines the **destination grid**

* For example - 




```r
dem = st_warp(src = dem, crs = 32636, method = "near", cellsize = 90)
```

* Plot - 

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-32-1.png" alt="Reprojection result" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-321)Reprojection result</p>
</div><div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-32-2.png" alt="Reprojection result" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-322)Reprojection result</p>
</div>

## Calculations based on neighboring cells

* Calculations based on **neighboring cells** include - 
    * **"Moving window"** calculations - Transformation of raster values using the values from a neighborhood surrounding each pixel (e.g. focal filter, topographic indices)

<div class="figure" style="text-align: center">
<img src="images/lesson_09_focal_example.png" alt="Focal filter" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-33)Focal filter</p>
</div>

http://courses.washington.edu/gis250/lessons/raster_analysis1/index.html

* Calculations based on **neighboring cells** include - 
    * **Segmentation** - Assignment of connected pixels with same (or similar) values into unique segments

<div class="figure" style="text-align: center">
<img src="images/lesson_09_segmentation_example.jpg" alt="Segmentation" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-34)Segmentation</p>
</div>

https://grass.osgeo.org/grass74/manuals/i.segment.html

## Topographic indices

* The most commonly used **topographic** indices are slope and aspect -
    * **Slope** quantifies the maximal change between neighboring cells
    * **Aspect** expresses the *direction* of the maximal change
* Slope and aspect, as well as several other topographic indices such as **flow direction**, can be calculated using the `terrain` function
* The most useful parameters of `terrain` are -
    * `x` - The input **raster**
    * `opt` - The **index** to calculate, can be `"slope"`, `"aspect"`, etc. 
    * `unit` - The **units**, can be `"radians"` (default) or `"degrees"`

* For example - 


```r
slope = raster_slope(dem)
aspect = raster_aspect(dem)
```

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-36-1.png" alt="Topographic aspect and slope calculation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-361)Topographic aspect and slope calculation</p>
</div><div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-36-2.png" alt="Topographic aspect and slope calculation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-362)Topographic aspect and slope calculation</p>
</div><div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-36-3.png" alt="Topographic aspect and slope calculation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-363)Topographic aspect and slope calculation</p>
</div>

## Focal filters

<div class="figure" style="text-align: center">
<img src="images/lesson_09_focal.pdf" alt="Focal filtering" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-37)Focal filtering</p>
</div>

http://rpubs.com/etiennebr/visualraster

* The `focal` function applies a **focal filter** ("moving window"), given - 
    * `x` - The input **raster**
    * `w` - A `matrix` which defines the **neighborhood size** and the **weights**
    * `fun` - The applied **function** (default is `sum`)
* The `w` matrix needs to have an **odd** number of rows and columns (such as $3\times3$, $7\times5$, etc.) because its **central cell** defines the focal window center
* The `w` matrix values determine the **weights**; raster values within the window are first **multiplied** by the weights in `w`, then **passed** to the function `fun`

* For example, the following **matrix** defines a $3\times3$ window with weights of `1` (therefore, essentially no weighting)
* The central cell `[2,2]` is the focal window center


```r
matrix(1, nrow = 3, ncol = 3)
##      [,1] [,2] [,3]
## [1,]    1    1    1
## [2,]    1    1    1
## [3,]    1    1    1
```

* Question: how can we define a non-symmetric neighborhood, such as $2\times2$, even though matrix `w` can't have an even number of rows and columns?

* There are various types of filters for different needs, such as -
    * **Low Pass** filter - Smoothing, reducing noise, through averaging
    * **High Pass** filter - Expresses the deviation of the central cell value from the local average

<div class="figure" style="text-align: center">
<img src="images/lesson_09_filter_low_pass.png" alt="Example of filters (Low pass and High pass)" width="50%" />
<p class="caption">(\#fig:unnamed-chunk-391)Example of filters (Low pass and High pass)</p>
</div><div class="figure" style="text-align: center">
<img src="images/lesson_09_filter_high_pass.png" alt="Example of filters (Low pass and High pass)" width="50%" />
<p class="caption">(\#fig:unnamed-chunk-392)Example of filters (Low pass and High pass)</p>
</div>

http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-analyst-toolbox/how-filter-works.htm

* For example, the following expression applies a **Low Pass** filter with a focal window of $5\times5$ -


```r
w_lp = matrix(1, nrow = 5, ncol = 5)
w_lp
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    1    1    1    1
## [2,]    1    1    1    1    1
## [3,]    1    1    1    1    1
## [4,]    1    1    1    1    1
## [5,]    1    1    1    1    1
```


```r
lp = raster_focal(
  x = ndvi, 
  w = w_lp, 
  fun = mean
)
```

* And the next one applies a **High Pass** filter with a focal window of $5\times5$ - 


```r
w_hp = matrix(-1, nrow = 5, ncol = 5)
w_hp[3, 3] = 24
w_hp
##      [,1] [,2] [,3] [,4] [,5]
## [1,]   -1   -1   -1   -1   -1
## [2,]   -1   -1   -1   -1   -1
## [3,]   -1   -1   24   -1   -1
## [4,]   -1   -1   -1   -1   -1
## [5,]   -1   -1   -1   -1   -1
```


```r
hp = raster_focal(
  x = ndvi, 
  w = w_hp
)
```

* Plot - 


```r
plot(c(lp, hp, along = 3))
```

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-44-1.png" alt="Low Pass and High Pass filters" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-44)Low Pass and High Pass filters</p>
</div>

* Question: what will we get as a result of the following expression?


```r
x = raster_focal(
  ndvi, 
  w = matrix(1, nrow = 5, ncol = 5), 
  fun = length
)
```

* When we apply a **Low Pass** filter more than once, consecutively, we get a higher degree of smoothing
* For example, the following code applies a $7\times7$ Low Pass filter on `l_rec` **10 times** - 


```r
l_rec_lp = l_rec
for(i in 1:10) {
  l_rec_lp = raster_focal(
    x = l_rec_lp,
    w = matrix(1, nrow = 7, ncol = 7),
    fun = mean
  )
}
```

* Plot - 

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-47-1.png" alt="Low Pass filter applied 10 times" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-471)Low Pass filter applied 10 times</p>
</div><div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-47-2.png" alt="Low Pass filter applied 10 times" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-472)Low Pass filter applied 10 times</p>
</div>

* Question 1: why does the outer boundary now has `NA`s?
* Question 2: why does the values range no longer includes `1`?

* Given a raster with `0` and `1` values (such as `l_rec`), we may want to convert all `0` cells neighboring to a `1` cell to become `1`
* This can be achieved with a **focal filter** and `max` - 


```r
get_neighbors = function(m, pos) {
  v = c(
    m[pos[1]-1, pos[2]-1],
    m[pos[1]-1, pos[2]  ],
    m[pos[1]-1, pos[2]+1],
    m[pos[1],   pos[2]-1],
    m[pos[1],   pos[2]+1],
    m[pos[1]+1, pos[2]-1],
    m[pos[1]+1, pos[2]  ],
    m[pos[1]+1, pos[2]+1]
  )
  return(v)
}

focal2 = function(r, fun) {
  template = r[,,,1]
  input = template[[1]][,,1]
  output = input
  output[] = NA
  for(i in 2:(nrow(input) - 1)) {
    for(j in 2:(ncol(input) - 1)) {
      v = get_neighbors(input, c(i, j))
      output[i, j] = fun(v)
    }
  }
  template[[1]] = array(output, dim = c(nrow(output), ncol(output), 1))
  return(template)
}
```


```r
l_rec_focal = focal2(l_rec, max)
```

* Plot - 

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-50-1.png" alt="&quot;Buffering&quot; `1` values in a raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-50)"Buffering" `1` values in a raster</p>
</div>

Note that our custom focal filter function is quite minimal, and can be improved in several ways:

* Dealing with `NA` values
* Dealing with the first/last rows and and columns

## Segmentation

<div class="figure" style="text-align: center">
<img src="images/lesson_09_clump.pdf" alt="Segmentation with the `clump` function" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-51)Segmentation with the `clump` function</p>
</div>

http://rpubs.com/etiennebr/visualraster

* The `clump` function detects **segments** of **connected** pixels with **any value** other than `0` or `NA`, returning a raster where each segment has a **unique ID**
* Cells with `0` or `NA` are treated as **background**, they are not part of any segment
* Using `gaps=FALSE` "forces" the segment IDs to be **consecutive** integers `1`, `2`, ..., `n` (where `n` is the number of segments)
* Note: the `igraph` package needs to be installed for the `clump` function to work

* For example - 


```r
l_rec_focal_clump = st_as_sf(l_rec_focal, merge = TRUE)
l_rec_focal_clump = l_rec_focal_clump[l_rec_focal_clump$NDVI == 1, ]
```

* Question 1: What is the exact number of segments in `l_rec_focal_clump`?
* Question 2: If we ran the `clump` function on `l_rec` instead of `l_rec_focal`, do you think the number of segments would be higher or lower?

* Plot - 


```r
plot(l_rec_focal_clump)
```

<div class="figure" style="text-align: center">
<img src="09-lesson_09_files/figure-html/unnamed-chunk-53-1.png" alt="Segments detected with `raster_clump`" width="62%" />
<p class="caption">(\#fig:unnamed-chunk-53)Segments detected with `raster_clump`</p>
</div>















<!--chapter:end:09-lesson_09.Rmd-->

# Processing spatio-temporal data {#processing-spatio-temporal-data}



## Contents

* Aggregation of spatio-temporal data
* Lists
* Reshaping of trajectory data

## Aims

* Present several characteristics of spatio-temporal data
* Demonstrate aggregation of raster spatio-temporal data
* Demonstrate reshaping of vector trajectory data

## Preparation


```r
library(stars)
library(sf)
library(dplyr)
library(data.table)
```

## Spatio-temporal data

* It can be argued that all data are **spatio-temporal**, since they were measured in certain **location(s)** and **time(s)**, even if the locations and times were not recorded and/or are irrelevant for analysis
* We define spatio-temporal data as data where the locations and times of observation were **recorded** and are **relevant** for analysis

* For example - 
    * Time-series of satellite images
    * Temperature measurements in meteorological stations over time
    * Voting results in administrative units during several election campaigns
    * Movement tracks of people or animals, with or without associated measurements (heart rate, activity type, etc.)
    * Spatial pattern of epidemic disease outbreak
    * Volcanic eruption events
* Methods and tools for processing and analyzing spatio-temporal data are generally **less developed** than methods for working with spatial or temporal data

<div class="figure" style="text-align: center">
<img src="images/lesson_07_space_time1.pdf" alt="Space-time dataset types" width="60%" />
<p class="caption">(\#fig:unnamed-chunk-3)Space-time dataset types</p>
</div>

https://www.jstatsoft.org/article/view/v051i07

<div class="figure" style="text-align: center">
<img src="images/lesson_10_spacetime_pm_points.png" alt="Grid layout: PM point measurements" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-4)Grid layout: PM point measurements</p>
</div>

https://edzer.github.io/UseR2016/

<div class="figure" style="text-align: center">
<img src="images/lesson_10_spacetime_raster.pdf" alt="Grid layout: NDVI image time series" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-5)Grid layout: NDVI image time series</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_10_spacetime_tweets.pdf" alt="Irregular layout: Tweets" width="40%" />
<p class="caption">(\#fig:unnamed-chunk-6)Irregular layout: Tweets</p>
</div>

http://onlinelibrary.wiley.com/doi/10.1111/j.1467-9671.2012.01359.x/abstract

<div class="figure" style="text-align: center">
<img src="images/lesson_10_spacetime_coral_disease.png" alt="Irregular layout: Coral disease cases" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-7)Irregular layout: Coral disease cases</p>
</div>

http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0004993

<div class="figure" style="text-align: center">
<img src="images/flickr_boston.pdf" alt="Trajectory: Flickr user paths" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-8)Trajectory: Flickr user paths</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_10_storm_trajecctories.png" alt="Trajectory: Storm paths" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-9)Trajectory: Storm paths</p>
</div>

https://www.r-spatial.org/r/2017/08/28/nest.html

<div class="figure" style="text-align: center">
<img src="images/lesson_07_space_time2.pdf" alt="Time measurement types" width="75%" />
<p class="caption">(\#fig:unnamed-chunk-10)Time measurement types</p>
</div>

https://www.jstatsoft.org/article/view/v051i07

<div class="figure" style="text-align: center">
<img src="images/lesson_10_earthquakes.png" alt="Instance time: Earthquakes" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-11)Instance time: Earthquakes</p>
</div>

https://earthquake.usgs.gov/earthquakes/map/

<div class="figure" style="text-align: center">
<img src="images/flickr_boston.pdf" alt="Instance, moving object time: Flickr user paths" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-12)Instance, moving object time: Flickr user paths</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_10_israel_borders.png" alt="Consecutive intervals time: Israel borders over time" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-13)Consecutive intervals time: Israel borders over time</p>
</div>

http://perceptionasreality.blogspot.com/2011/05/national-borders-in-flux-1967-israel.html

* **Processing** and **visualization** of spatio-temporal data are **challenging**, because of their **three-dimensional** nature
* One of the basic approaches for working with spatio-temporal data is to **simplify** them using aggregation, in the spatial and/or temporal dimension, to help with visualization and exploratory analysis

<div class="figure" style="text-align: center">
<img src="images/lesson_10_spacetime_jss_paper.png" alt="Pebesma 2012, JSS" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-14)Pebesma 2012, JSS</p>
</div>

https://www.jstatsoft.org/article/view/v051i07

## Aggregation of spatio-temporal raster data

* Let's go back to the `modis_south.tif` raster


```r
r = read_stars("data/MOD13A3_2000_2019.tif")
```

* And also load the associated `dates.csv` table - 


```r
dates = read.csv("data/MOD13A3_2000_2019_dates.csv", stringsAsFactors = FALSE)
dates$date = as.Date(dates$date)
dates$month = as.numeric(format(dates$date, "%m"))
tab = data.frame(
  month = c(12, 1:11),
  season = rep(c("winter","spring","summer","fall"), each = 3),
  stringsAsFactors = FALSE
)
dates = left_join(dates, tab, by = "month")
```


```r
head(dates)
##   layer       date month season
## 1     1 2000-02-01     2 winter
## 2     2 2000-03-01     3 spring
## 3     3 2000-04-01     4 spring
## 4     4 2000-05-01     5 spring
## 5     5 2000-06-01     6 summer
## 6     6 2000-07-01     7 summer
```

* To **aggregate** the raster on the temporal dimension, we need to - 
    * Select **subsets** of raster layers (e.g. seasons)
    * Apply an **overlay** function to summarize each subset into a single layer (e.g. mean)
* However, we can select layers only based on layer **numbers** or layer **names**, *not* based on a **logical** vector

* Subset of raster layers using a `numeric` vector (of layer indices):


```r
# r[[3:4]]
```

* Subset of raster layers using a `character` vector (of layer names) - 


```r
# r[[c("modis_south.3", "modis_south.4")]]
```

* Subset of raster layers using a `logical` vector - 


```r
r[,,,dates$month == 1]
## stars object with 3 dimensions and 1 attribute
## attribute(s), summary of first 1e+05 cells:
##  MOD13A3_2000_2019.tif 
##  Min.   :-0.19         
##  1st Qu.: 0.14         
##  Median : 0.35         
##  Mean   : 0.34         
##  3rd Qu.: 0.49         
##  Max.   : 0.89         
##  NA's   :52588         
## dimension(s):
##      from  to  offset    delta                       refsys point values
## x       1 145 3250139  926.625 +proj=sinu +lon_0=0 +x_0=... FALSE   NULL
## y       1 464 3706965 -926.625 +proj=sinu +lon_0=0 +x_0=... FALSE   NULL
## band    1  19      NA       NA                           NA    NA   NULL
##         
## x    [x]
## y    [y]
## band
```

* We can easily bypass the issue using the `which` function, converting a `logical` vector to a `numeric` one - 


```r
# which(dates$month == 1)
```


```r
# r[[which(dates$month == 1)]]
```



* Question 1: how can we create a subset of `modis_south.tif` with just the images taken during spring?
* Question 2: how can we then calculate the "average" spring NDVI image?

* Now, let's use the same method to create a **seasonal** summary of average NDVI images, including each of the **four** seasons
* We would like to create a raster named `season_means`, having **4 layers**, where each layer is the average NDVI per season - 
    * `"winter"`
    * `"spring"`
    * `"summer"`
    * `"fall"`
* The averages will ignore `NA` values
* We can combine the average layers using the `stack` function

* Function for calculating mean, with `NA`'s excluded -


```r
f = function(x) mean(x, na.rm = TRUE)
```

* Vector of season names -


```r
seasons = c("winter", "spring", "summer", "fall")
```

* Empty `RasterStack` object -

* For each season we -
    * **Subset** layers
    * **Calculate** mean
    * **Add** result to the `season_means` object


```r
season_means = list()
for(i in seasons) {
  v = which(dates$season == i)
  s = r[,,,v]
  season_means[[i]] = st_apply(s, 1:2, mean, na.rm = TRUE)
}
season_means = do.call(c, season_means)
season_means = st_redimension(season_means)
names(season_means) = "NDVI"
```

* And use the `levelplot` function from `rasterVis` to **display** the result - 


```r
plot(season_means)
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-27-1.png" alt="Average NDVI per season" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-27)Average NDVI per season</p>
</div>

* In case we need to summarize the seasonal NDVI in a **different way**, all we have to do is replace the **aggregation function** `f`
* For example, we can decide to have `NA` instead of less reliable pixels where >25% of values are missing
* Instead of the previous function - 


```r
f = function(x) mean(x, na.rm = TRUE)
```

* We use a new definition - 


```r
f_NA = function(x) {
  if(mean(is.na(x)) > 0.25)
    return(NA)
  else
    return(mean(x, na.rm = TRUE))
}
```


```r
season_means = list()
for(i in seasons) {
  v = which(dates$season == i)
  s = r[,,,v]
  season_means[[i]] = st_apply(s, 1:2, f_NA)
}
season_means = do.call(c, season_means)
season_means = st_redimension(season_means)
names(season_means) = "NDVI"
```


```r
plot(season_means)
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-31-1.png" alt="Average NDVI per season, pixels with &gt;25\% `NA` excluded" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-31)Average NDVI per season, pixels with >25\% `NA` excluded</p>
</div>

* Our second example is aggregation in **just one** of the spatial dimensions
* In this case, we will summarize the **west-east** gradient (i.e. a raster row) into a single value
* That way, we will be able to visualize the **north-south** gradient over **time**
* First, we will define a function named `raster_rowMeans` which **accepts** -
    * A raster 
    * A layer number
* and **returns** the vector of **row means** of the specified layer (ignoring `NA`s)


```r
# raster_rowMeans = function(x, layer) {
  # rowMeans(as.matrix(x[[layer]]), na.rm = TRUE)
# }
```

* Using this function we can observe the **north-south** NDVI gradient for specified points in time


```r
x = st_apply(r[,,,1], 1, mean, na.rm = TRUE)[[1]]   # Winter
y = st_apply(r[,,,7], 1, mean, na.rm = TRUE)[[1]]   # Summer
```

* Plot - 


```r
plot(x, type = "l", col = "blue")
lines(y, col = "red")
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-34-1.png" alt="North-south NDVI gradient in two different dates: a winter day (blue) and a summer day (red)" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-34)North-south NDVI gradient in two different dates: a winter day (blue) and a summer day (red)</p>
</div>

* Next we will create a raster `s`, where each **column** will contain the row means of one **layer** of `r`

<div class="figure" style="text-align: center">
<img src="images/lesson_10_row_means.pdf" alt="Raster row means" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-35)Raster row means</p>
</div>

* Raster `s` needs to have - 
    * The same number of **rows** as `r`
    * As **many** columns as `r` **layers**


```r
# s = raster(
#   nrows = nrow(r), 
#   ncols = nlayers(r), 
#   xmn = 0, 
#   xmx = nlayers(r), 
#   ymn = 0, 
#   ymx = nrow(r)
# )
```

* Once the `s` template is ready, we can calculate the values within a `for` loop
* Each **column** in `s` gets the **row means** of a layer in `r` -


```r
r = read_stars("data/MOD13A3_2000_2019.tif")
s = st_apply(r, c(1, 3), mean, na.rm = TRUE)
s = st_set_dimensions(s, "x", values = dim(r)["x"]:1)
s = st_set_dimensions(s, "band", names = "y", values = 1:dim(r)["band"])
s = st_set_dimensions(s, xy = c("y", "x"))
```

* Plot:


```r
plot(s)
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-38-1.png" alt="Row means of `r` over time" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-38)Row means of `r` over time</p>
</div>

## Lists

* A `list` is a **collection** of objects of **any** class
* There are no restrictions as for the **class** and **dimensions** of each list element
* Lists are therefore the most **flexible** of the base R data structures

* A list can be **created** with the `list` function - 


```r
x = list(c(1, 3), c(4, 5, 6), 8)
```


```r
x
## [[1]]
## [1] 1 3
## 
## [[2]]
## [1] 4 5 6
## 
## [[3]]
## [1] 8
```

* List **indices** are marked with `[[`, followed by element contents 

* List elements can be named using `names` -


```r
names(x)
## NULL
```


```r
names(x) = c("a", "b", "c")
```


```r
x
## $a
## [1] 1 3
## 
## $b
## [1] 4 5 6
## 
## $c
## [1] 8
```

## List subsetting

* The `[` operator gives a `list` **subset**, as a **new list** - 


```r
x[1:2]
## $a
## [1] 1 3
## 
## $b
## [1] 4 5 6
```


```r
x[1]
## $a
## [1] 1 3
```

* The `[[` and `$` operators give the **contents** of a **single** `list` element - 


```r
x[[2]]
## [1] 4 5 6
```


```r
x$b
## [1] 4 5 6
```

<div class="figure" style="text-align: center">
<img src="images/lesson_10_pepper.pdf" alt="Subsetting a `list` using the `[` and `[[` operators" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-48)Subsetting a `list` using the `[` and `[[` operators</p>
</div>

http://r4ds.had.co.nz/vectors.html

## The `lapply` function

* The `lapply` function "splits" a `list` to individual elements
* Calls a function on each element
* Combines the results to a new list

<div class="figure" style="text-align: center">
<img src="images/lesson_10_apply_vs_lapply.pdf" alt="`apply` and `lapply`" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-49)`apply` and `lapply`</p>
</div>


```r
lapply(x, mean)
## $a
## [1] 2
## 
## $b
## [1] 5
## 
## $c
## [1] 8
lapply(x, range)
## $a
## [1] 1 3
## 
## $b
## [1] 4 6
## 
## $c
## [1] 8 8
lapply(x, is.na)
## $a
## [1] FALSE FALSE
## 
## $b
## [1] FALSE FALSE FALSE
## 
## $c
## [1] FALSE
```

## The `split` function

* The `split` function can **split** a `data.frame` to a `list` of smaller `data.frame`s, according to **unique** values of the given vector

<div class="figure" style="text-align: center">
<img src="images/lesson_10_split.pdf" alt="The `split` function" width="50%" />
<p class="caption">(\#fig:unnamed-chunk-51)The `split` function</p>
</div>


```r
dat = data.frame(
  y = c(3, 5, 1, 4, 5),
  g = c("f", "m", "f", "f", "m"), 
  stringsAsFactors = FALSE
)
```


```r
dat
##   y g
## 1 3 f
## 2 5 m
## 3 1 f
## 4 4 f
## 5 5 m
```


```r
dat_s = split(dat, dat$g)
```


```r
dat_s
## $f
##   y g
## 1 3 f
## 3 1 f
## 4 4 f
## 
## $m
##   y g
## 2 5 m
## 5 5 m
```

## The `do.call` function

* The `do.call` function can be used to pass a `list` of function **arguments** to a function
* The following two expressions are **equivalent** - 


```r
f(a, b, c, d)
```


```r
do.call(f, list(a, b, c, d))
```

* `do.call` is useful when we want to call a function with a **large** or **variable** number of arguments - as `list` elements - without having to specify their **names**

* For example - 


```r
c(x[[1]], x[[2]], x[[3]])
## [1] 1 3 4 5 6 8
```


```r
do.call(c, x)
## a1 a2 b1 b2 b3  c 
##  1  3  4  5  6  8
```

## Storm trajectory data

* As an example of how `list`s, `split` and `do.call` can be useful when working with **spatial data**, we will create a line layer from a table of point observations `storms` - 


```r
storms = as.data.frame(storms)
vars = c(
  "name", "year", "month", "day", "hour", 
  "long", "lat"
)
storms = storms[, vars]
```

* The dataset contains **storm location** info at consecutive points over time - 


```r
head(storms)
##   name year month day hour  long  lat
## 1  Amy 1975     6  27    0 -79.0 27.5
## 2  Amy 1975     6  27    6 -79.0 28.5
## 3  Amy 1975     6  27   12 -79.0 29.5
## 4  Amy 1975     6  27   18 -79.0 30.5
## 5  Amy 1975     6  28    0 -78.8 31.5
## 6  Amy 1975     6  28    6 -78.7 32.4
```

## Storm IDs

* To distinguish between individual storm tracks we can create a unique **ID** variable
* Storm name is not unique - there are storms of the same name in different years


```r
x = paste(storms$name, storms$year)
x = unique(sort(x))
tail(x)
## [1] "Two 2010"   "Two 2014"   "Vince 2005" "Wilma 2005" "Zeta 2005" 
## [6] "Zeta 2006"
```

* We could create an ID that combines **year** and **storm name**... 
* However a storm can span over two different years!


```r
head(storms[storms$name == "Zeta", ], 10)
##      name year month day hour  long  lat
## 7372 Zeta 2005    12  30    0 -35.6 23.9
## 7373 Zeta 2005    12  30    6 -36.1 24.2
## 7374 Zeta 2005    12  30   12 -36.6 24.7
## 7375 Zeta 2005    12  30   18 -37.0 25.2
## 7376 Zeta 2005    12  31    0 -37.3 25.6
## 7377 Zeta 2005    12  31    6 -37.6 25.7
## 7378 Zeta 2005    12  31   12 -37.9 25.7
## 7379 Zeta 2005    12  31   18 -38.1 25.7
## 7380 Zeta 2006     1   1    0 -38.3 25.6
## 7381 Zeta 2006     1   1    6 -38.4 25.4
```

* We need a unique ID for each **consecutive sequence** of storm names, assuming that no two consecutive storms will be given the same name, using function `rleid` from `data.table`


```r
storms$id = rleid(storms$name)
```


```r
head(storms)
##   name year month day hour  long  lat id
## 1  Amy 1975     6  27    0 -79.0 27.5  1
## 2  Amy 1975     6  27    6 -79.0 28.5  1
## 3  Amy 1975     6  27   12 -79.0 29.5  1
## 4  Amy 1975     6  27   18 -79.0 30.5  1
## 5  Amy 1975     6  28    0 -78.8 31.5  1
## 6  Amy 1975     6  28    6 -78.7 32.4  1
```

## To points

* The table can be converted to a **point layer** with `st_as_sf` using the `long` and `lat` columns -


```r
pnt = st_as_sf(
  storms, 
  coords = c("long", "lat"), 
  crs = 4326
)
```


```r
pnt
## Simple feature collection with 10010 features and 6 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: -109.3 ymin: 7.2 xmax: -6 ymax: 51.9
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
## First 10 features:
##    name year month day hour id           geometry
## 1   Amy 1975     6  27    0  1   POINT (-79 27.5)
## 2   Amy 1975     6  27    6  1   POINT (-79 28.5)
## 3   Amy 1975     6  27   12  1   POINT (-79 29.5)
## 4   Amy 1975     6  27   18  1   POINT (-79 30.5)
## 5   Amy 1975     6  28    0  1 POINT (-78.8 31.5)
## 6   Amy 1975     6  28    6  1 POINT (-78.7 32.4)
## 7   Amy 1975     6  28   12  1   POINT (-78 33.3)
## 8   Amy 1975     6  28   18  1     POINT (-77 34)
## 9   Amy 1975     6  29    0  1 POINT (-75.8 34.4)
## 10  Amy 1975     6  29    6  1   POINT (-74.8 34)
```

* Plot:


```r
plot(pnt)
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-68-1.png" alt="The `storms` points" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-68)The `storms` points</p>
</div>

## Points to lines

* How can we go from a **point** layer to a **line** layer?
    * **Select** all points of the same storm
    * **Order** by time, earliest to latest
    * **Merge** point to a line
    * **Repeat** for all storms in the point layer

* We **split** the point layer by storm **ID** - 


```r
lines = split(pnt, pnt$id)
```

## Trajectory data


```r
lines[1]
## $`1`
## Simple feature collection with 30 features and 6 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: -79 ymin: 27.5 xmax: -51.6 ymax: 44.5
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
## First 10 features:
##    name year month day hour id           geometry
## 1   Amy 1975     6  27    0  1   POINT (-79 27.5)
## 2   Amy 1975     6  27    6  1   POINT (-79 28.5)
## 3   Amy 1975     6  27   12  1   POINT (-79 29.5)
## 4   Amy 1975     6  27   18  1   POINT (-79 30.5)
## 5   Amy 1975     6  28    0  1 POINT (-78.8 31.5)
## 6   Amy 1975     6  28    6  1 POINT (-78.7 32.4)
## 7   Amy 1975     6  28   12  1   POINT (-78 33.3)
## 8   Amy 1975     6  28   18  1     POINT (-77 34)
## 9   Amy 1975     6  29    0  1 POINT (-75.8 34.4)
## 10  Amy 1975     6  29    6  1   POINT (-74.8 34)
```

* Ordering the points, or making sure they are aready ordered, is essential to connect storm track points in **chronological order** -


```r
f = function(x) x[order(x$year, x$month, x$day, x$hour), ]
lines = lapply(lines, f)
```


```r
plot(lines[[1]])
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-72-1.png" alt="The `storms` points" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-72)The `storms` points</p>
</div>

* Then, we **combine** all `POINT` geometries to a single `MULTIPOINT` geometry
* Note: `st_combine` combines geometries without dissovling borders (unlike `st_union`)


```r
lines = lapply(lines, st_combine)
```


```r
lines[1]
## $`1`
## Geometry set for 1 feature 
## geometry type:  MULTIPOINT
## dimension:      XY
## bbox:           xmin: -79 ymin: 27.5 xmax: -51.6 ymax: 44.5
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
## MULTIPOINT (-79 27.5, -79 28.5, -79 29.5, -79 3...
```


```r
plot(lines[[1]])
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-75-1.png" alt="The `storms` points" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-75)The `storms` points</p>
</div>

* Now the `MULTIPOINT` can be **cast** to `LINESTRING` - 


```r
lines = lapply(lines, st_cast, "LINESTRING")
```


```r
lines[1]
## $`1`
## Geometry set for 1 feature 
## geometry type:  LINESTRING
## dimension:      XY
## bbox:           xmin: -79 ymin: 27.5 xmax: -51.6 ymax: 44.5
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
## LINESTRING (-79 27.5, -79 28.5, -79 29.5, -79 3...
```


```r
plot(lines[[1]])
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-78-1.png" alt="The `storms` points" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-78)The `storms` points</p>
</div>

* We have a `list` of **individual** `LINESTRING` geometries
* The list can be **combined** back to an `sfc` geometry column with `do.call` - 


```r
geometry = do.call(c, lines)
```


```r
geometry
## Geometry set for 425 features 
## geometry type:  LINESTRING
## dimension:      XY
## bbox:           xmin: -109.3 ymin: 7.2 xmax: -6 ymax: 51.9
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
## First 5 geometries:
## LINESTRING (-79 27.5, -79 28.5, -79 29.5, -79 3...
## LINESTRING (-69.8 22.4, -71.1 21.9, -72.5 21.6,...
## LINESTRING (-48.9 34.9, -49.1 35.2, -48.9 35.3,...
## LINESTRING (-72.8 26, -73 26.3, -73.4 26, -73.2...
## LINESTRING (-58 23, -58.1 23.7, -58.2 24.3, -58...
```


```r
plot(geometry)
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-81-1.png" alt="The `storms` points" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-81)The `storms` points</p>
</div>

* To attach storm **IDs** back to the geometries, we can rely on the fact that feature order was kept intact - 


```r
attr = data.frame(
  id = names(lines), 
  stringsAsFactors = FALSE
)
```


```r
head(attr)
##   id
## 1  1
## 2  2
## 3  3
## 4  4
## 5  5
## 6  6
```


```r
lines = st_sf(geometry, attr)
lines
## Simple feature collection with 425 features and 1 field
## geometry type:  LINESTRING
## dimension:      XY
## bbox:           xmin: -109.3 ymin: 7.2 xmax: -6 ymax: 51.9
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
## First 10 features:
##    id                       geometry
## 1   1 LINESTRING (-79 27.5, -79 2...
## 2   2 LINESTRING (-69.8 22.4, -71...
## 3   3 LINESTRING (-48.9 34.9, -49...
## 4   4 LINESTRING (-72.8 26, -73 2...
## 5   5 LINESTRING (-58 23, -58.1 2...
## 6   6 LINESTRING (-88.4 26.9, -88...
## 7   7 LINESTRING (-80 32.8, -79 3...
## 8   8 LINESTRING (-62.9 26.9, -64...
## 9   9 LINESTRING (-97 25.7, -97.4...
## 10 10 LINESTRING (-90.4 25.3, -91...
```


```r
plot(lines)
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-85-1.png" alt="The `storms` line layer" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-85)The `storms` line layer</p>
</div>

* Overall distance that each storm has traveled - 


```r
lines$length = st_length(lines)
lines
## Simple feature collection with 425 features and 2 fields
## geometry type:  LINESTRING
## dimension:      XY
## bbox:           xmin: -109.3 ymin: 7.2 xmax: -6 ymax: 51.9
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
## First 10 features:
##    id                       geometry        length
## 1   1 LINESTRING (-79 27.5, -79 2... 3510012.0 [m]
## 2   2 LINESTRING (-69.8 22.4, -71... 3177598.3 [m]
## 3   3 LINESTRING (-48.9 34.9, -49... 1469864.8 [m]
## 4   4 LINESTRING (-72.8 26, -73 2... 2148308.5 [m]
## 5   5 LINESTRING (-58 23, -58.1 2... 3226682.2 [m]
## 6   6 LINESTRING (-88.4 26.9, -88... 1600143.2 [m]
## 7   7 LINESTRING (-80 32.8, -79 3... 2145905.6 [m]
## 8   8 LINESTRING (-62.9 26.9, -64... 2392209.7 [m]
## 9   9 LINESTRING (-97 25.7, -97.4...  455724.8 [m]
## 10 10 LINESTRING (-90.4 25.3, -91...  953824.1 [m]
```


```r
plot(lines[, "length"])
```

<div class="figure" style="text-align: center">
<img src="10-lesson_10_files/figure-html/unnamed-chunk-87-1.png" alt="The `storms` line layer, with length" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-87)The `storms` line layer, with length</p>
</div>

## Exercise 5 - Submission date **2019-02-03**













<!--chapter:end:10-lesson_10.Rmd-->

# Combining rasters and vector layers {#combining-rasters-and-vector-layers}



## Contents

* **Raster**→**Vector** and **Vector**→**Raster** conversions
* **Clipping** and **masking** a raster based on a vector layer
* **Extracting** raster values based on a vector layer

## Aims

* Learn how to move from vector to raster representation, and vice versa
* Learn how to get raster values from locations defined in a vector layer

## Preparation


```r
library(sf)
library(units)
library(stars)
library(nngeo)
```

## Vector layer → raster

* Recreating the `l_rec_focal_clump` raster from **Lesson 09** - 


```r
l = read_stars("data/landsat_04_10_2000.tif")
ndvi = (l[,,,4] - l[,,,3]) / (l[,,,4] + l[,,,3]) 
l_rec = ndvi
l_rec[l_rec <= 0.2] = 0
l_rec[l_rec > 0.2] = 1
l_rec_focal = raster_focal(l_rec, w = matrix(1, nrow = 3, ncol = 3), fun = max)
l_rec_focal_clump = raster_clump(l_rec_focal)
```

* In the following examples we will use a point layer with the locations of Lehavim and Lahav Kibbutz -


```r
towns = st_read("data/towns.geojson", stringsAsFactors = FALSE)
## Reading layer `towns' from data source `/home/michael/Dropbox/Courses/R_2019/data/towns.geojson' using driver `GeoJSON'
## Simple feature collection with 2 features and 1 field
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 34.81695 ymin: 31.37384 xmax: 34.87131 ymax: 31.37936
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
towns = st_transform(towns, st_crs(l))
towns
## Simple feature collection with 2 features and 1 field
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 672790.3 ymin: 3472460 xmax: 677950.1 ymax: 3473160
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
##            name                 geometry
## 1 Lahav Kibbutz POINT (677950.1 3473160)
## 2       Lehavim POINT (672790.3 3472460)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-5-1.png" alt="Location of Lehavim and Lahav Kibbutz" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-5)Location of Lehavim and Lahav Kibbutz</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_11_rasterize.pdf" alt="Conversion of points, lines and polygons to raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-6)Conversion of points, lines and polygons to raster</p>
</div>

http://rpubs.com/etiennebr/visualraster

* The `rasterize` function **converts** a vector layer to a raster, given -
    * `x` - A vector layer
    * `y` - A raster "template"
* The resulting raster will have `NA` values in pixels that **do not overlap** with the vector layer
* The **value** of those pixels which **do overlap** can be determined in several ways, using the `field` and `fun` parameters - 
    * `field` determines which values will be **passed** to the raster; this can be - 
        * A constant value (e.g. `105`)
        * A vector of the same length as the number of features
        * A name of a vector layer attribute (e.g. `"annual"`)
    * `fun` determines how pixel value is calculated when **more than one** feature overlaps with the same pixel
        * A function, such as `min`, `max`, `mean`
        * A text value, such as `"first"`, `"last"`, `"count"`, `"sum"`, `"min"`, `"max"`

* For example, let's **transform** the `towns` vector layer to a raster, using `r` as a template -


```r
r = read_stars("data/modis_south.tif")
template = r[,,,1]
template[[1]][] = NA
towns$id = 1:2
towns_r = st_rasterize(towns[, "id"], template)
```

* The result has the **same dimensions** of `r` but **different values** -


```r
towns_r
## stars object with 2 dimensions and 1 attribute
## attribute(s):
##       id       
##  Min.   :1.00  
##  1st Qu.:1.25  
##  Median :1.50  
##  Mean   :1.50  
##  3rd Qu.:1.75  
##  Max.   :2.00  
##  NA's   :9998  
## dimension(s):
##   from  to  offset delta                       refsys point values    
## x    1 100  660000   500 +proj=utm +zone=36 +ellps... FALSE   NULL [x]
## y    1 100 3495000  -500 +proj=utm +zone=36 +ellps... FALSE   NULL [y]
```

* Plot - 


```r
plot(towns_r, col = c("pink", "yellow"), reset = FALSE)
plot(st_geometry(towns), add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-9-1.png" alt="Point layer converted to raster" width="85%" />
<p class="caption">(\#fig:unnamed-chunk-9)Point layer converted to raster</p>
</div>

* **Cropping** the raster will help see the result more clearly - 


```r
b = st_bbox(towns)
b = st_as_sfc(b)
b = st_buffer(b, 3000)
towns_r = st_crop(towns_r, b)
```


```r
plot(towns_r, col = c("pink", "yellow"), reset = FALSE)
plot(st_geometry(towns), add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-11-1.png" alt="Point layer converted to raster \&amp; cropped" width="672" />
<p class="caption">(\#fig:unnamed-chunk-11)Point layer converted to raster \& cropped</p>
</div>

## Raster → Points

* The **Raster→Points** transformation is done using function `rasterToPoints`
* Pixel **centers** - except for pixels with `NA` in all layers - become points
* We need to use `spatial=TRUE` to get a **spatial** (`Spatial*`) object
* The **attribute table** of the point layer contains the raster values

* For example, let's take a **subset** of the `r` raster with - 
    * Layers 1-2
    * Columns 1-3
    * Rows 1-3


```r
u = r[, 1:3, 1:3, 1:2]
```

* We will **replace** some of the pixel values with `NA` - 


```r
sel = u
sel[[1]][] = 0
sel[[1]][3,2,1] = 1
sel[[1]][2,3,] = 1
u[sel == 1] = NA
```

* Now, we **transform** `u` to a point layer `p` -


```r
p = st_as_sf(u, as_points = TRUE)
```

* Note that there are **8 points** even though the raster has **9 pixels**, because one of the pixels had `NA` in all layers and was **not converted** to a point


```r
p
## Simple feature collection with 8 features and 2 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 660250 ymin: 3493750 xmax: 661250 ymax: 3494750
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
##   modis_south.tif.V1 modis_south.tif.V2               geometry
## 1             0.4242             0.4518 POINT (660250 3494750)
## 2             0.3995             0.3334 POINT (660750 3494750)
## 3             0.4190             0.3430 POINT (661250 3494750)
## 4             0.4495             0.4846 POINT (660250 3494250)
## 5             0.2925             0.3223 POINT (660750 3494250)
## 6                 NA             0.3535 POINT (661250 3494250)
## 7             0.4998             0.5841 POINT (660250 3493750)
## 8             0.7126             0.5086 POINT (661250 3493750)
```


```r
plot(u[,,,1], reset = FALSE)
plot(st_geometry(p), add = TRUE)
text(st_coordinates(p), as.character(round(p$modis_south.tif.V1, 2)),pos = 3)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-16-1.png" alt="Point layer created from a raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-161)Point layer created from a raster</p>
</div>

```r
plot(u[,,,2], reset = FALSE)
plot(st_geometry(p), add = TRUE)
text(st_coordinates(p), as.character(round(p$modis_south.tif.V2, 2)),pos = 3)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-16-2.png" alt="Point layer created from a raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-162)Point layer created from a raster</p>
</div>

## Extracting raster values based on point layer

<div class="figure" style="text-align: center">
<img src="images/lesson_11_extract.pdf" alt="Extracting raster values" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-17)Extracting raster values</p>
</div>

http://rpubs.com/etiennebr/visualraster

* The `extract` function can be used to **"extract"** raster values based on another spatial layer
* The simplest case is extracting values based on a **point** layer, because then each feature always intersects **just one** raster cell
* For example, we can determine the `modis_avg` value for **each point** in the `rainfall` layer as follows - 


```r
rainfall = st_read("data/rainfall_pnt.shp", stringsAsFactors = FALSE)
## Reading layer `rainfall_pnt' from data source `/home/michael/Dropbox/Courses/R_2019/data/rainfall_pnt.shp' using driver `ESRI Shapefile'
## Simple feature collection with 169 features and 12 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 629301.4 ymin: 3270290 xmax: 761589.2 ymax: 3681163
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
modis_avg = read_stars("data/modis_average.tif")
rainfall$ndvi = raster_extract(modis_avg, rainfall)
```

* Note: `extract` works with `sf` layers, so we don't need to convert to `sp` layers with `as(..., "Spatial")`

* Plot - 


```r
plot(modis_avg, reset = FALSE)
text(st_coordinates(rainfall), as.character(round(rainfall$ndvi, 2)), cex = 0.5, col = "black")
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-19-1.png" alt="Raster values extracted to points" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-19)Raster values extracted to points</p>
</div>

* **Plotting** NDVI as function of rainfall in December - 

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-20-1.png" alt="Average NDVI as function of average rainfall in December" width="62%" />
<p class="caption">(\#fig:unnamed-chunk-20)Average NDVI as function of average rainfall in December</p>
</div>

* What is the **number** and **proportion** of `rainfall` points that have an `NA` value in the `ndvi` column?


```r
sum(is.na(rainfall$ndvi))   # Number of stations
## [1] 2
```


```r
mean(is.na(rainfall$ndvi))  # Proportion of stations
## [1] 0.01183432
```

* Why did these 2 stations get `NA`?

* As another example, we will **extract** NDVI values from the first layer of `modis_south.tif`, to a column named `ndvi_south1` - 


```r
rainfall$ndvi_south1 = raster_extract(r[,,,1], rainfall)
```

* Subset - 


```r
rs = rainfall[!is.na(rainfall$ndvi_south1), ]
```

* Plot - 


```r
m = max(
  c(rs$ndvi, rs$ndvi_south1), 
  na.rm = TRUE
)
plot(
  rainfall$ndvi, rainfall$ndvi_south1,
  xlab = "NDVI average (2000-2012)",
  ylab = "NDVI on 2000-02-18",
  xlim = c(0, m), ylim = c(0, m)
)
abline(a = 0, b = 1, col = "red")
text(
  rainfall$ndvi, rainfall$ndvi_south1,
  rainfall$name,
  pos = 1
)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-26-1.png" alt="Average NDVI vs. NDVI from particular date" width="70%" />
<p class="caption">(\#fig:unnamed-chunk-26)Average NDVI vs. NDVI from particular date</p>
</div>

* Map - 


```r
plot(r[,,,1], reset = FALSE)
plot(st_geometry(rs), add = TRUE)
text(
  st_coordinates(rs), 
  rs$name, 
  pos = 3
)
text(
  st_coordinates(rs), 
  as.character(round(rs$ndvi_south1, 2)), 
  pos = 1
)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-27-1.png" alt="Raster values extracted to points" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-27)Raster values extracted to points</p>
</div>

* Similarly to the behavior or raster subsetting (**Lesson 06**), `extract` returns a `matrix` when the raster has **more than one** layer
* In the resulting matrix, **rows** represent vector layer features and **columns** represent raster layers - 


```r
v = rainfall[rainfall$name %in% c("Lahav", "Yatir"), ]
x = raster_extract(r[,,,1:3], v)
```


```r
class(x)
## [1] "matrix"
```


```r
x
##      layer.1 layer.2 layer.3
## [1,]  0.3338  0.4366  0.6072
## [2,]  0.3475  0.3591  0.3481
```

* We can rely on the fact that row and column **order** matches the feature and layer order, respectively, to assign **names** - 


```r
rownames(x) = v$name
```


```r
dates = read.csv("data/dates2.csv")
dates$date = as.Date(dates$date)
colnames(x) = format(dates$date[1:3])
```


```r
x
##       2000-02-18 2000-03-05 2000-03-21
## Lahav     0.3338     0.4366     0.6072
## Yatir     0.3475     0.3591     0.3481
```

<div class="figure" style="text-align: center">
<img src="images/lesson_11_arcgis_extract_multi_values_1.png" alt="&quot;Extract Multi Values to Points&quot; tool in ArcGIS" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-34)"Extract Multi Values to Points" tool in ArcGIS</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/lesson_11_arcgis_extract_multi_values_2.png" alt="&quot;Extract Multi Values to Points&quot; tool in ArcGIS" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-35)"Extract Multi Values to Points" tool in ArcGIS</p>
</div>

* The following example uses a **GPX** (GPS Exchange Format) file
* A GPX file contains one or more **layers**, of the following types - 
    * `waypoints`
    * `tracks` (recorder track as line)
    * `routes`
    * `track_points` (recorder track as points)
    * `route_points`
    
* To find out which **layers** the file contains we can use `st_layers` - 


```r
st_layers("data/track.gpx")
## Driver: GPX 
## Available layers:
##     layer_name     geometry_type features fields
## 1    waypoints             Point        0     23
## 2       routes       Line String        0     12
## 3       tracks Multi Line String        1     13
## 4 route_points             Point        0     25
## 5 track_points             Point     5091     26
```

* Then we can read a **particular layer** into R - 


```r
track = st_read("data/track.gpx", "track_points")
## Reading layer `track_points' from data source `/home/michael/Dropbox/Courses/R_2019/data/track.gpx' using driver `GPX'
## Simple feature collection with 5091 features and 26 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 34.81256 ymin: 31.78945 xmax: 35.20186 ymax: 31.89124
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
```

* **Plotting** the track points on top of an elevation raster - 


```r
elevation = read_stars("data/elevation.tif")
track = st_transform(track, st_crs(elevation))
```


```r
ext = st_bbox(track)
ext[1:2] = ext[1:2] - 20000
ext[3:4] = ext[3:4] + 20000
plot(st_crop(elevation, ext), reset = FALSE)
plot(st_geometry(track), add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-39-1.png" alt="GPS track and elevation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-39)GPS track and elevation</p>
</div>

* **Extracting** elevation values - 


```r
profile = raster_extract(elevation, track)
```

* Plot - 


```r
plot(profile, type = "l", ylab = "Elevation (m)")
lines(track$ele, col = "red")
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-41-1.png" alt="Elevation profile" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-41)Elevation profile</p>
</div>

## Raster to contour lines

* Reconstructing the **Haifa DEM** from **Lesson 09** - 


```r
dem1 = read_stars("data/srtm_43_06.tif")
dem2 = read_stars("data/srtm_44_06.tif")
dem = c(dem1, dem2, along = "x")
dem = st_set_crs(dem, 4326)
haifa = st_read("data/haifa.geojson", stringsAsFactors = FALSE)
## Reading layer `haifa' from data source `/home/michael/Dropbox/Courses/R_2019/data/haifa.geojson' using driver `GeoJSON'
## Simple feature collection with 1 feature and 1 field
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 34.98957 ymin: 32.79405 xmax: 34.98957 ymax: 32.79405
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
haifa_ext = st_buffer(haifa, 0.25, endCapStyle = "SQUARE")
## Warning in st_buffer.sfc(st_geometry(x), dist, nQuadSegs, endCapStyle =
## endCapStyle, : st_buffer does not correctly buffer longitude/latitude data
## dist is assumed to be in decimal degrees (arc_degrees).
dem = dem[haifa_ext]
## although coordinates are longitude/latitude, st_intersects assumes that they are planar
dem = st_normalize(dem)
dem = st_warp(src = dem, crs = 32636, method = "near", cellsize = 90)
```

* Raster **contours** can be created using the `rasterToContour` function
* The `levels` parameter determines the raster **values** where contour lines are drawn - 


```r
range(dem$srtm_43_06.tif, na.rm = TRUE)
## [1] -14 541
```


```r
dem_contour = st_contour(dem, breaks = seq(-100, 600, 100), contour_lines = TRUE)
```

* The result is a `LINESTRING` layer with one feature per contour line - 


```r
dem_contour
## Simple feature collection with 355 features and 1 field
## geometry type:  LINESTRING
## dimension:      XY
## bbox:           xmin: 678646 ymin: 3602433 xmax: 710056 ymax: 3658413
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +datum=WGS84 +units=m +no_defs
## First 10 features:
##    srtm_43_06.tif                       geometry
## 1       (100,200] LINESTRING (707152.2 365841...
## 2         (0,100] LINESTRING (701371 3658233,...
## 3         (0,100] LINESTRING (702237.2 365823...
## 4       (100,200] LINESTRING (704971 3657198,...
## 5         (0,100] LINESTRING (702271 3657085,...
## 6         (0,100] LINESTRING (701326 3657018,...
## 7        [-100,0] LINESTRING (695566 3656084,...
## 8       (300,400] LINESTRING (709156 3655998,...
## 9       (200,300] LINESTRING (708031 3655729,...
## 10      (200,300] LINESTRING (708301 3655665,...
```

Plot - 


```r
plot(dem, reset = FALSE)
plot(st_geometry(dem_contour), col = "red", add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-46-1.png" alt="Contour lines" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-46)Contour lines</p>
</div>

## Raster → Polygons

* The `rasterToPolygons` function makes the **Raster→Polygons** conversion
* Similarly to `rasterToPoints`, the function creates a **polygon** in place of each raster **pixel**, except for `NA` pixels
* A useful option `dissolve=TRUE` **dissolves** all polygons that have the same raster value into a single feature
* Note: the `rgeos` package needs to be installed to use `dissolve=TRUE`


```r
pol = st_as_sf(l_rec_focal_clump, merge = TRUE)
```

* Plot - 


```r
plot(l, rgb = c(3, 2, 1), reset = FALSE)
plot(st_geometry(pol), border = "yellow", add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-48-1.png" alt="Raster to polygons" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-48)Raster to polygons</p>
</div>

* Next, we subset only those polygons with **area** >1 $km^2$ -


```r
pol$area = st_area(pol)
pol
## Simple feature collection with 536 features and 2 fields
## geometry type:  POLYGON
## dimension:      XY
## bbox:           xmin: 663975 ymin: 3459405 xmax: 687645 ymax: 3488145
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
## First 10 features:
##    clumps                       geometry        area
## 1       3 POLYGON ((675615 3488145, 6...  5400 [m^2]
## 2       4 POLYGON ((676455 3488145, 6...  5400 [m^2]
## 3       6 POLYGON ((681945 3488145, 6...  8100 [m^2]
## 4       7 POLYGON ((684765 3488145, 6... 10800 [m^2]
## 5      12 POLYGON ((687195 3488145, 6... 20700 [m^2]
## 6      13 POLYGON ((686985 3488085, 6... 13500 [m^2]
## 7      11 POLYGON ((686505 3488145, 6... 29700 [m^2]
## 8       1 POLYGON ((665865 3488145, 6... 45000 [m^2]
## 9       9 POLYGON ((685545 3488145, 6... 47700 [m^2]
## 10     14 POLYGON ((686835 3487905, 6... 27000 [m^2]
```


```r
large = pol$area > set_units(1, "km^2")
pol = pol[large, ]
pol
## Simple feature collection with 8 features and 2 fields
## geometry type:  POLYGON
## dimension:      XY
## bbox:           xmin: 666105 ymin: 3459465 xmax: 684885 ymax: 3488145
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
##     clumps                       geometry           area
## 84       5 POLYGON ((676575 3488145, 6... 10137600 [m^2]
## 105      2 POLYGON ((666375 3488145, 6...  1223100 [m^2]
## 148     56 POLYGON ((667065 3486405, 6...  1099800 [m^2]
## 225    200 POLYGON ((677775 3479775, 6...  1328400 [m^2]
## 251    221 POLYGON ((675435 3478245, 6...  1931400 [m^2]
## 356    281 POLYGON ((674865 3474345, 6...  9492300 [m^2]
## 391    314 POLYGON ((679815 3472005, 6...  6784200 [m^2]
## 518    432 POLYGON ((675915 3461625, 6...  1939500 [m^2]
```


```r
plot(l, rgb = c(3, 2, 1), reset = FALSE)
plot(
  st_geometry(pol),
  border = "yellow",
  add = TRUE
)
plot(
  st_geometry(towns),
  col = "red",
  pch = 16,
  add = TRUE
)
text(
  st_coordinates(towns),
  towns$name,
  pos = 3,
  col = "white"
)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-51-1.png" alt="Large polygons" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-51)Large polygons</p>
</div>

## Distance calculation

* Our goal is to select the two large polygons corresponding to Lahav and Kramim **forests**
* To do that, we can - 
    * **Sort** the polygons **by distance** to Lahav Kibbutz
    * **Select** the first two
* First, we create a **distance matrix** between the towns and the polygons - 


```r
dist_towns = st_distance(towns, pol, byid = TRUE)
dist_towns
## Units: [m]
##          [,1]     [,2]     [,3]     [,4]     [,5]       [,6]     [,7]
## [1,] 12751.21 14524.94 14860.25 5484.667 3863.122   29.48651 1910.615
## [2,] 14371.27 12697.15 12300.32 7529.195 5308.062 1119.09009 6372.634
##          [,8]
## [1,] 11687.64
## [2,] 11276.68
```

* Second, we determine the nearest polygon **IDs** - 


```r
dist_order = order(dist_towns[1, ])
```


```r
dist_order
## [1] 6 7 5 4 8 1 2 3
```


```r
dist_order[1:2]
## [1] 6 7
```

* Third, we use the IDs to **subset** the polygons - 


```r
forests = pol[dist_order[1:2], ]
forests
## Simple feature collection with 2 features and 2 fields
## geometry type:  POLYGON
## dimension:      XY
## bbox:           xmin: 673875 ymin: 3467775 xmax: 681765 ymax: 3474345
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
##     clumps                       geometry          area
## 356    281 POLYGON ((674865 3474345, 6... 9492300 [m^2]
## 391    314 POLYGON ((679815 3472005, 6... 6784200 [m^2]
```

* For convenience, we can add forest **names** - 


```r
forests$name = c("Lahav", "Kramim")
forests
## Simple feature collection with 2 features and 3 fields
## geometry type:  POLYGON
## dimension:      XY
## bbox:           xmin: 673875 ymin: 3467775 xmax: 681765 ymax: 3474345
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
##     clumps                       geometry          area   name
## 356    281 POLYGON ((674865 3474345, 6... 9492300 [m^2]  Lahav
## 391    314 POLYGON ((679815 3472005, 6... 6784200 [m^2] Kramim
```

Plot - 


```r
plot(l, rgb = c(3, 2, 1), reset = FALSE)
plot(
  st_geometry(forests),
  border = "yellow",
  add = TRUE
)
text(
  st_coordinates(st_centroid(forests)),
  forests$name,
  col = "white",
  font = 2
)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-58-1.png" alt="Lahav and Kramim forests" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-58)Lahav and Kramim forests</p>
</div>

## Shifting vector layer

* For more convenient **label placement** we can shift forest centroids 3 km to the north - 


```r
forests_ctr = st_centroid(forests, byid = TRUE)
st_coordinates(forests_ctr)
##          X       Y
## 1 675923.3 3472282
## 2 679936.8 3469963
```


```r
forests_ctr = st_geometry(forests_ctr) + c(0, 3000)
st_coordinates(forests_ctr)
##          X       Y
## 1 675923.3 3475282
## 2 679936.8 3472963
```



```r
plot(l, rgb = c(3, 2, 1), reset = FALSE)
plot(
  st_geometry(forests),
  border = "yellow",
  add = TRUE
)
text(
  st_coordinates(forests_ctr),
  forests$name,
  col = "white",
  font = 2
)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-61-1.png" alt="Shifted labels" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-61)Shifted labels</p>
</div>

## Extracting raster values based on polygon layer

* When **extracting** raster values based on a polygon (or line) layer, each feature may intersect an **unequal** number of pixels
* The `extract` function offers two ways of dealing with this variation - 
    * **Summarizing** the values to a single value per feature, using a function (`fun`), so that the returned object is a vector (single layer raster) or a matrix (multi-layer raster)
    * **Keeping** all values in a `list`, using `fun=NULL`
* The `na.rm` parameter determines whether `NA` values are **passed** to the function

* For example, the following expression calculates the **average** `r` value for each **feature** in `forests`, that is the average NDVI time series per forest - 


```r
r_forests = raster_extract(
  r, 
  forests, 
  fun = mean, 
  na.rm = TRUE
)
```

* The result is a `matrix` with 2 **rows** (features) and 280 **columns** (raster layers)


```r
dim(r_forests)
## [1]   2 280
```


```r
r_forests[, 1:3]
##        layer.1   layer.2   layer.3
## [1,] 0.3725111 0.3959158 0.4102210
## [2,] 0.3416607 0.3850857 0.3956179
```

* We will **transform** the `matrix` to a more convenient `data.frame`, using `t` and `as.data.frame` - 


```r
r_forests = as.data.frame(t(r_forests))
```


```r
head(r_forests)
##                V1        V2
## layer.1 0.3725111 0.3416607
## layer.2 0.3959158 0.3850857
## layer.3 0.4102210 0.3956179
## layer.4 0.3746000 0.3523357
## layer.5 0.3170184 0.3028429
## layer.6 0.2676316 0.2579357
```

* Also, we will assign forest **names** to the columns -


```r
colnames(r_forests) = forests$name
```


```r
head(r_forests)
##             Lahav    Kramim
## layer.1 0.3725111 0.3416607
## layer.2 0.3959158 0.3850857
## layer.3 0.4102210 0.3956179
## layer.4 0.3746000 0.3523357
## layer.5 0.3170184 0.3028429
## layer.6 0.2676316 0.2579357
```

* And add a **date** column -


```r
r_forests$date = dates$date
```


```r
head(r_forests)
##             Lahav    Kramim       date
## layer.1 0.3725111 0.3416607 2000-02-18
## layer.2 0.3959158 0.3850857 2000-03-05
## layer.3 0.4102210 0.3956179 2000-03-21
## layer.4 0.3746000 0.3523357 2000-04-06
## layer.5 0.3170184 0.3028429 2000-04-22
## layer.6 0.2676316 0.2579357 2000-05-08
```

* Now we can plot the **NDVI time series** of both forests - 


```r
plot(
  dates$date,
  r_forests$Lahav,
  type = "l",
  col = "blue",
  xlab = "Time",
  ylab = "NDVI"
)
lines(
  dates$date,
  r_forests$Kramim,
  type = "l",
  col = "red"
)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-71-1.png" alt="Average NDVI time series for Lahav and Kramim forests" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-71)Average NDVI time series for Lahav and Kramim forests</p>
</div>

## Distance to nearest point

* Another example of a spatial operator involving a raster and a vector layer is the calculation of a raster of **distances to nearest** point
* The raster can be **calculated** using the `distanceFromPoints` function, given a raster and a point layer - 


```r
grid = st_as_sf(modis_avg, as_points = TRUE)
distance = st_distance(grid, rainfall)
distance = apply(distance, 1, min)
grid$distance = distance
distance = st_rasterize(grid[, "distance"], modis_avg)
```

* Plot - 


```r
plot(distance, reset = FALSE)
plot(st_geometry(rainfall), col = "red", add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="11-lesson_11_files/figure-html/unnamed-chunk-73-1.png" alt="Distance to nearest meteorological station" width="43%" />
<p class="caption">(\#fig:unnamed-chunk-73)Distance to nearest meteorological station</p>
</div>











<!--chapter:end:11-lesson_11.Rmd-->

# Spatial interpolation of point data {#spatial-interpolation-of-point-data}



## Contents

* Spatial interpolation of point data using - 
    * Inverse Distance Weighted (IDW) interpolation
    * Ordinary Kriging (OK)
    * Universal Kriging (UK)

## Aims

* Use geostatistical functions from the `gstat` package to spatially interpolate point data
* Practically learn to - 
    * Calculate an empirical variogram
    * Fit a variogram model
    * Interpolate using three methods: IDW, OK, UK
    * Evaluate interpolation accuracy using Leave-One-Out Cross Validation

## Preparation


```r
library(sf)
library(stars)
library(gstat)
library(automap)
```

## Spatial interpolation

* **Spatial interpolation** is the prediction of a given phenomenon in unmeasured locations
* For that, we need a spatial interpolation **model** - a set of procedures to calculate **predicted values** of the variable of interest, given **calibration data**
* Calibrarion data usually includes - 
    * **Field measurements** - available for a limited number of locations, for example: rainfall data from meteorological stations
    * **Covariates** - available for each and every location within the area of interest, for example: elevation from a DEM
* Spatial interpolation models can be divided into two categories - 
    * **Deterministic models** - Models using arbitrary parameter values, for example: IDW
    * **Statistical models** - Models using parameters chosen objectively based on the data, for example: Kriging

## Spatial interpolation

<div class="figure" style="text-align: center">
<img src="images/lesson_12_interpolation_elev_input.png" alt="Spatial interpolation (Input elevation point data, Interpolated elevation surface)" width="40%" />
<p class="caption">(\#fig:unnamed-chunk-31)Spatial interpolation (Input elevation point data, Interpolated elevation surface)</p>
</div><div class="figure" style="text-align: center">
<img src="images/lesson_12_interpolation_elev_output.png" alt="Spatial interpolation (Input elevation point data, Interpolated elevation surface)" width="40%" />
<p class="caption">(\#fig:unnamed-chunk-32)Spatial interpolation (Input elevation point data, Interpolated elevation surface)</p>
</div>

http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-analyst-toolbox/understanding-interpolation-analysis.htm

<div class="figure" style="text-align: center">
<img src="images/lesson_12_interpolation_ozone_input.png" alt="Spatial interpolation (Point locations of ozone monitoring stations, Interpolated prediction surface)" width="28%" />
<p class="caption">(\#fig:unnamed-chunk-41)Spatial interpolation (Point locations of ozone monitoring stations, Interpolated prediction surface)</p>
</div><div class="figure" style="text-align: center">
<img src="images/lesson_12_interpolation_ozone_output.png" alt="Spatial interpolation (Point locations of ozone monitoring stations, Interpolated prediction surface)" width="28%" />
<p class="caption">(\#fig:unnamed-chunk-42)Spatial interpolation (Point locations of ozone monitoring stations, Interpolated prediction surface)</p>
</div>

http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-analyst-toolbox/understanding-interpolation-analysis.htm

* Keep in mind that data **structure** does not imply **meaning**
* For example, it does not make sense to spatially interpolate point data when they refer to a **localized phenomenon**

<div class="figure" style="text-align: center">
<img src="images/lesson_12_point_vs_continuous_phenomena1.png" alt="Localized phenomenon" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-5)Localized phenomenon</p>
</div>

https://edzer.github.io/UseR2016/

* Keep in mind that data **structure** does not imply **meaning**
* Similarly, it does not make sense to sum up point measurements of a **continuous phenomenon**

<div class="figure" style="text-align: center">
<img src="images/lesson_12_point_vs_continuous_phenomena2.png" alt="Continuous phenomenon" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-6)Continuous phenomenon</p>
</div>

https://edzer.github.io/UseR2016/

* The predicted value for a particular point is calculated as a **weighted average** of measured values in other points

$$\hat{Z}(s_{0})=\frac{\sum_{i=1}^{n}w(s_{i})Z(s_{i})}{\sum_{i=1}^{n}w(s_{i})}$$

* Where - 
    * $\hat{Z}(s_{0})$ is the predicted value at location $s_{0}$
    * $w(s_{i})$ is the weight of measured point $i$
    * $Z(s_{i})$ is the value of measured point $i$
* The weights $w(s_{i})$ of each measured point are a function its distance from the predicted point

<div class="figure" style="text-align: center">
<img src="images/lesson_12_interpolation_distances.png" alt="Distances between predicted point and all measured points" width="60%" />
<p class="caption">(\#fig:unnamed-chunk-7)Distances between predicted point and all measured points</p>
</div>

http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-analyst-toolbox/how-kriging-works.htm

* In IDW, the weight is the inverse of distance to the power of $p$ -

$$w(s_{i})=\frac{1}{d(s_{0}, s_{i})^p}$$

* Where - 
    * $w(s_{i})$ is the weight of measured point $i$
    * $d(s_{0}, s_{i})$ is the distance between predicted point $s_{0}$ and measured point $s_{i}$
* The default is $p=2$ - 

$$w(s_{i})=\frac{1}{d(s_{0}, s_{i})^2}$$



<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-9-1.png" alt="Spatial interpolation of annual rainfall using IDW with different values of $p$" width="50%" />
<p class="caption">(\#fig:unnamed-chunk-91)Spatial interpolation of annual rainfall using IDW with different values of $p$</p>
</div><div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-9-2.png" alt="Spatial interpolation of annual rainfall using IDW with different values of $p$" width="50%" />
<p class="caption">(\#fig:unnamed-chunk-92)Spatial interpolation of annual rainfall using IDW with different values of $p$</p>
</div><div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-9-3.png" alt="Spatial interpolation of annual rainfall using IDW with different values of $p$" width="50%" />
<p class="caption">(\#fig:unnamed-chunk-93)Spatial interpolation of annual rainfall using IDW with different values of $p$</p>
</div>



<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-11-1.png" alt="Nearest Neighbor interpolation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-11)Nearest Neighbor interpolation</p>
</div>



<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-13-1.png" alt="Voronoi polygons" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-13)Voronoi polygons</p>
</div>

* In Kriging, the weight is a particular function of distance known as the **variogram model**
* The variogram model is fitted to characterize the autocorrelation structure in the measured data, based on the **empirical variogram**

<div class="figure" style="text-align: center">
<img src="images/lesson_12_variogram_model1.png" alt="Variogram models (Spherical model, Exponential model)" width="45%" />
<p class="caption">(\#fig:unnamed-chunk-141)Variogram models (Spherical model, Exponential model)</p>
</div><div class="figure" style="text-align: center">
<img src="images/lesson_12_variogram_model1.png" alt="Variogram models (Spherical model, Exponential model)" width="45%" />
<p class="caption">(\#fig:unnamed-chunk-142)Variogram models (Spherical model, Exponential model)</p>
</div>

http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-analyst-toolbox/how-kriging-works.htm



<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-16-1.png" alt="Spatial interpolation of annual rainfall using IDW, OK and UK" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-161)Spatial interpolation of annual rainfall using IDW, OK and UK</p>
</div><div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-16-2.png" alt="Spatial interpolation of annual rainfall using IDW, OK and UK" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-162)Spatial interpolation of annual rainfall using IDW, OK and UK</p>
</div><div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-16-3.png" alt="Spatial interpolation of annual rainfall using IDW, OK and UK" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-163)Spatial interpolation of annual rainfall using IDW, OK and UK</p>
</div>

* For the examples, we will load the `rainfall_pnt` layer - 


```r
rainfall = st_read(
  "data/rainfall_pnt.shp", 
  stringsAsFactors = FALSE
)
## Reading layer `rainfall_pnt' from data source `/home/michael/Dropbox/Courses/R_2019/data/rainfall_pnt.shp' using driver `ESRI Shapefile'
## Simple feature collection with 169 features and 12 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 629301.4 ymin: 3270290 xmax: 761589.2 ymax: 3681163
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
```

* And the `elevation.tif` raster - 


```r
elevation = read_stars("data/elevation.tif")
```

* We also **re-calculate** the `annual` rainfall column - 


```r
m = c(
  "sep", "oct", "nov", "dec", "jan",
  "feb", "mar", "apr", "may"
)
rainfall$annual = apply(
  st_set_geometry(rainfall[, m], NULL),
  1,
  sum
)
```

* Plot - 


```r
plot(elevation, reset = FALSE)
plot(st_geometry(rainfall), add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-21-1.png" alt="Rainfall data points and elevation raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-21)Rainfall data points and elevation raster</p>
</div>

* We will **subset** the `rainfall` layer to include only the points overlapping with the `elevation` layer
* First, **extracting** the elevation values - 


```r
x = aggregate(elevation, rainfall, function(x) x[1], as_points = FALSE)
rainfall$elev_1km = x[[1]]
```

* Then **subsetting** where extracted value is not `NA` -


```r
rainfall = rainfall[!is.na(rainfall$elev_1km), ]
```

* Plot - 


```r
plot(elevation, reset = FALSE)
plot(st_geometry(rainfall), add = TRUE)
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-25-1.png" alt="Rainfall data points and elevation raster" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-25)Rainfall data points and elevation raster</p>
</div>

## The `gstat` object

* To interpolate, we first need to create an **object** of class `gstat`, using a **function** of the same name `gstat`
* A `gstat` object contains **all necessary information** to conduct spatial interpolation, namely -
    * The **model** definition
    * The **calibration data**
* Based on its arguments, the `gstat` function **"understands"** what type of interpolation model we want to use - 
    * No variogram model → **IDW**
    * Variogram model, no covariates → **Ordinary Kriging**
    * Variogram model, with covariates → **Universal Kriging**

<div class="figure" style="text-align: center">
<img src="images/lesson_12_gstat_predict_method.pdf" alt="\texttt{gstat} predict methods" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-26)\texttt{gstat} predict methods</p>
</div>

Applied Spatial Data Analysis with R (2013)

* We are going to use three **parameters** of the `gstat` function - 
    * `formula` - The prediction **"formula"**; used to specify the names of the dependent variable and the covariates
    * `data` - The calibration **data**
    * `model` - The **variogram model**
* To interpolate using the **IDW** method we create the following `gstat` object - 


```r
g = gstat(
  formula = annual ~ 1,
  data = as(rainfall, "Spatial")
)
```

* Note: we need to specify the parameter names!

## Working with `formula` objects

* `formula` objects are used to specify **relation** between objects in R, in particular - the role of different data **columns** in **statistical models**
* A `formula` object is **created** using the `~` operator, which separates names of **dependent variables** (to the left) and **independent variables** (to the right)
* The `~ 1` part means there are **no independent variables**


```r
f = annual ~ 1
f
## annual ~ 1
class(f)
## [1] "formula"
```

* We can also **convert** `character` values to `formula` using the `as.formula` function - 


```r
f = "annual ~ 1"
f
## [1] "annual ~ 1"
class(f)
## [1] "character"
```


```r
f = as.formula(f)
f
## annual ~ 1
class(f)
## [1] "formula"
```

## Making predictions

* Now that our model is defined, we can use the `interpolate` function to **make predictions**
* The `interpolate` function accepts - 
    * A **raster**, such as `elevation`
    * A **model**, such as a `gstat` model named `g`
* The raster serves for two **purposes** - 
    * Specifying the **locations** where we want to make predictions (in all methods)
    * Specifying **covariate** values (in Universal Kriging only)


```r
z = predict(g, elevation)
## [inverse distance weighted interpolation]
```

* Plot:


```r
plot(z, reset = FALSE)
plot(st_geometry(rainfall), add = TRUE)
plot(st_contour(z), add = TRUE)
## Warning in gdal_polygonize(x, mask, use_integer = FALSE, geotransform =
## get_geotransform(x), : range of breaks does not cover range of cell values
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-32-1.png" alt="Predicted values using IDW" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-32)Predicted values using IDW</p>
</div>

* Using a different color scale - 


```r
plot(z, col = rainbow(20), reset = FALSE)
plot(st_geometry(rainfall), add = TRUE)
plot(st_contour(z), add = TRUE)
## Warning in gdal_polygonize(x, mask, use_integer = FALSE, geotransform =
## get_geotransform(x), : range of breaks does not cover range of cell values
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-33-1.png" alt="Predicted values using IDW, using different color scale" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-33)Predicted values using IDW, using different color scale</p>
</div>

## Ordinary Kriging

* Kriging methods require a **variogram model**
* As a first step, we can calculate the **empirical variogram** using `variogram` which accepts - 
    * `formula` - Specifies the **dependent variable** and the **covariates**, just like in `gstat`
    * `data` - The **point layer**


```r
v_emp_ok = variogram(
  annual ~ 1, 
  as(rainfall, "Spatial")
)
```

* Using `plot` to examine it - 


```r
plot(v_emp_ok)
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-35-1.png" alt="Empyrical variogram" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-35)Empyrical variogram</p>
</div>

* There are several ways to fit a **variogram model** to an empirical variogram
* We will use the simplest one - **automatic fitting** using function `autofitVariogram` from package `automap` - 


```r
v_mod_ok = autofitVariogram(
  annual ~ 1, 
  as(rainfall, "Spatial")
)
```

* Note: use `show.vgms()` to display variogram function types

* Plot:


```r
plot(v_mod_ok)
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-37-1.png" alt="Variogram model" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-37)Variogram model</p>
</div>

* The `$var_model` component of the resulting object specifies the **fitted model** - 


```r
v_mod_ok$var_model
##   model      psill    range kappa
## 1   Nug   782.1762     0.00     0
## 2   Ste 19127.5501 27948.46    10
```

* The variogram model is then **passed** to the `gstat` function, and then Ordinary Kriging interpolation can be done - 


```r
g = gstat(
  formula = annual ~ 1,
  model = v_mod_ok$var_model,
  data = as(rainfall, "Spatial")
)
z = predict(g, elevation)
## [using ordinary kriging]
```

* **Universal Kriging** interpolation uses a model with one or more **covariates** / **independent variables**
* The covariates need to be known for both - 
    * The **point layer**, as a column such as `elev_1km` in `rainfall`
    * The **predicted locations**, as raster values such as in `elevation`
* The `formula` now **specifies** the name(s) of the covariate(s) to the right of the `~` symbol - 


```r
v_emp_uk = variogram(
  annual ~ elev_1km, 
  as(rainfall, "Spatial")
)
v_mod_uk = autofitVariogram(
  annual ~ elev_1km, 
  as(rainfall, "Spatial")
)
```

## Universal Kriging

* Comparing the Ordinary Kriging and Universal Kriging variogram models - 


```r
plot(
  v_emp_ok, 
  model = v_mod_ok$var_model, 
  ylim = c(0, 25000), 
  main = "OK"
)
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-41-1.png" alt="OK and UK variogram models" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-411)OK and UK variogram models</p>
</div>

```r
plot(
  v_emp_uk, 
  model = v_mod_uk$var_model, 
  ylim = c(0, 25000), 
  main = "UK"
)
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-41-2.png" alt="OK and UK variogram models" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-412)OK and UK variogram models</p>
</div>

* Next we create a `gstat` **object** where the `formula` contains the **covariate** and the respective **variogram model** - 


```r
g = gstat(
  formula = annual ~ elev_1km,
  model = v_mod_uk$var_model,
  data = as(rainfall, "Spatial")
)
```

* Note: the `elev_1km` column needs to be present in the `data`

* The `interpolate` function needs another argument `xyOnly=FALSE`, to specify that the raster is **not only** used for prediction locations (X, Y) but also for **covariate data**


```r
z = predict(g, elevation)
## Error in eval(predvars, data, env): object 'elev_1km' not found
```

* We get an error!
* The reason is that `interpolate` looks for a layer of the **same name** as specified in the `formula` of the `gstat` object

* We can change the layer names to make sure they match - 


```r
names(elevation)
## [1] "elevation.tif"
```


```r
names(elevation) = "elev_1km"
names(elevation)
## [1] "elev_1km"
```

* Now `interpolate` works - 


```r
z = predict(g, elevation)
## [using universal kriging]
```

* Plot:


```r
plot(z, reset = FALSE)
plot(st_geometry(rainfall), add = TRUE)
plot(st_contour(z), add = TRUE)
## Warning in gdal_polygonize(x, mask, use_integer = FALSE, geotransform =
## get_geotransform(x), : range of breaks does not cover range of cell values
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-47-1.png" alt="Universal Kriging predictions" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-47)Universal Kriging predictions</p>
</div>

## Ordinary Kriging

* Another example: suppose that we did not have a DEM for Israel, but only the **elevation measurements** at the meteorological stations 
* How can we produce an elevation raster using **Ordinary Kriging**?
* First, we read the data - 


```r
rainfall = st_read(
  "data/rainfall_pnt.shp", 
  stringsAsFactors = FALSE
)
## Reading layer `rainfall_pnt' from data source `/home/michael/Dropbox/Courses/R_2019/data/rainfall_pnt.shp' using driver `ESRI Shapefile'
## Simple feature collection with 169 features and 12 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 629301.4 ymin: 3270290 xmax: 761589.2 ymax: 3681163
## epsg (SRID):    32636
## proj4string:    +proj=utm +zone=36 +ellps=WGS84 +units=m +no_defs
modis_avg = read_stars("data/modis_average.tif")
```

* Second, we prepare the `gstat` object - 


```r
v = autofitVariogram(
  altitude ~ 1, 
  as(rainfall, "Spatial")
)
g = gstat(
  formula = altitude ~ 1,
  model = v$var_model,
  data = as(rainfall, "Spatial")
)
```

* Finally, we interpolate - 


```r
z = predict(g, modis_avg)
## [using ordinary kriging]
```

* Plot - 


```r
plot(z, reset = FALSE)
plot(st_geometry(rainfall), add = TRUE)
plot(st_contour(z), add = TRUE)
## Warning in gdal_polygonize(x, mask, use_integer = FALSE, geotransform =
## get_geotransform(x), : range of breaks does not cover range of cell values
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-51-1.png" alt="Ordinary Kriging prediction of elevation" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-51)Ordinary Kriging prediction of elevation</p>
</div>

* In the next example we use kriging inside a `for` **loop**, to make a series of predictions for **different variables**
* We will use **Ordinary Kriging** to predict **monthly rainfall**, i.e. `sep` through `may` columns in the `rainfall` layer
* In each `for` loop "round", the formula is **re-defined** according to the **current** month `i` - 


```r
i = "may"
as.formula(paste0(i, " ~ 1"))
## may ~ 1
```

* **Setting up** -


```r
m = c(
  "sep", "oct", "nov", "dec", "jan",
  "feb", "mar", "apr", "may"
)
result = list()
```

* The `for` **loop** - 


```r
for(i in m) {
  f = as.formula(paste0(i, " ~ 1"))
  v = autofitVariogram(f, as(rainfall, "Spatial"))
  g = gstat(
    formula = f,
    model = v$var_model,
    data = as(rainfall, "Spatial")
  )
  z = predict(g, elevation)
  z = z["var1.pred"]
  result[[i]] = z
}
## [using ordinary kriging]
## [using ordinary kriging]
## [using ordinary kriging]
## [using ordinary kriging]
## [using ordinary kriging]
## [using ordinary kriging]
## [using ordinary kriging]
## [using ordinary kriging]
## [using ordinary kriging]
result = do.call(c, result)
names(result) = m
result = st_redimension(result)
```

## Ordinary Kriging

* Plot: 


```r
plot(result)
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-55-1.png" alt="Montly rainfall predictions using Ordinary Kriging" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-55)Montly rainfall predictions using Ordinary Kriging</p>
</div>

## Cross-validation

* In **Leave-One-Out Cross Validation** we -
    * **Take out** one point out of the calibration data
    * Make a **prediction** for that point
    * **Repeat** for all points
* In the end we get a table with an **observed value** and a **predicted value** for all points
* We can run Leave-One-Out Cross Validation using the `gstat.cv` **function**, which accepts a `gstat` object - 




```r
cv = gstat.cv(g)
```

* The result can be **converted** back to an `sf` object - 


```r
cv = st_as_sf(cv)
```


```r
cv
## Simple feature collection with 169 features and 6 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 629301.4 ymin: 3270290 xmax: 761589.2 ymax: 3681163
## epsg (SRID):    NA
## proj4string:    NA
## First 10 features:
##    var1.pred  var1.var observed    residual      zscore fold
## 1   5.617118 0.7121553      6.7  1.08288234  1.28319870    1
## 2   5.725242 0.5317479      4.5 -1.22524176 -1.68023056    2
## 3   4.967079 0.7313000      3.8 -1.16707897 -1.36474801    3
## 4   4.043898 0.8877221      4.8  0.75610168  0.80249379    4
## 5   5.190195 0.8125869      4.7 -0.49019520 -0.54379367    5
## 6   4.474226 1.0677832      2.7 -1.77422621 -1.71698877    6
## 7   4.022178 0.6807608      4.9  0.87782204  1.06392058    7
## 8   4.887956 0.6790070      4.9  0.01204434  0.01461659    8
## 9   4.490841 0.6547277      4.3 -0.19084095 -0.23585289    9
## 10  3.820534 0.7729485      4.5  0.67946579  0.77284484   10
##                    geometry
## 1  POINT (696533.1 3660837)
## 2  POINT (697119.1 3656748)
## 3  POINT (696509.3 3652434)
## 4  POINT (696541.7 3641332)
## 5  POINT (697875.3 3630156)
## 6  POINT (687006.2 3633330)
## 7  POINT (689553.7 3626282)
## 8  POINT (694694.5 3624388)
## 9  POINT (686489.5 3619716)
## 10 POINT (683148.4 3616846)
```

* The result of `gstat.cv` has the following **attributes** - 
    * `var1.pred` - Predicted value
    * `var1.var` - Variance (only for Kriging)
    * `observed` - Observed value
    * `residual` - Observed-Predicted
    * `zscore` - Z-score (only for Kriging)
    * `fold` - Cross-validation ID
* A **bubble plot** is convenient to examine the residuals, since it shows positive and negative values in different color - 


```r
bubble(as(cv, "Spatial"), "residual")
```

<div class="figure" style="text-align: center">
<img src="12-lesson_12_files/figure-html/unnamed-chunk-61-1.png" alt="Cross-validation residuals" width="100%" />
<p class="caption">(\#fig:unnamed-chunk-61)Cross-validation residuals</p>
</div>

* Using the "predicted" and "observed" columns we can calculate prediction accuracy indices, such as the **Root Mean Square Error (RMSE)** - 

$$
RMSE=\sqrt{\frac{\sum_{i=1}^{n} (pred_i-obs_i)^2}{n}}
$$

* Where $pred_i$ and $obs_i$ are **predicted** and **observed** values for point $i$, respectively


```r
sqrt(sum((cv$var1.pred - cv$observed)^2) / nrow(cv))
## [1] 0.8923544
```

## Exercise 6 - Submission date **2019-02-24**














<!--chapter:end:12-lesson_12.Rmd-->

# Files


<!--chapter:end:15-files.Rmd-->


# BGU course 2019

## Course aims

* General knowledge in programming
* Overview of spatial data processing and analysis in R

## Course topics

**Part I - Introduction to R programming**

1. The R environment
2. Vectors
3. Time series + function definition
4. Tables + conditionals and loops

**Part II - Processing and analysis of spatial data in R**

5. Matrices and rasters
6. Raster algebra
7. Vector layers
8. Geometric operations with vector layers
9. Geometric operations with rasters
10. Working with spatio-temporal data
11. Combining rasters and vector layers
12. Spatial interpolation of point data

## Course details

* **Course number**: 128.1.0043
* **Time**: Sunday 16:10-19:00
* **Place**: Building 72, room 249
* **Instructor**: Michael Dorman (dorman@post.bgu.ac.il)
* **Grading**: 6 exercises (50%) + Exam (50%)
* **Requirements** - 
    * Basic knowledge of GIS (e.g. "Intro to GIS" course)
    * Self study
* **Getting help** - 
    * Forum on **Moodle** (http://moodle2.bgu.ac.il)
    * Meetings (Monday 15:00-16:00, schedule by e-mail)

## Lecture plan

| Lesson | Date | Slides | Exercise |
|:--:|:---:|-----------|:-----------:|
| 01 | 2018-10-28 | [**The R environment**](the-r-environment.html) | |
| 02 | 2018-11-11 | [**Vectors**](exercises/vectors.html) | [**Exercise 1**](exercises/exercise_01.pdf) ([**Solution**](exercises/exercise_01_solution.pdf)) | 
| 03 | 2018-11-18 | [**Time series and function definitions**](time-series-and-function-definitions.html) | | 
| 04 | 2018-11-22 | [**Tables, conditionals and loops**](tables-conditionals-and-loops.html) | [**Exercise 2**](exercises/exercise_02.pdf) ([**Solution**](exercises/exercise_02_solution.pdf)) | 
| 05 | 2018-11-25 | [**Matrices and rasters**](matrices-and-rasters.html) | | 
| 06 | 2018-12-02 | [**Raster algebra**](raster-algebra.html) | [**Exercise 3**](exercises/exercise_03.pdf) ([**Solution**](exercises/exercise_03_solution.pdf)) | 
| 07 | 2018-12-13 | [**Vector layers**](vector-layers.html) | | 
| 08 | 2018-12-16 | [**Geometric operations with vector layers**](geometric-operations-with-vector-layers.html) | [**Exercise 4**](exercises/exercise_04.pdf) ([**Solution**](exercises/exercise_04_solution.pdf)) | 
| 09 | 2018-12-23 | [**Geometric operations with rasters**](geometric-operations-with-rasters.html) | | 
| 10 | 2018-12-27 | [**Working with spatio-temporal data**](processing-spatio-temporal-data.html) | [**Exercise 5**](exercises/exercise_05.pdf) ([**Solution**](exercises/exercise_05_solution.pdf)) | 
| 11 | 2018-12-30 | [**Combining rasters and vector layers**](combining-rasters-and-vector-layers.html) | | 
| 12 | 2019-01-06 | [**Spatial interpolation of point data**](spatial-interpolation-of-point-data.html) | [**Exercise 6**](exercises/exercise_06.pdf) ([**Solution**](exercises/exercise_06_solution.pdf)) | 
| 13 |            | [**Exam question examples**](lesson_14_exam.pdf) | | 

## Other documents

* [**Exercise instructions**](exercises/exercise_instructions.pdf) 
* [**Sample exam questions**](sample_exam_questions.pdf)

## Data for examples

* [**Course data (ZIP file)**](https://www.dropbox.com/sh/odsq9nz4a4fe41v/AACHrKiQCqBHjnL9GP-bxN6da?dl=1)

## Other resources

### Tutorials

* Adrian Baddeley, 2008. **Analysing spatial point patterns in R**. [[**PDF**](resources/PointPatterTutorial.pdf)]

### Papers

* Pebesma, E., Bivand, R. S. (2005). **Classes and Methods for Spatial Data: the sp Package**. R news, 5(2), 9-13. [[**PDF**](resources/Rnews_2005-2.pdf)]
* Pebesma, E. (2018). **Simple Features for R: Standardized Support for Spatial Vector Data**. The R Journal, 10(1):439-446. [[**PDF**](resources/RJ-2018-009.pdf)]

### Books - General

* Murrell, P. (2010). **Introduction to Data Technologies**. Chapman and Hall/CRC. [[**PDF**](resources/Murrell 2010 Introduction to Data Technologies.pdf)] [[**Website**](https://www.stat.auckland.ac.nz/~paul/ItDT/)]
* Wickham, H. (2014). **Advanced R**. Chapman and Hall/CRC. [[**HTML**](http://adv-r.had.co.nz/)]

### Books - Spatial data

* Hengl, T. (2009). **A Practical Guide to Geostatistical Mapping**. [[**PDF**](resources/Hengl 2009 A Practical Guide to Geostatistical Mapping.pdf)]
* Lovelace, R., Nowosad, J., Muenchow, J. (2019). **Geocomputation with R**. Chapman and Hall/CRC. [[**HTML**](https://geocompr.robinlovelace.net/)]
* Pebesma, E., Bivand, R. (in preparation). **Spatial Data Science**. [[**HTML**](https://keen-swartz-3146c4.netlify.com/)]


<!--chapter:end:21-bgu-course.Rmd-->


# References {-}


<!--chapter:end:99-references.Rmd-->


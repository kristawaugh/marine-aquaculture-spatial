Spatial Assignment Answers
================
Zexuan Zhao and Krista Waugh

Habitat Suitability for Pacific spiny Lumpsucker
================================================

[![Build Status](https://travis-ci.com/espm-157/2018-spatial-spatial_zexuan_krista.svg?token=TJpEEbz7PiUQtcZQe2Sj&branch=master)](https://travis-ci.com/espm-157/2018-spatial-spatial_zexuan_krista)

In this report, we will analysize sea surface temperature, net primary productivity, and marine protected areas along the west coast of the United States to map potential areas of marine aquaculture for the Pacific spiny Lumpsucker (Eumicrotremus orbis). Our conclusion of the study is that the majority of Pacific spiny Lumpsuckers can be found off the coast of the California and Oregon border, with populations spanning the coast of California all the way down to Los Angeles, where there is another large population.

The following is our spatial data:

**1. Sea Surface Temperature** (raster data)
**2. Net Primary Productivity** (raster data)
**3. Marine Protected Areas** (vector data)

Optimum Pacific spiny Lumpsucker habitat
----------------------------------------

The temperature range and net primary productivity where the Pacific spiny lumpsucker shows optimum growth is: Sea surface temperatures between 12 and 18 degrees Celsius, and net Primary Productivity between 2.6 and 3 mgC/m2/day. We will begin to look through our data to extract these values to give us a better idea of where, within our dataset, the Pacific spiny lumpsuckers are located.

### Marine Protected areas

We'll start with a data file of Marine Protected Areas monitored by the US Federal government on the west coast: `mpas_westcoast.shp`.

``` r
westcoast <- st_read("shapefiles/mpas_westcoast.shp")
```

    ## Reading layer `mpas_westcoast' from data source `C:\Users\amos0\Documents\GitHub\2018-spatial-spatial_zexuan_krista\spatial\shapefiles\mpas_westcoast.shp' using driver `ESRI Shapefile'
    ## Simple feature collection with 348 features and 25 fields
    ## geometry type:  MULTIPOLYGON
    ## dimension:      XY
    ## bbox:           xmin: -2707616 ymin: -457193.8 xmax: -1950642 ymax: 1553906
    ## epsg (SRID):    NA
    ## proj4string:    +proj=aea +lat_1=29.5 +lat_2=45.5 +lat_0=37.5 +lon_0=-96 +x_0=0 +y_0=0 +datum=NAD83 +units=m +no_defs

``` r
str(westcoast)
```

    ## Classes 'sf' and 'data.frame':   348 obs. of  26 variables:
    ##  $ Site_ID   : Factor w/ 348 levels "BOEM18","CA1",..: 2 3 4 5 6 7 8 9 10 11 ...
    ##  $ Area_KM_To: num  253.722 4.245 0.362 46.22 0.358 ...
    ##  $ Date_GIS_U: Date, format: NA NA ...
    ##  $ Shape_Leng: num  1.1943 0.1771 0.0244 0.5114 0.0258 ...
    ##  $ Shape_Area: num  2.73e-02 4.35e-04 3.71e-05 4.72e-03 3.44e-05 ...
    ##  $ Site_Name : Factor w/ 348 levels "Abalone Cove State Marine Conservation Area",..: 245 223 85 108 283 89 107 246 143 135 ...
    ##  $ Site_Label: Factor w/ 348 levels "Abalone Cove SMCA",..: 244 223 85 108 281 89 107 247 144 136 ...
    ##  $ Gov_Level : Factor w/ 4 levels "Federal","Local",..: 4 4 4 4 4 4 4 4 4 4 ...
    ##  $ State     : Factor w/ 10 levels "Bureau of Ocean Energy Management",..: 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ NS_Full   : Factor w/ 3 levels "Eligible","Member",..: 2 2 2 3 1 2 2 2 2 2 ...
    ##  $ Prot_Lvl  : Factor w/ 5 levels "No Access","No Take",..: 3 3 3 3 3 3 3 2 2 2 ...
    ##  $ Mgmt_Plan : Factor w/ 5 levels "MPA Programmatic Management Plan",..: 1 1 1 2 5 1 1 1 1 1 ...
    ##  $ Mgmt_Agen : Factor w/ 23 levels "Bureau Of Land Management",..: 6 6 6 3 15 6 6 3 3 3 ...
    ##  $ Fish_Rstr : Factor w/ 10 levels "Commercial and Recreational Fishing Prohibited",..: 7 7 7 7 7 7 7 1 1 1 ...
    ##  $ Pri_Con_Fo: Factor w/ 3 levels "Cultural Heritage",..: 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ Cons_Focus: Factor w/ 5 levels "Natural Heritage",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Prot_Focus: Factor w/ 2 levels "Ecosystem","Focal Resource": 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Permanence: Factor w/ 1 level "Permanent": 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Constancy : Factor w/ 2 levels "Seasonal","Year-round": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ Estab_Yr  : Factor w/ 50 levels "0","1909","1913",..: 18 18 18 15 10 18 18 43 43 43 ...
    ##  $ URL       : Factor w/ 54 levels "http://channelislands.noaa.gov/",..: 52 52 52 20 NA 52 52 19 19 19 ...
    ##  $ Vessel    : Factor w/ 3 levels "Prohibited","Restricted",..: NA NA NA 2 NA NA NA 3 3 3 ...
    ##  $ Anchor    : Factor w/ 3 levels "Prohibited","Restricted",..: NA NA NA 3 NA NA NA 3 3 3 ...
    ##  $ Area_KM_Ma: num  249.424 4.238 0.344 46.063 0.348 ...
    ##  $ FID       : num  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ geometry  :sfc_MULTIPOLYGON of length 348; first list element: List of 1
    ##   ..$ :List of 1
    ##   .. ..$ : num [1:2246, 1:2] -2291279 -2291273 -2291256 -2291269 -2291278 ...
    ##   ..- attr(*, "class")= chr  "XY" "MULTIPOLYGON" "sfg"
    ##  - attr(*, "sf_column")= chr "geometry"
    ##  - attr(*, "agr")= Factor w/ 3 levels "constant","aggregate",..: NA NA NA NA NA NA NA NA NA NA ...
    ##   ..- attr(*, "names")= chr  "Site_ID" "Area_KM_To" "Date_GIS_U" "Shape_Leng" ...

### Visual plot of Marine protected areas

Visually, much of the coastline appears to be managed by the National Marine Fisheries Service, with some influence by National Marine Sanctuaries and Washington and the National Park Service in the north.

``` r
westcoast %>% 
  ggplot(aes(fill = State))+
    geom_sf()
```

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-2-1.png)

### Quantitatve analysis of area protected by each marine protection organization

The National Marine Fisheries Service controls by far the largest area of the coastline, 386.5 square kilometers, nearly ten times the area of the next largest organization controlling the Pacific coast of the United States, National Marine Sanctuaries.

``` r
area <- westcoast %>% 
  st_area() %>% 
  unclass() 
westcoast %>% 
  mutate(area = area) %>% 
  group_by(State) %>% 
  summarize(area = sum(area)) %>% 
  st_set_geometry(NULL) %>% 
  arrange(desc(area))
```

    ## # A tibble: 10 x 2
    ##    State                                               area
    ##    <fct>                                              <dbl>
    ##  1 National Marine Fisheries Service          386552971333.
    ##  2 National Marine Sanctuaries                 32546360192.
    ##  3 National Park Service                        5849214400.
    ##  4 California                                   4610480333.
    ##  5 Washington                                   2220097659.
    ##  6 National Wildlife Refuge System               618526056.
    ##  7 Bureau of Ocean Energy Management             223273358.
    ##  8 National Estuarine Research Reserve System    103350646.
    ##  9 Oregon                                         27691101.
    ## 10 Marine National Monuments                       7708487.

Sea Surface Temperature
-----------------------

We will use the `average_annual_sst_[year].tif` data, which are 5 annual average sea surface temperatures for our region, one for each year fom 2008 to 20012. To make them easier to work with, we will combine them using the stack() function. But first, we will look at the data for each year by plotting them individually, and graphing average sea surface temperature for each year.

``` r
files <- list.files("rasters", full.names = TRUE, pattern = "sst")
sst <- map(files, raster)
names(sst) <- c("sst_2008", "sst_2009","sst_2010", "sst_2011","sst_2012")
sst
```

    ## $sst_2008
    ## class       : RasterLayer 
    ## dimensions  : 480, 408, 195840  (nrow, ncol, ncell)
    ## resolution  : 0.04166185, 0.04165702  (x, y)
    ## extent      : -131.9848, -114.9867, 29.99305, 49.98842  (xmin, xmax, ymin, ymax)
    ## coord. ref. : +proj=longlat +ellps=WGS84 +no_defs 
    ## data source : C:\Users\amos0\Documents\GitHub\2018-spatial-spatial_zexuan_krista\spatial\rasters\average_annual_sst_2008.tif 
    ## names       : average_annual_sst_2008 
    ## values      : 278.7, 301.445  (min, max)
    ## 
    ## 
    ## $sst_2009
    ## class       : RasterLayer 
    ## dimensions  : 480, 408, 195840  (nrow, ncol, ncell)
    ## resolution  : 0.04166185, 0.04165702  (x, y)
    ## extent      : -131.9848, -114.9867, 29.99305, 49.98842  (xmin, xmax, ymin, ymax)
    ## coord. ref. : +proj=longlat +ellps=WGS84 +no_defs 
    ## data source : C:\Users\amos0\Documents\GitHub\2018-spatial-spatial_zexuan_krista\spatial\rasters\average_annual_sst_2009.tif 
    ## names       : average_annual_sst_2009 
    ## values      : 278.08, 301.5  (min, max)
    ## 
    ## 
    ## $sst_2010
    ## class       : RasterLayer 
    ## dimensions  : 480, 408, 195840  (nrow, ncol, ncell)
    ## resolution  : 0.04166185, 0.04165702  (x, y)
    ## extent      : -131.9848, -114.9867, 29.99305, 49.98842  (xmin, xmax, ymin, ymax)
    ## coord. ref. : +proj=longlat +ellps=WGS84 +no_defs 
    ## data source : C:\Users\amos0\Documents\GitHub\2018-spatial-spatial_zexuan_krista\spatial\rasters\average_annual_sst_2010.tif 
    ## names       : average_annual_sst_2010 
    ## values      : 279.92, 300.96  (min, max)
    ## 
    ## 
    ## $sst_2011
    ## class       : RasterLayer 
    ## dimensions  : 480, 408, 195840  (nrow, ncol, ncell)
    ## resolution  : 0.04166185, 0.04165702  (x, y)
    ## extent      : -131.9848, -114.9867, 29.99305, 49.98842  (xmin, xmax, ymin, ymax)
    ## coord. ref. : +proj=longlat +ellps=WGS84 +no_defs 
    ## data source : C:\Users\amos0\Documents\GitHub\2018-spatial-spatial_zexuan_krista\spatial\rasters\average_annual_sst_2011.tif 
    ## names       : average_annual_sst_2011 
    ## values      : 278.86, 307.2733  (min, max)
    ## 
    ## 
    ## $sst_2012
    ## class       : RasterLayer 
    ## dimensions  : 480, 408, 195840  (nrow, ncol, ncell)
    ## resolution  : 0.04166185, 0.04165702  (x, y)
    ## extent      : -131.9848, -114.9867, 29.99305, 49.98842  (xmin, xmax, ymin, ymax)
    ## coord. ref. : +proj=longlat +ellps=WGS84 +no_defs 
    ## data source : C:\Users\amos0\Documents\GitHub\2018-spatial-spatial_zexuan_krista\spatial\rasters\average_annual_sst_2012.tif 
    ## names       : average_annual_sst_2012 
    ## values      : 278.13, 310.2  (min, max)

### Visualizing sea surface temperature from 2008 to 2012

The temperatures are in Kelvin during these steps, but will be converted to Celsius for the final steps.

``` r
raster_visualize <- function(raster){
  raster %>% 
    tm_shape() +
    tm_raster() +
    tm_layout(legend.outside = TRUE)
}
sst %>% map(raster_visualize)
```

    ## $sst_2008

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-4-1.png)

    ## 
    ## $sst_2009

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-4-2.png)

    ## 
    ## $sst_2010

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-4-3.png)

    ## 
    ## $sst_2011

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-4-4.png)

    ## 
    ## $sst_2012

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-4-5.png)

#### Sea surface temperature average vs maxiumum

2009 had the highest average annual temperature, but the maximum recorded temperature for each year shows that 2011 and 2012 exhibit by far the highest recorded temperatures from our data, with the highest temperature recorded in 2012 being just over 310 degrees Kelvin (37 degrees Celsius), and the lowest maximum temperature in 2010 at about 301 Kelvin (28 degrees celsius).

``` r
data <- data_frame(year = 2008:2012)
for(i in 1:5){
data$value[i] <- sst[[i]] %>% 
    cellStats(mean) 
}
data %>% 
  ggplot(aes(x = year, y = value)) +
    geom_line() +
    ggtitle("Average Annual Sea Surface Temperature")
```

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-5-1.png)

``` r
data <- data_frame(year = 2008:2012)
for(i in 1:5){
data$value[i] <- sst[[i]] %>% 
    cellStats(max) 
}
data %>% 
  ggplot(aes(x = year, y = value)) +
    geom_line() + 
    ggtitle("Maximum Recorded Sea Surface Temperature")
```

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-6-1.png)

### Combining the raster layers

Here we stack our raster layers for each year 2008 to 2012 to get a single layer, which we will then use to get an average sea surface temperature in degrees Celsius.

``` r
sst_stack <- stack(sst)
```

### Raster calcuations

When we stack our rasters, we will write a small custom function to take the mean and convert to Celsius. We will then apply this function to our rasterstack to calculate a new raster we can use for analysis. The conversion between Kelvin and Celsius is: *C* = *K* − 273.15

``` r
convert <- function(x){
  x - 273.15
}
raster_mean <- function(raster){
  cellStats(raster, mean) %>% 
    convert()
}
```

``` r
sst_stack_celsius <- calc(sst_stack, fun = convert)
plot(sst_stack_celsius)
```

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-9-1.png)

Net Primary Productivity
------------------------

Since Lumpsuckers may be influenced by more than just sea surface temperature, we also include Net Primary Production (NPP) in our analysis.

#### NPP raster data

We used the raster() command to read in our data for net primary productivity along the west coast of the US.

``` r
npp <- raster("rasters/annual_npp.tif")
plot(npp)
```

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-10-1.png)

### Reprojecting net primary productivity and sea surface temperature

Here we reset the CRS of sea surface temperature to match the CRS of net primary productivity.

``` r
sst_stack_projected <- projectRaster(from = sst_stack_celsius, to = npp)
summary(values(sst_stack_projected))
```

    ##     sst_2008         sst_2009         sst_2010         sst_2011     
    ##  Min.   : 6.59    Min.   : 4.93    Min.   : 6.77    Min.   : 5.71   
    ##  1st Qu.:12.28    1st Qu.:12.74    1st Qu.:12.62    1st Qu.:12.45   
    ##  Median :14.22    Median :14.85    Median :14.46    Median :14.07   
    ##  Mean   :14.12    Mean   :14.68    Mean   :14.48    Mean   :14.09   
    ##  3rd Qu.:16.09    3rd Qu.:16.69    3rd Qu.:16.34    3rd Qu.:15.78   
    ##  Max.   :28.30    Max.   :28.35    Max.   :27.81    Max.   :34.12   
    ##  NA's   :225157   NA's   :225357   NA's   :225457   NA's   :225038  
    ##     sst_2012     
    ##  Min.   : 5.35   
    ##  1st Qu.:12.50   
    ##  Median :14.11   
    ##  Mean   :14.23   
    ##  3rd Qu.:15.99   
    ##  Max.   :36.26   
    ##  NA's   :224934

### Finally, we can finish our data preparation and begin our analysis

``` r
sst_npp <- stack(sst_stack_projected, npp)
```

Analysis
--------

Now that our data is prepped, we can move onto the analysis. For this specific analysis, we use the SST and NPP data to find areas along the US West Coast that are suitable for growing lumpsucker fish. This requires removal of all cells from NPP and SST that are not within the ideal growth parameter range.

### Sample Points & Extract values from Rasters

We generate 1000 sample points from the Pacific coast of the US in order to represent sea surface temperature and net primary productivity of our area of study.

``` r
set.seed(2018)
random_points <- st_sample(westcoast, 1000, type = "random") %>%
  st_sf() %>% 
  na.omit() %>% 
  st_join(westcoast)
plot(st_geometry(random_points))
```

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-13-1.png)

#### R Question: Why does your new dataframe of points likely have fewer than 1000 points?

See the `st_sample()` documentation and explain.

### Extract Raster Values and Identify Habitat

Here, we extracted values from the combined data of sea surface temperature and net primary productvity to identify Pacific spiny Lumpsuckers optimum habitat areas. Lumpsucker fish grow best in waters that are **between 12 and 18 degrees Celsius.** and with an NPP between **2.6 and 3 mgC/m2/day**.

``` r
sample_points <- raster::extract(sst_npp, random_points, sp = T) %>% 
  na.omit() %>% 
  st_as_sf() %>% 
  select(starts_with("sst"), ends_with("npp") ) %>% 
  mutate(point_ID = 1:nrow(.)) %>% 
  gather(year, sst, starts_with("sst")) %>% 
  separate(year, into = c("key", "year"), sep = "_") %>% 
  select(point_ID, year, annual_npp, sst) %>% 
  group_by(point_ID) %>% 
  summarize(habitat = (max(sst) < 18 & min(sst) > 12 & mean(annual_npp) > 2.6 & mean(annual_npp) < 3))
sample_points %>% 
  ggplot(aes(col = habitat)) +
  geom_sf()
```

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-14-1.png)

### Percentage of sampled points where Lumpsuckers would be found

``` r
sample_points %>% 
  summarize(percentage = sum(habitat, na.rm = TRUE) / n()) %>% 
  st_set_geometry(NULL) %>% 
  pull()
```

    ## [1] 0.4647059

#### Minimum latitude where lumpsucker fish are likely to be found

``` r
coordinates <- sample_points %>% 
  filter(habitat == TRUE) %>% 
  st_geometry() %>% 
  st_transform(4236) %>% 
  st_coordinates() %>% 
  as_data_frame() %>% 
  summarize(max_long = max(X),
            min_long = min(X),
            max_lat  = max(Y),
            min_lat  = min(Y))
coordinates$min_lat
```

    ## [1] 31.04812

#### Pacific spiny Lumpsucker habitat

``` r
sample_points %>% 
  filter(habitat == TRUE) %>% 
  st_geometry() %>% 
  st_transform(4236) %>%
  ggplot() +
    geom_sf() +
    geom_sf(data = st_geometry(world)) +
    coord_sf(xlim = c(coordinates$min_long,
                      coordinates$max_long),
             ylim = c(coordinates$min_lat,
                      coordinates$max_lat)) 
```

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-17-1.png)

The majority of Pacific spiny Lumpsuckers can be found off the coast of the California and Oregon border, with populations spanning the coast of California all the way down to Los Angeles, where there is another large population. See the leaflet below:

``` r
leaflet() %>% 
  setView(lng = -123.5, lat = 38.5, zoom = 5) %>%
  addTiles() %>% 
  addMarkers(-127, 43, label = "Habitat 1") %>% 
  addMarkers(-119, 33, label = "Habitat 2")
```

![](spatial-assignment_files/figure-markdown_github/unnamed-chunk-18-1.png)

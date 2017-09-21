


# Exploratory Data Analysis of Tropical Storms in R  

The disastrous impact of recent hurricanes, Harvey and Irma, generated a large influx of data within the online community. I was curious about the history of hurricanes and tropical storms so I found a data set on [data.world](https://data.world/dhs/historical-tropical-storm) and started some basic Exploratory data analysis (EDA).  


EDA is crucial to starting any project. Through EDA you can start to identify errors & inconsistencies in your data, find interesting patterns, see correlations and start to develop hypotheses to test. For most people, basic spreadsheets and charts are handy and provide a great place to start. They are an easy-to-use method to manipulate and visualize your data quickly. Data scientists may cringe at the idea of using a graphical user interface (GUI) to kick-off the EDA process but those tools are very effective and efficient when used properly. However, if you're reading this, you're probably trying to take EDA to the next level. The best way to learn is to get your hands dirty, let's get started.  


The original source of the data was can be found at [DHS.gov](https://hifld-dhs-gii.opendata.arcgis.com/datasets/3ea21accbfab4ed8b14ede2e802cc2ec_0).  


----


#### Step 1:  Take a look at your data set and see how it is laid out  



|  FID| YEAR| MONTH| DAY|AD_TIME | BTID|NAME     |  LAT|   LONG| WIND_KTS| PRESSURE|CAT |BASIN           | Shape_Leng|
|----:|----:|-----:|---:|:-------|----:|:--------|----:|------:|--------:|--------:|:---|:---------------|----------:|
| 2001| 1957|     8|   8|1800Z   |   63|NOTNAMED | 22.5| -140.0|       50|        0|TS  |Eastern Pacific |   1.140175|
| 2002| 1961|    10|   3|1200Z   |  116|PAULINE  | 22.1| -140.2|       45|        0|TS  |Eastern Pacific |   1.166190|
| 2003| 1962|     8|  29|0600Z   |  124|C        | 18.0| -140.0|       45|        0|TS  |Eastern Pacific |   2.102380|
| 2004| 1967|     7|  14|0600Z   |  168|DENISE   | 16.6| -139.5|       45|        0|TS  |Eastern Pacific |   2.121320|
| 2005| 1972|     8|  16|1200Z   |  251|DIANA    | 18.5| -139.8|       70|        0|H1  |Eastern Pacific |   1.702939|
| 2006| 1976|     7|  22|0000Z   |  312|DIANA    | 18.6| -139.8|       30|        0|TD  |Eastern Pacific |   1.600000|
  
  
Fortunately, this is a tidy data set which will make life easier and appears to be cleaned up substantially. The column names are relatively straightforward with the exception of "ID" columns.

The description as given by [DHS.gov](https://hifld-dhs-gii.opendata.arcgis.com/datasets/3ea21accbfab4ed8b14ede2e802cc2ec_0): 

>This dataset represents Historical North Atlantic and Eastern North Pacific Tropical Cyclone Tracks with 6-hourly (0000, 0600, 1200, 1800 UTC) center locations and intensities for all subtropical depressions and storms, extratropical storms, tropical lows, waves, disturbances, depressions and storms, and all hurricanes, from 1851 through 2008. These data are intended for geographic display and analysis at the national level, and for large regional areas. The data should be displayed and analyzed at scales appropriate for 1:2,000,000-scale data.  


#### Step 2:  View some descriptive statistics  


|   |     YEAR    |    MONTH      |     DAY      |   WIND_KTS    |   PRESSURE    |
|:--|:------------|:--------------|:-------------|:--------------|:--------------|
|   |Min.   :1851 |Min.   : 1.000 |Min.   : 1.00 |Min.   : 10.00 |Min.   :   0.0 |
|   |1st Qu.:1928 |1st Qu.: 8.000 |1st Qu.: 8.00 |1st Qu.: 35.00 |1st Qu.:   0.0 |
|   |Median :1970 |Median : 9.000 |Median :16.00 |Median : 50.00 |Median :   0.0 |
|   |Mean   :1957 |Mean   : 8.541 |Mean   :15.87 |Mean   : 54.73 |Mean   : 372.3 |
|   |3rd Qu.:1991 |3rd Qu.: 9.000 |3rd Qu.:23.00 |3rd Qu.: 70.00 |3rd Qu.: 990.0 |
|   |Max.   :2008 |Max.   :12.000 |Max.   :31.00 |Max.   :165.00 |Max.   :1024.0 |


We can confirm that this particular data had storms from 1851 - 2010, which means the data goes back roughly 100 years before naming storms started! We can also see that the minimum pressure values are 0, which likely means it could not be measured (due to the fact zero pressure is not possible in this case). We can see that there are recorded months from January to December along with days extending from 1 to 31. Whenever you see all of the dates laid out that way, you can smile and think to yourself, "if I need to, I can put dates in an easy to use format such as YYYY-mm-dd (2017-09-12)!"  


#### Step 3: Make a basic plot  


<img src="https://www.stoltzmaniac.com/wp-content/uploads/2017/09/unnamed-chunk-2-1-2.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />
 

This is a great illustration of our data set and we can easily notice an upward trend in the number of storms over time. Before we go running to tell the world that the number of storms per year is growing, we need to drill down a bit deeper. This could simply be caused because more types of storms were added to the data set (we know there are hurricanes, tropical storms, waves, etc.) being recorded. However, this could be a potential starting point for developing a hypothesis for time-series data.  


**You will notice the data starts at 1950 rather than 1851.** I made this choice because storms were not named until this point so it would be difficult to try and count the unique storms per year. It could likely be done by finding a way to utilize the "ID" columns. However, this is a preliminary analysis so I didn't want to dig too deep.  


#### Step 4: Make some calculations


|YEAR | Distinct_Storms| Distinct_Storms_Change| Distinct_Storms_Pct_Change|
|:----|---------------:|----------------------:|--------------------------:|
|1951 |              10|                     -3|                      -0.23|
|1952 |               6|                     -4|                      -0.40|
|1953 |               8|                      2|                       0.33|
|1954 |               8|                      0|                       0.00|
|1955 |              10|                      2|                       0.25|
|1956 |               7|                     -3|                      -0.30|
|1957 |               9|                      2|                       0.29|
|1958 |              10|                      1|                       0.11|
|1959 |              13|                      3|                       0.30|
|1960 |              13|                      0|                       0.00|
  
  
In this case, we can see the number of storms, nominal change and percentage change per year. These calculations help to shed light on what the growth rate looks like each year.  So we can use another summary table:  



|   |Distinct_Storms |Distinct_Storms_Change |Distinct_Storms_Pct_Change |
|:--|:---------------|:----------------------|:--------------------------|
|   |Min.   : 6.00   |Min.   :-15.0000       |Min.   :-0.42000           |
|   |1st Qu.:15.75   |1st Qu.: -3.0000       |1st Qu.:-0.12000           |
|   |Median :25.00   |Median :  1.0000       |Median : 0.04000           |
|   |Mean   :22.81   |Mean   :  0.3448       |Mean   : 0.05966           |
|   |3rd Qu.:28.00   |3rd Qu.:  3.7500       |3rd Qu.: 0.25000           |
|   |Max.   :43.00   |Max.   : 16.0000       |Max.   : 1.14000           |
  
From the table we can state the following for the given time period:  

  * The mean number of storms is 23 per year (with a minimum of 6 and maximum of 43)
  * The mean change in the number of storms per year is 0.34 (with a minimum of -15 and maximum of 16)
  * The mean percent change in the number of storms per year is 6% (with a minimum of -42% and maximum of 114%)

Again, we have to be careful because these numbers are in aggregate and may not tell the whole story. Dividing these into groups of storms is likely much more meaningful.  




#### Step 5: Make a more interesting plot  


<img src="https://www.stoltzmaniac.com/wp-content/uploads/2017/09/unnamed-chunk-5-1-2.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" style="display: block; margin: auto;" />
  

Because I was most interested in hurricanes, I filtered out only the data which was classified as "H (1-5)." By utilizing a data visualization technique called "small multiples" I was able to pull out the different types and view them within the same graph. While this is possible to do in tables and spreadsheets, it's much easier to visualize this way. By holding the axes constant, we can see the majority of the storms are classified as H1 and then it appears to consistently drop down toward H5 (with very few actually being classified as H5). We can also see that most have an upward trend from 1950 - 2010. The steepest appears to be H1 (but it also flattens out over the last decade).  


#### Step 6: Make a filtered calculation  


|   |Distinct_Storms |Distinct_Storms_Change |Distinct_Storms_Pct_Change |
|:--|:---------------|:----------------------|:--------------------------|
|   |Min.   : 4.00   |Min.   :-11.00000      |Min.   :-0.56000           |
|   |1st Qu.: 9.25   |1st Qu.: -4.00000      |1st Qu.:-0.25750           |
|   |Median :13.50   |Median :  0.00000      |Median : 0.00000           |
|   |Mean   :12.76   |Mean   :  0.05172      |Mean   : 0.08379           |
|   |3rd Qu.:15.00   |3rd Qu.:  3.00000      |3rd Qu.: 0.35250           |
|   |Max.   :24.00   |Max.   : 10.00000      |Max.   : 1.80000           |


Now we are looking strictly at hurricane data (classified as H1-H5):  

  * The mean number of hurricanes is 13 per year (with a minimum of 4 and maximum of 24)
  * The mean change in the number of hurricanes per year is 0.05 (with a minimum of -11 and maximum of 10)
  * The mean percent change in the number of hurricanes per year is 8% (with a minimum of -56% and maximum of 180%)  
    
While it doesn't really make sense to say "we had an average growth of 0.05 hurricanes per year between 1950 and 2010" ... it may make sense to say "we saw an average of growth of 8% per year in the number of hurricanes between 1950 and 2010."  

That's a great thing to put in quotes!

> During EDA we discovered an average of growth of 8% per year in the number of hurricanes between 1950 and 2010.  

**Side Note:** Be ready, as soon as you make a statement like that, you will likely have to explain how you arrived at that conclusion. That's where having an RMarkdown notebook and data online in a repository will help you out! Reproducible research is all of the hype right now.   
  

#### Step 7: Try visualizing your statements  

<img src="https://www.stoltzmaniac.com/wp-content/uploads/2017/09/unnamed-chunk-7-1-2.png" title="plot of chunk unnamed-chunk-7" alt="plot of chunk unnamed-chunk-7" style="display: block; margin: auto;" />


A histogram and/or density plot is a great way to visualize the distribution of the data you are making statements about. This plot helps to show that we are looking at a right-skewed distribution with substantial variance. Knowing that we have n = 58 (meaning 58 years after being aggregated), it's not surprising that our histogram looks sparse and our density plot has an unusual shape. At this point, you can make a decision to jot this down, research it in depth and then attack it with full force.  


However, that's not what we're covering in this post.  


#### Step 8: Plot another aspect of your data


<img src="https://www.stoltzmaniac.com/wp-content/uploads/2017/09/unnamed-chunk-8-1-2.png" title="plot of chunk unnamed-chunk-8" alt="plot of chunk unnamed-chunk-8" style="display: block; margin: auto;" />


60K pieces of data can get out of hand quickly, we need to back this down into manageable chunks. Building on the knowledge from our last exploration, we should be able to think of a way to cut this down to get some better information. The concept of small multiples could come in handy again! Splitting the data up by type of storm could prove to be valuable. We can also tell that we are missing

-----

<img src="https://www.stoltzmaniac.com/wp-content/uploads/2017/09/unnamed-chunk-9-1-2.png" title="plot of chunk unnamed-chunk-9" alt="plot of chunk unnamed-chunk-9" style="display: block; margin: auto;" />
  

After filtering the data down to hurricanes and utilizing a heat map rather than plotting individual points we can get a better handle on what is happening where. The H4 and H5 sections are probably the most interesting. It appears as if H4 storms are more frequent on the West coast of Mexico whereas the H5 are most frequent in the Gulf of Mexico.  


Because we're still in EDA mode, we'll continue with another plot.  


<img src="https://www.stoltzmaniac.com/wp-content/uploads/2017/09/unnamed-chunk-10-1-2.png" title="plot of chunk unnamed-chunk-10" alt="plot of chunk unnamed-chunk-10" style="display: block; margin: auto;" />


Here are some of the other storms from the data set. We can see that TD, TS and L have large geographical spreads. The E, SS, and SD storms are concentrated further North toward New England.  

Digging into this type of data and building probabilistic models is a fascinating field. The actuarial sciences are extremely difficult and insurance companies really need good models. Having mapped this data, it's pretty clear you could dig in and find out what parts of the country should expect what types of storms (and you've also known this just from being alive for 10+ years). More hypotheses could be formed about location at this stage and could be tested!  


#### Step 9: Look for a relationship


<img src="https://www.stoltzmaniac.com/wp-content/uploads/2017/09/unnamed-chunk-11-1-2.png" title="plot of chunk unnamed-chunk-11" alt="plot of chunk unnamed-chunk-11" style="display: block; margin: auto;" />
  
   
What is the relationship between WIND_KTS and PRESSURE? This chart helps us to see that low PRESSURE and WIND_KTS are likely negatively correlated. We can also see that the WIND_KTS is essentially the predictor in the data set which can perfectly predict how a storm is classified. Well, it turns out, that's basically the distinguishing feature when scientists are determining how to categorize these storms!  


#### Step N......  

We have done some basic EDA and identified some patterns in the data. While doing some EDA can simply be just for fun, in most data analysis, it's important to find a place to apply these discoveries by making and testing hypotheses! There are plenty of industries where you could find a use for this:  

  * Insurance - improve statistical modeling and risk analysis
  * Real Estate Development - identify strategic investment locations
  * Agriculture - crop selection
  * ...  
  
The rest is up to you! This is a great data set and there are a lot more pieces of information lurking within it. I want people to do their own EDA and send me anything interesting! 

Some fun things to check out:  

  * What was the most common name for a hurricane?
  * Do the names actually follow an alphabetical pattern through time? (This is one is tricky)
  * If the names are in alphabetical order, how often does a letter get repeated in a year?
  * Can we merge this data with FEMA, charitable donations, or other aid data?

  
To get you started on the first one, here's the Top 10 most common names for tropical storms. Why do you think it's Florence?


<img src="https://www.stoltzmaniac.com/wp-content/uploads/2017/09/unnamed-chunk-12-1-2.png" title="plot of chunk unnamed-chunk-12" alt="plot of chunk unnamed-chunk-12" style="display: block; margin: auto;" />


Thank you for reading, I hope this helps you with your own data. The code is all written in R and is located on my [GitHub](https://github.com/stoltzmaniac/Tropical-Storm-Data-Analysis). You can also find other data visualization posts and usages of ggplot2 on my blog [Stoltzmaniac](https://www.stoltzmaniac.com?utm_campaign=bottom_of_tropical_storm_post)

---
title: "Homework 5"
author: "Bryan Correa Gonzalez"
date: "2025-01-27"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and/or complete the exercises in RMarkdown. Please embed all of your code and push the final work to your repository. Your report should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run.  

## Load the tidyverse

```r
library("tidyverse")
library("janitor")
```

## Data 
For this assignment, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.

# have to look at the read.me to understand what the variables mean

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the data folder.   

**1. Load `IvindoData_DryadVersion.csv` and store it as a new object called `gabon`.**

```r
gabon <- read.csv("data/IvindoData_DryadVersion.csv")
gabon <- clean_names(gabon)
```

**2. Use one or more of the summary functions you have learned to get an idea of the structure of the data.**  

```r
summary(gabon)
```

```
##   transect_id       distance        hunt_cat         num_households 
##  Min.   : 1.00   Min.   : 2.700   Length:24          Min.   :13.00  
##  1st Qu.: 5.75   1st Qu.: 5.668   Class :character   1st Qu.:24.75  
##  Median :14.50   Median : 9.720   Mode  :character   Median :29.00  
##  Mean   :13.50   Mean   :11.879                      Mean   :37.88  
##  3rd Qu.:20.25   3rd Qu.:17.683                      3rd Qu.:54.00  
##  Max.   :27.00   Max.   :26.760                      Max.   :73.00  
##    land_use            veg_rich       veg_stems       veg_liana     
##  Length:24          Min.   :10.88   Min.   :23.44   Min.   : 4.750  
##  Class :character   1st Qu.:13.10   1st Qu.:28.69   1st Qu.: 9.033  
##  Mode  :character   Median :14.94   Median :32.45   Median :11.940  
##                     Mean   :14.83   Mean   :32.80   Mean   :11.040  
##                     3rd Qu.:16.54   3rd Qu.:37.08   3rd Qu.:13.250  
##                     Max.   :18.75   Max.   :47.56   Max.   :16.380  
##     veg_dbh        veg_canopy    veg_understory     ra_apes      
##  Min.   :28.45   Min.   :2.500   Min.   :2.380   Min.   : 0.000  
##  1st Qu.:40.65   1st Qu.:3.250   1st Qu.:2.875   1st Qu.: 0.000  
##  Median :43.90   Median :3.430   Median :3.000   Median : 0.485  
##  Mean   :46.09   Mean   :3.469   Mean   :3.020   Mean   : 2.045  
##  3rd Qu.:50.58   3rd Qu.:3.750   3rd Qu.:3.167   3rd Qu.: 3.815  
##  Max.   :76.48   Max.   :4.000   Max.   :3.880   Max.   :12.930  
##     ra_birds      ra_elephant       ra_monkeys      ra_rodent    
##  Min.   :31.56   Min.   :0.0000   Min.   : 5.84   Min.   :1.060  
##  1st Qu.:52.51   1st Qu.:0.0000   1st Qu.:22.70   1st Qu.:2.047  
##  Median :57.90   Median :0.3600   Median :31.74   Median :3.230  
##  Mean   :58.64   Mean   :0.5450   Mean   :31.30   Mean   :3.278  
##  3rd Qu.:68.17   3rd Qu.:0.8925   3rd Qu.:39.88   3rd Qu.:4.093  
##  Max.   :85.03   Max.   :2.3000   Max.   :54.12   Max.   :6.310  
##   ra_ungulate     rich_all_species evenness_all_species diversity_all_species
##  Min.   : 0.000   Min.   :15.00    Min.   :0.6680       Min.   :1.966        
##  1st Qu.: 1.232   1st Qu.:19.00    1st Qu.:0.7542       1st Qu.:2.248        
##  Median : 2.545   Median :20.00    Median :0.7760       Median :2.316        
##  Mean   : 4.166   Mean   :20.21    Mean   :0.7699       Mean   :2.310        
##  3rd Qu.: 5.157   3rd Qu.:22.00    3rd Qu.:0.8083       3rd Qu.:2.429        
##  Max.   :13.860   Max.   :24.00    Max.   :0.8330       Max.   :2.566        
##  rich_bird_species evenness_bird_species diversity_bird_species
##  Min.   : 8.00     Min.   :0.5590        Min.   :1.162         
##  1st Qu.:10.00     1st Qu.:0.6825        1st Qu.:1.603         
##  Median :11.00     Median :0.7220        Median :1.680         
##  Mean   :10.33     Mean   :0.7137        Mean   :1.661         
##  3rd Qu.:11.00     3rd Qu.:0.7722        3rd Qu.:1.784         
##  Max.   :13.00     Max.   :0.8240        Max.   :2.008         
##  rich_mammal_species evenness_mammal_species diversity_mammal_species
##  Min.   : 6.000      Min.   :0.6190          Min.   :1.378           
##  1st Qu.: 9.000      1st Qu.:0.7073          1st Qu.:1.567           
##  Median :10.000      Median :0.7390          Median :1.699           
##  Mean   : 9.875      Mean   :0.7477          Mean   :1.698           
##  3rd Qu.:11.000      3rd Qu.:0.7847          3rd Qu.:1.815           
##  Max.   :12.000      Max.   :0.8610          Max.   :2.065
```

```r
glimpse(gabon)
```

```
## Rows: 24
## Columns: 26
## $ transect_id              <int> 1, 2, 2, 3, 4, 5, 6, 7, 8, 9, 13, 14, 15, 16,…
## $ distance                 <dbl> 7.14, 17.31, 18.32, 20.85, 15.95, 17.47, 24.0…
## $ hunt_cat                 <chr> "Moderate", "None", "None", "None", "None", "…
## $ num_households           <int> 54, 54, 29, 29, 29, 29, 29, 54, 25, 73, 46, 5…
## $ land_use                 <chr> "Park", "Park", "Park", "Logging", "Park", "P…
## $ veg_rich                 <dbl> 16.67, 15.75, 16.88, 12.44, 17.13, 16.50, 14.…
## $ veg_stems                <dbl> 31.20, 37.44, 32.33, 29.39, 36.00, 29.22, 31.…
## $ veg_liana                <dbl> 5.78, 13.25, 4.75, 9.78, 13.25, 12.88, 8.38, …
## $ veg_dbh                  <dbl> 49.57, 34.59, 42.82, 36.62, 41.52, 44.07, 51.…
## $ veg_canopy               <dbl> 3.78, 3.75, 3.43, 3.75, 3.88, 2.50, 4.00, 4.0…
## $ veg_understory           <dbl> 2.89, 3.88, 3.00, 2.75, 3.25, 3.00, 2.38, 2.7…
## $ ra_apes                  <dbl> 1.87, 0.00, 4.49, 12.93, 0.00, 2.48, 3.78, 6.…
## $ ra_birds                 <dbl> 52.66, 52.17, 37.44, 59.29, 52.62, 38.64, 42.…
## $ ra_elephant              <dbl> 0.00, 0.86, 1.33, 0.56, 1.00, 0.00, 1.11, 0.4…
## $ ra_monkeys               <dbl> 38.59, 28.53, 41.82, 19.85, 41.34, 43.29, 46.…
## $ ra_rodent                <dbl> 4.22, 6.04, 1.06, 3.66, 2.52, 1.83, 3.10, 1.2…
## $ ra_ungulate              <dbl> 2.66, 12.41, 13.86, 3.71, 2.53, 13.75, 3.10, …
## $ rich_all_species         <int> 22, 20, 22, 19, 20, 22, 23, 19, 19, 19, 21, 2…
## $ evenness_all_species     <dbl> 0.793, 0.773, 0.740, 0.681, 0.811, 0.786, 0.8…
## $ diversity_all_species    <dbl> 2.452, 2.314, 2.288, 2.006, 2.431, 2.429, 2.5…
## $ rich_bird_species        <int> 11, 10, 11, 8, 8, 10, 11, 11, 11, 9, 11, 11, …
## $ evenness_bird_species    <dbl> 0.732, 0.704, 0.688, 0.559, 0.799, 0.771, 0.8…
## $ diversity_bird_species   <dbl> 1.756, 1.620, 1.649, 1.162, 1.660, 1.775, 1.9…
## $ rich_mammal_species      <int> 11, 10, 11, 11, 12, 12, 12, 8, 8, 10, 10, 11,…
## $ evenness_mammal_species  <dbl> 0.736, 0.705, 0.650, 0.619, 0.736, 0.694, 0.7…
## $ diversity_mammal_species <dbl> 1.764, 1.624, 1.558, 1.484, 1.829, 1.725, 1.9…
```
  
**3. Use `mutate()` Change the variables `HuntCat`, `LandUse`, and `TransectID` to factors.**

```r
gabon <- gabon %>% 
  mutate(hunt_cat = as.factor(hunt_cat)) %>% 
  mutate(land_use = as.factor(land_use)) %>% 
  mutate(transect_id = as.factor(transect_id)) 
  str(gabon)
```

```
## 'data.frame':	24 obs. of  26 variables:
##  $ transect_id             : Factor w/ 23 levels "1","2","3","4",..: 1 2 2 3 4 5 6 7 8 9 ...
##  $ distance                : num  7.14 17.31 18.32 20.85 15.95 ...
##  $ hunt_cat                : Factor w/ 3 levels "High","Moderate",..: 2 3 3 3 3 3 3 3 1 1 ...
##  $ num_households          : int  54 54 29 29 29 29 29 54 25 73 ...
##  $ land_use                : Factor w/ 3 levels "Logging","Neither",..: 3 3 3 1 3 3 3 1 2 1 ...
##  $ veg_rich                : num  16.7 15.8 16.9 12.4 17.1 ...
##  $ veg_stems               : num  31.2 37.4 32.3 29.4 36 ...
##  $ veg_liana               : num  5.78 13.25 4.75 9.78 13.25 ...
##  $ veg_dbh                 : num  49.6 34.6 42.8 36.6 41.5 ...
##  $ veg_canopy              : num  3.78 3.75 3.43 3.75 3.88 2.5 4 4 3 3.25 ...
##  $ veg_understory          : num  2.89 3.88 3 2.75 3.25 3 2.38 2.71 3.25 3.13 ...
##  $ ra_apes                 : num  1.87 0 4.49 12.93 0 ...
##  $ ra_birds                : num  52.7 52.2 37.4 59.3 52.6 ...
##  $ ra_elephant             : num  0 0.86 1.33 0.56 1 0 1.11 0.43 2.2 0 ...
##  $ ra_monkeys              : num  38.6 28.5 41.8 19.9 41.3 ...
##  $ ra_rodent               : num  4.22 6.04 1.06 3.66 2.52 1.83 3.1 1.26 4.37 6.31 ...
##  $ ra_ungulate             : num  2.66 12.41 13.86 3.71 2.53 ...
##  $ rich_all_species        : int  22 20 22 19 20 22 23 19 19 19 ...
##  $ evenness_all_species    : num  0.793 0.773 0.74 0.681 0.811 0.786 0.818 0.757 0.773 0.668 ...
##  $ diversity_all_species   : num  2.45 2.31 2.29 2.01 2.43 ...
##  $ rich_bird_species       : int  11 10 11 8 8 10 11 11 11 9 ...
##  $ evenness_bird_species   : num  0.732 0.704 0.688 0.559 0.799 0.771 0.801 0.687 0.784 0.573 ...
##  $ diversity_bird_species  : num  1.76 1.62 1.65 1.16 1.66 ...
##  $ rich_mammal_species     : int  11 10 11 11 12 12 12 8 8 10 ...
##  $ evenness_mammal_species : num  0.736 0.705 0.65 0.619 0.736 0.694 0.776 0.79 0.821 0.783 ...
##  $ diversity_mammal_species: num  1.76 1.62 1.56 1.48 1.83 ...
```

**4. Use `filter` to make three new dataframes focused only on 1. national parks, 2. logging concessions, and 3. neither. Have a look at the README in the data folder so you understand the variables.**

```r
national_parks <- gabon %>% 
  filter(land_use == "Park")
```


```r
logging_parks <- gabon %>% 
  filter(land_use == "Logging")
```


```r
neither_parks <- gabon %>% 
  filter(land_use == "Neither")
```

**5. How many transects are recorded for each land use type?**

```r
national_parks %>% 
  select(transect_id)
```

```
##   transect_id
## 1           1
## 2           2
## 3           2
## 4           4
## 5           5
## 6           6
## 7          24
```

```r
logging_parks %>% 
  select(transect_id)
```

```
##    transect_id
## 1            3
## 2            7
## 3            9
## 4           13
## 5           14
## 6           16
## 7           18
## 8           19
## 9           20
## 10          22
## 11          25
## 12          26
## 13          27
```

```r
neither_parks %>% 
  select(transect_id)
```

```
##   transect_id
## 1           8
## 2          15
## 3          17
## 4          21
```


**6. For which land use type (national parks, logging, or neither) is average all species diversity the greatest?**


```r
mean(national_parks$diversity_all_species)
```

```
## [1] 2.425143
```

```r
mean(logging_parks$diversity_all_species)
```

```
## [1] 2.232538
```


```r
mean(neither_parks$diversity_all_species)
```

```
## [1] 2.3575
```
The National parks have the greatest all species diversity.

**7. Use `filter` to find the transect that has the highest relative abundance of elephants. What land use type is this? Use `arrange()` to sort your results.** 

```r
gabon2 <- gabon %>% 
  select("transect_id", "land_use", "ra_elephant") %>%
  filter("ra_elephant" == max("ra_elephant")) %>% 
  arrange(desc(ra_elephant))
gabon2
```

```
##    transect_id land_use ra_elephant
## 1           18  Logging        2.30
## 2            8  Neither        2.20
## 3            2     Park        1.33
## 4            6     Park        1.11
## 5            4     Park        1.00
## 6           13  Logging        0.99
## 7            2     Park        0.86
## 8           21  Neither        0.77
## 9            3  Logging        0.56
## 10          14  Logging        0.52
## 11           7  Logging        0.43
## 12          16  Logging        0.36
## 13          19  Logging        0.36
## 14          15  Neither        0.29
## 15           1     Park        0.00
## 16           5     Park        0.00
## 17           9  Logging        0.00
## 18          17  Neither        0.00
## 19          20  Logging        0.00
## 20          22  Logging        0.00
## 21          24     Park        0.00
## 22          25  Logging        0.00
## 23          26  Logging        0.00
## 24          27  Logging        0.00
```
**8. Use `filter` to find all transects that have greater than 15 tree species or a breast height diameter between 50 and 60cm.  **

```r
gabon3 <- gabon %>% 
  select("transect_id", "veg_rich", "veg_dbh") %>% 
  filter(veg_rich > 15 | between(veg_dbh, 50,60))
gabon3
```

```
##    transect_id veg_rich veg_dbh
## 1            1    16.67   49.57
## 2            2    15.75   34.59
## 3            2    16.88   42.82
## 4            4    17.13   41.52
## 5            5    16.50   44.07
## 6            6    14.75   51.22
## 7            9    16.00   69.30
## 8           14    15.75   52.12
## 9           15    10.88   54.77
## 10          17    14.25   57.71
## 11          21    16.25   50.36
## 12          22    17.13   39.31
## 13          24    16.75   44.21
## 14          26    18.75   35.58
```

**9.Which transects and land use types have more than 10 tree species and 10 mammal species? Use `arrange()` to sort by the number of tree species.**

```r
gabon4 <- gabon %>% 
  select ("transect_id", "land_use", "veg_rich", "rich_mammal_species") %>% 
  filter(veg_rich >10 & rich_mammal_species == 10) %>% 
  arrange(desc(veg_rich))
gabon4
```

```
##   transect_id land_use veg_rich rich_mammal_species
## 1          26  Logging    18.75                  10
## 2          21  Neither    16.25                  10
## 3           9  Logging    16.00                  10
## 4           2     Park    15.75                  10
## 5          25  Logging    15.00                  10
## 6          13  Logging    12.38                  10
```

**10. Explore the data! Develop one question on your own that includes at least two lines of code. **

###  Which transect has the highest degree of bird specie richness while also having the highest degree of mammal specie richness?

```r
gabon5 <- gabon %>% 
  select("transect_id", "rich_bird_species", "rich_mammal_species") %>% 
  filter("rich_bird_species" == max("rich_bird_species") & "rich_mammal_species" ==max("rich_mammal_species")) %>% 
  arrange(desc(rich_bird_species), rich_mammal_species)
gabon5
```

```
##    transect_id rich_bird_species rich_mammal_species
## 1           16                13                   9
## 2           24                12                  12
## 3            7                11                   8
## 4            8                11                   8
## 5           15                11                   8
## 6           17                11                   9
## 7           18                11                   9
## 8           13                11                  10
## 9           26                11                  10
## 10           1                11                  11
## 11           2                11                  11
## 12          14                11                  11
## 13           6                11                  12
## 14          20                10                   6
## 15          27                10                   9
## 16           2                10                  10
## 17          25                10                  10
## 18           5                10                  12
## 19          22                10                  12
## 20           9                 9                  10
## 21          21                 9                  10
## 22          19                 8                   7
## 23           3                 8                  11
## 24           4                 8                  12
```

```r
filter(gabon5, transect_id == 24)
```

```
##   transect_id rich_bird_species rich_mammal_species
## 1          24                12                  12
```

### Although the code appears to give the answer of TransectID 16, it is actually Transect 24 that has both the highest specie richness for birds and mammals. 

## Knit and Upload
Please knit your work as a .pdf or .html file and upload to Canvas. Homework is due before the start of the next lab. No late work is accepted. Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

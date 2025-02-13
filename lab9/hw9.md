---
title: "Homework 9"
author: "Bryan Correa Gonzalez"
date: "2025-02-13"
output:
  html_document:
    theme: spacelab
    toc: no
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
```

## Data
For this homework, we will use a data set compiled by the Office of Environment and Heritage in New South Whales, Australia. It contains the enterococci counts in water samples obtained from Sydney beaches as part of the Beachwatch Water Quality Program. _Enterococci_ are bacteria common in the intestines of mammals; they are rarely present in clean water. So, _Enterococci_ values are a measurement of pollution. `cfu` stands for colony forming units and measures the number of viable bacteria in a sample [cfu](https://en.wikipedia.org/wiki/Colony-forming_unit).   

This homework loosely follows the tutorial of [R Ladies Sydney](https://rladiessydney.org/). If you get stuck, check it out!  

1. Start by loading the data `sydneybeaches`. Do some exploratory analysis to get an idea of the data structure.

```r
sydney_beaches <- read.csv("data/sydneybeaches.csv") %>% clean_names()
```


```r
glimpse(sydney_beaches)
```

```
## Rows: 3,690
## Columns: 8
## $ beach_id              <dbl> 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, …
## $ region                <chr> "Sydney City Ocean Beaches", "Sydney City Ocean …
## $ council               <chr> "Randwick Council", "Randwick Council", "Randwic…
## $ site                  <chr> "Clovelly Beach", "Clovelly Beach", "Clovelly Be…
## $ longitude             <dbl> 151.2675, 151.2675, 151.2675, 151.2675, 151.2675…
## $ latitude              <dbl> -33.91449, -33.91449, -33.91449, -33.91449, -33.…
## $ date                  <chr> "02/01/2013", "06/01/2013", "12/01/2013", "18/01…
## $ enterococci_cfu_100ml <int> 19, 3, 2, 13, 8, 7, 11, 97, 3, 0, 6, 0, 1, 8, 3,…
```


2. Are these data "tidy" per the definitions of the tidyverse? How do you know? Are they in wide or long format?

Yes this data is tidy. Each variable has its own column. Each observation has its own row. Each value has its own cells. They are in the long format as each beach has multiple enterococci_cfu_100ml accordgin to every date which has its own column (the dates would be columns if it was wide).

```r
sydney_beaches %>% 
  head()
```

```
##   beach_id                    region          council           site longitude
## 1       25 Sydney City Ocean Beaches Randwick Council Clovelly Beach  151.2675
## 2       25 Sydney City Ocean Beaches Randwick Council Clovelly Beach  151.2675
## 3       25 Sydney City Ocean Beaches Randwick Council Clovelly Beach  151.2675
## 4       25 Sydney City Ocean Beaches Randwick Council Clovelly Beach  151.2675
## 5       25 Sydney City Ocean Beaches Randwick Council Clovelly Beach  151.2675
## 6       25 Sydney City Ocean Beaches Randwick Council Clovelly Beach  151.2675
##    latitude       date enterococci_cfu_100ml
## 1 -33.91449 02/01/2013                    19
## 2 -33.91449 06/01/2013                     3
## 3 -33.91449 12/01/2013                     2
## 4 -33.91449 18/01/2013                    13
## 5 -33.91449 30/01/2013                     8
## 6 -33.91449 05/02/2013                     7
```

3. We are only interested in the variables site, date, and enterococci_cfu_100ml. Make a new object focused on these variables only. Name the object `sydneybeaches_long`

```r
sydneybeaches_long <- sydney_beaches %>% 
  select(site, date, enterococci_cfu_100ml)
head(sydneybeaches_long)
```

```
##             site       date enterococci_cfu_100ml
## 1 Clovelly Beach 02/01/2013                    19
## 2 Clovelly Beach 06/01/2013                     3
## 3 Clovelly Beach 12/01/2013                     2
## 4 Clovelly Beach 18/01/2013                    13
## 5 Clovelly Beach 30/01/2013                     8
## 6 Clovelly Beach 05/02/2013                     7
```

4. Pivot the data such that the dates are column names and each beach only appears once (wide format). Name the object `sydneybeaches_wide`

```r
sydneybeaches_wide <- sydneybeaches_long %>% 
  pivot_wider(
              names_from = "date",
              values_from = "enterococci_cfu_100ml")
head(sydneybeaches_wide)
```

```
## # A tibble: 6 × 345
##   site          `02/01/2013` `06/01/2013` `12/01/2013` `18/01/2013` `30/01/2013`
##   <chr>                <int>        <int>        <int>        <int>        <int>
## 1 Clovelly Bea…           19            3            2           13            8
## 2 Coogee Beach            15            4           17           18           22
## 3 Gordons Bay …           NA           NA           NA           NA           NA
## 4 Little Bay B…            9            3           72            1           44
## 5 Malabar Beach            2            4          390           15           13
## 6 Maroubra Bea…            1            1           20            2           11
## # ℹ 339 more variables: `05/02/2013` <int>, `11/02/2013` <int>,
## #   `23/02/2013` <int>, `07/03/2013` <int>, `25/03/2013` <int>,
## #   `02/04/2013` <int>, `12/04/2013` <int>, `18/04/2013` <int>,
## #   `24/04/2013` <int>, `01/05/2013` <int>, `20/05/2013` <int>,
## #   `31/05/2013` <int>, `06/06/2013` <int>, `12/06/2013` <int>,
## #   `24/06/2013` <int>, `06/07/2013` <int>, `18/07/2013` <int>,
## #   `24/07/2013` <int>, `08/08/2013` <int>, `22/08/2013` <int>, …
```

5. Pivot the data back so that the dates are data and not column names.

```r
sd_revert <- sydneybeaches_wide %>% 
  pivot_longer(-site,
               names_to = "date",
               values_to = "enterococci_cfu_100ml") 
head(sd_revert)
```

```
## # A tibble: 6 × 3
##   site           date       enterococci_cfu_100ml
##   <chr>          <chr>                      <int>
## 1 Clovelly Beach 02/01/2013                    19
## 2 Clovelly Beach 06/01/2013                     3
## 3 Clovelly Beach 12/01/2013                     2
## 4 Clovelly Beach 18/01/2013                    13
## 5 Clovelly Beach 30/01/2013                     8
## 6 Clovelly Beach 05/02/2013                     7
```

6. We haven't dealt much with dates yet, but separate the date into columns day, month, and year. Do this on the `sydneybeaches_long` data.

```r
dates_sb <- sydneybeaches_long %>% 
  separate(date, into=c("day", "month", "year"), sep = "/")
head(dates_sb)
```

```
##             site day month year enterococci_cfu_100ml
## 1 Clovelly Beach  02    01 2013                    19
## 2 Clovelly Beach  06    01 2013                     3
## 3 Clovelly Beach  12    01 2013                     2
## 4 Clovelly Beach  18    01 2013                    13
## 5 Clovelly Beach  30    01 2013                     8
## 6 Clovelly Beach  05    02 2013                     7
```

7. What is the average `enterococci_cfu_100ml` by year for each beach. Think about which data you will use- long or wide.

```r
mean_entero <- dates_sb %>% 
  select(site, year, enterococci_cfu_100ml) %>% 
  group_by(site, year) %>% 
  summarize(mean(enterococci_cfu_100ml))
```

```
## `summarise()` has grouped output by 'site'. You can override using the
## `.groups` argument.
```

```r
head(mean_entero)
```

```
## # A tibble: 6 × 3
## # Groups:   site [1]
##   site        year  `mean(enterococci_cfu_100ml)`
##   <chr>       <chr>                         <dbl>
## 1 Bondi Beach 2013                           32.2
## 2 Bondi Beach 2014                           11.1
## 3 Bondi Beach 2015                           14.3
## 4 Bondi Beach 2016                           19.4
## 5 Bondi Beach 2017                           13.2
## 6 Bondi Beach 2018                           NA
```

8. Make the output from question 7 easier to read by pivoting it to wide format.

```r
mean_entero_wide <- mean_entero %>% 
  pivot_wider(
              names_from = "year",
              values_from = "mean(enterococci_cfu_100ml)")
head(mean_entero_wide)
```

```
## # A tibble: 6 × 7
## # Groups:   site [6]
##   site               `2013` `2014` `2015` `2016` `2017` `2018`
##   <chr>               <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
## 1 Bondi Beach         32.2    11.1  14.3    19.4  13.2      NA
## 2 Bronte Beach        26.8    17.5  NA      61.3  16.8      NA
## 3 Clovelly Beach       9.28   13.8   8.82   11.3   7.93     NA
## 4 Coogee Beach        39.7    52.6  40.3    NA    20.7      NA
## 5 Gordons Bay (East)  24.8    16.7  36.2    39.0  13.7      NA
## 6 Little Bay Beach   122.     19.5  25.5    31.2  18.2      NA
```

9. What was the most polluted beach in 2013?
Little Bay Beach

```r
mean_entero_wide %>% 
  select(site, "2013")%>%
  arrange(desc(`2013`)) %>% 
  head(,n=1)
```

```
## # A tibble: 1 × 2
## # Groups:   site [1]
##   site             `2013`
##   <chr>             <dbl>
## 1 Little Bay Beach   122.
```

10. Explore the data! Do one analysis of your choice that includes a minimum of three lines of code.  

What is the overall most polluted beach? (Which beach has the highest average of entero bacteria across all recorded times?)

```r
mean_entero_wide %>% 
  pivot_longer(-site,
               names_to = "year",
               values_to = "enterococci_cfu_100ml") %>% 
  group_by(site) %>% 
  summarize(mean_overall_entero = mean(enterococci_cfu_100ml, na.rm = T)) %>% 
  arrange(desc(mean_overall_entero)) %>% 
  head(,n=1)
```

```
## # A tibble: 1 × 2
##   site          mean_overall_entero
##   <chr>                       <dbl>
## 1 Malabar Beach                72.7
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   

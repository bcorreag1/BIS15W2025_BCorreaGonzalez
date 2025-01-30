---
title: "Homework 6"
author: "Bryan Correa Gonzalez
"
date: "2025-01-30"
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

## Load the superhero data
Let's have a little fun with this one! We are going to explore data on superheroes. These are data taken from comic books and assembled by devoted fans. The include a good mix of categorical and continuous data.  Data taken from: https://www.kaggle.com/claudiodavi/superhero-set  

Load the `heroes_information.csv` and `super_hero_powers.csv` data. Make sure the columns are cleanly named.

```r
superhero_info <- read_csv("data/heroes_information.csv", na = c("", "-99", "-")) %>% clean_names() %>% mutate(across(everything(), tolower))
```

```
## Rows: 734 Columns: 10
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (8): name, Gender, Eye color, Race, Hair color, Publisher, Skin color, A...
## dbl (2): Height, Weight
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
superhero_powers <- read_csv("data/super_hero_powers.csv", na = c("", "-99", "-")) %>% clean_names() %>% mutate(across(everything(), tolower))
```

```
## Rows: 667 Columns: 168
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr   (1): hero_names
## lgl (167): Agility, Accelerated Healing, Lantern Power Ring, Dimensional Awa...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. For the superhero_info data, how many bad, good, and neutral superheros are there? Try using count() and/ or tabyl().

```r
superhero_info %>% 
  count(alignment)
```

```
## # A tibble: 4 × 2
##   alignment     n
##   <chr>     <int>
## 1 bad         207
## 2 good        496
## 3 neutral      24
## 4 <NA>          7
```


```r
superhero_info %>% 
  tabyl(alignment)
```

```
##  alignment   n     percent valid_percent
##        bad 207 0.282016349    0.28473177
##       good 496 0.675749319    0.68225585
##    neutral  24 0.032697548    0.03301238
##       <NA>   7 0.009536785            NA
```

2. Notice that we have some bad superheros! Who are they? List their names below.  

```r
superhero_info %>% 
  select (name, alignment) %>% 
  filter(alignment == "bad")
```

```
## # A tibble: 207 × 2
##    name          alignment
##    <chr>         <chr>    
##  1 abomination   bad      
##  2 abraxas       bad      
##  3 absorbing man bad      
##  4 air-walker    bad      
##  5 ajax          bad      
##  6 alex mercer   bad      
##  7 alien         bad      
##  8 amazo         bad      
##  9 ammo          bad      
## 10 angela        bad      
## # ℹ 197 more rows
```



3. How many distinct "races" are represented in `superhero_info`?

```r
superhero_info %>% 
  summarize(n_race=n_distinct(race, na.rm=T))
```

```
## # A tibble: 1 × 1
##   n_race
##    <int>
## 1     61
```

## Good and Bad
4. Let's make two different data frames, one focused on the "good guys" and another focused on the "bad guys".

```r
good_guys <- filter(superhero_info, alignment == "good")
bad_guys <- filter(superhero_info, alignment == "bad")
```


5. Who are the good Vampires?

```r
good_guys %>% 
  filter(race == "vampire")
```

```
## # A tibble: 2 × 10
##   name  gender eye_color race   hair_color height publisher skin_color alignment
##   <chr> <chr>  <chr>     <chr>  <chr>      <chr>  <chr>     <chr>      <chr>    
## 1 angel male   <NA>      vampi… <NA>       <NA>   dark hor… <NA>       good     
## 2 blade male   brown     vampi… black      188    marvel c… <NA>       good     
## # ℹ 1 more variable: weight <chr>
```

6. Who has the height advantage- bad guys or good guys? Convert their height to meters and sort from tallest to shortest.  

The good guys appear to have to have the height advantage.


```r
good_guys %>% 
  select(name, race, height) %>% 
  mutate(height = as.numeric(height)) %>% 
  mutate(height_meters = height/100) %>% 
  arrange(desc(height_meters))
```

```
## # A tibble: 496 × 4
##    name          race              height height_meters
##    <chr>         <chr>              <dbl>         <dbl>
##  1 fin fang foom kakarantharaian     975           9.75
##  2 groot         flora colossus      701           7.01
##  3 wolfsbane     <NA>                366           3.66
##  4 sasquatch     <NA>                305           3.05
##  5 ymir          frost giant         305.          3.05
##  6 rey           human               297           2.97
##  7 hellboy       demon               259           2.59
##  8 hulk          human / radiation   244           2.44
##  9 kilowog       bolovaxian          234           2.34
## 10 cloak         <NA>                226           2.26
## # ℹ 486 more rows
```


```r
bad_guys %>% 
  select(name, race, height) %>% 
  mutate(height = as.numeric(height)) %>% 
  mutate(height_meters = height/100) %>% 
  arrange(desc(height_meters))
```

```
## # A tibble: 207 × 4
##    name           race            height height_meters
##    <chr>          <chr>            <dbl>         <dbl>
##  1 modok          cyborg             366          3.66
##  2 onslaught      mutant             305          3.05
##  3 sauron         maiar              279          2.79
##  4 solomon grundy zombie             279          2.79
##  5 darkseid       new god            267          2.67
##  6 amazo          android            257          2.57
##  7 alien          xenomorph xx121    244          2.44
##  8 doomsday       alien              244          2.44
##  9 killer croc    metahuman          244          2.44
## 10 venom iii      symbiote           229          2.29
## # ℹ 197 more rows
```

## `superhero_powers`
Have a quick look at the `superhero_powers` data frame.  

7. How many superheros have a combination of agility, stealth, super_strength, and stamina?

```r
best_supers <- superhero_powers %>% 
  select(hero_names, agility, stealth, super_strength, stamina) %>% 
  filter(agility == "true", stealth == "true", super_strength == "true", stamina == "true") %>% 
  summarize(total = n()) 
best_supers
```

```
## # A tibble: 1 × 1
##   total
##   <int>
## 1    40
```

8. Who is the most powerful superhero? Have a look at the code chunk below. Use the internet to annotate each line of code so you know how it works. It's OK to use AI to help you with this task.

```r
test <- superhero_powers %>%
  # calls the superhero_powers df
  mutate(across(-1, ~ ifelse(. == TRUE, 1, 0))) %>% 
  # transforms all but the first column then checks if each data entry is "true" or "false". if true it will assign it a value of 1. if false it will assign it a value of 0. 
  mutate(total_powers = rowSums(across(-1))) %>% 
  # first it creates a new column calles "total_powers". then calculates the sum of all rows, excluding the first column for each super hero.
  select(hero_names, total_powers) %>% 
  # only selects and outputs the "hero_names" and "total_powers" columns
  arrange(-total_powers)
  # sorts the data set by "total_powers" from highest to lowest numerical values.
```

## Your Favorite
9. Pick your favorite superhero and let's see their powers!  

```r
superhero_powers %>% 
  filter(hero_names == "batman") %>% 
  select(hero_names, where(~. == "true"))
```

```
## # A tibble: 1 × 18
##   hero_names agility durability stealth underwater_breathing marksmanship
##   <chr>      <chr>   <chr>      <chr>   <chr>                <chr>       
## 1 batman     true    true       true    true                 true        
## # ℹ 12 more variables: weapons_master <chr>, intelligence <chr>,
## #   super_strength <chr>, stamina <chr>, super_speed <chr>,
## #   weapon_based_powers <chr>, peak_human_condition <chr>, reflexes <chr>,
## #   gliding <chr>, power_suit <chr>, vision_night <chr>, vision_infrared <chr>
```

10. Can you find your hero in the superhero_info data? Show their info!  

```r
superhero_info %>% 
  filter(name == "batman")
```

```
## # A tibble: 2 × 10
##   name   gender eye_color race  hair_color height publisher skin_color alignment
##   <chr>  <chr>  <chr>     <chr> <chr>      <chr>  <chr>     <chr>      <chr>    
## 1 batman male   blue      human black      188    dc comics <NA>       good     
## 2 batman male   blue      human black      178    dc comics <NA>       good     
## # ℹ 1 more variable: weight <chr>
```

## Knit and Upload
Please knit your work as a .pdf or .html file and upload to Canvas. Homework is due before the start of the next lab. No late work is accepted. Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

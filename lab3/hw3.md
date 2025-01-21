---
title: "Homework 3"
author: "Type Your Name Here"
date: "2025-01-21"
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
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.1     ✔ readr     2.1.4
## ✔ forcats   1.0.0     ✔ stringr   1.5.0
## ✔ ggplot2   3.4.2     ✔ tibble    3.2.1
## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
## ✔ purrr     1.0.1     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the ]8;;http://conflicted.r-lib.org/conflicted package]8;; to force all conflicts to become errors
```

```r
options(scipen=999) # turn off scientific notation
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder and the reference is below.  

**Database of vertebrate home range sizes.**. 
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <- read.csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

**2. What are the dimensions of the dataframe?**  

```r
dim(homerange)
```

```
## [1] 569  24
```

**3. Are there any NA's in the dataframe? Try using summary to determine which variables have more or less NA's.**

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2           log10.hra     
##  Length:569                 Min.   :         0   Min.   :-1.523  
##  Class :character           1st Qu.:      4500   1st Qu.: 3.653  
##  Mode  :character           Median :     39344   Median : 4.595  
##                             Mean   :  21456509   Mean   : 4.709  
##                             3rd Qu.:   1038100   3rd Qu.: 6.016  
##                             Max.   :3550830977   Max.   : 9.550  
##                                                                  
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild       dimension            preymass         log10.preymass   
##  Length:569         Length:569         Min.   :     0.67   Min.   :-0.1739  
##  Class :character   Class :character   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Mode  :character   Median :    53.75   Median : 1.7304  
##                                        Mean   :  3989.88   Mean   : 2.0188  
##                                        3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                                        Max.   :130233.20   Max.   : 5.1147  
##                                        NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

```r
glimpse(homerange)
```

```
## Rows: 569
## Columns: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fishe…
## $ common.name                <chr> "american eel", "blacktail redhorse", "cent…
## $ class                      <chr> "actinopterygii", "actinopterygii", "actino…
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprini…
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae"…
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cli…
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fundu…
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recapt…
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2", …
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00,…
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600,…
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, 3…
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437,…
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home range…
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic",…
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ect…
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimmi…
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "car…
## $ dimension                  <chr> "3D", "2D", "2D", "2D", "2D", "2D", "2D", "…
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, N…
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA, …
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, NA…
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 20…
```
From summary we can learn that preymass, log10.preymass, and PPMR have NA's. From glimpse we can learn that additionally to those three, prey.size.reference, alternative.mass.reference, and N also have NA's/

**4. What are the names of the columns in the dataframe?**

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

**5. Based on the summary output, do you see anything in the data that looks strange? Think like a biologist and consider the variables.**  
Under "mass" we can see that something has a minimum of 0g which makes no sense as nothing can weigh 0g. The max mass is 4000000g which is really high. Im also skeptical of the homerange size of 3550830977m2 which seems extremely high but I guess it would depend on how they measured.

**6. The `min` and `max` functions can be used to find the minimum and maximum values in a vector. Use these functions to find the minimum and maximum values for the variable `mean.mass.g`.**  

```r
min(homerange$mean.mass.g)
```

```
## [1] 0.22
```

```r
max(homerange$mean.mass.g)
```

```
## [1] 4000000
```

**7. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
homerange$taxon <- as.factor(homerange$taxon)
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
homerange$order <- as.factor(homerange$order)
levels(homerange$order)
```

```
##  [1] "accipitriformes"       "afrosoricida"          "anguilliformes"       
##  [4] "anseriformes"          "apterygiformes"        "artiodactyla"         
##  [7] "caprimulgiformes"      "carnivora"             "charadriiformes"      
## [10] "columbidormes"         "columbiformes"         "coraciiformes"        
## [13] "cuculiformes"          "cypriniformes"         "dasyuromorpha"        
## [16] "dasyuromorpia"         "didelphimorphia"       "diprodontia"          
## [19] "diprotodontia"         "erinaceomorpha"        "esociformes"          
## [22] "falconiformes"         "gadiformes"            "galliformes"          
## [25] "gruiformes"            "lagomorpha"            "macroscelidea"        
## [28] "monotrematae"          "passeriformes"         "pelecaniformes"       
## [31] "peramelemorphia"       "perciformes"           "perissodactyla"       
## [34] "piciformes"            "pilosa"                "proboscidea"          
## [37] "psittaciformes"        "rheiformes"            "roden"                
## [40] "rodentia"              "salmoniformes"         "scorpaeniformes"      
## [43] "siluriformes"          "soricomorpha"          "squamata"             
## [46] "strigiformes"          "struthioniformes"      "syngnathiformes"      
## [49] "testudines"            "tinamiformes"          "tetraodontiformes\xa0"
```

```r
str(homerange)
```

```
## 'data.frame':	569 obs. of  24 variables:
##  $ taxon                     : Factor w/ 9 levels "birds","lake fishes",..: 2 6 6 6 6 6 5 5 5 5 ...
##  $ common.name               : chr  "american eel" "blacktail redhorse" "central stoneroller" "rosyside dace" ...
##  $ class                     : chr  "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii" ...
##  $ order                     : Factor w/ 51 levels "accipitriformes",..: 3 14 14 14 14 21 23 23 32 32 ...
##  $ family                    : chr  "anguillidae" "catostomidae" "cyprinidae" "cyprinidae" ...
##  $ genus                     : chr  "anguilla" "moxostoma" "campostoma" "clinostomus" ...
##  $ species                   : chr  "rostrata" "poecilura" "anomalum" "funduloides" ...
##  $ primarymethod             : chr  "telemetry" "mark-recapture" "mark-recapture" "mark-recapture" ...
##  $ N                         : chr  "16" NA "20" "26" ...
##  $ mean.mass.g               : num  887 562 34 4 4 ...
##  $ log10.mass                : num  2.948 2.75 1.531 0.602 0.602 ...
##  $ alternative.mass.reference: chr  NA NA NA NA ...
##  $ mean.hra.m2               : num  282750 282.1 116.1 125.5 87.1 ...
##  $ log10.hra                 : num  5.45 2.45 2.06 2.1 1.94 ...
##  $ hra.reference             : chr  "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 ...
##  $ realm                     : chr  "aquatic" "aquatic" "aquatic" "aquatic" ...
##  $ thermoregulation          : chr  "ectotherm" "ectotherm" "ectotherm" "ectotherm" ...
##  $ locomotion                : chr  "swimming" "swimming" "swimming" "swimming" ...
##  $ trophic.guild             : chr  "carnivore" "carnivore" "carnivore" "carnivore" ...
##  $ dimension                 : chr  "3D" "2D" "2D" "2D" ...
##  $ preymass                  : num  NA NA NA NA NA NA 1.39 NA NA NA ...
##  $ log10.preymass            : num  NA NA NA NA NA ...
##  $ PPMR                      : num  NA NA NA NA NA NA 530 NA NA NA ...
##  $ prey.size.reference       : chr  NA NA NA NA ...
```

**8. Use `select` to pull out the variables taxon and common.name.**  

```r
select(homerange, taxon, common.name)
```

```
##             taxon                      common.name
## 1     lake fishes                     american eel
## 2    river fishes               blacktail redhorse
## 3    river fishes              central stoneroller
## 4    river fishes                    rosyside dace
## 5    river fishes                    longnose dace
## 6    river fishes                     muskellunge 
## 7   marine fishes                          pollack
## 8   marine fishes                           saithe
## 9   marine fishes                lined surgeonfish
## 10  marine fishes          orangespine unicornfish
## 11  marine fishes            bluespine unicornfish
## 12  marine fishes                    redlip blenny
## 13  marine fishes                   giant trevally
## 14    lake fishes                        rock bass
## 15    lake fishes                     pumpkinseed 
## 16    lake fishes                        bluegill 
## 17   river fishes                  longear sunfish
## 18   river fishes                  smallmouth bass
## 19    lake fishes                  largemouth bass
## 20    lake fishes                    white crappie
## 21  marine fishes eastern triangular butterflyfish
## 22  marine fishes          Tahititan butterflyfish
## 23  marine fishes            chevron butterflyfish
## 24  marine fishes              melon butterflyfish
## 25  marine fishes           teardrop butterflyfish
## 26  marine fishes                         red moki
## 27  marine fishes              redspotted hawkfish
## 28  marine fishes                   dwarf hawkfish
## 29  marine fishes                          cabezon
## 30  marine fishes              japanese shrimpgoby
## 31  marine fishes                  bluebanded goby
## 32  marine fishes                       rusty goby
## 33  marine fishes                    blackeye goby
## 34  marine fishes                  longfinned goby
## 35  marine fishes                     bermuda chub
## 36  marine fishes                  spanish hogfish
## 37  marine fishes                  humphead wrasse
## 38  marine fishes     mediterranean rainbow wrasse
## 39  marine fishes                    slippery dick
## 40  marine fishes                yellowhead wrasse
## 41  marine fishes                     clown wrasse
## 42  marine fishes                  blackear wrasse
## 43  marine fishes        bluestreak cleaner wrasse
## 44  marine fishes                    ballan wrasse
## 45  marine fishes                     maori wrasse
## 46  marine fishes            california sheepshead
## 47  marine fishes                           cunner
## 48  marine fishes                  bluehead wrasse
## 49  marine fishes                      moon wrasse
## 50  marine fishes               thumbprint emperor
## 51  marine fishes                   mutton snapper
## 52  marine fishes             schoolmaster snapper
## 53  marine fishes                checkered snapper
## 54  marine fishes                     gray snapper
## 55  marine fishes               yellowtail snapper
## 56  marine fishes                  ocean whitefish
## 57  marine fishes                 european seabass
## 58  marine fishes                   white goatfish
## 59  marine fishes             whitesaddle goatfish
## 60    lake fishes                     yellow perch
## 61  marine fishes                    canary damsel
## 62  marine fishes                       cherubfish
## 63  marine fishes                       damselfish
## 64  marine fishes              twinspot damselfish
## 65  marine fishes              whitetail dascyllus
## 66  marine fishes                     wards damsel
## 67  marine fishes               australian gregory
## 68  marine fishes               bicolor damselfish
## 69  marine fishes                 cocoa damselfish
## 70  marine fishes             steephead parrotfish
## 71  marine fishes               striped parrotfish
## 72  marine fishes             rivulated parrotfish
## 73  marine fishes               redband parrotfish
## 74  marine fishes               redtail parrotfish
## 75  marine fishes                redfin parrotfish
## 76  marine fishes             stoplight parrotfish
## 77  marine fishes                     peacock hind
## 78  marine fishes                          graysby
## 79  marine fishes                   yellowfin hind
## 80  marine fishes                       coral hind
## 81  marine fishes                         red hind
## 82  marine fishes                    dusky grouper
## 83  marine fishes                      red grouper
## 84  marine fishes                   nassau grouper
## 85  marine fishes                   greasy grouper
## 86  marine fishes                  redbanded perch
## 87  marine fishes             half-banded seaperch
## 88  marine fishes                    black grouper
## 89  marine fishes                        kelp bass
## 90  marine fishes                 barred sand bass
## 91  marine fishes                    coral grouper
## 92  marine fishes                      coral trout
## 93  marine fishes                           comber
## 94  marine fishes                   painted comber
## 95  marine fishes                           salema
## 96  marine fishes                gilthead seabream
## 97   river fishes                  cutthroat trout
## 98   river fishes                       gila trout
## 99   river fishes                    rainbow trout
## 100  river fishes                  atlantic salmon
## 101   lake fishes                      brown trout
## 102  river fishes                  mottled sculpin
## 103  river fishes                   banded sculpin
## 104  river fishes                         sculpin 
## 105 marine fishes                  copper rockfish
## 106 marine fishes          japanese black rockfish
## 107 marine fishes               quillback rockfish
## 108 marine fishes                   black rockfish
## 109 marine fishes                    blue rockfish
## 110   lake fishes                  yellow bullhead
## 111 marine fishes            long-snouted seahorse
## 112 marine fishes                    worm pipefish
## 113 marine fishes        atlantic sharpnose puffer
## 114         birds                     golden eagle
## 115         birds                   common buzzard
## 116         birds           short-toed snake eagle
## 117         birds                  Bonelli's eagle
## 118         birds                     booted eagle
## 119         birds                 Egyptian vulture
## 120         birds                          gadwall
## 121         birds              northern brown kiwi
## 122         birds                European nightjar
## 123         birds                    oystercatcher
## 124         birds                        inca dove
## 125         birds               common wood pigeon
## 126         birds             European turtle dove
## 127         birds                  European roller
## 128         birds                           hoopoe
## 129         birds             great spotted cuckoo
## 130         birds                    common cuckoo
## 131         birds               greater roadrunner
## 132         birds             banded ground-cuckoo
## 133         birds                    Cooper's hawk
## 134         birds                 Northern goshawk
## 135         birds             Eurasian sparrowhawk
## 136         birds               sharp-shinned hawk
## 137         birds                  red-tailed hawk
## 138         birds              red-shouldered hawk
## 139         birds                  Swainson's hawk
## 140         birds                      hen harrier
## 141         birds                Montagu's harrier
## 142         birds                         red kite
## 143         birds                         caracara
## 144         birds            red-throated caracara
## 145         birds                    lanner falcon
## 146         birds                   prairie falcon
## 147         birds                 peregrine falcon
## 148         birds                 American kestrel
## 149         birds                 European kestrel
## 150         birds                     hazel grouse
## 151         birds                      sage grouse
## 152         birds                     dusky grouse
## 153         birds                 willow ptarmigan
## 154         birds                   grey partridge
## 155         birds                     black grouse
## 156         birds             western capercaillie
## 157         birds          greater prairie-chicken
## 158         birds                  brown wood rail
## 159         birds                        corncrake
## 160         birds                        king rail
## 161         birds                melodious warbler
## 162         birds                  long-tailed tit
## 163         birds                         woodlark
## 164         birds         red-throated ant tanager
## 165         birds          red-crowned ant tanager
## 166         birds             Eurasian treecreeper
## 167         birds         streaked fantail warbler
## 168         birds                     common raven
## 169         birds               spotted nutcracker
## 170         birds             Peruvian plantcutter
## 171         birds              grasshopper sparrow
## 172         birds                   indigo bunting
## 173         birds                   Abert's towhee
## 174         birds                    canyon towhee
## 175         birds            American tree sparrow
## 176         birds                 chipping sparrow
## 177         birds                    common linnet
## 178         birds                 common chaffinch
## 179         birds                   European serin
## 180         birds               eastern meadowlark
## 181         birds               western meadowlard
## 182         birds             yellow-breasted chat
## 183         birds                red-backed shrike
## 184         birds                loggerhead shrike
## 185         birds               lesser grey shrike
## 186         birds                  woodchat shrike
## 187         birds             northern mockingbird
## 188         birds                    white wagtail
## 189         birds           western yellow wagtail
## 190         birds               spotted flycatcher
## 191         birds                northern wheatear
## 192         birds                  common redstart
## 193         birds                         whinchat
## 194         birds           black-capped chickadee
## 195         birds               Carolina chickadee
## 196         birds                     Oak titmouse
## 197         birds                        marsh tit
## 198         birds                 mourning warbler
## 199         birds              common yellowthroat
## 200         birds             prothonotary warbler
## 201         birds                         ovenbird
## 202         birds             Blackburnian warbler
## 203         birds               Kirtland's warbler
## 204         birds                 magnolia warbler
## 205         birds           chestnut-sided warbler
## 206         birds          American yellow warbler
## 207         birds                American redstart
## 208         birds     black-throated green warbler
## 209         birds                   Canada warbler
## 210         birds        Western Bonelli's warbler
## 211         birds           tooth-billed bowerbird
## 212         birds                 common firecrest
## 213         birds                        goldcrest
## 214         birds                European nuthatch
## 215         birds                          wrentit
## 216         birds                Marmora's warbler
## 217         birds                 Dartford warbler
## 218         birds                   Berwick's wren
## 219         birds                    Carolina wren
## 220         birds                       house wren
## 221         birds                    Eurasian wren
## 222         birds                 eastern bluebird
## 223         birds               eastern wood pewee
## 224         birds                 least flycatcher
## 225         birds         American gray flycatcher
## 226         birds                 eastern kingbird
## 227         birds               black-capped vireo
## 228         birds                     Bell's vireo
## 229         birds                 white-eyed vireo
## 230         birds                   red-eyed vireo
## 231         birds                    great bittern
## 232         birds                    least bittern
## 233         birds                 black woodpecker
## 234         birds                 Eurasian wryneck
## 235         birds          white-backed woodpecker
## 236         birds       middle spotted woodpeckers
## 237         birds   Eurasian three-toed woodpecker
## 238         birds           grey-headed woodpecker
## 239         birds        European green woodpecker
## 240         birds                           kakapo
## 241         birds                     greater rhea
## 242         birds                      lesser rhea
## 243         birds                       boreal owl
## 244         birds                   long-eared owl
## 245         birds                       little owl
## 246         birds               Eurasian eagle-owl
## 247         birds                 great horned owl
## 248         birds               Eurasian pygmy owl
## 249         birds                        snowy owl
## 250         birds                        tawny owl
## 251         birds                         barn owl
## 252         birds                          ostrich
## 253         birds                   ornate tinamou
## 254       mammals                giant golden mole
## 255       mammals              Grant's golden mole
## 256       mammals                        pronghorn
## 257       mammals                           impala
## 258       mammals                       hartebeest
## 259       mammals                    barbary sheep
## 260       mammals                   American bison
## 261       mammals                   European bison
## 262       mammals                             goat
## 263       mammals                     Spanish ibex
## 264       mammals                   Peter's dukier
## 265       mammals                       bay dikier
## 266       mammals                 mountain gazelle
## 267       mammals             G\xfcnther's dik-dik
## 268       mammals                    mountain goat
## 269       mammals                           argali
## 270       mammals                    bighorn sheep
## 271       mammals                         steenbok
## 272       mammals                          chamois
## 273       mammals                     common eland
## 274       mammals                         bushbuck
## 275       mammals                     greater kudu
## 276       mammals                            moose
## 277       mammals                           chital
## 278       mammals                         roe deer
## 279       mammals                         red deer
## 280       mammals                        sika deer
## 281       mammals                      fallow deer
## 282       mammals                 Reeves's muntjac
## 283       mammals                        mule deer
## 284       mammals                white-tailed deer
## 285       mammals                      pampas deer
## 286       mammals                             pudu
## 287       mammals                         reindeer
## 288       mammals                          giraffe
## 289       mammals                            okapi
## 290       mammals                   desert warthog
## 291       mammals                  Chacoan peccary
## 292       mammals                 collared peccary
## 293       mammals             white-lipped peccary
## 294       mammals                 water chevrotain
## 295       mammals                        red panda
## 296       mammals                       arctic fox
## 297       mammals                   Ethiopian wolf
## 298       mammals                           culpeo
## 299       mammals          South American gray fox
## 300       mammals                          kit fox
## 301       mammals                     Ruppel's fox
## 302       mammals                        swift fox
## 303       mammals   thick-tailed three-toed jerboa
## 304       mammals                            fossa
## 305       mammals                          cheetah
## 306       mammals                          caracal
## 307       mammals                              cat
## 308       mammals                          wildcat
## 309       mammals                       jaguarundi
## 310       mammals                           ocelot
## 311       mammals                           margay
## 312       mammals                           serval
## 313       mammals                      Canada lynx
## 314       mammals                    Eurasian lynx
## 315       mammals                     Iberian lynx
## 316       mammals                           bobcat
## 317       mammals                   Geoffroy's cat
## 318       mammals                           jaguar
## 319       mammals                          leopard
## 320       mammals                            tiger
## 321       mammals                      leopard cat
## 322       mammals                           cougar
## 323       mammals                     snow leopard
## 324       mammals                   marsh mongoose
## 325       mammals                  yellow mongoose
## 326       mammals            common dwarf mongoose
## 327       mammals                Egyptian mongoose
## 328       mammals            white-tailed mongoose
## 329       mammals                         aardwolf
## 330       mammals                            tayra
## 331       mammals                   greater grison
## 332       mammals                        wolverine
## 333       mammals                  American marten
## 334       mammals                     beech marten
## 335       mammals             European pine marten
## 336       mammals                           fisher
## 337       mammals                            stoat
## 338       mammals               long-tailed weasel
## 339       mammals                           ferret
## 340       mammals                    European mink
## 341       mammals              black-footed ferret
## 342       mammals                     least weasel
## 343       mammals                  Siberian weasel
## 344       mammals                  American badger
## 345       mammals                         kinkajou
## 346       mammals                      giant panda
## 347       mammals                       sloth bear
## 348       mammals                     common genet
## 349       mammals                       cape genet
## 350       mammals               large indian civet
## 351       mammals                    Western quoll
## 352       mammals                      tiger quoll
## 353       mammals             white-footed dunnart
## 354       mammals                 brown antechinus
## 355       mammals   Northern three-striped opossum
## 356       mammals       elegant fat-tailed opossum
## 357       mammals         Lumholtz's tree-kangaroo
## 358       mammals              antilopine kangaroo
## 359       mammals            black-striped wallaby
## 360       mammals            Western grey kangaroo
## 361       mammals            Eastern grey kangaroo
## 362       mammals                  common wallaroo
## 363       mammals               red-necked wallaby
## 364       mammals                     red kangaroo
## 365       mammals              allied rock-wallaby
## 366       mammals                  eastern bettong
## 367       mammals              long-footed potoroo
## 368       mammals                   greater glider
## 369       mammals        bridled nail-tail wallaby
## 370       mammals             red-legged pademelon
## 371       mammals             red-necked pademelon
## 372       mammals                    swamp wallaby
## 373       mammals          common brushtail possum
## 374       mammals      northern hairy-nosed wombat
## 375       mammals                    common wombat
## 376       mammals                European hedgehog
## 377       mammals              long-eared hedgehog
## 378       mammals                     pygmy rabbit
## 379       mammals                    snowshoe hare
## 380       mammals                      Arctic hare
## 381       mammals          black-tailed jackrabbit
## 382       mammals                        cape hare
## 383       mammals                    European hare
## 384       mammals                      Indian hare
## 385       mammals                    mountain hare
## 386       mammals                  European rabbit
## 387       mammals                     swamp rabbit
## 388       mammals               eastern cottontail
## 389       mammals                     marsh rabbit
## 390       mammals                     plateau pika
## 391       mammals                    American pika
## 392       mammals            rufous elephant shrew
## 393       mammals         four-toed elephant shrew
## 394       mammals     golden-rumped elephant shrew
## 395       mammals            east African mole rat
## 396       mammals                 golden bandicoot
## 397       mammals         Southern brown bandicoot
## 398       mammals                            horse
## 399       mammals                 white rhinoceros
## 400       mammals                 black rhinoceros
## 401       mammals                      maned sloth
## 402       mammals                   Asian elephant
## 403       mammals            African bush elephant
## 404       mammals       southern grasshopper mouse
## 405       mammals                  mountain beaver
## 406       mammals               cape dune mole rat
## 407       mammals              Damaraland mole rat
## 408       mammals                  common mole rat
## 409       mammals                    cape mole rat
## 410       mammals                 silvery mole rat
## 411       mammals                   naked mole rat
## 412       mammals                  Patagonian mara
## 413       mammals                  plains viscacha
## 414       mammals          western red-backed vole
## 415       mammals            large-headed rice rat
## 416       mammals           Siberian brown lemming
## 417       mammals                       field vole
## 418       mammals                  California vole
## 419       mammals                     montane vole
## 420       mammals                     prairie vole
## 421       mammals                      meadow vole
## 422       mammals                    woodland vole
## 423       mammals                       water vole
## 424       mammals                     wood lemming
## 425       mammals             bushy-tailed woodrat
## 426       mammals             dusky-footed woodrat
## 427       mammals                   desert woodrat
## 428       mammals          Southern plains woodrat
## 429       mammals                          muskrat
## 430       mammals                     cotton mouse
## 431       mammals         salt marsh harvest mouse
## 432       mammals             southern bog lemming
## 433       mammals          dwarf fat-tailed jerboa
## 434       mammals               Cuvier's spiny rat
## 435       mammals                 Tome's spiny rat
## 436       mammals              Brazilian porcupine
## 437       mammals         North American porcupine
## 438       mammals            Botta's pocket gopher
## 439       mammals              spectacled dormouse
## 440       mammals                   hazel dormouse
## 441       mammals               giant kangaroo rat
## 442       mammals           Merriam's kangaroo rat
## 443       mammals               Ord's kangaroo rat
## 444       mammals       banner-tailed kangaroo rat
## 445       mammals           Stephen's kangaroo rat
## 446       mammals                   cape porcupine
## 447       mammals         Indian crested porcupine
## 448       mammals   African brush-tailed porcupine
## 449       mammals              yellow-necked mouse
## 450       mammals                       wood mouse
## 451       mammals               Indian desert jird
## 452       mammals              broad-toothed mouse
## 453       mammals               Malagasy giant rat
## 454       mammals         White-bellied\xa0nesomys
## 455       mammals                     island mouse
## 456       mammals                           coruro
## 457       mammals                Siberian chipmunk
## 458       mammals           Northern parl squirrel
## 459       mammals         Northern flying squirrel
## 460       mammals         Southern flying squirrel
## 461       mammals            yellow-bellied marmot
## 462       mammals                        groundhog
## 463       mammals                red bush squirrel
## 464       mammals                 Abert's squirrel
## 465       mammals            eastern gray squirrel
## 466       mammals                Japanese squirrel
## 467       mammals                     fox squirrel
## 468       mammals                     red squirrel
## 469       mammals       California ground squirrel
## 470       mammals        Columbian ground squirrel
## 471       mammals       Franklin's ground squirrel
## 472       mammals           arctic ground squirrel
## 473       mammals          spotted ground squirrel
## 474       mammals   thirteen-lined ground squirrel
## 475       mammals                    rock squirrel
## 476       mammals             yellow-pine chipmunk
## 477       mammals                   least chipmunk
## 478       mammals                Colorado chipmunk
## 479       mammals                   Uinta chipmunk
## 480       mammals            American red squirrel
## 481       mammals          striped ground squirrel
## 482       mammals       greater white-footed shrew
## 483       mammals                     arctic shrew
## 484       mammals                   cinereus shrew
## 485       mammals                    crowned shrew
## 486       mammals                    slender shrew
## 487       mammals                long-clawed shrew
## 488       mammals                  star-nosed mole
## 489       mammals                     eastern mole
## 490       mammals                    European mole
## 491       mammals                       Roman mole
## 492       lizards                spiny tail lizard
## 493        snakes               western worm snake
## 494        snakes               eastern worm snake
## 495        snakes                            racer
## 496        snakes             yellow bellied racer
## 497        snakes                   ringneck snake
## 498        snakes             eastern indigo snake
## 499        snakes            great plains ratsnake
## 500        snakes                 western ratsnake
## 501        snakes                    hognose snake
## 502        snakes               European whipsnake
## 503        snakes                Eastern kingsnake
## 504        snakes                        milksnake
## 505        snakes                        coachwhip
## 506        snakes                      grass snake
## 507        snakes           copperbelly watersnake
## 508        snakes              Northern watersnake
## 509        snakes               redbacked ratsnake
## 510        snakes                     gopher snake
## 511        snakes                       pine snake
## 512        snakes             butlers garter snake
## 513        snakes              giant garter snakes
## 514        snakes                Aesculapian snake
## 515        snakes                broadheaded snake
## 516        snakes                      tiger snake
## 517        snakes                       blacksnake
## 518       lizards            Galapagos land iguana
## 519       lizards           Bahamian Andros iguana
## 520       lizards                      blue iguana
## 521       lizards            Anegada ground iguana
## 522       lizards          Angel island chuckwalla
## 523       lizards                common chuckwalla
## 524       lizards                    desert iguana
## 525       lizards                  Tenerife lizard
## 526       lizards             High Mountain Lizard
## 527        snakes       southwestern carpet python
## 528       lizards                      land mullet
## 529        snakes                       copperhead
## 530        snakes                      cottonmouth
## 531        snakes              namaqua dwarf adder
## 532        snakes                     fer-de-lance
## 533        snakes              western diamondback
## 534        snakes                       sidewinder
## 535        snakes               timber rattlesnake
## 536        snakes          blacktailed rattlesnake
## 537        snakes         midget faded rattlesnake
## 538        snakes         twin-spotted rattlesnake
## 539        snakes               Mojave rattlesnake
## 540        snakes                tiger rattlesnake
## 541        snakes                chinese pit viper
## 542        snakes                   Armenian viper
## 543        snakes                  snubnosed viper
## 544       turtles       Eastern long-necked turtle
## 545       turtles      Dalh's toad-headed tortoise
## 546       turtles           common snapping turtle
## 547       turtles           midland painted turtle
## 548       turtles                   chicken turtle
## 549       turtles                Blanding's turtle
## 550       turtles             European pond turtle
## 551       turtles       yellow-blotched map turtle
## 552       turtles                ornate box turtle
## 553       turtles              Spanish pond turtle
## 554       turtles               Eastern mud turtle
## 555       turtles        stripe-necked musk turtle
## 556       turtles                  stinkpot turtle
## 557     tortoises              red-footed tortoise
## 558     tortoises                  desert tortoise
## 559     tortoises                  gopher tortoise
## 560     tortoises              travancore tortoise
## 561     tortoises    Speke's hinge-backed tortoise
## 562     tortoises               impressed tortoise
## 563     tortoises        bushmanland tent tortoise
## 564     tortoises                 leopard tortoise
## 565     tortoises            spur-thighed tortoise
## 566     tortoises           mediterranean tortoise
## 567     tortoises          Russian steppe tortoise
## 568     tortoises                Egyptian tortoise
## 569       turtles   Eastern spiny softshell turtle
```

**9. Use `filter` to pull out all mammals from the data.**

```r
filter(homerange, taxon=="mammals")
```

```
##       taxon                    common.name    class           order
## 1   mammals              giant golden mole mammalia    afrosoricida
## 2   mammals            Grant's golden mole mammalia    afrosoricida
## 3   mammals                      pronghorn mammalia    artiodactyla
## 4   mammals                         impala mammalia    artiodactyla
## 5   mammals                     hartebeest mammalia    artiodactyla
## 6   mammals                  barbary sheep mammalia    artiodactyla
## 7   mammals                 American bison mammalia    artiodactyla
## 8   mammals                 European bison mammalia    artiodactyla
## 9   mammals                           goat mammalia    artiodactyla
## 10  mammals                   Spanish ibex mammalia    artiodactyla
## 11  mammals                 Peter's dukier mammalia    artiodactyla
## 12  mammals                     bay dikier mammalia    artiodactyla
## 13  mammals               mountain gazelle mammalia    artiodactyla
## 14  mammals           G\xfcnther's dik-dik mammalia    artiodactyla
## 15  mammals                  mountain goat mammalia    artiodactyla
## 16  mammals                         argali mammalia    artiodactyla
## 17  mammals                  bighorn sheep mammalia    artiodactyla
## 18  mammals                       steenbok mammalia    artiodactyla
## 19  mammals                        chamois mammalia    artiodactyla
## 20  mammals                   common eland mammalia    artiodactyla
## 21  mammals                       bushbuck mammalia    artiodactyla
## 22  mammals                   greater kudu mammalia    artiodactyla
## 23  mammals                          moose mammalia    artiodactyla
## 24  mammals                         chital mammalia    artiodactyla
## 25  mammals                       roe deer mammalia    artiodactyla
## 26  mammals                       red deer mammalia    artiodactyla
## 27  mammals                      sika deer mammalia    artiodactyla
## 28  mammals                    fallow deer mammalia    artiodactyla
## 29  mammals               Reeves's muntjac mammalia    artiodactyla
## 30  mammals                      mule deer mammalia    artiodactyla
## 31  mammals              white-tailed deer mammalia    artiodactyla
## 32  mammals                    pampas deer mammalia    artiodactyla
## 33  mammals                           pudu mammalia    artiodactyla
## 34  mammals                       reindeer mammalia    artiodactyla
## 35  mammals                        giraffe mammalia    artiodactyla
## 36  mammals                          okapi mammalia    artiodactyla
## 37  mammals                 desert warthog mammalia    artiodactyla
## 38  mammals                Chacoan peccary mammalia    artiodactyla
## 39  mammals               collared peccary mammalia    artiodactyla
## 40  mammals           white-lipped peccary mammalia    artiodactyla
## 41  mammals               water chevrotain mammalia    artiodactyla
## 42  mammals                      red panda mammalia       carnivora
## 43  mammals                     arctic fox mammalia       carnivora
## 44  mammals                 Ethiopian wolf mammalia       carnivora
## 45  mammals                         culpeo mammalia       carnivora
## 46  mammals        South American gray fox mammalia       carnivora
## 47  mammals                        kit fox mammalia       carnivora
## 48  mammals                   Ruppel's fox mammalia       carnivora
## 49  mammals                      swift fox mammalia       carnivora
## 50  mammals thick-tailed three-toed jerboa mammalia       carnivora
## 51  mammals                          fossa mammalia       carnivora
## 52  mammals                        cheetah mammalia       carnivora
## 53  mammals                        caracal mammalia       carnivora
## 54  mammals                            cat mammalia       carnivora
## 55  mammals                        wildcat mammalia       carnivora
## 56  mammals                     jaguarundi mammalia       carnivora
## 57  mammals                         ocelot mammalia       carnivora
## 58  mammals                         margay mammalia       carnivora
## 59  mammals                         serval mammalia       carnivora
## 60  mammals                    Canada lynx mammalia       carnivora
## 61  mammals                  Eurasian lynx mammalia       carnivora
## 62  mammals                   Iberian lynx mammalia       carnivora
## 63  mammals                         bobcat mammalia       carnivora
## 64  mammals                 Geoffroy's cat mammalia       carnivora
## 65  mammals                         jaguar mammalia       carnivora
## 66  mammals                        leopard mammalia       carnivora
## 67  mammals                          tiger mammalia       carnivora
## 68  mammals                    leopard cat mammalia       carnivora
## 69  mammals                         cougar mammalia       carnivora
## 70  mammals                   snow leopard mammalia       carnivora
## 71  mammals                 marsh mongoose mammalia       carnivora
## 72  mammals                yellow mongoose mammalia       carnivora
## 73  mammals          common dwarf mongoose mammalia       carnivora
## 74  mammals              Egyptian mongoose mammalia       carnivora
## 75  mammals          white-tailed mongoose mammalia       carnivora
## 76  mammals                       aardwolf mammalia       carnivora
## 77  mammals                          tayra mammalia       carnivora
## 78  mammals                 greater grison mammalia       carnivora
## 79  mammals                      wolverine mammalia       carnivora
## 80  mammals                American marten mammalia       carnivora
## 81  mammals                   beech marten mammalia       carnivora
## 82  mammals           European pine marten mammalia       carnivora
## 83  mammals                         fisher mammalia       carnivora
## 84  mammals                          stoat mammalia       carnivora
## 85  mammals             long-tailed weasel mammalia       carnivora
## 86  mammals                         ferret mammalia       carnivora
## 87  mammals                  European mink mammalia       carnivora
## 88  mammals            black-footed ferret mammalia       carnivora
## 89  mammals                   least weasel mammalia       carnivora
## 90  mammals                Siberian weasel mammalia       carnivora
## 91  mammals                American badger mammalia       carnivora
## 92  mammals                       kinkajou mammalia       carnivora
## 93  mammals                    giant panda mammalia       carnivora
## 94  mammals                     sloth bear mammalia       carnivora
## 95  mammals                   common genet mammalia       carnivora
## 96  mammals                     cape genet mammalia       carnivora
## 97  mammals             large indian civet mammalia       carnivora
## 98  mammals                  Western quoll mammalia   dasyuromorpha
## 99  mammals                    tiger quoll mammalia   dasyuromorpha
## 100 mammals           white-footed dunnart mammalia   dasyuromorpha
## 101 mammals               brown antechinus mammalia   dasyuromorpia
## 102 mammals Northern three-striped opossum mammalia didelphimorphia
## 103 mammals     elegant fat-tailed opossum mammalia didelphimorphia
## 104 mammals       Lumholtz's tree-kangaroo mammalia     diprodontia
## 105 mammals            antilopine kangaroo mammalia     diprodontia
## 106 mammals          black-striped wallaby mammalia     diprodontia
## 107 mammals          Western grey kangaroo mammalia     diprodontia
## 108 mammals          Eastern grey kangaroo mammalia     diprodontia
## 109 mammals                common wallaroo mammalia     diprodontia
## 110 mammals             red-necked wallaby mammalia     diprodontia
## 111 mammals                   red kangaroo mammalia     diprodontia
## 112 mammals            allied rock-wallaby mammalia     diprodontia
## 113 mammals                eastern bettong mammalia     diprodontia
## 114 mammals            long-footed potoroo mammalia     diprodontia
## 115 mammals                 greater glider mammalia     diprodontia
## 116 mammals      bridled nail-tail wallaby mammalia   diprotodontia
## 117 mammals           red-legged pademelon mammalia   diprotodontia
## 118 mammals           red-necked pademelon mammalia   diprotodontia
## 119 mammals                  swamp wallaby mammalia   diprotodontia
## 120 mammals        common brushtail possum mammalia   diprotodontia
## 121 mammals    northern hairy-nosed wombat mammalia   diprotodontia
## 122 mammals                  common wombat mammalia   diprotodontia
## 123 mammals              European hedgehog mammalia  erinaceomorpha
## 124 mammals            long-eared hedgehog mammalia  erinaceomorpha
## 125 mammals                   pygmy rabbit mammalia      lagomorpha
## 126 mammals                  snowshoe hare mammalia      lagomorpha
## 127 mammals                    Arctic hare mammalia      lagomorpha
## 128 mammals        black-tailed jackrabbit mammalia      lagomorpha
## 129 mammals                      cape hare mammalia      lagomorpha
## 130 mammals                  European hare mammalia      lagomorpha
## 131 mammals                    Indian hare mammalia      lagomorpha
## 132 mammals                  mountain hare mammalia      lagomorpha
## 133 mammals                European rabbit mammalia      lagomorpha
## 134 mammals                   swamp rabbit mammalia      lagomorpha
## 135 mammals             eastern cottontail mammalia      lagomorpha
## 136 mammals                   marsh rabbit mammalia      lagomorpha
## 137 mammals                   plateau pika mammalia      lagomorpha
## 138 mammals                  American pika mammalia      lagomorpha
## 139 mammals          rufous elephant shrew mammalia   macroscelidea
## 140 mammals       four-toed elephant shrew mammalia   macroscelidea
## 141 mammals   golden-rumped elephant shrew mammalia   macroscelidea
## 142 mammals          east African mole rat mammalia    monotrematae
## 143 mammals               golden bandicoot mammalia peramelemorphia
## 144 mammals       Southern brown bandicoot mammalia peramelemorphia
## 145 mammals                          horse mammalia  perissodactyla
## 146 mammals               white rhinoceros mammalia  perissodactyla
## 147 mammals               black rhinoceros mammalia  perissodactyla
## 148 mammals                    maned sloth mammalia          pilosa
## 149 mammals                 Asian elephant mammalia     proboscidea
## 150 mammals          African bush elephant mammalia     proboscidea
## 151 mammals     southern grasshopper mouse mammalia           roden
## 152 mammals                mountain beaver mammalia        rodentia
## 153 mammals             cape dune mole rat mammalia        rodentia
## 154 mammals            Damaraland mole rat mammalia        rodentia
## 155 mammals                common mole rat mammalia        rodentia
## 156 mammals                  cape mole rat mammalia        rodentia
## 157 mammals               silvery mole rat mammalia        rodentia
## 158 mammals                 naked mole rat mammalia        rodentia
## 159 mammals                Patagonian mara mammalia        rodentia
## 160 mammals                plains viscacha mammalia        rodentia
## 161 mammals        western red-backed vole mammalia        rodentia
## 162 mammals          large-headed rice rat mammalia        rodentia
## 163 mammals         Siberian brown lemming mammalia        rodentia
## 164 mammals                     field vole mammalia        rodentia
## 165 mammals                California vole mammalia        rodentia
## 166 mammals                   montane vole mammalia        rodentia
## 167 mammals                   prairie vole mammalia        rodentia
## 168 mammals                    meadow vole mammalia        rodentia
## 169 mammals                  woodland vole mammalia        rodentia
## 170 mammals                     water vole mammalia        rodentia
## 171 mammals                   wood lemming mammalia        rodentia
## 172 mammals           bushy-tailed woodrat mammalia        rodentia
## 173 mammals           dusky-footed woodrat mammalia        rodentia
## 174 mammals                 desert woodrat mammalia        rodentia
## 175 mammals        Southern plains woodrat mammalia        rodentia
## 176 mammals                        muskrat mammalia        rodentia
## 177 mammals                   cotton mouse mammalia        rodentia
## 178 mammals       salt marsh harvest mouse mammalia        rodentia
## 179 mammals           southern bog lemming mammalia        rodentia
## 180 mammals        dwarf fat-tailed jerboa mammalia        rodentia
## 181 mammals             Cuvier's spiny rat mammalia        rodentia
## 182 mammals               Tome's spiny rat mammalia        rodentia
## 183 mammals            Brazilian porcupine mammalia        rodentia
## 184 mammals       North American porcupine mammalia        rodentia
## 185 mammals          Botta's pocket gopher mammalia        rodentia
## 186 mammals            spectacled dormouse mammalia        rodentia
## 187 mammals                 hazel dormouse mammalia        rodentia
## 188 mammals             giant kangaroo rat mammalia        rodentia
## 189 mammals         Merriam's kangaroo rat mammalia        rodentia
## 190 mammals             Ord's kangaroo rat mammalia        rodentia
## 191 mammals     banner-tailed kangaroo rat mammalia        rodentia
## 192 mammals         Stephen's kangaroo rat mammalia        rodentia
## 193 mammals                 cape porcupine mammalia        rodentia
## 194 mammals       Indian crested porcupine mammalia        rodentia
## 195 mammals African brush-tailed porcupine mammalia        rodentia
## 196 mammals            yellow-necked mouse mammalia        rodentia
## 197 mammals                     wood mouse mammalia        rodentia
## 198 mammals             Indian desert jird mammalia        rodentia
## 199 mammals            broad-toothed mouse mammalia        rodentia
## 200 mammals             Malagasy giant rat mammalia        rodentia
## 201 mammals       White-bellied\xa0nesomys mammalia        rodentia
## 202 mammals                   island mouse mammalia        rodentia
## 203 mammals                         coruro mammalia        rodentia
## 204 mammals              Siberian chipmunk mammalia        rodentia
## 205 mammals         Northern parl squirrel mammalia        rodentia
## 206 mammals       Northern flying squirrel mammalia        rodentia
## 207 mammals       Southern flying squirrel mammalia        rodentia
## 208 mammals          yellow-bellied marmot mammalia        rodentia
## 209 mammals                      groundhog mammalia        rodentia
## 210 mammals              red bush squirrel mammalia        rodentia
## 211 mammals               Abert's squirrel mammalia        rodentia
## 212 mammals          eastern gray squirrel mammalia        rodentia
## 213 mammals              Japanese squirrel mammalia        rodentia
## 214 mammals                   fox squirrel mammalia        rodentia
## 215 mammals                   red squirrel mammalia        rodentia
## 216 mammals     California ground squirrel mammalia        rodentia
## 217 mammals      Columbian ground squirrel mammalia        rodentia
## 218 mammals     Franklin's ground squirrel mammalia        rodentia
## 219 mammals         arctic ground squirrel mammalia        rodentia
## 220 mammals        spotted ground squirrel mammalia        rodentia
## 221 mammals thirteen-lined ground squirrel mammalia        rodentia
## 222 mammals                  rock squirrel mammalia        rodentia
## 223 mammals           yellow-pine chipmunk mammalia        rodentia
## 224 mammals                 least chipmunk mammalia        rodentia
## 225 mammals              Colorado chipmunk mammalia        rodentia
## 226 mammals                 Uinta chipmunk mammalia        rodentia
## 227 mammals          American red squirrel mammalia        rodentia
## 228 mammals        striped ground squirrel mammalia        rodentia
## 229 mammals     greater white-footed shrew mammalia    soricomorpha
## 230 mammals                   arctic shrew mammalia    soricomorpha
## 231 mammals                 cinereus shrew mammalia    soricomorpha
## 232 mammals                  crowned shrew mammalia    soricomorpha
## 233 mammals                  slender shrew mammalia    soricomorpha
## 234 mammals              long-clawed shrew mammalia    soricomorpha
## 235 mammals                star-nosed mole mammalia    soricomorpha
## 236 mammals                   eastern mole mammalia    soricomorpha
## 237 mammals                  European mole mammalia    soricomorpha
## 238 mammals                     Roman mole mammalia    soricomorpha
##              family           genus          species primarymethod    N
## 1   chrysochloridae    chrysospalax       trevelyani    telemetry* <NA>
## 2   chrysochloridae      eremitalpa           granti    telemetry* <NA>
## 3    antilocapridae     antilocapra        americana    telemetry* <NA>
## 4           bovidae       aepyceros         melampus    telemetry* <NA>
## 5           bovidae      alcelaphus       buselaphus    telemetry* <NA>
## 6           bovidae      ammotragus           lervia    telemetry* <NA>
## 7           bovidae           bison            bison    telemetry* <NA>
## 8           bovidae           bison          bonasus    telemetry* <NA>
## 9           bovidae           capra           hircus    telemetry* <NA>
## 10          bovidae           capra        pyrenaica    telemetry* <NA>
## 11          bovidae     cephalophus       callipygus    telemetry* <NA>
## 12          bovidae     cephalophus         dorsalis    telemetry* <NA>
## 13          bovidae         gazella          gazella    telemetry* <NA>
## 14          bovidae         madoqua        guentheri    telemetry* <NA>
## 15          bovidae        oreamnos       americanus    telemetry* <NA>
## 16          bovidae            ovis            ammon    telemetry* <NA>
## 17          bovidae            ovis       canadensis    telemetry* <NA>
## 18          bovidae      raphicerus       campestris    telemetry* <NA>
## 19          bovidae       rupicapra        rupicapra    telemetry* <NA>
## 20          bovidae     taurotragus             oryx    telemetry* <NA>
## 21          bovidae     tragelaphus         scriptus    telemetry* <NA>
## 22          bovidae     tragelaphus     strepsiceros    telemetry* <NA>
## 23         cervidae           alces            alces    telemetry* <NA>
## 24         cervidae            axis             axis    telemetry* <NA>
## 25         cervidae       capreolus        capreolus    telemetry* <NA>
## 26         cervidae          cervus          elaphus    telemetry* <NA>
## 27         cervidae          cervus           nippon    telemetry* <NA>
## 28         cervidae            dama             dama    telemetry* <NA>
## 29         cervidae       muntiacus          reevesi    telemetry* <NA>
## 30         cervidae      odocoileus         hemionus    telemetry* <NA>
## 31         cervidae      odocoileus      virginianus    telemetry* <NA>
## 32         cervidae      ozotoceros      bezoarticus    telemetry* <NA>
## 33         cervidae            pudu             puda    telemetry* <NA>
## 34         cervidae        rangifer         tarandus    telemetry* <NA>
## 35       giraffidae         giraffa   camelopardalis    telemetry* <NA>
## 36       giraffidae          okapia        johnstoni    telemetry* <NA>
## 37           suidae    phacochoerus      aethiopicus    telemetry* <NA>
## 38      tayassuidae       catagonus          wagneri    telemetry* <NA>
## 39      tayassuidae          pecari           tajacu    telemetry* <NA>
## 40      tayassuidae         tayassu           pecari    telemetry* <NA>
## 41       tragulidae      hyemoschus        aquaticus    telemetry* <NA>
## 42        ailuridae         ailurus          fulgens    telemetry* <NA>
## 43          canidae          alopex          lagopus    telemetry* <NA>
## 44          canidae           canis         simensis    telemetry* <NA>
## 45          canidae     pseudalopex         culpaeus    telemetry* <NA>
## 46          canidae     pseudalopex          griseus    telemetry* <NA>
## 47          canidae          vulpes          macroti    telemetry* <NA>
## 48          canidae          vulpes         ruppelli    telemetry* <NA>
## 49          canidae          vulpes            velox    telemetry* <NA>
## 50        dipodidae      stylodipus            telum    telemetry* <NA>
## 51       eupleridae    cryptoprocta            ferox    telemetry* <NA>
## 52          felidae        acinonyx          jubatus    telemetry* <NA>
## 53          felidae         caracal          caracal    telemetry* <NA>
## 54          felidae           felis            catus    telemetry* <NA>
## 55          felidae           felis       sylvestris    telemetry* <NA>
## 56          felidae     herpailurus     yagouaroundi    telemetry* <NA>
## 57          felidae       leopardus         pardalis    telemetry* <NA>
## 58          felidae       leopardus           wiedii    telemetry* <NA>
## 59          felidae     leptailurus           serval    telemetry* <NA>
## 60          felidae            lynx       canadensis    telemetry* <NA>
## 61          felidae            lynx             lynx    telemetry* <NA>
## 62          felidae            lynx         pardinus    telemetry* <NA>
## 63          felidae            lynx            rufus    telemetry* <NA>
## 64          felidae       oncifelis        geoffroyi    telemetry* <NA>
## 65          felidae        panthera             onca    telemetry* <NA>
## 66          felidae        panthera           pardus    telemetry* <NA>
## 67          felidae        panthera           tigris    telemetry* <NA>
## 68          felidae    prionailurus      bengalensis    telemetry* <NA>
## 69          felidae            puma         concolor    telemetry* <NA>
## 70          felidae           uncia            uncia    telemetry* <NA>
## 71      herpestidae          atilax      paludinosus    telemetry* <NA>
## 72      herpestidae        cynictis      penicillata    telemetry* <NA>
## 73      herpestidae        helogale          parvula            \\ <NA>
## 74      herpestidae       herpestes       inchneumon     telemetry   20
## 75      herpestidae       ichneumia        albicauda    telemetry* <NA>
## 76         hyanidae        proteles        cristatus    telemetry* <NA>
## 77       mustelidae            eira          barbata    telemetry* <NA>
## 78       mustelidae        galictis          vittata    telemetry* <NA>
## 79       mustelidae            gulo             gulo    telemetry* <NA>
## 80       mustelidae          martes        americana    telemetry* <NA>
## 81       mustelidae          martes            foina    telemetry* <NA>
## 82       mustelidae          martes           martes    telemetry* <NA>
## 83       mustelidae          martes         pennanti    telemetry* <NA>
## 84       mustelidae         mustela          erminea    telemetry* <NA>
## 85       mustelidae         mustela          frenata    telemetry* <NA>
## 86       mustelidae         mustela             furo    telemetry* <NA>
## 87       mustelidae         mustela         lutreola    telemetry* <NA>
## 88       mustelidae         mustela         nigripes    telemetry* <NA>
## 89       mustelidae         mustela          nivalis    telemetry* <NA>
## 90       mustelidae         mustela         sibirica    telemetry* <NA>
## 91       mustelidae         taxidea            taxus    telemetry* <NA>
## 92      procyonidae           potos           flavus    telemetry* <NA>
## 93          ursidae      ailuropoda      melanoleuca    telemetry* <NA>
## 94          ursidae        melursus          ursinus    telemetry* <NA>
## 95       viverridae         genetta          genetta    telemetry* <NA>
## 96       viverridae         genetta          tigrina    telemetry* <NA>
## 97       viverridae         viverra          zibetha    telemetry* <NA>
## 98       dasyuridae        dasyurus        geoffroii    telemetry* <NA>
## 99       dasyuridae        dasyurus        maculatus     telemetry   19
## 100      dasyuridae     sminthopsis         leucopus    telemetry* <NA>
## 101      dasyuridae      antechinus         stuartii    telemetry* <NA>
## 102     didelphidae     monodelphis        americana    telemetry* <NA>
## 103     didelphidae        thylamys          elegans    telemetry* <NA>
## 104    macropodidae     dendrolagus        lumholtzi    telemetry* <NA>
## 105    macropodidae        macropus      antilopinus    telemetry* <NA>
## 106    macropodidae        macropus         dorsalis    telemetry* <NA>
## 107    macropodidae        macropus      fuliginosus    telemetry* <NA>
## 108    macropodidae        macropus        giganteus    telemetry* <NA>
## 109    macropodidae        macropus         robustus    telemetry* <NA>
## 110    macropodidae        macropus      rufogriseus    telemetry* <NA>
## 111    macropodidae        macropus            rufus    telemetry* <NA>
## 112    macropodidae       petrogale        assimilis    telemetry* <NA>
## 113      potoroidae       bettongia         gaimardi    telemetry* <NA>
## 114      potoroidae        potorous         longipes    telemetry* <NA>
## 115 pseudocheiridae     petauroides           volans    telemetry* <NA>
## 116    macropodidae     onychogalea         fraenata    telemetry* <NA>
## 117    macropodidae       thylogale       stigmatica    telemetry* <NA>
## 118    macropodidae       thylogale           thetis    telemetry* <NA>
## 119    macropodidae        wallabia          bicolor    telemetry* <NA>
## 120   phalangeridae     trichosurus        vulpecula    telemetry* <NA>
## 121      vombatidae     lasiorhinus         krefftii    telemetry* <NA>
## 122      vombatidae        vombatus          ursinus    telemetry* <NA>
## 123     erinaceidae       erinaceus        europaeus    telemetry* <NA>
## 124     erinaceidae     hemiechinus          auritus    telemetry* <NA>
## 125       leporidae     brachylagus       idahoensis    telemetry* <NA>
## 126       leporidae           lepus       americanus    telemetry* <NA>
## 127       leporidae           lepus         arcticus    telemetry* <NA>
## 128       leporidae           lepus     californicus    telemetry* <NA>
## 129       leporidae           lepus         capensis    telemetry* <NA>
## 130       leporidae           lepus        europaeus    telemetry* <NA>
## 131       leporidae           lepus      nigricollis    telemetry* <NA>
## 132       leporidae           lepus          timidus    telemetry* <NA>
## 133       leporidae     oryctolagus        cuniculus    telemetry* <NA>
## 134       leporidae      sylvilagus        aquaticus    telemetry* <NA>
## 135       leporidae      sylvilagus       floridanus    telemetry* <NA>
## 136       leporidae      sylvilagus        palustris    telemetry* <NA>
## 137     ochotonidae        ochotona        curzoniae    telemetry* <NA>
## 138     ochotonidae        ochotona         princeps    telemetry* <NA>
## 139 macroscelididae    elephantulus        rufescens    telemetry* <NA>
## 140 macroscelididae     petrodromus    tetradactylus    telemetry* <NA>
## 141 macroscelididae     rhynchocyon      chrysopygus    telemetry* <NA>
## 142  tachyglossidae    tachyoryctes        splendens    telemetry* <NA>
## 143     peramelidae         isoodon          auratus    telemetry* <NA>
## 144     peramelidae         isoodon         obesulus    telemetry* <NA>
## 145         equidae           equus         caballus    telemetry* <NA>
## 146  rhinocerotidae   ceratotherium            simum    telemetry* <NA>
## 147  rhinocerotidae         diceros         bicornis    telemetry* <NA>
## 148    bradypodidae        bradypus        torquatus    telemetry* <NA>
## 149    elephantidae         elephas          maximus    telemetry* <NA>
## 150    elephantidae       loxodonta         africana    telemetry* <NA>
## 151      cricetidae       onychomys         torridus    telemetry* <NA>
## 152   aplodontiidae      aplodontia             rufa    telemetry* <NA>
## 153    bathyergidae      bathyergus          suillus    telemetry* <NA>
## 154    bathyergidae       cryptomys       damarensis    telemetry* <NA>
## 155    bathyergidae       cryptomys      hottentotus    telemetry* <NA>
## 156    bathyergidae       georychus         capensis    telemetry* <NA>
## 157    bathyergidae    heliophobius argenteocinereus    telemetry* <NA>
## 158    bathyergidae  heterocephalus           glaber    telemetry* <NA>
## 159        caviidae      dolichotus        patagonus    telemetry* <NA>
## 160   chinchillidae      lagostomus          maximus    telemetry* <NA>
## 161      cricetidae   clethrionomys     californicus    telemetry* <NA>
## 162      cricetidae       hylaeamys     megacephalus    telemetry* <NA>
## 163      cricetidae          lemmus        sibiricus    telemetry* <NA>
## 164      cricetidae        microtus         agrestis    telemetry* <NA>
## 165      cricetidae        microtus     californicus    telemetry* <NA>
## 166      cricetidae        microtus         montanus    telemetry* <NA>
## 167      cricetidae        microtus      ochrogaster    telemetry* <NA>
## 168      cricetidae        microtus   pennsylvanicus    telemetry* <NA>
## 169      cricetidae        microtus        pinetorum    telemetry* <NA>
## 170      cricetidae        microtus      richardsoni    telemetry* <NA>
## 171      cricetidae          myopus     schisticolor    telemetry* <NA>
## 172      cricetidae         neotoma          cinerea    telemetry* <NA>
## 173      cricetidae         neotoma         fuscipes    telemetry* <NA>
## 174      cricetidae         neotoma           lepida    telemetry* <NA>
## 175      cricetidae         neotoma         micropus    telemetry* <NA>
## 176      cricetidae         ondatra        zibethica    telemetry* <NA>
## 177      cricetidae      peromyscus       gossypinus    telemetry* <NA>
## 178      cricetidae reithrodontomys      raviventris    telemetry* <NA>
## 179      cricetidae      synaptomys          cooperi    telemetry* <NA>
## 180       dipodidae      pygeretmus          pumilio    telemetry* <NA>
## 181      echimyidae      proechimys          cuvieri    telemetry* <NA>
## 182      echimyidae      proechimys     semispinosus    telemetry* <NA>
## 183  erethizontidae         coendou      prehensilis    telemetry* <NA>
## 184  erethizontidae       erethizon         dorsatum    telemetry* <NA>
## 185       geomyidae        thomomys           bottae    telemetry* <NA>
## 186        gliridae      graphiurus         ocularis    telemetry* <NA>
## 187        gliridae     muscardinus     avellanarius    telemetry* <NA>
## 188    heteromyidae       dipodomys           ingens    telemetry* <NA>
## 189    heteromyidae       dipodomys         merriami    telemetry* <NA>
## 190    heteromyidae       dipodomys            ordii    telemetry* <NA>
## 191    heteromyidae       dipodomys      spectabilis    telemetry* <NA>
## 192    heteromyidae       dipodomys        stephensi    telemetry* <NA>
## 193     hystricidae         hystrix africaeaustralis    telemetry* <NA>
## 194     hystricidae         hystrix           indica    telemetry* <NA>
## 195     hystridicae       atherurus        africanus    telemetry* <NA>
## 196         muridae        apodemus      flavicollis    telemetry* <NA>
## 197         muridae        apodemus       sylvaticus    telemetry* <NA>
## 198         muridae        meriones        hurrianae    telemetry* <NA>
## 199         muridae       pseudomys           fuscus    telemetry* <NA>
## 200      nesomyidae      hypogeomys         antimena    telemetry* <NA>
## 201      nesomyidae         nesomys        audeberti    telemetry* <NA>
## 202      nesomyidae         nesomys            rufus    telemetry* <NA>
## 203    octodontidae      spalacopus           cyanus    telemetry* <NA>
## 204       sciuridae        eutamias        sibiricus    telemetry* <NA>
## 205       sciuridae      funambulus         pennanti    telemetry* <NA>
## 206       sciuridae       glaucomys         sabrinus    telemetry* <NA>
## 207       sciuridae       glaucomys           volans    telemetry* <NA>
## 208       sciuridae         marmota     flaviventris    telemetry* <NA>
## 209       sciuridae         marmota            monax    telemetry* <NA>
## 210       sciuridae       paraxerus        palliatus    telemetry* <NA>
## 211       sciuridae         sciurus           aberti    telemetry* <NA>
## 212       sciuridae         sciurus     carolinensis    telemetry* <NA>
## 213       sciuridae         sciurus              lis    telemetry* <NA>
## 214       sciuridae         sciurus            niger    telemetry* <NA>
## 215       sciuridae         sciurus         vulgaris     telemetry <NA>
## 216       sciuridae    spermophilus         beecheyi    telemetry* <NA>
## 217       sciuridae    spermophilus      columbianus    telemetry* <NA>
## 218       sciuridae    spermophilus       franklinii    telemetry* <NA>
## 219       sciuridae    spermophilus          parryii    telemetry* <NA>
## 220       sciuridae    spermophilus        spilosoma    telemetry* <NA>
## 221       sciuridae    spermophilus tridecemlineatus    telemetry* <NA>
## 222       sciuridae    spermophilus       variegatus    telemetry* <NA>
## 223       sciuridae          tamias          amoenus    telemetry* <NA>
## 224       sciuridae          tamias          minimus    telemetry* <NA>
## 225       sciuridae          tamias   quadrivittatus    telemetry* <NA>
## 226       sciuridae          tamias         umbrinus    telemetry* <NA>
## 227       sciuridae    tamiasciurus       hudsonicus    telemetry* <NA>
## 228       sciuridae           xerus       erythropus    telemetry* <NA>
## 229       soricidae       crocidura          russula    telemetry* <NA>
## 230       soricidae           sorex         arcticus    telemetry* <NA>
## 231       soricidae           sorex         cinereus    telemetry* <NA>
## 232       soricidae           sorex        coronatus    telemetry* <NA>
## 233       soricidae           sorex      gracillimus    telemetry* <NA>
## 234       soricidae           sorex     unguiculatus    telemetry* <NA>
## 235        talpidae       condylura         cristata    telemetry* <NA>
## 236        talpidae        scalopus        aquaticus    telemetry* <NA>
## 237        talpidae           talpa         europaea    telemetry* <NA>
## 238        talpidae           talpa           romana    telemetry* <NA>
##     mean.mass.g log10.mass alternative.mass.reference   mean.hra.m2 log10.hra
## 1        436.52  2.6400041                       <NA>        616.60  2.790004
## 2         23.00  1.3617278                       <NA>      46299.89  4.665580
## 3      46099.90  4.6637000                       <NA>   10125348.97  7.005410
## 4      63503.84  4.8028000                       <NA>    3224482.32  6.508460
## 5     136000.34  5.1335400                       <NA>    2176857.50  6.337830
## 6     167498.14  5.2240100                       <NA>    9050029.61  6.956650
## 7     629999.20  5.7993400                       <NA>  265778594.20  8.424520
## 8     628000.52  5.7979600                       <NA>   10140514.72  7.006060
## 9      50999.98  4.7075700                       <NA>   64528266.75  7.809750
## 10     69499.23  4.8419800                       <NA>     700003.16  5.845100
## 11     18143.87  4.2587299                       <NA>     416169.26  5.619270
## 12     20411.74  4.3098800                       <NA>     357001.47  5.552670
## 13     21474.84  4.3319299                       <NA>    1872837.08  6.272500
## 14      4600.02  3.6627597                       <NA>      27333.17  4.436690
## 15    629999.20  5.7993400                       <NA>   23285737.64  7.367090
## 16    113998.73  5.0569000                       <NA>    5882473.78  6.769560
## 17     90719.36  4.9577000                       <NA>   27544823.89  7.440040
## 18     11300.04  4.0530800                       <NA>     619997.59  5.792390
## 19     30999.88  4.4913600                       <NA>    3408003.25  6.532500
## 20    635038.42  5.8028000                       <NA>   52399844.72  7.719330
## 21     54431.46  4.7358500                       <NA>      37109.06  4.569480
## 22    197314.95  5.2951600                       <NA> 1070039969.00  9.029400
## 23    307227.44  5.4874600                       <NA>   93825308.27  7.972320
## 24     62823.19  4.7981200                       <NA>    3647707.45  6.562020
## 25     24050.27  4.3811200                       <NA>     674636.76  5.829070
## 26    234757.78  5.3706200                       <NA>   74865201.87  7.874280
## 27     29450.32  4.4690900                       <NA>     851490.88  5.930180
## 28     71449.63  4.8540000                       <NA>     985008.55  5.993440
## 29     13499.88  4.1303299                       <NA>     162054.09  5.209660
## 30     53864.17  4.7313000                       <NA>   35072764.57  7.544970
## 31     87884.04  4.9439100                       <NA>    2488341.60  6.395910
## 32     35000.16  4.5440700                       <NA>    7900052.91  6.897630
## 33      7499.98  3.8750601                       <NA>     197665.10  5.295930
## 34    102058.69  5.0088500                       <NA> 3550830977.00  9.550330
## 35   1339985.19  6.1271000                       <NA>  136536888.00  8.135250
## 36    230001.15  5.3617300                       <NA>    5899972.67  6.770850
## 37     80513.74  4.9058700                       <NA>    1742007.42  6.241050
## 38     34700.04  4.5403300                       <NA>   10979940.84  7.040600
## 39     23205.98  4.3655999                       <NA>    2486222.54  6.395540
## 40     20250.23  4.3064300                       <NA>   14599904.00  7.164350
## 41     10850.01  4.0354301                       <NA>     191999.46  5.283300
## 42      5399.95  3.7323897                       <NA>    1024990.88  6.010720
## 43      4989.53  3.6980596                       <NA>   28499024.85  7.454830
## 44     27749.81  4.4432600                       <NA>    5393739.90  6.731890
## 45      7370.04  3.8674698                       <NA>    4928672.94  6.692730
## 46      3989.97  3.6009696                       <NA>    2000000.02  6.301030
## 47      4499.97  3.6532096                       <NA>    8772835.78  6.943140
## 48      3249.97  3.5118794                       <NA>   30399749.15  7.482870
## 49      2089.30  3.3200008                       <NA>    5495408.74  6.740000
## 50        60.00  1.7781513                       <NA>       4487.04  3.651960
## 51      9549.93  3.9800002                       <NA>     891250.94  5.950000
## 52     50000.00  4.6989700                       <NA>  815060787.90  8.911190
## 53     12999.90  4.1139400                       <NA>  376634414.00  8.575920
## 54      3394.53  3.5307797                       <NA>    1472448.11  6.168040
## 55      4825.03  3.6835000                       <NA>    2794988.34  6.446380
## 56      6803.93  3.8327598                       <NA>   67079528.30  7.826590
## 57      9989.64  3.9995498                       <NA>    6849360.11  6.835650
## 58      3628.77  3.5597594                       <NA>   10949896.14  7.039410
## 59     11999.97  4.0791802                       <NA>    2390011.55  6.378400
## 60     10205.87  4.0088500                       <NA>   82748475.24  7.917760
## 61     29999.91  4.4771200                       <NA>  181042275.70  8.257780
## 62     11049.94  4.0433599                       <NA>    9499921.14  6.977720
## 63     11339.92  4.0546100                       <NA>   39877690.65  7.600730
## 64      3589.96  3.5550896                       <NA>    7126724.98  6.852890
## 65     84040.77  4.9244900                       <NA>   82735138.83  7.917690
## 66     48374.89  4.6846200                       <NA>  504940260.80  8.703240
## 67    112000.51  5.0492200                       <NA>   53583367.03  7.729030
## 68      2500.00  3.3979400                       <NA>    2406855.40  6.381450
## 69     89999.48  4.9542400                       <NA>  312003883.70  8.494160
## 70     30500.01  4.4843000                       <NA>   17353217.10  7.239380
## 71      3599.98  3.5563001                       <NA>    2219984.80  6.346350
## 72       620.00  2.7923917                       <NA>     592570.46  5.772740
## 73       281.84  2.4500026                       <NA>     281838.29  5.450000
## 74      2810.00  3.4487063                       <NA>    3100000.00  6.491362
## 75      3599.98  3.5563001                       <NA>     387266.56  5.588010
## 76     10000.00  4.0000000                       <NA>    3799968.53  6.579780
## 77      4466.22  3.6499401                       <NA>   14617395.58  7.164870
## 78      1750.01  3.2430405                       <NA>    4150018.19  6.618050
## 79     21545.67  4.3333600                       <NA>  361917847.30  8.558610
## 80       883.49  2.9462016                       <NA>    7066103.59  6.849180
## 81      1799.99  3.2552701                       <NA>    4356522.89  6.639140
## 82      2475.03  3.3935805                       <NA>    9093477.57  6.958730
## 83      3175.19  3.5017697                       <NA>   16755600.61  7.224160
## 84       270.54  2.4322315                       <NA>    1323244.20  6.121640
## 85       150.19  2.1766410                       <NA>     176750.24  5.247360
## 86       808.74  2.9078089                       <NA>     899994.80  5.954240
## 87       562.34  2.7499990                       <NA>     208929.61  5.320000
## 88       912.01  2.9599996                       <NA>    1000000.00  6.000000
## 89        88.10  1.9449759                       <NA>     648858.50  5.812150
## 90       524.81  2.7200021                       <NA>    4073802.78  6.610000
## 91      8618.27  3.9354201                       <NA>    3808816.06  6.580790
## 92      2887.62  3.4605400                       <NA>     279247.95  5.445990
## 93     87500.39  4.9420100                       <NA>    4135042.71  6.616480
## 94     97750.73  4.9901200                       <NA>   10000000.00  7.000000
## 95      1750.01  3.2430405                       <NA>    7809981.41  6.892650
## 96      2150.01  3.3324405                       <NA>      57500.29  4.759670
## 97      8000.00  3.9030900                       <NA>   11999965.57  7.079180
## 98      1096.48  3.0400007                       <NA>    2290867.65  6.360000
## 99      2810.00  3.4487063                       <NA>   11595000.00  7.064271
## 100       23.00  1.3617278                       <NA>      11410.11  4.057290
## 101       27.50  1.4393327                       <NA>      35000.16  4.544070
## 102       19.50  1.2900346                       <NA>        467.74  2.670005
## 103       29.00  1.4623980                       <NA>        707.94  2.849996
## 104     6649.97  3.8228197                       <NA>      19300.12  4.285560
## 105    27250.22  4.4353700                       <NA>     641327.70  5.807080
## 106    11249.93  4.0511498                       <NA>     914997.69  5.961420
## 107    22124.83  4.3448799                       <NA>    3236532.71  6.510080
## 108    10375.05  4.0159902                       <NA>    6133381.80  6.787700
## 109    21250.05  4.3273600                       <NA>     970912.29  5.987180
## 110    16850.00  4.2265999                       <NA>     163000.90  5.212190
## 111    46249.82  4.6651100                       <NA>    7739982.88  6.888740
## 112     4646.01  3.6670801                       <NA>     119000.83  5.075550
## 113     1660.01  3.2201107                       <NA>     456667.39  5.659600
## 114     1899.98  3.2787490                       <NA>     373275.94  5.572030
## 115     1299.99  3.1139400                       <NA>      15454.68  4.189060
## 116     5000.00  3.6989700                       <NA>     425001.05  5.628390
## 117     4649.97  3.6674502                       <NA>      35666.46  4.552260
## 118     5399.95  3.7323897                       <NA>     138563.87  5.141650
## 119    14999.96  4.1760901                       <NA>     152760.12  5.184010
## 120     2875.01  3.4586394                       <NA>      50134.88  4.700140
## 121    25499.99  4.4065400                       <NA>     250000.00  5.397940
## 122    25999.80  4.4149700                       <NA>     107999.07  5.033420
## 123      800.00  2.9030900                       <NA>     194236.12  5.288330
## 124      296.00  2.4712917                       <NA>      40377.55  4.606140
## 125      340.20  2.5317343                       <NA>       4858.81  3.686530
## 126     1360.79  3.1337911                       <NA>      32716.74  4.514770
## 127     4050.05  3.6074604                       <NA>    2900013.37  6.462400
## 128     2267.98  3.3556392                       <NA>    1592758.75  6.202150
## 129     3549.11  3.5501195                       <NA>     530005.04  5.724280
## 130     5250.01  3.7201601                       <NA>     286615.72  5.457300
## 131     3129.97  3.4955402                       <NA>      13899.85  4.143010
## 132     2825.01  3.4510200                       <NA>     453241.85  5.656330
## 133     1600.00  3.2041200                       <NA>      62999.92  4.799340
## 134     2150.01  3.3324405                       <NA>      18299.95  4.262450
## 135     1360.79  3.1337911                       <NA>      28920.11  4.461200
## 136     1349.99  3.1303306                       <NA>      39600.44  4.597700
## 137      155.30  2.1911715                       <NA>       1376.00  3.138618
## 138      146.50  2.1658376                       <NA>       1866.34  3.270991
## 139       58.00  1.7634280                       <NA>       3393.13  3.530600
## 140      201.00  2.3031961                       <NA>      11999.97  4.079180
## 141      535.20  2.7285161                       <NA>      29000.13  4.462400
## 142      257.00  2.4099331                       <NA>        100.00  2.000000
## 143      390.50  2.5916210                       <NA>     116834.20  5.067570
## 144      775.00  2.8893017                       <NA>      21133.43  4.324970
## 145   427996.29  5.6314400                       <NA>   22295129.54  7.348210
## 146  2249986.95  6.3521800                       <NA>   15912558.01  7.201740
## 147  1050001.69  6.0211900                       <NA>   42065882.07  7.623930
## 148     3899.96  3.5910602                       <NA>      44999.74  4.653210
## 149  4000000.08  6.6020600                       <NA>  109999319.90  8.041390
## 150  4000000.08  6.6020600                       <NA> 1753759352.00  9.243970
## 151       22.00  1.3424227                       <NA>      25945.38  4.414060
## 152     1133.99  3.0546092                       <NA>       1037.41  3.015950
## 153      625.00  2.7958800                       <NA>       2685.84  3.429080
## 154      148.00  2.1702617                       <NA>      12999.90  4.113940
## 155       65.00  1.8129134                       <NA>       1582.01  3.199209
## 156      242.00  2.3838154                       <NA>        272.00  2.434569
## 157      155.00  2.1903317                       <NA>        172.00  2.235528
## 158       39.00  1.5910646                       <NA>       5400.95  3.732470
## 159     8000.00  3.9030900                       <NA>     976989.73  5.989890
## 160     5190.03  3.7151699                       <NA>      10000.00  4.000000
## 161       22.57  1.3535316                       <NA>       1596.98  3.203299
## 162       66.30  1.8215135                       <NA>       7738.91  3.888680
## 163       92.14  1.9644482                       <NA>       8322.04  3.920230
## 164       38.00  1.5797836                       <NA>        700.42  2.845359
## 165       70.87  1.8504624                       <NA>         85.50  1.931966
## 166       56.70  1.7535831                       <NA>        151.60  2.180699
## 167       35.44  1.5494937                       <NA>        674.47  2.828963
## 168       49.61  1.6955692                       <NA>        411.74  2.614623
## 169       29.50  1.4698220                       <NA>         36.67  1.564311
## 170       85.50  1.9319661                       <NA>        419.20  2.622421
## 171       30.00  1.4771213                       <NA>        982.13  2.992169
## 172      395.48  2.5971245                       <NA>      47616.78  4.677760
## 173      308.30  2.4889735                       <NA>       2537.00  3.404320
## 174      132.29  2.1215270                       <NA>        533.00  2.726727
## 175      255.15  2.4067956                       <NA>        580.55  2.763840
## 176     1360.79  3.1337911                       <NA>       5995.01  3.777790
## 177       27.54  1.4399639                       <NA>       5011.87  3.700000
## 178       11.05  1.0433623                       <NA>       2132.90  3.328970
## 179       38.27  1.5828585                       <NA>       4549.99  3.658010
## 180       52.50  1.7201593                       <NA>       3127.81  3.495240
## 181      350.00  2.5440680                       <NA>       5788.15  3.762540
## 182      428.00  2.6314438                       <NA>       1038.51  3.016411
## 183     4250.01  3.6283900                       <NA>     186668.05  5.271070
## 184     8618.27  3.9354201                       <NA>     361501.41  5.558110
## 185      160.18  2.2046083                       <NA>         71.14  1.852114
## 186       68.80  1.8375884                       <NA>     109299.96  5.038620
## 187       31.00  1.4913617                       <NA>       4369.99  3.640480
## 188      153.56  2.1862781                       <NA>        431.70  2.635182
## 189       41.82  1.6213840                       <NA>       7374.80  3.867750
## 190       56.70  1.7535831                       <NA>      17699.87  4.247970
## 191      144.58  2.1601082                       <NA>       3008.50  3.478350
## 192       76.20  1.8819550                       <NA>       1480.44  3.170391
## 193    17000.04  4.2304499                       <NA>    1689779.36  6.227830
## 194    14999.96  4.1760901                       <NA>    1411984.73  6.149830
## 195     2749.98  3.4393295                       <NA>     151178.49  5.179490
## 196       31.60  1.4996871                       <NA>       7574.95  3.879380
## 197       21.20  1.3263359                       <NA>      13052.09  4.115680
## 198       88.30  1.9459607                       <NA>        132.70  2.122871
## 199      122.00  2.0863598                       <NA>        630.00  2.799341
## 200     1185.00  3.0737184                       <NA>      35000.16  4.544070
## 201      215.60  2.3336488                       <NA>       9499.92  3.977720
## 202      165.45  2.2186668                       <NA>       5000.00  3.698970
## 203      100.86  2.0037190                       <NA>         40.30  1.605305
## 204       95.80  1.9813655                       <NA>       1932.81  3.286189
## 205      102.50  2.0107239                       <NA>       1799.99  3.255270
## 206      148.84  2.1727197                       <NA>      79000.53  4.897630
## 207       64.50  1.8095597                       <NA>      29195.77  4.465320
## 208     3401.97  3.5317305                       <NA>      56963.94  4.755600
## 209     3401.97  3.5317305                       <NA>     165390.29  5.218510
## 210      375.00  2.5740313                       <NA>      27499.83  4.439330
## 211      793.80  2.8997111                       <NA>     130888.05  5.116900
## 212      532.98  2.7267109                       <NA>       4900.04  3.690200
## 213      264.30  2.4220972                       <NA>     170820.50  5.232540
## 214      952.99  2.9790883                       <NA>     128265.54  5.108110
## 215      327.50  2.5152113                       <NA>      74908.31  4.874530
## 216      725.75  2.8607870                       <NA>        518.84  2.715033
## 217      578.34  2.7621832                       <NA>        535.50  2.728759
## 218      637.87  2.8047322                       <NA>     168437.97  5.226440
## 219      794.49  2.9000884                       <NA>      30109.25  4.478700
## 220      106.00  2.0253059                       <NA>      15041.81  4.177300
## 221      198.45  2.2976511                       <NA>      15599.83  4.193120
## 222      748.43  2.8741512                       <NA>      42505.00  4.628440
## 223       26.93  1.4302364                       <NA>       8163.19  3.911860
## 224       42.52  1.6285933                       <NA>      14902.19  4.173250
## 225       42.52  1.6285933                       <NA>      53250.05  4.726320
## 226       42.52  1.6285933                       <NA>      32460.11  4.511350
## 227      223.96  2.3501705                       <NA>       4753.35  3.677000
## 228      502.00  2.7007037                       <NA>     123999.52  5.093420
## 229       10.00  1.0000000                       <NA>        234.42  2.369995
## 230        8.13  0.9100905                       <NA>       4786.30  3.680000
## 231        4.17  0.6201361                       <NA>       5011.87  3.700000
## 232        9.33  0.9698816                       <NA>        371.54  2.570006
## 233        4.37  0.6404814                       <NA>        275.42  2.439995
## 234       14.13  1.1501422                       <NA>         77.62  1.889974
## 235       47.86  1.6799727                       <NA>       3630.78  3.560000
## 236      103.50  2.0149403                       <NA>       7428.65  3.870910
## 237       96.50  1.9845273                       <NA>       3004.35  3.477751
## 238       81.42  1.9107311                       <NA>       2828.59  3.451570
##                                                                                                                                                                                                                              hra.reference
## 1                                               Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 2   Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 3   Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 4   Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 5   Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 6   Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 7   Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 8   Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 9   Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 10  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 11  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 12  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 13  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 14  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 15  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 16  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 17  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 18  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 19  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 20  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 21  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 22  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 23  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 24  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 25  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 26  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 27  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 28  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 29  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 30  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 31  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 32  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 33  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 34  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 35  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 36  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 37  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 38  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 39  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 40  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 41  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 42  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 43  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 44  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 45  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 46  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 47  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 48  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 49                                              Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 50  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 51                                              Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 52  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 53  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 54  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 55  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 56  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 57  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 58  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 59  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 60  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 61  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 62  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 63  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 64  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 65  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 66  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 67  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 68  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 69  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 70  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 71  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 72  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 73                                              Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 74                                                                                          Palomares F. 1994. Site fidelity and effects of body mass on home-range size of Egyptian mongooses. Canadian Journal of Zoology 72, 465 - 469.
## 75  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 76  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 77  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 78  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 79  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 80  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 81  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 82  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 83  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 84  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 85  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 86  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 87                                              Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 88                                              Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 89  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 90                                              Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 91  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 92  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 93  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 94  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 95  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 96  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 97  Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 98                                              Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 99              Belcher CA, Darrant JP. 2004. Home range and spatial organization of the marsupial carnivore, Dasyurus maculatus maculatus (Marsupialia: Dasyuridae) in south-eastern Australia. Journal of Zoology (London) 262, 271-280.
## 100 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 101 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 102                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 103                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 104 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 105 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 106 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 107 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 108 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 109 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 110 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 111 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 112 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 113 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 114 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 115 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 116 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 117 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 118 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 119 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 120 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 121 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 122 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 123 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 124 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 125 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 126 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 127 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 128 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 129 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 130 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 131 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 132 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 133 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 134 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 135 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 136 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 137 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 138 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 139 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 140 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 141 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 142 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 143 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 144 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 145 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 146 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 147 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 148 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 149 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 150 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 151 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 152 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 153 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 154 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 155 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 156 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 157 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 158 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 159 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 160 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 161 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 162 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 163 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 164 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 165 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 166 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 167 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 168 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 169 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 170 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 171 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 172 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 173 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 174 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 175 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 176 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 177                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 178 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 179 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 180 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 181 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 182 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 183 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 184 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 185 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 186 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 187 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 188 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 189 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 190 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 191 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 192 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 193 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 194 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 195 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 196 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 197 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 198 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 199 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 200 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 201 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 202 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 203 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 204 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 205 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 206 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 207 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 208 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 209 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 210 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 211 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 212 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 213 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 214 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 215 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 216 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 217 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 218 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 219 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 220 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 221 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 222 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 223 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 224 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 225 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 226 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 227 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 228 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 229                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 230                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 231                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 232                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 233                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 234                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 235                                             Tucker, M. A., T. J. Ord, and T. L. Rogers. 2014. Evolutionary predictors of mammalian home range size: body mass, diet and the environment. Global Ecology and Biogeography 23:1105-1114.
## 236 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 237 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
## 238 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
##           realm thermoregulation locomotion trophic.guild dimension  preymass
## 1   terrestrial        endotherm    walking     carnivore        2D        NA
## 2   terrestrial        endotherm    walking     carnivore        2D        NA
## 3   terrestrial        endotherm    walking     herbivore        2D        NA
## 4   terrestrial        endotherm    walking     herbivore        2D        NA
## 5   terrestrial        endotherm    walking     herbivore        2D        NA
## 6   terrestrial        endotherm    walking     herbivore        2D        NA
## 7   terrestrial        endotherm    walking     herbivore        2D        NA
## 8   terrestrial        endotherm    walking     herbivore        2D        NA
## 9   terrestrial        endotherm    walking     herbivore        2D        NA
## 10  terrestrial        endotherm    walking     herbivore        2D        NA
## 11  terrestrial        endotherm    walking     herbivore        2D        NA
## 12  terrestrial        endotherm    walking     herbivore        2D        NA
## 13  terrestrial        endotherm    walking     herbivore        2D        NA
## 14  terrestrial        endotherm    walking     herbivore        2D        NA
## 15  terrestrial        endotherm    walking     herbivore        2D        NA
## 16  terrestrial        endotherm    walking     herbivore        2D        NA
## 17  terrestrial        endotherm    walking     herbivore        2D        NA
## 18  terrestrial        endotherm    walking     herbivore        2D        NA
## 19  terrestrial        endotherm    walking     herbivore        2D        NA
## 20  terrestrial        endotherm    walking     herbivore        2D        NA
## 21  terrestrial        endotherm    walking     herbivore        2D        NA
## 22  terrestrial        endotherm    walking     herbivore        2D        NA
## 23  terrestrial        endotherm    walking     herbivore        2D        NA
## 24  terrestrial        endotherm    walking     herbivore        2D        NA
## 25  terrestrial        endotherm    walking     herbivore        2D        NA
## 26  terrestrial        endotherm    walking     herbivore        2D        NA
## 27  terrestrial        endotherm    walking     herbivore        2D        NA
## 28  terrestrial        endotherm    walking     herbivore        2D        NA
## 29  terrestrial        endotherm    walking     herbivore        2D        NA
## 30  terrestrial        endotherm    walking     herbivore        2D        NA
## 31  terrestrial        endotherm    walking     herbivore        2D        NA
## 32  terrestrial        endotherm    walking     herbivore        2D        NA
## 33  terrestrial        endotherm    walking     herbivore        2D        NA
## 34  terrestrial        endotherm    walking     herbivore        2D        NA
## 35  terrestrial        endotherm    walking     herbivore        2D        NA
## 36  terrestrial        endotherm    walking     herbivore        2D        NA
## 37  terrestrial        endotherm    walking     herbivore        2D        NA
## 38  terrestrial        endotherm    walking     herbivore        2D        NA
## 39  terrestrial        endotherm    walking     herbivore        2D        NA
## 40  terrestrial        endotherm    walking     herbivore        2D        NA
## 41  terrestrial        endotherm    walking     herbivore        2D        NA
## 42  terrestrial        endotherm    walking     herbivore        2D        NA
## 43  terrestrial        endotherm    walking     carnivore        2D        NA
## 44  terrestrial        endotherm    walking     carnivore        2D        NA
## 45  terrestrial        endotherm    walking     carnivore        2D    427.68
## 46  terrestrial        endotherm    walking     carnivore        2D        NA
## 47  terrestrial        endotherm    walking     carnivore        2D        NA
## 48  terrestrial        endotherm    walking     carnivore        2D        NA
## 49  terrestrial        endotherm    walking     carnivore        2D        NA
## 50  terrestrial        endotherm    walking     herbivore        2D        NA
## 51  terrestrial        endotherm    walking     carnivore        2D        NA
## 52  terrestrial        endotherm    walking     carnivore        2D        NA
## 53  terrestrial        endotherm    walking     carnivore        2D  18055.42
## 54  terrestrial        endotherm    walking     carnivore        2D        NA
## 55  terrestrial        endotherm    walking     carnivore        2D        NA
## 56  terrestrial        endotherm    walking     carnivore        2D        NA
## 57  terrestrial        endotherm    walking     carnivore        2D   1527.47
## 58  terrestrial        endotherm    walking     carnivore        2D   1109.72
## 59  terrestrial        endotherm    walking     carnivore        2D        NA
## 60  terrestrial        endotherm    walking     carnivore        2D  10521.52
## 61  terrestrial        endotherm    walking     carnivore        2D   4065.03
## 62  terrestrial        endotherm    walking     carnivore        2D   3890.80
## 63  terrestrial        endotherm    walking     carnivore        2D        NA
## 64  terrestrial        endotherm    walking     carnivore        2D    361.53
## 65  terrestrial        endotherm    walking     carnivore        2D        NA
## 66  terrestrial        endotherm    walking     carnivore        2D  30234.31
## 67  terrestrial        endotherm    walking     carnivore        2D 130233.20
## 68  terrestrial        endotherm    walking     carnivore        2D        NA
## 69  terrestrial        endotherm    walking     carnivore        2D        NA
## 70  terrestrial        endotherm    walking     carnivore        2D  57547.19
## 71  terrestrial        endotherm    walking     carnivore        2D        NA
## 72  terrestrial        endotherm    walking     carnivore        2D        NA
## 73  terrestrial        endotherm    walking     carnivore        2D        NA
## 74  terrestrial        endotherm    walking     carnivore        2D    143.37
## 75  terrestrial        endotherm    walking     carnivore        2D        NA
## 76  terrestrial        endotherm    walking     carnivore        2D        NA
## 77  terrestrial        endotherm    walking     carnivore        2D        NA
## 78  terrestrial        endotherm    walking     carnivore        2D        NA
## 79  terrestrial        endotherm    walking     carnivore        2D        NA
## 80  terrestrial        endotherm    walking     carnivore        2D     23.15
## 81  terrestrial        endotherm    walking     carnivore        2D        NA
## 82  terrestrial        endotherm    walking     carnivore        2D     95.19
## 83  terrestrial        endotherm    walking     carnivore        2D    656.03
## 84  terrestrial        endotherm    walking     carnivore        2D     47.55
## 85  terrestrial        endotherm    walking     carnivore        2D     14.58
## 86  terrestrial        endotherm    walking     carnivore        2D        NA
## 87  terrestrial        endotherm    walking     carnivore        2D        NA
## 88  terrestrial        endotherm    walking     carnivore        2D        NA
## 89  terrestrial        endotherm    walking     carnivore        2D     30.59
## 90  terrestrial        endotherm    walking     carnivore        2D        NA
## 91  terrestrial        endotherm    walking     carnivore        2D        NA
## 92  terrestrial        endotherm    walking     herbivore        2D        NA
## 93  terrestrial        endotherm    walking     herbivore        2D        NA
## 94  terrestrial        endotherm    walking     carnivore        2D        NA
## 95  terrestrial        endotherm    walking     carnivore        2D     42.00
## 96  terrestrial        endotherm    walking     carnivore        2D        NA
## 97  terrestrial        endotherm    walking     carnivore        2D        NA
## 98  terrestrial        endotherm    walking     carnivore        2D        NA
## 99  terrestrial        endotherm    walking     carnivore        2D        NA
## 100 terrestrial        endotherm    walking     carnivore        2D        NA
## 101 terrestrial        endotherm    walking     carnivore        2D        NA
## 102 terrestrial        endotherm    walking     carnivore        2D        NA
## 103 terrestrial        endotherm    walking     carnivore        2D        NA
## 104 terrestrial        endotherm    walking     herbivore        2D        NA
## 105 terrestrial        endotherm    walking     herbivore        2D        NA
## 106 terrestrial        endotherm    walking     herbivore        2D        NA
## 107 terrestrial        endotherm    walking     herbivore        2D        NA
## 108 terrestrial        endotherm    walking     herbivore        2D        NA
## 109 terrestrial        endotherm    walking     herbivore        2D        NA
## 110 terrestrial        endotherm    walking     herbivore        2D        NA
## 111 terrestrial        endotherm    walking     herbivore        2D        NA
## 112 terrestrial        endotherm    walking     herbivore        2D        NA
## 113 terrestrial        endotherm    walking     herbivore        2D        NA
## 114 terrestrial        endotherm    walking     herbivore        2D        NA
## 115 terrestrial        endotherm    walking     herbivore        2D        NA
## 116 terrestrial        endotherm    walking     herbivore        2D        NA
## 117 terrestrial        endotherm    walking     herbivore        2D        NA
## 118 terrestrial        endotherm    walking     herbivore        2D        NA
## 119 terrestrial        endotherm    walking     herbivore        2D        NA
## 120 terrestrial        endotherm    walking     herbivore        2D        NA
## 121 terrestrial        endotherm    walking     herbivore        2D        NA
## 122 terrestrial        endotherm    walking     herbivore        2D        NA
## 123 terrestrial        endotherm    walking     carnivore        2D        NA
## 124 terrestrial        endotherm    walking     carnivore        2D        NA
## 125 terrestrial        endotherm    walking     herbivore        2D        NA
## 126 terrestrial        endotherm    walking     herbivore        2D        NA
## 127 terrestrial        endotherm    walking     herbivore        2D        NA
## 128 terrestrial        endotherm    walking     herbivore        2D        NA
## 129 terrestrial        endotherm    walking     herbivore        2D        NA
## 130 terrestrial        endotherm    walking     herbivore        2D        NA
## 131 terrestrial        endotherm    walking     herbivore        2D        NA
## 132 terrestrial        endotherm    walking     herbivore        2D        NA
## 133 terrestrial        endotherm    walking     herbivore        2D        NA
## 134 terrestrial        endotherm    walking     herbivore        2D        NA
## 135 terrestrial        endotherm    walking     herbivore        2D        NA
## 136 terrestrial        endotherm    walking     herbivore        2D        NA
## 137 terrestrial        endotherm    walking     herbivore        2D        NA
## 138 terrestrial        endotherm    walking     herbivore        2D        NA
## 139 terrestrial        endotherm    walking     carnivore        2D        NA
## 140 terrestrial        endotherm    walking     carnivore        2D        NA
## 141 terrestrial        endotherm    walking     carnivore        2D        NA
## 142 terrestrial        endotherm    walking     carnivore        2D        NA
## 143 terrestrial        endotherm    walking     carnivore        2D        NA
## 144 terrestrial        endotherm    walking     carnivore        2D        NA
## 145 terrestrial        endotherm    walking     herbivore        2D        NA
## 146 terrestrial        endotherm    walking     herbivore        2D        NA
## 147 terrestrial        endotherm    walking     herbivore        2D        NA
## 148 terrestrial        endotherm    walking     herbivore        2D        NA
## 149 terrestrial        endotherm    walking     herbivore        2D        NA
## 150 terrestrial        endotherm    walking     herbivore        2D        NA
## 151 terrestrial        endotherm    walking     carnivore        2D        NA
## 152 terrestrial        endotherm    walking     herbivore        2D        NA
## 153 terrestrial        endotherm    walking     herbivore        2D        NA
## 154 terrestrial        endotherm    walking     herbivore        2D        NA
## 155 terrestrial        endotherm    walking     herbivore        2D        NA
## 156 terrestrial        endotherm    walking     herbivore        2D        NA
## 157 terrestrial        endotherm    walking     herbivore        2D        NA
## 158 terrestrial        endotherm    walking     herbivore        2D        NA
## 159 terrestrial        endotherm    walking     herbivore        2D        NA
## 160 terrestrial        endotherm    walking     herbivore        2D        NA
## 161 terrestrial        endotherm    walking     herbivore        2D        NA
## 162 terrestrial        endotherm    walking     herbivore        2D        NA
## 163 terrestrial        endotherm    walking     herbivore        2D        NA
## 164 terrestrial        endotherm    walking     herbivore        2D        NA
## 165 terrestrial        endotherm    walking     herbivore        2D        NA
## 166 terrestrial        endotherm    walking     herbivore        2D        NA
## 167 terrestrial        endotherm    walking     herbivore        2D        NA
## 168 terrestrial        endotherm    walking     herbivore        2D        NA
## 169 terrestrial        endotherm    walking     herbivore        2D        NA
## 170 terrestrial        endotherm    walking     herbivore        2D        NA
## 171 terrestrial        endotherm    walking     herbivore        2D        NA
## 172 terrestrial        endotherm    walking     herbivore        2D        NA
## 173 terrestrial        endotherm    walking     herbivore        2D        NA
## 174 terrestrial        endotherm    walking     herbivore        2D        NA
## 175 terrestrial        endotherm    walking     herbivore        2D        NA
## 176 terrestrial        endotherm    walking     herbivore        2D        NA
## 177 terrestrial        endotherm    walking     carnivore        2D        NA
## 178 terrestrial        endotherm    walking     herbivore        2D        NA
## 179 terrestrial        endotherm    walking     herbivore        2D        NA
## 180 terrestrial        endotherm    walking     herbivore        2D        NA
## 181 terrestrial        endotherm    walking     herbivore        2D        NA
## 182 terrestrial        endotherm    walking     herbivore        2D        NA
## 183 terrestrial        endotherm    walking     herbivore        2D        NA
## 184 terrestrial        endotherm    walking     herbivore        2D        NA
## 185 terrestrial        endotherm    walking     herbivore        2D        NA
## 186 terrestrial        endotherm    walking     herbivore        2D        NA
## 187 terrestrial        endotherm    walking     herbivore        2D        NA
## 188 terrestrial        endotherm    walking     herbivore        2D        NA
## 189 terrestrial        endotherm    walking     herbivore        2D        NA
## 190 terrestrial        endotherm    walking     herbivore        2D        NA
## 191 terrestrial        endotherm    walking     herbivore        2D        NA
## 192 terrestrial        endotherm    walking     herbivore        2D        NA
## 193 terrestrial        endotherm    walking     herbivore        2D        NA
## 194 terrestrial        endotherm    walking     herbivore        2D        NA
## 195 terrestrial        endotherm    walking     herbivore        2D        NA
## 196 terrestrial        endotherm    walking     herbivore        2D        NA
## 197 terrestrial        endotherm    walking     herbivore        2D        NA
## 198 terrestrial        endotherm    walking     herbivore        2D        NA
## 199 terrestrial        endotherm    walking     herbivore        2D        NA
## 200 terrestrial        endotherm    walking     herbivore        2D        NA
## 201 terrestrial        endotherm    walking     herbivore        2D        NA
## 202 terrestrial        endotherm    walking     herbivore        2D        NA
## 203 terrestrial        endotherm    walking     herbivore        2D        NA
## 204 terrestrial        endotherm    walking     herbivore        2D        NA
## 205 terrestrial        endotherm    walking     herbivore        2D        NA
## 206 terrestrial        endotherm    walking     herbivore        2D        NA
## 207 terrestrial        endotherm    walking     herbivore        2D        NA
## 208 terrestrial        endotherm    walking     herbivore        2D        NA
## 209 terrestrial        endotherm    walking     herbivore        2D        NA
## 210 terrestrial        endotherm    walking     herbivore        2D        NA
## 211 terrestrial        endotherm    walking     herbivore        2D        NA
## 212 terrestrial        endotherm    walking     herbivore        2D        NA
## 213 terrestrial        endotherm    walking     herbivore        2D        NA
## 214 terrestrial        endotherm    walking     herbivore        2D        NA
## 215 terrestrial        endotherm    walking     herbivore        2D        NA
## 216 terrestrial        endotherm    walking     herbivore        2D        NA
## 217 terrestrial        endotherm    walking     herbivore        2D        NA
## 218 terrestrial        endotherm    walking     herbivore        2D        NA
## 219 terrestrial        endotherm    walking     herbivore        2D        NA
## 220 terrestrial        endotherm    walking     herbivore        2D        NA
## 221 terrestrial        endotherm    walking     herbivore        2D        NA
## 222 terrestrial        endotherm    walking     herbivore        2D        NA
## 223 terrestrial        endotherm    walking     herbivore        2D        NA
## 224 terrestrial        endotherm    walking     herbivore        2D        NA
## 225 terrestrial        endotherm    walking     herbivore        2D        NA
## 226 terrestrial        endotherm    walking     herbivore        2D        NA
## 227 terrestrial        endotherm    walking     herbivore        2D        NA
## 228 terrestrial        endotherm    walking     herbivore        2D        NA
## 229 terrestrial        endotherm    walking     carnivore        2D        NA
## 230 terrestrial        endotherm    walking     carnivore        2D        NA
## 231 terrestrial        endotherm    walking     carnivore        2D        NA
## 232 terrestrial        endotherm    walking     carnivore        2D        NA
## 233 terrestrial        endotherm    walking     carnivore        2D        NA
## 234 terrestrial        endotherm    walking     carnivore        2D        NA
## 235 terrestrial        endotherm    walking     carnivore        2D        NA
## 236 terrestrial        endotherm    walking     carnivore        2D        NA
## 237 terrestrial        endotherm    walking     carnivore        2D        NA
## 238 terrestrial        endotherm    walking     carnivore        2D        NA
##     log10.preymass     PPMR
## 1               NA       NA
## 2               NA       NA
## 3               NA       NA
## 4               NA       NA
## 5               NA       NA
## 6               NA       NA
## 7               NA       NA
## 8               NA       NA
## 9               NA       NA
## 10              NA       NA
## 11              NA       NA
## 12              NA       NA
## 13              NA       NA
## 14              NA       NA
## 15              NA       NA
## 16              NA       NA
## 17              NA       NA
## 18              NA       NA
## 19              NA       NA
## 20              NA       NA
## 21              NA       NA
## 22              NA       NA
## 23              NA       NA
## 24              NA       NA
## 25              NA       NA
## 26              NA       NA
## 27              NA       NA
## 28              NA       NA
## 29              NA       NA
## 30              NA       NA
## 31              NA       NA
## 32              NA       NA
## 33              NA       NA
## 34              NA       NA
## 35              NA       NA
## 36              NA       NA
## 37              NA       NA
## 38              NA       NA
## 39              NA       NA
## 40              NA       NA
## 41              NA       NA
## 42              NA       NA
## 43              NA       NA
## 44              NA       NA
## 45        2.631119 17.23248
## 46              NA       NA
## 47              NA       NA
## 48              NA       NA
## 49              NA       NA
## 50              NA       NA
## 51              NA       NA
## 52              NA       NA
## 53        4.256608  0.72000
## 54              NA       NA
## 55              NA       NA
## 56              NA       NA
## 57        3.183973  6.54000
## 58        3.045213  3.27000
## 59              NA       NA
## 60        4.022078  0.97000
## 61        3.609064  7.38000
## 62        3.590039  2.84000
## 63              NA       NA
## 64        2.558144  9.93000
## 65              NA       NA
## 66        4.480500  1.60000
## 67        5.114722  0.86000
## 68              NA       NA
## 69              NA       NA
## 70        4.760024  0.53000
## 71              NA       NA
## 72              NA       NA
## 73              NA       NA
## 74        2.156458 19.60000
## 75              NA       NA
## 76              NA       NA
## 77              NA       NA
## 78              NA       NA
## 79              NA       NA
## 80        1.364551 38.17000
## 81              NA       NA
## 82        1.978591 26.00000
## 83        2.816924  4.84000
## 84        1.677151  5.69000
## 85        1.163758 10.30000
## 86              NA       NA
## 87              NA       NA
## 88              NA       NA
## 89        1.485579  2.88000
## 90              NA       NA
## 91              NA       NA
## 92              NA       NA
## 93              NA       NA
## 94              NA       NA
## 95        1.623249 41.67000
## 96              NA       NA
## 97              NA       NA
## 98              NA       NA
## 99              NA       NA
## 100             NA       NA
## 101             NA       NA
## 102             NA       NA
## 103             NA       NA
## 104             NA       NA
## 105             NA       NA
## 106             NA       NA
## 107             NA       NA
## 108             NA       NA
## 109             NA       NA
## 110             NA       NA
## 111             NA       NA
## 112             NA       NA
## 113             NA       NA
## 114             NA       NA
## 115             NA       NA
## 116             NA       NA
## 117             NA       NA
## 118             NA       NA
## 119             NA       NA
## 120             NA       NA
## 121             NA       NA
## 122             NA       NA
## 123             NA       NA
## 124             NA       NA
## 125             NA       NA
## 126             NA       NA
## 127             NA       NA
## 128             NA       NA
## 129             NA       NA
## 130             NA       NA
## 131             NA       NA
## 132             NA       NA
## 133             NA       NA
## 134             NA       NA
## 135             NA       NA
## 136             NA       NA
## 137             NA       NA
## 138             NA       NA
## 139             NA       NA
## 140             NA       NA
## 141             NA       NA
## 142             NA       NA
## 143             NA       NA
## 144             NA       NA
## 145             NA       NA
## 146             NA       NA
## 147             NA       NA
## 148             NA       NA
## 149             NA       NA
## 150             NA       NA
## 151             NA       NA
## 152             NA       NA
## 153             NA       NA
## 154             NA       NA
## 155             NA       NA
## 156             NA       NA
## 157             NA       NA
## 158             NA       NA
## 159             NA       NA
## 160             NA       NA
## 161             NA       NA
## 162             NA       NA
## 163             NA       NA
## 164             NA       NA
## 165             NA       NA
## 166             NA       NA
## 167             NA       NA
## 168             NA       NA
## 169             NA       NA
## 170             NA       NA
## 171             NA       NA
## 172             NA       NA
## 173             NA       NA
## 174             NA       NA
## 175             NA       NA
## 176             NA       NA
## 177             NA       NA
## 178             NA       NA
## 179             NA       NA
## 180             NA       NA
## 181             NA       NA
## 182             NA       NA
## 183             NA       NA
## 184             NA       NA
## 185             NA       NA
## 186             NA       NA
## 187             NA       NA
## 188             NA       NA
## 189             NA       NA
## 190             NA       NA
## 191             NA       NA
## 192             NA       NA
## 193             NA       NA
## 194             NA       NA
## 195             NA       NA
## 196             NA       NA
## 197             NA       NA
## 198             NA       NA
## 199             NA       NA
## 200             NA       NA
## 201             NA       NA
## 202             NA       NA
## 203             NA       NA
## 204             NA       NA
## 205             NA       NA
## 206             NA       NA
## 207             NA       NA
## 208             NA       NA
## 209             NA       NA
## 210             NA       NA
## 211             NA       NA
## 212             NA       NA
## 213             NA       NA
## 214             NA       NA
## 215             NA       NA
## 216             NA       NA
## 217             NA       NA
## 218             NA       NA
## 219             NA       NA
## 220             NA       NA
## 221             NA       NA
## 222             NA       NA
## 223             NA       NA
## 224             NA       NA
## 225             NA       NA
## 226             NA       NA
## 227             NA       NA
## 228             NA       NA
## 229             NA       NA
## 230             NA       NA
## 231             NA       NA
## 232             NA       NA
## 233             NA       NA
## 234             NA       NA
## 235             NA       NA
## 236             NA       NA
## 237             NA       NA
## 238             NA       NA
##                                                                                                                                                                                                                                      prey.size.reference
## 1                                                                                                                                                                                                                                                   <NA>
## 2                                                                                                                                                                                                                                                   <NA>
## 3                                                                                                                                                                                                                                                   <NA>
## 4                                                                                                                                                                                                                                                   <NA>
## 5                                                                                                                                                                                                                                                   <NA>
## 6                                                                                                                                                                                                                                                   <NA>
## 7                                                                                                                                                                                                                                                   <NA>
## 8                                                                                                                                                                                                                                                   <NA>
## 9                                                                                                                                                                                                                                                   <NA>
## 10                                                                                                                                                                                                                                                  <NA>
## 11                                                                                                                                                                                                                                                  <NA>
## 12                                                                                                                                                                                                                                                  <NA>
## 13                                                                                                                                                                                                                                                  <NA>
## 14                                                                                                                                                                                                                                                  <NA>
## 15                                                                                                                                                                                                                                                  <NA>
## 16                                                                                                                                                                                                                                                  <NA>
## 17                                                                                                                                                                                                                                                  <NA>
## 18                                                                                                                                                                                                                                                  <NA>
## 19                                                                                                                                                                                                                                                  <NA>
## 20                                                                                                                                                                                                                                                  <NA>
## 21                                                                                                                                                                                                                                                  <NA>
## 22                                                                                                                                                                                                                                                  <NA>
## 23                                                                                                                                                                                                                                                  <NA>
## 24                                                                                                                                                                                                                                                  <NA>
## 25                                                                                                                                                                                                                                                  <NA>
## 26                                                                                                                                                                                                                                                  <NA>
## 27                                                                                                                                                                                                                                                  <NA>
## 28                                                                                                                                                                                                                                                  <NA>
## 29                                                                                                                                                                                                                                                  <NA>
## 30                                                                                                                                                                                                                                                  <NA>
## 31                                                                                                                                                                                                                                                  <NA>
## 32                                                                                                                                                                                                                                                  <NA>
## 33                                                                                                                                                                                                                                                  <NA>
## 34                                                                                                                                                                                                                                                  <NA>
## 35                                                                                                                                                                                                                                                  <NA>
## 36                                                                                                                                                                                                                                                  <NA>
## 37                                                                                                                                                                                                                                                  <NA>
## 38                                                                                                                                                                                                                                                  <NA>
## 39                                                                                                                                                                                                                                                  <NA>
## 40                                                                                                                                                                                                                                                  <NA>
## 41                                                                                                                                                                                                                                                  <NA>
## 42                                                                                                                                                                                                                                                  <NA>
## 43                                                                                                                                                                                                                                                  <NA>
## 44                                                                                                                                                                                                                                                  <NA>
## 45                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 46                                                                                                                                                                                                                                                  <NA>
## 47                                                                                                                                                                                                                                                  <NA>
## 48                                                                                                                                                                                                                                                  <NA>
## 49                                                                                                                                                                                                                                                  <NA>
## 50                                                                                                                                                                                                                                                  <NA>
## 51                                                                                                                                                                                                                                                  <NA>
## 52                                                                                                                                                                                                                                                  <NA>
## 53                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 54                                                                                                                                                                                                                                                  <NA>
## 55                                                                                                                                                                                                                                                  <NA>
## 56                                                                                                                                                                                                                                                  <NA>
## 57                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 58                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 59                                                                                                                                                                                                                                                  <NA>
## 60                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 61                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 62                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 63                                                                                                                                                                                                                                                  <NA>
## 64                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 65                                                                                                                                                                                                                                                  <NA>
## 66                                                               Radloff FG, Du Toit JT. 2004. Large predators and their prey in a southern African savanna: a predator\x92s size determines its prey size range. Journal of Animal Ecology 73, 410-423.
## 67                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 68                                                                                                                                                                                                                                                  <NA>
## 69                                                                                                                                                                                                                                                  <NA>
## 70                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 71                                                                                                                                                                                                                                                  <NA>
## 72                                                                                                                                                                                                                                                  <NA>
## 73                                                                                                                                                                                                                                                  <NA>
## 74  Jaksic FM, Delibes M.1987. A Comparative Analysis of Food-Niche Relationships and Trophic Guild Structure in TwoAssemblages of Vertebrate Predators Differing in Species Richness: Causes, Correlations, and Consequences. Oecologia 71(3), 461-472.
## 75                                                                                                                                                                                                                                                  <NA>
## 76                                                                                                                                                                                                                                                  <NA>
## 77                                                                                                                                                                                                                                                  <NA>
## 78                                                                                                                                                                                                                                                  <NA>
## 79                                                                                                                                                                                                                                                  <NA>
## 80                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 81                                                                                                                                                                                                                                                  <NA>
## 82                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 83                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 84                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 85                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 86                                                                                                                                                                                                                                                  <NA>
## 87                                                                                                                                                                                                                                                  <NA>
## 88                                                                                                                                                                                                                                                  <NA>
## 89                                                   Carbone C, Daryl C, Conrad S, Marcus C, Belby J. 2014. Geometric factors influencing the diet of vertebrate predators in marine and terrestrial environments. Ecology Letters 17(12): 1553\x961559.
## 90                                                                                                                                                                                                                                                  <NA>
## 91                                                                                                                                                                                                                                                  <NA>
## 92                                                                                                                                                                                                                                                  <NA>
## 93                                                                                                                                                                                                                                                  <NA>
## 94                                                                                                                                                                                                                                                  <NA>
## 95  Jaksic FM, Delibes M.1987. A Comparative Analysis of Food-Niche Relationships and Trophic Guild Structure in TwoAssemblages of Vertebrate Predators Differing in Species Richness: Causes, Correlations, and Consequences. Oecologia 71(3), 461-472.
## 96                                                                                                                                                                                                                                                  <NA>
## 97                                                                                                                                                                                                                                                  <NA>
## 98                                                                                                                                                                                                                                                  <NA>
## 99                                                                                                                                                                                                                                                  <NA>
## 100                                                                                                                                                                                                                                                 <NA>
## 101                                                                                                                                                                                                                                                 <NA>
## 102                                                                                                                                                                                                                                                 <NA>
## 103                                                                                                                                                                                                                                                 <NA>
## 104                                                                                                                                                                                                                                                 <NA>
## 105                                                                                                                                                                                                                                                 <NA>
## 106                                                                                                                                                                                                                                                 <NA>
## 107                                                                                                                                                                                                                                                 <NA>
## 108                                                                                                                                                                                                                                                 <NA>
## 109                                                                                                                                                                                                                                                 <NA>
## 110                                                                                                                                                                                                                                                 <NA>
## 111                                                                                                                                                                                                                                                 <NA>
## 112                                                                                                                                                                                                                                                 <NA>
## 113                                                                                                                                                                                                                                                 <NA>
## 114                                                                                                                                                                                                                                                 <NA>
## 115                                                                                                                                                                                                                                                 <NA>
## 116                                                                                                                                                                                                                                                 <NA>
## 117                                                                                                                                                                                                                                                 <NA>
## 118                                                                                                                                                                                                                                                 <NA>
## 119                                                                                                                                                                                                                                                 <NA>
## 120                                                                                                                                                                                                                                                 <NA>
## 121                                                                                                                                                                                                                                                 <NA>
## 122                                                                                                                                                                                                                                                 <NA>
## 123                                                                                                                                                                                                                                                 <NA>
## 124                                                                                                                                                                                                                                                 <NA>
## 125                                                                                                                                                                                                                                                 <NA>
## 126                                                                                                                                                                                                                                                 <NA>
## 127                                                                                                                                                                                                                                                 <NA>
## 128                                                                                                                                                                                                                                                 <NA>
## 129                                                                                                                                                                                                                                                 <NA>
## 130                                                                                                                                                                                                                                                 <NA>
## 131                                                                                                                                                                                                                                                 <NA>
## 132                                                                                                                                                                                                                                                 <NA>
## 133                                                                                                                                                                                                                                                 <NA>
## 134                                                                                                                                                                                                                                                 <NA>
## 135                                                                                                                                                                                                                                                 <NA>
## 136                                                                                                                                                                                                                                                 <NA>
## 137                                                                                                                                                                                                                                                 <NA>
## 138                                                                                                                                                                                                                                                 <NA>
## 139                                                                                                                                                                                                                                                 <NA>
## 140                                                                                                                                                                                                                                                 <NA>
## 141                                                                                                                                                                                                                                                 <NA>
## 142                                                                                                                                                                                                                                                 <NA>
## 143                                                                                                                                                                                                                                                 <NA>
## 144                                                                                                                                                                                                                                                 <NA>
## 145                                                                                                                                                                                                                                                 <NA>
## 146                                                                                                                                                                                                                                                 <NA>
## 147                                                                                                                                                                                                                                                 <NA>
## 148                                                                                                                                                                                                                                                 <NA>
## 149                                                                                                                                                                                                                                                 <NA>
## 150                                                                                                                                                                                                                                                 <NA>
## 151                                                                                                                                                                                                                                                 <NA>
## 152                                                                                                                                                                                                                                                 <NA>
## 153                                                                                                                                                                                                                                                 <NA>
## 154                                                                                                                                                                                                                                                 <NA>
## 155                                                                                                                                                                                                                                                 <NA>
## 156                                                                                                                                                                                                                                                 <NA>
## 157                                                                                                                                                                                                                                                 <NA>
## 158                                                                                                                                                                                                                                                 <NA>
## 159                                                                                                                                                                                                                                                 <NA>
## 160                                                                                                                                                                                                                                                 <NA>
## 161                                                                                                                                                                                                                                                 <NA>
## 162                                                                                                                                                                                                                                                 <NA>
## 163                                                                                                                                                                                                                                                 <NA>
## 164                                                                                                                                                                                                                                                 <NA>
## 165                                                                                                                                                                                                                                                 <NA>
## 166                                                                                                                                                                                                                                                 <NA>
## 167                                                                                                                                                                                                                                                 <NA>
## 168                                                                                                                                                                                                                                                 <NA>
## 169                                                                                                                                                                                                                                                 <NA>
## 170                                                                                                                                                                                                                                                 <NA>
## 171                                                                                                                                                                                                                                                 <NA>
## 172                                                                                                                                                                                                                                                 <NA>
## 173                                                                                                                                                                                                                                                 <NA>
## 174                                                                                                                                                                                                                                                 <NA>
## 175                                                                                                                                                                                                                                                 <NA>
## 176                                                                                                                                                                                                                                                 <NA>
## 177                                                                                                                                                                                                                                                 <NA>
## 178                                                                                                                                                                                                                                                 <NA>
## 179                                                                                                                                                                                                                                                 <NA>
## 180                                                                                                                                                                                                                                                 <NA>
## 181                                                                                                                                                                                                                                                 <NA>
## 182                                                                                                                                                                                                                                                 <NA>
## 183                                                                                                                                                                                                                                                 <NA>
## 184                                                                                                                                                                                                                                                 <NA>
## 185                                                                                                                                                                                                                                                 <NA>
## 186                                                                                                                                                                                                                                                 <NA>
## 187                                                                                                                                                                                                                                                 <NA>
## 188                                                                                                                                                                                                                                                 <NA>
## 189                                                                                                                                                                                                                                                 <NA>
## 190                                                                                                                                                                                                                                                 <NA>
## 191                                                                                                                                                                                                                                                 <NA>
## 192                                                                                                                                                                                                                                                 <NA>
## 193                                                                                                                                                                                                                                                 <NA>
## 194                                                                                                                                                                                                                                                 <NA>
## 195                                                                                                                                                                                                                                                 <NA>
## 196                                                                                                                                                                                                                                                 <NA>
## 197                                                                                                                                                                                                                                                 <NA>
## 198                                                                                                                                                                                                                                                 <NA>
## 199                                                                                                                                                                                                                                                 <NA>
## 200                                                                                                                                                                                                                                                 <NA>
## 201                                                                                                                                                                                                                                                 <NA>
## 202                                                                                                                                                                                                                                                 <NA>
## 203                                                                                                                                                                                                                                                 <NA>
## 204                                                                                                                                                                                                                                                 <NA>
## 205                                                                                                                                                                                                                                                 <NA>
## 206                                                                                                                                                                                                                                                 <NA>
## 207                                                                                                                                                                                                                                                 <NA>
## 208                                                                                                                                                                                                                                                 <NA>
## 209                                                                                                                                                                                                                                                 <NA>
## 210                                                                                                                                                                                                                                                 <NA>
## 211                                                                                                                                                                                                                                                 <NA>
## 212                                                                                                                                                                                                                                                 <NA>
## 213                                                                                                                                                                                                                                                 <NA>
## 214                                                                                                                                                                                                                                                 <NA>
## 215                                                                                                                                                                                                                                                 <NA>
## 216                                                                                                                                                                                                                                                 <NA>
## 217                                                                                                                                                                                                                                                 <NA>
## 218                                                                                                                                                                                                                                                 <NA>
## 219                                                                                                                                                                                                                                                 <NA>
## 220                                                                                                                                                                                                                                                 <NA>
## 221                                                                                                                                                                                                                                                 <NA>
## 222                                                                                                                                                                                                                                                 <NA>
## 223                                                                                                                                                                                                                                                 <NA>
## 224                                                                                                                                                                                                                                                 <NA>
## 225                                                                                                                                                                                                                                                 <NA>
## 226                                                                                                                                                                                                                                                 <NA>
## 227                                                                                                                                                                                                                                                 <NA>
## 228                                                                                                                                                                                                                                                 <NA>
## 229                                                                                                                                                                                                                                                 <NA>
## 230                                                                                                                                                                                                                                                 <NA>
## 231                                                                                                                                                                                                                                                 <NA>
## 232                                                                                                                                                                                                                                                 <NA>
## 233                                                                                                                                                                                                                                                 <NA>
## 234                                                                                                                                                                                                                                                 <NA>
## 235                                                                                                                                                                                                                                                 <NA>
## 236                                                                                                                                                                                                                                                 <NA>
## 237                                                                                                                                                                                                                                                 <NA>
## 238                                                                                                                                                                                                                                                 <NA>
```

**10. What is the largest `mean.hra.m2` for mammals? This is a very large number! Which animal has this homerange? Look them up online and see if you can figure out why this number is so large.**

```r
max(homerange$mean.hra.m2)
```

```
## [1] 3550830977
```

```r
filter(homerange, mean.hra.m2=="3550830977")
```

```
##     taxon common.name    class        order   family    genus  species
## 1 mammals    reindeer mammalia artiodactyla cervidae rangifer tarandus
##   primarymethod    N mean.mass.g log10.mass alternative.mass.reference
## 1    telemetry* <NA>    102058.7    5.00885                       <NA>
##   mean.hra.m2 log10.hra
## 1  3550830977   9.55033
##                                                                                                                                                                                                                            hra.reference
## 1 Kelt, D. A., and D. Van Vuren. 1999. Energetic constraints and the relationship between body size and home range area in mammals. Ecology 80:337-340; Kelt, D. A., and D. Van Vuren. In press. Home ranges of recent mammals. Ecology.
##         realm thermoregulation locomotion trophic.guild dimension preymass
## 1 terrestrial        endotherm    walking     herbivore        2D       NA
##   log10.preymass PPMR prey.size.reference
## 1             NA   NA                <NA>
```
The mammal, reindeer, appears to have a home range value of 3550830977m2. This number is very large to due to the areas in which reindeer live including the arctic tundra. In the arctic tundra food is sparse to reindeer must travel/migrate long distances to scavenge for food as they are herbivores and the arctic has seasonal vegetation. Additionally, food is also scarce for the predators of reindeer so they have to travel large distances to avoid the predators. 

## Knit and Upload
Please knit your work as a .pdf or .html file and upload to Canvas. Homework is due before the start of the next lab. No late work is accepted. Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

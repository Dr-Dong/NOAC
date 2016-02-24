# Novel oral anticoagulants network meta-analysis
Benjamin Chan  
`r Sys.time()`  


This network meta-analysis is an update to
[Fu *et al*, 2014](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4244213/),
*J Cardiovasc Med (Hagerstown).* 2014 Dec; 15(12): 873-879.

**Sensitivity analysis**
In light of the [*Cohen 2016*](http://dx.doi.org/10.1136/bmj.i575),
*Rivaroxaban: can we trust the evidence?*,
these results are from a sensitivity analysis where the data are altered.
The warfarin arm of the ROCKET-AF is assumed to have 10% fewer responses than originally reported.
The effect of this sensitivity analysis is bias ROCKET-AF in favor of warfarin
and the see how that affects indirect comparisons.
The issue only affects the bleeding outcome.

Results from the NMA using data as originally reported in the studies is found [here](http://dx.doi.org/10.5281/zenodo.46116).


# Results

## Mortality

* [Data](mtcMortalityData.csv)
* Treatment [network](mtcMortality_files/figure-html/network-1.png)
* Direct and indirect [odds ratio](mtcMortalityOddsRatios.csv) matrix
* Forest plots, `forest-#.png` files, are in this [folder](mtcMortality_files/figure-html)
* [Full details](mtcMortality.md), including model diagnostics

## Stroke

* [Data](mtcStrokeData.csv)
* Treatment [network](mtcStroke_files/figure-html/network-1.png)
* Direct and indirect [odds ratio](mtcStrokeOddsRatios.csv) matrix
* Forest plots, `forest-#.png` files, are in this [folder](mtcStroke_files/figure-html)
* [Full details](mtcStroke.md), including model diagnostics

## MI

* [Data](mtcMIData.csv)
* Treatment [network](mtcMI_files/figure-html/network-1.png)
* Direct and indirect [odds ratio](mtcMIOddsRatios.csv) matrix
* Forest plots, `forest-#.png` files, are in this [folder](mtcMI_files/figure-html)
* [Full details](mtcMI.md), including model diagnostics

## Bleeding

* [Data](mtcBleedingData.csv)
* Treatment [network](mtcBleeding_files/figure-html/network-1.png)
* Direct and indirect [odds ratio](mtcBleedingOddsRatios.csv) matrix
* Forest plots, `forest-#.png` files, are in this [folder](mtcBleeding_files/figure-html)
* [Full details](mtcBleeding.md), including model diagnostics


# Methods

Use the [`gemtc`](https://drugis.org/software/r-packages/gemtc) package.
Check the link for references.


```r
library(openxlsx)
library(data.table)
library(gemtc)
library(xtable)
```



Set `effect` to be used for the `linearModel` parameter in the `mtc.model` function.


```r
effect <- "fixed"
```

Set sampler parameters.


```r
nAdapt <- 5000  # Burn-in
# nChain <- 4  # gemtc defaults to 4 MCMC chains; no need to set
nIter <- 25000
thin <- 10
message(sprintf("Each MCMC chain will have %d samples.\nInferences will be based on a total of %d samples.",
                nIter / thin,
                4 * (nIter / thin)))
```

```
## Each MCMC chain will have 2500 samples.
## Inferences will be based on a total of 10000 samples.
```

Software version information.


```r
sessionInfo()
```

```
## R version 3.2.2 (2015-08-14)
## Platform: x86_64-w64-mingw32/x64 (64-bit)
## Running under: Windows 7 x64 (build 7601) Service Pack 1
## 
## locale:
## [1] LC_COLLATE=English_United States.1252 
## [2] LC_CTYPE=English_United States.1252   
## [3] LC_MONETARY=English_United States.1252
## [4] LC_NUMERIC=C                          
## [5] LC_TIME=English_United States.1252    
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
## [1] xtable_1.7-4        gemtc_0.7-1         coda_0.17-1        
## [4] data.table_1.9.6    openxlsx_3.0.0      RevoUtilsMath_3.2.2
## 
## loaded via a namespace (and not attached):
##  [1] Rcpp_0.12.1     lattice_0.20-33 digest_0.6.8    truncnorm_1.0-7
##  [5] plyr_1.8.3      grid_3.2.2      chron_2.3-47    meta_4.3-0     
##  [9] formatR_1.2     magrittr_1.5    evaluate_0.7.2  stringi_0.5-5  
## [13] rjags_4-5       rmarkdown_0.7   tools_3.2.2     stringr_1.0.0  
## [17] igraph_1.0.1    yaml_2.1.13     htmltools_0.2.6 knitr_1.11
```

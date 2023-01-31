Lab 04 - La Quinta is Spanish for next to Denny’s, Pt. 1
================
Heather Hawkins
01-31-23

### Load packages and data

``` r
library(tidyverse) 
library(dsbox) 
library(tidyverse)
library(skimr)
#install.packages("devtools")
#devtools::install_github("rstudio-education/dsbox")
```

``` r
library(readr)
states <- read_csv("data/states.csv")
```

### Exercise 1

``` r
nrow(dennys)
```

    ## [1] 1643

``` r
ncol(dennys)
```

    ## [1] 6

There are 1643 rows and 6 columns for the Denny’s data. The 6 rows
represent the address, city, state, zip code, longitude, and latitude,
while the rows represent each denny’s location.

### Exercise 2

``` r
nrow(laquinta)
```

    ## [1] 909

``` r
ncol(laquinta)
```

    ## [1] 6

There are 909 rows and 6 columns for the La Quinta data. The 6 rows
represent the address, city, state, zip code, longitude, and latitude,
while the rows represent each La Quinta location.

### Exercise 3

…

### Exercise 4

…

### Exercise 5

…

### Exercise 6

…

Add exercise headings as needed.

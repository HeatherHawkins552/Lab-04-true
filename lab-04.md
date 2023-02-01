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

Yes, La Quinta also has locations in Canada, Mexico, China, New
Zealand,Turkey, UAE, Chile, and Colombia.

Denny’s only has locations in the USA …

### Exercise 4

Filtering out locations that are not in the state data. If they are in
the US, they would be in the data set.

…

### Exercise 5

``` r
dennys %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 0 × 6
    ## # … with 6 variables: address <chr>, city <chr>, state <chr>, zip <chr>,
    ## #   longitude <dbl>, latitude <dbl>

None found, all Denny’s are in the US 5 \### Exercise 6

``` r
dennys %>% 
  mutate(country = "United States")
```

    ## # A tibble: 1,643 × 7
    ##    address                        city       state zip   longi…¹ latit…² country
    ##    <chr>                          <chr>      <chr> <chr>   <dbl>   <dbl> <chr>  
    ##  1 2900 Denali                    Anchorage  AK    99503  -150.     61.2 United…
    ##  2 3850 Debarr Road               Anchorage  AK    99508  -150.     61.2 United…
    ##  3 1929 Airport Way               Fairbanks  AK    99701  -148.     64.8 United…
    ##  4 230 Connector Dr               Auburn     AL    36849   -85.5    32.6 United…
    ##  5 224 Daniel Payne Drive N       Birmingham AL    35207   -86.8    33.6 United…
    ##  6 900 16th St S, Commons on Gree Birmingham AL    35294   -86.8    33.5 United…
    ##  7 5931 Alabama Highway, #157     Cullman    AL    35056   -86.9    34.2 United…
    ##  8 2190 Ross Clark Circle         Dothan     AL    36301   -85.4    31.2 United…
    ##  9 900 Tyson Rd                   Hope Hull… AL    36043   -86.4    32.2 United…
    ## 10 4874 University Drive          Huntsville AL    35816   -86.7    34.7 United…
    ## # … with 1,633 more rows, and abbreviated variable names ¹​longitude, ²​latitude

\###Exercise 7

14 La Quintas are outside of the usa.

``` r
laquinta %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 14 × 6
    ##    address                                     city  state zip   longi…¹ latit…²
    ##    <chr>                                       <chr> <chr> <chr>   <dbl>   <dbl>
    ##  1 Carretera Panamericana Sur KM 12            "\nA… AG    20345  -102.    21.8 
    ##  2 Av. Tulum Mza. 14 S.M. 4 Lote 2             "\nC… QR    77500   -86.8   21.2 
    ##  3 Ejercito Nacional 8211                      "Col… CH    32528  -106.    31.7 
    ##  4 Blvd. Aeropuerto 4001                       "Par… NL    66600  -100.    25.8 
    ##  5 Carrera 38 # 26-13 Avenida las Palmas con … "\nM… ANT   0500…   -75.6    6.22
    ##  6 AV. PINO SUAREZ No. 1001                    "Col… NL    64000  -100.    25.7 
    ##  7 Av. Fidel Velazquez #3000 Col. Central      "\nM… NL    64190  -100.    25.7 
    ##  8 63 King Street East                         "\nO… ON    L1H1…   -78.9   43.9 
    ##  9 Calle Las Torres-1 Colonia Reforma          "\nP… VE    93210   -97.4   20.6 
    ## 10 Blvd. Audi N. 3 Ciudad Modelo               "\nS… PU    75010   -97.8   19.2 
    ## 11 Ave. Zeta del Cochero No 407                "Col… PU    72810   -98.2   19.0 
    ## 12 Av. Benito Juarez 1230 B (Carretera 57) Co… "\nS… SL    78399  -101.    22.1 
    ## 13 Blvd. Fuerza Armadas                        "con… FM    11101   -87.2   14.1 
    ## 14 8640 Alexandra Rd                           "\nR… BC    V6X1…  -123.    49.2 
    ## # … with abbreviated variable names ¹​longitude, ²​latitude

Colombia (ANT) Mexico (VE, AG, CH, NL, PU, SLP, QR) Canada (ON, BC)
Honduras (FM)

\###Exercise 8

Adding country variable to the La Quinta dataset

``` r
laquinta <- laquinta %>%
  mutate(country = case_when(
    state %in% state.abb     ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    state == "ANT"           ~ "Colombia",
    state == "FM"      ~ "Honduras", 
    state %in% c("AG", "QR", "CH", "NL", "VE", "PU", "SL") ~ "Mexico"
  ))

laquinta <- laquinta %>%
  filter(country == "United States")
```

\###Exercise 9

``` r
dennys %>%
  dplyr::count(state) %>%
  inner_join(states, by = c("state" = "abbreviation"))
```

    ## # A tibble: 51 × 4
    ##    state     n name                     area
    ##    <chr> <int> <chr>                   <dbl>
    ##  1 AK        3 Alaska               665384. 
    ##  2 AL        7 Alabama               52420. 
    ##  3 AR        9 Arkansas              53179. 
    ##  4 AZ       83 Arizona              113990. 
    ##  5 CA      403 California           163695. 
    ##  6 CO       29 Colorado             104094. 
    ##  7 CT       12 Connecticut            5543. 
    ##  8 DC        2 District of Columbia     68.3
    ##  9 DE        1 Delaware               2489. 
    ## 10 FL      140 Florida               65758. 
    ## # … with 41 more rows

``` r
laquinta %>%
  dplyr::count(state) %>%
  inner_join(states, by = c("state" = "abbreviation"))
```

    ## # A tibble: 48 × 4
    ##    state     n name           area
    ##    <chr> <int> <chr>         <dbl>
    ##  1 AK        2 Alaska      665384.
    ##  2 AL       16 Alabama      52420.
    ##  3 AR       13 Arkansas     53179.
    ##  4 AZ       18 Arizona     113990.
    ##  5 CA       56 California  163695.
    ##  6 CO       27 Colorado    104094.
    ##  7 CT        6 Connecticut   5543.
    ##  8 FL       74 Florida      65758.
    ##  9 GA       41 Georgia      59425.
    ## 10 IA        4 Iowa         56273.
    ## # … with 38 more rows

Which states have the most and fewest Denny’s locations?

MOst= Califorina Least= Delaware

What about La Quinta? Most= Texas Least= Maine

Is this surprising? Why or why not?

\###Exercise 10

Which states have the most Denny’s locations per thousand square miles?
What about La Quinta? Next, we put the two datasets together into a
single data frame. However before we do so, we need to add an identifier
variable. We’ll call this establishment and set the value to “Denny’s”
and “La Quinta” for the dn and lq data frames, respectively.

dn \<- dn %\>% mutate(establishment = “Denny’s”) lq \<- lq %\>%
mutate(establishment = “La Quinta”) Because the two data frames have the
same columns, we can easily bind them with the bind_rows function:

dn_lq \<- bind_rows(dn, lq) We can plot the locations of the two
establishments using a scatter plot, and color the points by the
establishment type. Note that the latitude is plotted on the x-axis and
the longitude on the y-axis.

ggplot(dn_lq, mapping = aes(x = longitude, y = latitude, color =
establishment)) + geom_point() The following two questions ask you to
create visualizations. These visualizations should follow best practices
you learned in class, such as informative titles, axis labels, etc. See
<http://ggplot2.tidyverse.org/reference/labs.html> for help with the
syntax. You can also choose different themes to change the overall look
of your plots, see <http://ggplot2.tidyverse.org/reference/ggtheme.html>
for help with these.

\###Exercise 11

Filter the data for observations in North Carolina only, and recreate
the plot. You should also adjust the transparency of the points, by
setting the alpha level, so that it’s easier to see the overplotted
ones. Visually, does Mitch Hedberg’s joke appear to hold here?

\###Exercise 12

Now filter the data for observations in Texas only, and recreate the
plot, with an appropriate alpha level. Visually, does Mitch Hedberg’s
joke appear to hold here?

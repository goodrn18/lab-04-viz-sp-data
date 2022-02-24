Lab 04 - La Quinta is Spanish for next to Denny’s, Pt. 1
================
Rachel Good
2022-02-24

### Load packages and data

``` r
library(tidyverse) 
library(dsbox) 
```

``` r
states <- read_csv("data/states.csv")
```

### Exercise 1

Each row in the Denny’s dataset represents a restaurant location in the
US. The variables are: Address, City, State, Zip, Latitude, and
Longitude.

``` r
data("dennys")
nrow(dennys)
```

    ## [1] 1643

``` r
ncol(dennys)
```

    ## [1] 6

### Exercise 2

The rows and columns represent the same things as the dennys dataset in
which each row is a location. The column variables are the same.

``` r
data("laquinta")
nrow(laquinta)
```

    ## [1] 909

``` r
ncol(laquinta)
```

    ## [1] 6

### Exercise 3

There are no Denny’s locations outside the US. There are 2 Laquinta
locations in Canada, 6 in Mexico, 1 in China, 1 in New Zealand, 1 in
Honduras, 3 in Turkey, 1 in UAE, 1 in Chile, and 1 in Columbia - so 17
total locations outside the US.

### Exercise 4

We could potentially filter for State, but I am not sure how to filter
without having to list all 50 US State abbreviations, considering we
don’t know what was used for non-States without having to manually
search the data for State abbreviations we do not recognize.

Another idea would be to filter for locations above or below a certain
latitude.

### Exercise 5

There are no locations outside the US so filtering for state
abbreviations, gives us an empty tibble.

``` r
dennys %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 0 x 6
    ## # ... with 6 variables: address <chr>, city <chr>, state <chr>, zip <chr>,
    ## #   longitude <dbl>, latitude <dbl>

### Exercise 6

``` r
dennys %>%
  mutate(country = "United States")
```

    ## # A tibble: 1,643 x 7
    ##    address                        city    state zip   longitude latitude country
    ##    <chr>                          <chr>   <chr> <chr>     <dbl>    <dbl> <chr>  
    ##  1 2900 Denali                    Anchor~ AK    99503    -150.      61.2 United~
    ##  2 3850 Debarr Road               Anchor~ AK    99508    -150.      61.2 United~
    ##  3 1929 Airport Way               Fairba~ AK    99701    -148.      64.8 United~
    ##  4 230 Connector Dr               Auburn  AL    36849     -85.5     32.6 United~
    ##  5 224 Daniel Payne Drive N       Birmin~ AL    35207     -86.8     33.6 United~
    ##  6 900 16th St S, Commons on Gree Birmin~ AL    35294     -86.8     33.5 United~
    ##  7 5931 Alabama Highway, #157     Cullman AL    35056     -86.9     34.2 United~
    ##  8 2190 Ross Clark Circle         Dothan  AL    36301     -85.4     31.2 United~
    ##  9 900 Tyson Rd                   Hope H~ AL    36043     -86.4     32.2 United~
    ## 10 4874 University Drive          Huntsv~ AL    35816     -86.7     34.7 United~
    ## # ... with 1,633 more rows

### Exercise 7

As mentioned above: There are 2 Laquinta locations in Canada, 6 in
Mexico, 1 in China, 1 in New Zealand, 1 in Honduras, 3 in Turkey, 1 in
UAE, 1 in Chile, and 1 in Columbia. However, it looks like this data
does not include the locations in China, New Zealand, Turkey, or UAE.

### Exercise 8

``` r
laquinta %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 14 x 6
    ##    address                                  city  state zip   longitude latitude
    ##    <chr>                                    <chr> <chr> <chr>     <dbl>    <dbl>
    ##  1 Carretera Panamericana Sur KM 12         "\nA~ AG    20345    -102.     21.8 
    ##  2 Av. Tulum Mza. 14 S.M. 4 Lote 2          "\nC~ QR    77500     -86.8    21.2 
    ##  3 Ejercito Nacional 8211                   "Col~ CH    32528    -106.     31.7 
    ##  4 Blvd. Aeropuerto 4001                    "Par~ NL    66600    -100.     25.8 
    ##  5 Carrera 38 # 26-13 Avenida las Palmas c~ "\nM~ ANT   0500~     -75.6     6.22
    ##  6 AV. PINO SUAREZ No. 1001                 "Col~ NL    64000    -100.     25.7 
    ##  7 Av. Fidel Velazquez #3000 Col. Central   "\nM~ NL    64190    -100.     25.7 
    ##  8 63 King Street East                      "\nO~ ON    L1H1~     -78.9    43.9 
    ##  9 Calle Las Torres-1 Colonia Reforma       "\nP~ VE    93210     -97.4    20.6 
    ## 10 Blvd. Audi N. 3 Ciudad Modelo            "\nS~ PU    75010     -97.8    19.2 
    ## 11 Ave. Zeta del Cochero No 407             "Col~ PU    72810     -98.2    19.0 
    ## 12 Av. Benito Juarez 1230 B (Carretera 57)~ "\nS~ SL    78399    -101.     22.1 
    ## 13 Blvd. Fuerza Armadas                     "con~ FM    11101     -87.2    14.1 
    ## 14 8640 Alexandra Rd                        "\nR~ BC    V6X1~    -123.     49.2

``` r
laquinta %>%
  mutate(country = case_when(
    state %in% state.abb     ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    state == "ANT"           ~ "Colombia",
    state == "CH"            ~ "Chile", #check this one
    state %in% c("AG", "QR", "NL", "VE", "SL", "PU") ~ "Mexico",
    state == "FM"            ~ "Honduras"))
```

    ## # A tibble: 909 x 7
    ##    address                          city  state zip   longitude latitude country
    ##    <chr>                            <chr> <chr> <chr>     <dbl>    <dbl> <chr>  
    ##  1 793 W. Bel Air Avenue            "\nA~ MD    21001     -76.2     39.5 United~
    ##  2 3018 CatClaw Dr                  "\nA~ TX    79606     -99.8     32.4 United~
    ##  3 3501 West Lake Rd                "\nA~ TX    79601     -99.7     32.5 United~
    ##  4 184 North Point Way              "\nA~ GA    30102     -84.7     34.1 United~
    ##  5 2828 East Arlington Street       "\nA~ OK    74820     -96.6     34.8 United~
    ##  6 14925 Landmark Blvd              "\nA~ TX    75254     -96.8     33.0 United~
    ##  7 Carretera Panamericana Sur KM 12 "\nA~ AG    20345    -102.      21.8 Mexico 
    ##  8 909 East Frontage Rd             "\nA~ TX    78516     -98.1     26.2 United~
    ##  9 2116 Yale Blvd Southeast         "\nA~ NM    87106    -107.      35.1 United~
    ## 10 7439 Pan American Fwy Northeast  "\nA~ NM    87109    -107.      35.2 United~
    ## # ... with 899 more rows

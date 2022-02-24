Lab 04 - La Quinta is Spanish for next to Denny’s, Pt. 1
================
Rachel Good
2022-02-23

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

…

### Exercise 4

…

### Exercise 5

…

### Exercise 6

…

Add exercise headings as needed.

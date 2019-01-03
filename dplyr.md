
``` r
library(magrittr)
```

``` r
a <- "C:/Users/chase/Documents/old_dplyr"
b <- "C:/Users/chase/Documents/new_dplyr"
```

``` r
devtools::install_github("tidyverse/dplyr@v0.7.4.9005", 
                         lib = a, 
                         force = T)


devtools::install_github("tidyverse/dplyr@f0993bb", 
                         lib = b, 
                         force = T)
```

New first:

``` r
library("dplyr",
        lib.loc = b,
        warn.conflicts = FALSE)

sessionInfo()$otherPkgs$dplyr$Version
```

    ## [1] "0.8.0.9000"

``` r
z1 <- tibble(
  x = 1:3, 
  f = factor(c("Animal_1", "Animal_2", "Animal_2"), levels = c("Animal_1", "Animal_2", "Animal_3"))
)

z2 <- group_by(z1, f)

z3 <- dplyr::summarise(z2, count_animals = dplyr::n() )
z3
```

    ## # A tibble: 3 x 2
    ##   f        count_animals
    ##   <fct>            <int>
    ## 1 Animal_1             1
    ## 2 Animal_2             2
    ## 3 Animal_3             0

``` r
z4 <- z3$count_animals
try(names(z4) <- levels(z1$f))
z4
```

    ## Animal_1 Animal_2 Animal_3 
    ##        1        2        0

``` r
detach("package:dplyr", unload=TRUE)
```

Old second

``` r
library("dplyr",
        lib.loc = a,
        warn.conflicts = FALSE)

sessionInfo()$otherPkgs$dplyr$Version
```

    ## [1] "0.7.4.9005"

``` r
z1 <- tibble(
  x = 1:3, 
  f = factor(c("Animal_1", "Animal_2", "Animal_2"), levels = c("Animal_1", "Animal_2", "Animal_3"))
)

z2 <- group_by(z1, f)

z3 <- dplyr::summarise(z2, count_animals = dplyr::n() )
z3
```

    ## # A tibble: 2 x 2
    ##   f        count_animals
    ##   <fct>            <int>
    ## 1 Animal_1             1
    ## 2 Animal_2             2

``` r
z4 <- z3$count_animals
try(names(z4) <- levels(z1$f))
z4
```

    ## [1] 1 2

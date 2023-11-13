writing_functions
================
Shina Min
2023-11-11

## Do soemthing simple

``` r
x_vec = rnorm(30, mean = 5, sd = 3)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1]  0.356823969  0.817828510 -0.449120492 -0.532213321  0.007126837
    ##  [6]  0.747310525 -2.315743677  2.010278399  1.273937605  1.748657492
    ## [11] -0.843755993  1.644435294  0.345575844 -2.097457433  0.431194605
    ## [16] -0.662445775 -0.266727989  0.041451083 -0.582429793  0.074997233
    ## [21] -0.167095837  0.002250343 -0.466861860 -0.297921631 -0.592215248
    ## [26] -0.551574056  1.253525655 -1.166915272 -0.153216755  0.390301738

I want a function to compute z-scores

``` r
z_scores = function(x) {
  
  if(!is.numeric(x)) {
    stop("Input must be numeric")
  }
  
  if(length(x) < 3) {
    stop("Input must have a least three numbers")
  }
  
  z = (x - mean(x)) / sd(x)
  z
  
}

z_scores(x_vec)
```

    ##  [1]  0.356823969  0.817828510 -0.449120492 -0.532213321  0.007126837
    ##  [6]  0.747310525 -2.315743677  2.010278399  1.273937605  1.748657492
    ## [11] -0.843755993  1.644435294  0.345575844 -2.097457433  0.431194605
    ## [16] -0.662445775 -0.266727989  0.041451083 -0.582429793  0.074997233
    ## [21] -0.167095837  0.002250343 -0.466861860 -0.297921631 -0.592215248
    ## [26] -0.551574056  1.253525655 -1.166915272 -0.153216755  0.390301738

Try my function on some other things. These should give errors

``` r
z_scores(3)
```

    ## Error in z_scores(3): Input must have a least three numbers

``` r
z_scores("my name is Shina")
```

    ## Error in z_scores("my name is Shina"): Input must be numeric

``` r
z_scores(mtcars)
```

    ## Error in z_scores(mtcars): Input must be numeric

``` r
z_scores(c(TRUE, TRUE, FALSE, TRUE))
```

    ## Error in z_scores(c(TRUE, TRUE, FALSE, TRUE)): Input must be numeric

## Multiple outputs

``` r
mean_and_sd = function(x) {
  
  if (!is.numeric(x)) {
    stop("Argument x should be numeric")
  } else if (length(x) == 1) {
    stop("Cannot be computed for length 1 vectors")
  }
  
  mean_x = mean(x)
  sd_x = sd(x)

  list(mean = mean_x, 
       sd = sd_x)
}
```

check that the function works.

``` r
x_vec = rnorm(100, mean = 3, sd = 4)
mean_and_sd(x_vec)
```

    ## $mean
    ## [1] 3.169987
    ## 
    ## $sd
    ## [1] 3.940107

## Multiple inputs

I’d like to do this with a function

``` r
sim_data = tibble(
  x = rnorm(n = 100, mean = 2, sd = 3)
)

sim_data %>%
  summarize(
    mean = mean(x),
    sd = sd(x)
  )
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.02  2.48

``` r
sim_mean_sd = function(samp_size, mu = 3, sigma = 4) {
  
  sim_data = 
   tibble(
    x = rnorm(n = samp_size, mean = mu, sd = sigma)
)

sim_data %>%
  summarize(
    mean = mean(x),
    sd = sd(x)
  )
}

sim_mean_sd(samp_size = 100, mu = 6, sigma = 3)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  6.05  3.19

``` r
sim_mean_sd(samp_size = 100)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.27  4.32

## Let’s review Napoleon Dynamite

``` r
fellowship_ring = readxl::read_excel("./LotR_Words.xlsx", range = "B3:D6") |>
  mutate(movie = "fellowship_ring")

two_towers = readxl::read_excel("./LotR_Words.xlsx", range = "F3:H6") |>
  mutate(movie = "two_towers")

return_king = readxl::read_excel("./LotR_Words.xlsx", range = "J3:L6") |>
  mutate(movie = "return_king")

lotr_tidy = bind_rows(fellowship_ring, two_towers, return_king) |>
  janitor::clean_names() |>
  pivot_longer(
    female:male,
    names_to = "sex",
    values_to = "words") |> 
  mutate(race = str_to_lower(race)) |> 
  select(movie, everything())
```

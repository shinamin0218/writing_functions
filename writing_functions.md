writing_functions
================
Shina Min
2023-11-11

## Do soemthing simple

``` r
x_vec = rnorm(30, mean = 5, sd = 3)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1]  0.80250221 -0.56000458  1.18474046  2.42269020  0.08130757  0.45937307
    ##  [7] -1.02997729 -0.20324314  0.09130003 -0.85384282  0.73372496 -2.03609811
    ## [13] -0.53238790  1.21231890  1.46651553 -0.33062181 -0.32468882  0.24075149
    ## [19]  0.83023346 -1.52054864  0.16212885 -0.86218780 -1.13767223 -0.84418381
    ## [25]  0.99362009 -0.81108155  0.61943010  0.95597271 -0.15849184 -1.05157929

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

    ##  [1]  0.80250221 -0.56000458  1.18474046  2.42269020  0.08130757  0.45937307
    ##  [7] -1.02997729 -0.20324314  0.09130003 -0.85384282  0.73372496 -2.03609811
    ## [13] -0.53238790  1.21231890  1.46651553 -0.33062181 -0.32468882  0.24075149
    ## [19]  0.83023346 -1.52054864  0.16212885 -0.86218780 -1.13767223 -0.84418381
    ## [25]  0.99362009 -0.81108155  0.61943010  0.95597271 -0.15849184 -1.05157929

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
    ## [1] 3.077015
    ## 
    ## $sd
    ## [1] 3.75385

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
    ## 1  2.19  2.83

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
    ## 1  5.38  3.31

``` r
sim_mean_sd(samp_size = 100)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.16  3.94

writing_functions
================
Shina Min
2023-11-11

## Do soemthing simple

``` r
x_vec = rnorm(30, mean = 5, sd = 3)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1] -0.25008854  1.61212147 -1.55989250  2.11895411  0.17710089  0.16890039
    ##  [7] -0.27118072  0.20518909  0.35641922 -1.43518676 -0.61267497  0.45081820
    ## [13]  0.98120147 -1.45615001  1.29477260 -1.01358693  1.17995786  0.16014858
    ## [19]  0.05426893 -0.11032277 -1.55176574  0.11314562 -0.49054509  0.27842699
    ## [25] -0.20980554 -0.58270015 -0.38302457  2.00067730  0.17224280 -1.39742122

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

    ##  [1] -0.25008854  1.61212147 -1.55989250  2.11895411  0.17710089  0.16890039
    ##  [7] -0.27118072  0.20518909  0.35641922 -1.43518676 -0.61267497  0.45081820
    ## [13]  0.98120147 -1.45615001  1.29477260 -1.01358693  1.17995786  0.16014858
    ## [19]  0.05426893 -0.11032277 -1.55176574  0.11314562 -0.49054509  0.27842699
    ## [25] -0.20980554 -0.58270015 -0.38302457  2.00067730  0.17224280 -1.39742122

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

# Expected Total Number of Runs

Computes the exact expected total run count for mutually independent
Bernoulli trials whose success probabilities may vary by position.

## Usage

``` r
runs_mean(prob)
```

## Arguments

- prob:

  A non-empty numeric vector. Its `i`th element is the success
  probability of the `i`th Bernoulli trial and must be finite and in the
  closed interval `[0, 1]`.

## Value

A scalar double giving the expected number of runs.

## Details

The expectation is one plus the sum of the probabilities that successive
observations differ. It is conditional on the supplied probabilities and
the mutual-independence assumption.

## Examples

``` r
runs_mean(c(0.15, 0.40, 0.75, 0.60))
```

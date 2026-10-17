# Exact Distribution of the Total Run Count

Computes the exact probability mass and cumulative distribution of the
total number of runs in mutually independent Bernoulli trials. The
trials need not have a common success probability. The supplied
probabilities are treated as fixed and known; this function performs no
estimation.

## Usage

``` r
runs_distribution(prob)
```

## Arguments

- prob:

  A non-empty numeric vector. Its `i`th element is the success
  probability of the `i`th Bernoulli trial and must be finite and in the
  closed interval `[0, 1]`.

## Value

A data frame with one row for every possible run count and columns:

- `runs`:

  The possible total run counts from 1 to `length(prob)`.

- `probability`:

  The exact probability mass at each run count.

- `cumulative`:

  The inclusive lower cumulative probability.

## Details

The calculation uses a finite-state dynamic program indexed by the
number of observations processed, the current run count, and the last
binary value. Its time complexity is quadratic and its working memory is
linear in `length(prob)`.

## References

Fu, J. C. and Koutras, M. V. (1994). Distribution theory of runs: A
Markov chain approach. *Journal of the American Statistical
Association*, 89(427), 1050–1058.
[doi:10.1080/01621459.1994.10476841](https://doi.org/10.1080/01621459.1994.10476841)
.

## Examples

``` r
runs_distribution(c(0.15, 0.40, 0.75, 0.60))
```

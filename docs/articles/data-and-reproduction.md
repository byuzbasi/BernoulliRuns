# Inputs, reproducibility and scope

## Input dictionary

| Input | Meaning | Contract |
|:---|:---|:---|
| `prob` | Supplied success probabilities in sequence order | Non-empty numeric vector, finite values in \[0,1\] |
| `x` | Observed binary sequence | Zeros and ones in the same order as `prob` |
| `tail` | Inclusive one-sided probability | `"lower"` or `"upper"`, not a two-sided test |

The four exported functions are described in the [exact-distribution
guide](https://byuzbasi.github.io/BernoulliRuns/articles/exact-run-count-distribution.md).
No external dataset is needed: the small example uses supplied
probabilities.

## A deterministic reproducibility check

This four-position example is a numerical identity check, not a
simulation study.

``` r

library(BernoulliRuns)
prob <- c(.15, .40, .75, .60)
dist <- runs_distribution(prob)
stopifnot(abs(sum(dist$probability) - 1) < 1e-12)
stopifnot(abs(sum(dist$runs * dist$probability) - runs_mean(prob)) < 1e-12)
count_runs(c(0, 1, 1, 0))
```

    ## [1] 3

Record the package version with `packageVersion("BernoulliRuns")` and
the R environment with
[`sessionInfo()`](https://rdrr.io/r/utils/sessionInfo.html). Exact
refers to the model’s run-count distribution, subject to floating-point
arithmetic, not to guaranteed test calibration after estimating
probabilities from these same observations.

## Scientific and publication boundary

The trials must be mutually independent and their probabilities treated
as fixed. Longest runs, dependent sequences, estimated-probability
calibration and two-sided p-values are outside the public API.

Use `citation("BernoulliRuns")` to cite the software. The underlying
finite-state approach is credited to Fu and Koutras (1994), [DOI:
10.1080/01621459.1994.10476841](https://doi.org/10.1080/01621459.1994.10476841).
That reference is not a new paper by the package author.

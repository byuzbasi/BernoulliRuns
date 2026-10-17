# Exact Run-Count Distributions

## Model and assumptions

Let X_1,\ldots,X_n denote a non-empty ordered sequence of mutually
independent Bernoulli variables. At position i, the supplied number
p_i=P(X_i=1) is finite and belongs to \[0,1\]. The probabilities may
differ across positions and are treated as fixed inputs; the package
does not estimate them.

A run is a maximal consecutive block of equal values. Consequently, the
total run count R_n is one for the first block plus one for every change
between adjacent observations:

R_n=1+\sum\_{i=2}^{n}\mathbf{1}(X_i\ne X\_{i-1}).

Here \mathbf{1}(\cdot) equals one when its statement is true and zero
otherwise. This expression defines the package’s random variable and is
valid for non-empty binary sequences.

## Exact distribution

For a vector of position-specific probabilities,
[`runs_distribution()`](https://byuzbasi.github.io/BernoulliRuns/reference/runs_distribution.md)
returns every possible value of R_n, its exact probability mass, and its
inclusive lower cumulative probability.

``` r

library(BernoulliRuns)

prob <- c(0.15, 0.40, 0.75, 0.60)
distribution <- runs_distribution(prob)
knitr::kable(
  distribution,
  digits = 6,
  caption = "Exact distribution of the total run count"
)
```

| runs | probability | cumulative |
|-----:|------------:|-----------:|
|    1 |       0.078 |      0.078 |
|    2 |       0.492 |      0.570 |
|    3 |       0.352 |      0.922 |
|    4 |       0.078 |      1.000 |

Exact distribution of the total run count

The computation tracks the probability of each current run count
separately for sequences ending in zero and one. At the next position,
retaining the last value continues a run, whereas changing it opens a
new run. Mutual independence justifies multiplying each previous state
probability by p_i or 1-p_i. The procedure uses quadratic time and
linear working memory in the sequence length n.

The expectation can be calculated without first forming the full
distribution. It is one plus the sum, over adjacent positions, of the
two possible change probabilities:

E(R_n)=1+\sum\_{i=2}^{n} \\p\_{i-1}(1-p_i)+(1-p\_{i-1})p_i\\.

The two terms inside braces are respectively the probabilities of a
change from one to zero and from zero to one. The formula relies on the
same mutual- independence and fixed-probability assumptions.

``` r

runs_mean(prob)
#> [1] 2.43
sum(distribution$runs * distribution$probability)
#> [1] 2.43
```

## Observed sequence and one-sided tails

For an observed binary sequence,
[`count_runs()`](https://byuzbasi.github.io/BernoulliRuns/reference/count_runs.md)
evaluates the same run-count definition.
[`runs_tail()`](https://byuzbasi.github.io/BernoulliRuns/reference/runs_tail.md)
then calculates an inclusive lower probability P(R_n\le r\_{obs}) or
inclusive upper probability P(R_n\ge r\_{obs}), where r\_{obs} denotes
the observed number of runs.

``` r

x <- c(0, 1, 1, 0)
count_runs(x)
#> [1] 3
runs_tail(x, prob, tail = "lower")
#> 
#> Exact run-count distribution for independent Bernoulli trials
#> 
#> number of runs = 3 
#> p-value = 0.922 
#> alternative hypothesis: lower one-sided tail
runs_tail(x, prob, tail = "upper")
#> 
#> Exact run-count distribution for independent Bernoulli trials
#> 
#> number of runs = 3 
#> p-value = 0.43 
#> alternative hypothesis: upper one-sided tail
```

These are conditional probabilities under the supplied model. If the
same observations were used to estimate `prob`, a tail probability is
not automatically a calibrated exact test. The package intentionally
does not combine the two tails into a two-sided p-value and does not
model dependent or Markov sequences.

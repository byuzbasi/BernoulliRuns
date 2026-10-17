# Exact One-Sided Tail Probability for the Run Count

Computes the inclusive lower or upper tail probability of the observed
run count under mutually independent Bernoulli trials with fixed,
supplied success probabilities.

## Usage

``` r
runs_tail(x, prob, tail = c("lower", "upper"))
```

## Arguments

- x:

  A non-empty logical or numeric vector containing only zeroes and ones.
  It is the observed binary sequence.

- prob:

  A numeric vector of the same length as `x`. Its `i`th element is the
  success probability of the `i`th trial and must lie in `[0, 1]`.

- tail:

  A character string selecting the inclusive `"lower"` tail, \\P(R \le
  r\_{obs})\\, or inclusive `"upper"` tail, \\P(R \ge r\_{obs})\\.
  Partial matching follows
  [`match.arg()`](https://rdrr.io/r/base/match.arg.html).

## Value

An object of class `runs_exact_tail`, a list with components
`statistic`, `p.value`, `alternative`, `method`, and `probabilities`.

## Details

The result is a conditional probability under the supplied model. If
`prob` was estimated from the same observations, the result is not by
itself a calibrated exact test. The observed point is included in either
tail. The package deliberately does not define a two-sided p-value.

## Examples

``` r
x <- c(0, 1, 1, 0)
prob <- c(0.15, 0.40, 0.75, 0.60)
runs_tail(x, prob, tail = "upper")
```

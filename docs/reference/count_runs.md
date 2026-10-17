# Count Runs in a Binary Sequence

Counts maximal consecutive blocks of equal values in a non-empty binary
sequence. For example, `00110` contains the runs `00`, `11`, and `0`.

## Usage

``` r
count_runs(x)
```

## Arguments

- x:

  A non-empty logical or numeric vector containing only zeroes and ones.
  Missing and non-finite values are not allowed.

## Value

A scalar integer giving the number of runs in `x`.

## Examples

``` r
count_runs(c(0, 0, 1, 1, 0))
```

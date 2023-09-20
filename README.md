[[_TOC_]]

# Initialization
## c() function
### Numeric vectors
```r
vec <- c(1.5, 2, -1)    # numeric vector of length 3
str(vec)                # num [1:3] 1.5 2 -1
```

General signature is `num [1:n]` for vector of length $n$. 

### Character vectors
```r
letters <- c("x", "y", "z") # character vector of length 3
str(letters)                # chr [1:3] "x" "y" "z"
```

**R** always converts the output of `c()` operator with different data types as arguments to character vectors.

```r
test <- c(TRUE, "a", 35)    # different data types
str(test)                   # chr [1:3] "TRUE" "a" "35"
```

### Logical vectors

```r
logical <- c(TRUE, FALSE, !TRUE, !FALSE)    # '!' denotes logical NOT
str(logical)                                # logi [1:4] TRUE FALSE FALSE TRUE
```

Logical vectors can be used as a mask to filter other vectors.

```r
pos_neg <- c(-2, -1, 1, 2)          # num [1:4] -2 -1 1 2
str(pos_neg > 0)                    # logi [1:4] FALSE FALSE TRUE TRUE
pos_only <- pos_neg[pos_neg > 0]    # filtering pos_neg vector
str(pos_only)                       # num [1:2] 1 2
```

### Concatenation

This is the most general way to describe of what `c()` does in **R**.

```r
a <- c(1, 2, 3)     # num [1:3] 1 2 3
b <- c(3, 4, 5)     # num [1:3] 3 4 5
str(c(a, b))        # num [1:6] 1 2 3 3 4 5
```

## seq() function
Sequence.
```r
rng <- seq(0, 1, 0.2)   # sequence from 0 to 1 with 0.2 step
str(rng)                # num [1:6] 0 0.2 0.4 0.6 0.8 1
```

## rep() function
Repetition.
```r
bottles <- rep("bottle", 99)    # 99 bottles of beer
str(bottles)                    # chr [1:99] "bottle" "bottle" "bottle" "bottle" "bottle" "bottle" "bottle" ...
```

# Sampling
## Sampling from vectors
### Sampling with replacement

In this example we throw two fair $6$-sided dice.

```r
die <- seq(1, 6)
sample(die, 2, replace=TRUE)
```

### Sampling without replacement

Let's choose two colors out of three.

```r
colors <- c("red", "green", "blue")
sample(colors, 2)                   #  "red"  "blue"
```

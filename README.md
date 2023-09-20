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

## Sampling from distributions
### Table of distributions available
| Distribution          | Code          | Parameters    |
| -----------           | -----------   | -----------   |
| Beta                  | `beta`        |               |
| Binomial              | `binom`       |               |
| Cauchy                | `cauchy`      |               |
| Chi-Square            | `chisq`       |               |
| Exponential           | `exp`         |               |
| F                     | `f`           |               |
| Gamma                 | `gamma`       |               | 
| Geometric             | `geom`        |               | 
| Hypergeometric        | `hyper`       |               | 
| Logistic              | `logis`       |               | 
| Log Normal            | `lnorm`       |               | 
| Negative Binomial     | `nbinom`      |               | 
| Normal                | `norm`        |               | 
| Poisson               | `pois`        |               | 
| Student t-distribution| `t`           |               | 
| Uniform               | `unif`        |               | 
| Weibull               | `weibull`     |               | 

### Table of function prefixes
| Function                  | Prefix        |
| -----------               | -----------   |
| CDF (**p**robability)     | `p`           |
| PDF, PMF (**d**ensity)    | `d`           |
| **q**uantile              | `q`           |
| **r**andom sample         | `r`           |

### Discrete distribution example

```r
k <- seq(0, 2)
binom_pmf <- dbinom(k, 2, 0.5)  # PMF evaluated in points defined in vector k
plot(k, binom_pmf, type='h')
points(k, binom_pmf)
```

```r
samples <- rbinom(1000, 2, 0.5)     # The first argument is the number of samples, and the rest are parameters of the distribution
print(sum(samples == 0) / 1000)     # 0.257
print(sum(samples == 1) / 1000)     # 0.518
print(sum(samples == 2) / 1000)     # 0.225
```

### Continuous distribution example

```r
x <- seq(-3, 3, 0.01)
normal_pdf <- dnorm(x, 0, 1)
plot(x, normal_pdf, type='l')
```

```r
hist(rnorm(1000, 0, 1))
```

# Control

## replicate()

`replicate()` allows us to repeatedly evaluate some expression in **R** certain number of times and it stores the results in the array.    

Assume that the urn contains $7$ balls: $x$ red and $y$ black.In each trial of the experiment we're allowed to take two balls from the urn, and we can have as many trials as we need. The goal is to derive the probability of drawing one red followed by one black ball.
```r
x <- sample(seq(1,7), 1)                                                    # the number of red balls
y <- 7 - x                                                                  # the number of black balls
balls <- c(rep("red", x), rep("black", y))                                  # defining the urn
test <- replicate(10000, sample(balls, 2))                                  # 10000 trials, the results are stored in chr [1:2, 1:10000]
estimation <- sum((test[1,] == "red") & (test[2,] == "black")) / 10000      # checking how many times the condition is satisfied
print(estimation)                                                           # 0.2396
true_value <- (x/7)*(y/6)                                                   # Naive probability
print(true_value)                                                           # 0.2380952
```
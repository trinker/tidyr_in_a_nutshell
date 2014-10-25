tidyr In a Nutshell
===

This is a minimal guide, mostly for myself, to remind me of the most import tidyr functions and how they relate to **reshape2** functions that I'm familiar with. Also checkout [dplyr In a Nutshell](https://github.com/trinker/dplyr_in_a_nutshell)



# 2  Main Functions

List of dplyr functions and the base functions they're related to:

reshape2 Function    | tidyr Function(s) | Special Powers
---------------------|-------------------|----------------------------
`melt`               |  `gather`         | long format\*
`dcast`              |  `spread`         | wide format\*


\*[Hadley notes](http://vita.had.co.nz/papers/tidy-data.pdf) these terms are imprecise but good enough for my little noodle

## Arguments (when chaining)

![](tidyr.png)


# Demos
### Some Data

```r
library(tidyr); library(dplyr)

dat <- data.frame(
   id = LETTERS[1:5],
   x = sample(0:1, 5, TRUE),
   y = sample(0:1, 5, TRUE),
   z = sample(0:1, 5, TRUE)
)

dat
```

```
  id x y z
1  A 1 1 1
2  B 0 0 1
3  C 1 1 0
4  D 1 1 1
5  E 1 1 1
```

### gather in Action


```r
dat %>% gather(item, scores, -c(id))
```

```
   id item scores
1   A    x      1
2   B    x      0
3   C    x      1
4   D    x      1
5   E    x      1
6   A    y      1
7   B    y      0
8   C    y      1
9   D    y      1
10  E    y      1
11  A    z      1
12  B    z      1
13  C    z      0
14  D    z      1
15  E    z      1
```

### spread it Back Out


```r
dat %>% gather(item, scores, -c(id)) %>%
    spread(item, scores)
```

```
  id x y z
1  A 1 1 1
2  B 0 0 1
3  C 1 1 0
4  D 1 1 1
5  E 1 1 1
```

---

# Additional Demos

### gather


```r
dat %>% gather(item, scores, x:z) 
```

```
   id item scores
1   A    x      1
2   B    x      0
3   C    x      1
4   D    x      1
5   E    x      1
6   A    y      1
7   B    y      0
8   C    y      1
9   D    y      1
10  E    y      1
11  A    z      1
12  B    z      1
13  C    z      0
14  D    z      1
15  E    z      1
```

```r
dat %>% gather(item, scores, x, y, z) 
```

```
   id item scores
1   A    x      1
2   B    x      0
3   C    x      1
4   D    x      1
5   E    x      1
6   A    y      1
7   B    y      0
8   C    y      1
9   D    y      1
10  E    y      1
11  A    z      1
12  B    z      1
13  C    z      0
14  D    z      1
15  E    z      1
```

### spread


```r
dat %>% gather(item, scores, -c(id)) %>%
    spread(item, scores)
```

```
  id x y z
1  A 1 1 1
2  B 0 0 1
3  C 1 1 0
4  D 1 1 1
5  E 1 1 1
```

```r
dat %>% gather(item, scores, -c(id)) %>%
    spread(id, scores)
```

```
  item A B C D E
1    x 1 0 1 1 1
2    y 1 0 1 1 1
3    z 1 1 0 1 1
```




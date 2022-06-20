Writing Scientific Reports
================
Stefano Politi
(20 juin 2022)

-   [Creating a bullet list](#creating-a-bullet-list)
-   [Inserting a picture](#inserting-a-picture)
-   [Adding R code blocks](#adding-r-code-blocks)
-   [References](#references)

## Creating a bullet list

**Un-ordered bullet list**:

-   Item 1
    -   *Sub-item 1.1*
    -   *Sub-item 1.2*
-   Item 2
    -   *Sub-item 2.1*
    -   *Sub-item 2.2*

**Ordered list**:

1.  Item 1

<!-- -->

1.  *Sub-item 1.1*
2.  *Sub-item 1.2*

<!-- -->

2.  Item 2

<!-- -->

1.  *Sub-item 2.1*
2.  *Sub-item 2.2*

## Inserting a picture

![](RStudio_icon.png)

## Adding R code blocks

``` r
library(knitr)
library(dslabs)
data("stars")
kable(head(stars))
```

| star           | magnitude | temp | type |
|:---------------|----------:|-----:|:-----|
| Sun            |       4.8 | 5840 | G    |
| SiriusA        |       1.4 | 9620 | A    |
| Canopus        |      -3.1 | 7400 | F    |
| Arcturus       |      -0.4 | 4590 | K    |
| AlphaCentauriA |       4.3 | 5840 | G    |
| Vega           |       0.5 | 9900 | A    |

## References

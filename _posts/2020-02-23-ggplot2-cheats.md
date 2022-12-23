---
layout: posts
title: ggplot2 Tips and Tricks
# author: littleheron
date : 2020-02-22
lang: en
lang-ref: ggplot2-cheats
# categories: R reference, tidyverse
---

> "ggplot2 is a system for declaratively creating graphics, based on The Grammar of Graphics. You provide the data, tell ggplot2 how to map variables to aesthetics, what graphical primitives to use, and it takes care of the details." - (The overview of ggplot2, from tidyverse)

ggplot2 is one of the most popular data visualization library for R. It makes creating informative and elegant plots in R fairly easy, though the way its syntax is structured may need some getting used to for those more accustomed in base R.

Though easy enough to understand the basics, I found it difficult to remember some of the customizations that I use semi-frequently and always had to look up the manual or google them again when I needed. So I compiled some of them into one post here to use as a personal cheatsheet of sort.

## Basic syntax

The syntax works like this: you provide a data frame(tibbles and data tables work too) and aesthetic mapping. Then add on `geom` layers or provide custom scaling, axis, labels, etc.

```r
# scatter plot
ggplot(data=diamonds, aes(x=carat, y=price, colour=clarity)) + geom_point()

# boxplot
ggplot(data=diamonds, aes(x=carat, y=price, colour=clarity)) + geom_boxplot()
```

Full list of available geoms is in the cheatsheets provided [here](https://ggplot2.tidyverse.org/). There are also a number of ggplot2 tutorial posts in the web that can be found with a simple google search. 

### Base plot

```r
p = ggplot(data=diamonds, aes(x=carat, y=price, colour=clarity)) + geom_point()
p
```

Another nice thing about ggplot2 is that you can save a base plot into a variable, and then add layers on the variable to draw multiple versions of the plot with the same data mapping. This is especially useful when experimenting with different themes.


## Legends and Axis

### Reverse legend order

```r
p + guides(fill = guide_legend(reverse = TRUE))
```

### Removing legends

```r
p + theme(legend.position='none')
p + geom_text(show.legend=FALSE)
```

### Axis label remove

```r
p + theme(axis.title.x = element_blank())
```

### Axis label rotation

```r
x=90
y=45
p + theme(
  	axis.text.x = element_text(angle = x, hjust = 1),
	axis.text.y = element_text(angle = y, vjust = 1))

```


## Discrete Scales

### Default ggplot colours

```r
library(scales)
show_col(hue_pal()(4))
ggpal = hue_pal()(4)
```

## Multiple plots

### facet_grids

```r
p + facet_grid(.~group1)
p + facet_wrap(~group1)
```

### Using `gridExtra` package

```r
library(gridExtra)
p1
p2
p3

grid.arrange(p1, p2, p3, p4, ncol=2)
```

Custom grid arrange for more complexity

```r
grid.arrange(p1, p2, p3, p4, ncol=2, widths=c(2,1))
```

[grid image]

grid.arrange can also be used with `do.call` for a list of plots, useful when plots are created in a loop.

```r
gpls <- list(p1,p2,p3,p4)
do.call(gpls, grid.arrange)
```

Using `do.call` with arguments:

```r
input_list <- c(gpls, list(ncol=2, widths=c(2,1)))
do.call(input_list, grid.arrange)
```

[img]


## Themes!

### Built in themes

- `theme_bw()` : a clean black/white grid
- `theme_minimal()` : Minimal theme
- `theme_void()` : remove everything (axis, title...)

Set theme default

```r
theme_set(theme_bw())
theme_get()
```

### Mimic base R plot legend

```r
p + theme(
	legend.position = c(1,1), legend.justification = c(1,1),
	legend.background = element_rect(fill=NA, linetype='solid', color='grey45'),
	legend.key = element_rect(fill=NA, linetype='blank'))

```

`ggthemer` : ggplot2 theme package 


## vs Base R plot

**ggplot2 is...**

* Good for visually pleasing plots with multiple annotations and legends
* Easy to customize theme elements such as axis, colour scale, etc.
* Part of the tidyverse package and comes with its advantages like code readability.

**Base R is**

* Better suited for quickly creating simple plots with less typing.
* Input data can be a matrix or vector depending on the type of plot.
* May be easier to draw multiple types of plots in a single panel with `layout`.


---

#### References

* https://www.datanovia.com/en/blog/how-to-remove-legend-from-a-ggplot/
* https://www.shanelynn.ie/themes-and-colours-for-r-ggplots-with-ggthemr/


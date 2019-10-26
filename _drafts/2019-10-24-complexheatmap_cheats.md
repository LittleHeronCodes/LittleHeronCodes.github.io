---
layout: post
title:  ComplexHeatmap Cheats and Reference list
author: littleheron
date:   2019-10-21
categories: R reference
---


# ComplexHeatmap Cheats and Reference list

(If possible, add table of contents)

(Add Intro here.)

Pros: 

* Created with genomic data analysis in mind.
* Customability.
* Only heatmap package to allow parallel heatmap plotting. (closest I found before was ggplot2)
* Wide variety of possible annotations. (That thing you wanted to do for heatmap? You could probably do it.)

Cons:

* Difficult to master.
* Saving is a pain. (Then again, what isn't?)


Full reference manual : https://jokergoo.github.io/ComplexHeatmap-reference/book/index.html


---

## Dataset preparation

For the purpose of the post, we will use [DATA] 



## Basic plotting

```r
library(ComplexHeatmap)
library(circlize)

plotMat <- 

```

## Using `circlize`

ComplexHeatmap uses [`circlize`](https://cran.r-project.org/web/packages/circlize/circlize.pdf) package instead of [`RColorBrewer`](https://www.rdocumentation.org/packages/RColorBrewer/versions/1.1-2/topics/RColorBrewer) for color mapping functions.

* Handbook : https://jokergoo.github.io/circlize_book/book/
* Publication : https://academic.oup.com/bioinformatics/article/30/19/2811/2422259


```r
# Compare with RColorBrewer
library(RColorBrewer)


library(circlize)
colpal = colorRamp2(c(0,1,5), c('#3288bd','#fddbc7','#b2182b'))

```

### Some pretty palettes to use

```r
# red-white-blue
# red-white-green

# discrete pastel

# Extracting from RColorBrewer
library(RColorBrewer)
colpal <- brewer.pal(8, "Set2")[1:length(vennLs)]

```

Sources:
* http://colorbrewer2.org

## Using gpar

A lot of customizations require using `gpar`, which seems difficult and complex but not so once you get the hang of it. If a parameter name ends with `_gp`, it will need a gpar opject.



**linetype lookup**


## Creating legends


---

## Look ups for options frequently used / most complex

### Adding cell borders

```r
Heatmap(...,
	rect_gp = gpar(col='grey65', lwd=.5))
```

### Axis label option `row_names_gp` gpar

```r
Heatmap(..., 
	row_names_gp = gpar(fontsize = 11),
...)
```

Colorizing row labels

```r
row_lab_col = structure(rep('grey15', nrow(plotMat)), names=rownames(plotMat))
row_lab_col[1:3] = 'firebrick'

Heatmap(...,
	row_names_gp = gpar(col=row_lab_col),
	...)

```

### Axis label rotation

```r
Heatmap(...,
	row_names_rot = 45
	...)
```

### Cell annotations



## Saving a ComplexHeatmap plot


## Full ComplexHeatmap parameter lookup



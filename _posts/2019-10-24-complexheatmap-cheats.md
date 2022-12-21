---
layout: posts
title:  ComplexHeatmap Cheats and Reference list
# author: littleheron
date:   2020-01-25
lang: en
lang-ref: complexheatmap-cheats
classes: wide
categories: R reference
---

Heatmap, or heat map, is a common method of visualization when dealing with omics data such as gene expression in which individual values are represented by colours and mapped across a two-dimensional space. This shading matrix technique, as it turns out, has been around since 1873, where Loua used it to summarise different social statistics across 20 districts in Paris.

There are multiple types of heatmaps starting from density map to tree map and mosaic plots, but the typically used type in biology would look something like this:

[add image]

R has a number of packages for drawing heatmaps. pheatmap had been my long time favourite because it was easier to use and gave nicer looking plots than, say, heatmap.2, but then I discovered ComplexHeatmap, which immediately wiped out all other competitions with how customizable it is.

*Pros:*

* Created with genomic data analysis in mind.
* Customability.
* Only heatmap package to allow parallel heatmap plotting. (closest I found before was ggplot2)
* Wide variety of possible annotations. (That thing you wanted to do for heatmap? You could probably do it.)

*Cons:*

* Difficult to master.
* Saving figures with right dimension is a pain. That is not to say that saving was easy with every other packages, but saving with ComplexHeatmap is a special kind of pain for those who don't have a solid grasp on grobs and graphics (Me). 

The developer is kind enough to provide full reference manual [here](https://jokergoo.github.io/ComplexHeatmap-reference/book/index.html), and also gives detailed answers to questions in the form of github issue, so I can't complain really.

---

## Demo Data preparation

There are of course numerous practice dataset available such as diamond cut, flight, etc. However, since I would like to get better at data cleaning up, we will use [DATA] 


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
colpal <- colorRamp2(c(0,1,5), c('#3288bd','#fddbc7','#b2182b'))

```

### Some pretty palettes to use

```r
n = 4
# Extracting from RColorBrewer
library(RColorBrewer)
colpal <- brewer.pal(8, "Set2")[1:n]

# ggplot2 defaults
ggpal <- scales::hue_pal()(n)

# Viridis scale
virid <-
```

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



---

#### References

- *Wilkinson, Leland; Friendly, Michael (May 2009). "The History of the Cluster Heat Map". The American Statistician. 63 (2): 179–184. CiteSeerX 10.1.1.165.7924. [doi:10.1198/tas.2009.0033](https://www.tandfonline.com/doi/abs/10.1198/tas.2009.0033)*
- http://colorbrewer2.org



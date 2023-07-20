---
title: Adventures in R Package Creation (Part 1)
layout: posts
date: 2023-01-11
---

This part mostly follows [this guide](https://hilaryparker.com/2014/04/29/writing-an-r-package-from-scratch/), with some minor additions by myself.

## Why create custom R package?



## Step 0-a. Required packages

Two packages are required before building : `devtools`, `roxygen2`

```R
install.packages("devtools")
devtools::install_github('klutometis/roxygen')

library(devtools)
library(roxygen2)
```

`devtools` provides functions for creating the base structure and building the packages, for example, `build()`, `check()`.

`roxygen2` is for documentation and makes it easy to create manual pages from R script files.


## Step 0-b. Preparation and Git Initialize

To version control with git and make our new package into one that can be installed through devtools' `install_github` function, we need to initialize a git repository before going any further. If you are starting off with an empty directory, you can git initialize it easily.



If 

```sh
cd ./my_first_package
git init
git add .
git commit -m 'Package initialize'

# add remote 
git remote add origin git@github.com:LittleHeronCodes/my_first_package.git
git branch --set-upstream-to=origin/main main

# pull and merge
git fetch
git pull --allow-unrelated-histories
git push
```

If you're not interested in using GitHub for this, just make an empty directory or go straight to Step 1.


## Step 1. Package creation

Now we create the template for the package using devtools `create` function. Note the working directory, which is the directory where you want the package to be created.

```R
setwd('parent_dir')
create('my_first_package')
```

This will create a new directory `my_first_package` under `parent_dir` and add basic necessary files, or turn an empty `my_first_package` directory into an empty R package. If the directory is not empty, R will throw an error.

Inside `my_first_package`, `create` will write two files `DESCRIPTION`, `NAMESPACE`, and an `R` directory. `DESCRIPTION` is where the package's, well, description goes, and the file has information such as package version, title, authors, and license. This is also where you can add package dependencies. `R` directory is where all the R scripts containing the package functions and data will go. We do not have to worry about `NAMESPACE` as roxygen will handle that.


## Step 2. Writing functions

Now we need to populate our package with custom functions.

```R
# removeNAs from a vector
removeNAs <- function(x) {
    x[which(!is.na(x))]
}

```

Functions can each have their own file or several can be put together in a single file. I tend to categorize functions instead of making one script for every function, but this is a matter of preference.

Next, we write documentations for our functions, and this is where `roxygen2 comes in. Adding special comments before the function and roxygen2 will compile them to separate documentations later during package build. The documentations written here will later show up as help page for each function.

```R
#' removeNAs   <- this is the title
#'
#' Remove NA values from a vector  <- this is the description
#' Descriptions can be both single or multi-line.
#' Like
#' This
#'
#' @param x input vector
#' @return NA removed vectors
#' @export
#' @examples
#' a <- c(1, 2, 3, NA, 6, NA, 7)
#' removeNAs(a)
removeNAs <- function(x) {
    x[which(!is.na(x))]
}

```

The first line is the title. The second section is for description, and this can be put in multiple lines. Next we have tags for roxygen2 to parse.

These are the most basic tags:

- @param
- @return
- @examples
- @export

One note on the example : examples will actually be run upon build and return an error if it cannot be run as-is. Either create all the variables properly in the example as given above or use a `dontrun` wrapper like this:

```R
#' \dontrun{
#' removeNAs(vector_with_na_values)
#' }
```

Sometimes, functions have similar use and you want to put them together in the help page. We can use @describeIn for this:

```R
```



## Step 3. Process documentation

Creating the documentation is simple. Again, note the working directory :

```R
setwd('./my_first_package')
document()
```

Now the package directory will look like this, where we have `man` files:

[img]

We can also test build check if everything works fine by running `check` which will run `R CMD`. Incidentally, this is the result of check for my personal function pack Lazy2:

[img]


## Step 4. Install

Now we can install the package locally.

```R
setwd('./my_first_package')
install()
```

This can also be run from a different directory like this:

```R
setwd('~')
install('path/to/my_first_package')
```


### Optional :

If you've done the optional step and put this on git, commit/push and you can install your new shiny package directly from github.

```R
library(devtools)
install_github('LittleHeronCodes/my_first_package')
```

Congrats!


## Step 5?

Now that we have the basics of the package, for personal use this is really all we need. However, there are still plenty stuff that we can do. For example, we can put data in for quick load, and this is in fact one of the biggest reason I built the `Lazy2` package out of my custom functions--because I couldn't be bothered to constantly look up where I put the gene name mapping file. Also, once you start putting in a bunch of functions together, `check` will start complaining about dependencies, unbound variables, which can become problematic later on.

The next post will cover how to add datasets for easy load, managing package dependencies, and additional tricks.


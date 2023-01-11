---
title: Adventures in R Package Creation (Part 1)
layout: posts
date: 2023-01-11
---

This part mostly follows this guide, with some minor additions by myself : https://hilaryparker.com/2014/04/29/writing-an-r-package-from-scratch/

- Advantages in using Packages
- Cons : 

Systems information :


## Step 0. Required packages

Packages required before building : `devtools`, `roxygen2`

```R
install.packages("devtools")
devtools::install_github('klutometis/roxygen')

library(devtools)
library(roxygen2)
```

## Step 1. Package creation

Can either create an empty directory in advance or not. Note the working directory, which is the directory where you want the package to be created.

```R
setwd('parent_dir')
create('my_first_package')
```

This will automatically add two files `DESCRIPTION`, `NAMESPACE`, and an `R` directory. `DESCRIPTION` is where the package's, well, description goes, including package version, title and authors. This is also where you can add package dependencies. `R` directory is where all the R scripts containing the package functions and data will go. We do not have to worry about `NAMESPACE`.


### Optional step git initialize

Because I use GitHub for version control and to store my project scripts, also to make this package into one that can be installed through devtools' install_github function, I would turn this into a git repository before going any further.

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


## Step 2. Writing functions

```R

```

Next, write documentations for your functions. This is where roxygen2 comes in. Adding special comments before the function and roxygen2 will compile them to separate documentations later during package build.

```R

```

A note on the example : examples will actually be run upon build and return an error if it cannot be run as-is. Either create all the variables properly in the example or use a wrapper like this:

```R
#' \dontrun{
#' readGMT('file/path.gmt')
#' }
```

Functions can be placed in separate files or put together in a single file. Or split around.


## Step 3. Process documentation

Creating the documentation is simple. Again, note the working directory change :

```R
setwd('./my_first_package')
document()
```

Now the package directory will look like this:

[img]

We can also test build check if everything works fine by running `build`.


## Step 4. Install

Now we can install the package. 

```R
install()
```

This can also be run from the parent directory like this:

```R
setwd('..')
install('my_first_package')
```


### Optional :

If you've done the optional step and put this on git, you can install your new shiny package directly from github.

```R
library(devtools)
install_github('LittleHeronCodes/my_first_package')
```

Congrats!


## Step 5?

There are still lots of stuff that we can do. For example, we can put data in for quick load, and this is in fact one of the biggest reason I built the Lazy2 package out of my custom functions--because I couldn't be bothered to constantly look up where I put the gene name mapping file.

The next post will cover how to add datasets for easy load, managing package dependencies, and additional tricks.

- dataset
- Dependency
- .Rbuildignore
- zzz.R



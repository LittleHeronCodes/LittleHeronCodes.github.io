---
title: Adventures in R Package Creation (Part 2)
layout: posts
date: 2023-01-13
---

- attaching dataset
- Dependency
  - Import vs Suggested in DESCRIPTION
  - Package-level documentation with `use_this::use_package_doc()`
  - Piping problems (`use_pipe()`)
- .Rbuildignore
- zzz.R

## Welcome to dependency hell

If you have followed the [Part 1]() of R package creation, the DESCRIPTION file of your package might look something like this:




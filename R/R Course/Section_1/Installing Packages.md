In **R**, installing packages is straightforward using `install.packages()`

---

## Install a Package from CRAN

`install.packages("ggplot2")`

> Run this **once**. After installation, load it with:

`library(ggplot2)`

So to using package just type `library(package name)`.

---

## Install Multiple Packages

`install.packages(c("dplyr", "tidyr", "readr"))`

---

## Choose a CRAN Mirror (if prompted)
```
install.packages("ggplot2", repos = "https://cloud.r-project.org")
```
---

## Install from GitHub

Requires **remotes** (or **devtools**):
```
install.packages("remotes")
remotes::install_github("tidyverse/ggplot2")
```
---

## Install a Specific Version
```
remotes::install_version("ggplot2", version = "3.4.0")
```
---

## Check Installed Packages

`installed.packages()`

Or check a specific package:

`"ggplot2" %in% rownames(installed.packages())`

---

## Update Packages

`update.packages()`

---

## Common Errors & Fixes

### ❌ “Package is not available for this version of R”

- Update R
    
- Or install an older version:
    

`remotes::install_version("pkgname", "x.y.z")`

---

### ❌ Permission denied / non-writable library

`install.packages("ggplot2", lib = "~/R/library")`

Then add:

`.libPaths("~/R/library")`

---

### ❌ Compilation errors (Windows)

- Install **Rtools**
    
- Restart R
    

---

## Install Without Internet (Local File)

`install.packages("mypackage.tar.gz", repos = NULL, type = "source")`
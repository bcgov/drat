[![img](https://img.shields.io/badge/Lifecycle-Experimental-339999)](https://github.com/bcgov/repomountie/blob/8b2ebdc9756819625a56f7a426c29f99b777ab1d/doc/state-badges.md)


# drat - bcgov R package 📦 repository

We are using the [drat](https://cran.r-project.org/package=drat) R package to 
set up the infrastructure for a mini bcgov R package repository.

The intent is to make it easy for bcgov R users to install bcgov R packages 
that are not on CRAN, and keep them up to date.

### Usage

#### Package Users: Installation of bcgov R packages

The easiest way to set yourself up to use this drat repository is to first 
install the **drat** package:

```r
install.packages("drat")
```

Then add the bcgov drat repo to your list of repositories to install from:

```r
drat::addRepo("bcgov")
```

Add the above line to your `.Rprofile` file so that the bcgov drat repository is 
available every time you run **R**. [This discussion](https://csgillespie.github.io/efficientR/set-up.html#r-startup) 
of R startup processes is a good introduction if you have never edited your `.Rprofile` before.

Now you can install a package from the bcgov repository with `install.packages()`.
For example:

```r
install.packages(NAME_OF_PACKAGE_TO_INSTALL)
```

#### Package Authors: Adding a package to the bcgov drat repository.
On Github:

1. [Fork](https://help.github.com/articles/fork-a-repo/) this bcgov drat repository.

On the command line:

2. Clone this repository to your machine and open the directory:

    ```
    git clone https://github.com/[YOUR GITHUB USERNAME]/drat
    cd drat
    ```

3. Build the package that you want to add to the drat repository. This can be done on the command line or in R using `devtools`:

    a. Command-line: Move to the directory in which your package directory resides and 
replace *mypkg* with the name of your package. Either of these will build a file called
`mykg_pkg.ver.tar.gz` one directory up from your package directory:
    
    ```
    R CMD build "mypackage"
    ```
    
    b. R/Rstudio: In the console in your R package project:
    
    ```r
    devtools::build()
    ```

4. Open R, and use the `drat::insertPackage()` function to add the built package 
(`tar.gz` file) to the drat repo:

    ```r
    drat::insertPackage("mypackage_pkg.ver.tar.gz", "path/to/drat")
    ```

    * *If you are comfortable, you can add the argument `commit = TRUE` to the above function
    call and it will automatically commit the changes that add the package to the `gh-pages` 
    branch in the drat repository. Otherwise, go to step 4:*

5. Visually verify that the package has been added in `src/contrib`, then add, 
commit, and push the changes. Once you are satisfied you have added your package and would like to submit it to 
 the bcgov drat repository, [create a pull request](https://help.github.com/articles/creating-a-pull-request-from-a-fork/) to merge your changes (i.e. the addition of a new package) back in the bcgov drat repository.

#### Package Authors: Removing a package from the bcgov drat repository.
Removing a package from a drat repository is a multi-stage process whereby the source file of the package is removed, the drat repository index is updated and then the changes are committed and pushed. 

1. The first step is to [fork](https://help.github.com/articles/fork-a-repo/) this bcgov drat repository.

2. There are many way to remove the source file. Here we are removing it with R. If you are in the top-level `drat` directory you can set the directory where the source files are along with the specific source file you'd like to remove. From there removing the file is easily accomplished:

    ```r
    # Source directory
    pkgdir <- normalizePath("./src/contrib", winslash = "\\")
    
    # Filename of the package you would like to remove
    pkgname <- "FILENAME.tar.gz"
    
    # Remove the source file
    file.remove(file.path(pkgdir, pkgname))
    ```
  
3. Now that we have removed the file, we need to update our index so that the repository no longer looks for the removed package like this:

    ```r
    tools::write_PACKAGES(dir = pkgdir, type = "source")
    ```
  
4. After completing steps 1, 2 and 3, there should 4 changes in your repository: the package itself and the three PACKAGES files. Stage, commit and push those changes.  If you are happy with the results, you can submit a pull request to the bcgov drat repository. Once accepted, your package should now be completely removed from the bcgov drat repository.

### Project Status

*Under active development.*

## Getting Help or Reporting an Issue

To report bugs/issues/feature requests, please file an [issue](https://github.com/bcgov/%3Crepo-name%3E/issues/).

### How to Contribute

If you would like to contribute, please see our [CONTRIBUTING](CONTRIBUTING.md) guidelines.

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

### License

    Copyright 2017 Province of British Columbia

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at 

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

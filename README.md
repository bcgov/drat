<div id="devex-badge"><a rel="Inspiration" href="https://github.com/BCDevExchange/docs/blob/master/discussion/projectstates.md"><img alt="An idea being explored and shaped. Open for discussion, but may never go anywhere." style="border-width:0" src="https://assets.bcdevexchange.org/images/badges/inspiration.svg" title="An idea being explored and shaped. Open for discussion, but may never go anywhere." /></a></div>
============================

# drat - bcgov R package 📦 repository

We are using the [drat](https://cran.r-project.org/package=drat) R package to 
set up the infrastructure for a mini bcgov R package repository.

The intent is to make it easy for bcgov R users to install bcgov R packages, and
keep them up to date.

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
available every time you run **R**.

Now you can install a package from the bcgov repository with `install.packages()`.
For example:

```r
install.packages("bcgovr")
```

#### Package Authors: Adding a package to the bcgov drat repository.

On the command line:

1. Clone this repository to your machine, open the directory, and checkout the
`gh-pages` branch:

```
git clone https://github.com/bcgov/drat
cd drat
git checkout gh-pages
```

2. Move to the directory in which your package directory resides, and build the package:

```
R CMD build "mypkg-directory"
```

3. Open R, and use the `drat::insertPackage()` function to add the built package 
(`tar.gz` file) to the drat repo:

```r
drat::insertPackage("mypackage_0.01.tar.gz", "path/to/drat")
```

*If you comfortable, you can add the argument `commit = TRUE` to the above function
call and it will automatically commit the changes that add the package to the `gh-pages` 
branch in the drat repository. Otherwise, go to step 4:*

4. Back on the command line, navigate into the drat directory, and checkout the
`gh-pages` branch:

```
cd drat
git checkout gh-pages
```

Then visually verify that the package has been added in `src/contrib`, then add, 
commit, and push the changes.

### Project Status

#Under active development.

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

# swissmuni: Download (meta)data about Swiss municipalities from the [web services](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc?singleWsdl) provided by the [Federal Statistical Office](https://www.bfs.admin.ch/bfs/en/home.html)

swissmuni is an R package that provides functions to access municipality [snapshots](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/snapshots), [correspondances](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/correspondances) and [mutations](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/mutations) from the [web services](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc?singleWsdl) provided by the [Federal Statistical Office](https://www.bfs.admin.ch/bfs/en/home.html).

## Features

...

## Details

...

## Installation

To install the latest development version of `swissmuni`, run the following in R:

```r
if ( !("remotes" %in% rownames(installed.packages())) )
{
  install.packages(pkgs = "remotes",
                   repos = "https://cloud.r-project.org/")
}
remotes::install_git(url = "http://gitlab.com/salim_b/swissmuni.git")
```

## Development

This package is written using [literate programming](https://en.wikipedia.org/wiki/Literate_programming) techniques proposed by [Yihui Xie](https://yihui.name/rlp/). This means all the `-GEN.R` suffixed R source code found under [`R/`](R/) is generated from their respective [R Markdown](https://rmarkdown.rstudio.com/) counterparts found under [`Rmd/`](Rmd/) as instructed by the [`Makefile`](Makefile). Always make changes only to the `.Rmd` files – not the `.R` files – and then run the following from the root of this repository to regenerate the R source code and build and install the package:

```sh
make && Rscript -e "devtools::install('.', keep_source = TRUE)"
```

Make sure that [`make`](https://de.wikipedia.org/wiki/GNU_Make)[^make-windoof] is available on your system and that the R packages [`knitr`](https://cran.r-project.org/package=knitr) and [`rmarkdown`](https://cran.r-project.org/package=rmarkdown) are up to date beforehand.


[^make-windoof]: On Windows, `make` is included in [Rtools](https://cran.rstudio.com/bin/windows/Rtools/). On macOS, you have to install the [Xcode command line tools](https://stackoverflow.com/a/10301513/7196903).


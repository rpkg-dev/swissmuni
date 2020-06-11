# swissmuni: Download (meta)data about Swiss Municipalities from the Swiss Federal Statistical Office's Web Services

swissmuni provides functions to access municipality [snapshots](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/snapshots), [correspondances](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/correspondances) and [mutations](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/mutations) from the [web services](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc?singleWsdl) provided by the [Swiss Federal Statistical Office (FSO)](https://www.bfs.admin.ch/bfs/en/home.html). The accessed web services are part of the FSO's *Statistical Metadata System (SMS)*.

## Installation

To install the latest development version of **swissmuni**, run the following in R:

``` {.r}
if (!("remotes" %in% rownames(installed.packages()))) {
  install.packages(pkgs = "remotes",
                   repos = "https://cloud.r-project.org/")
}
remotes::install_gitlab(repo = "salim_b/r/pkgs/swissmuni")
```

## Development

### Literate Programming

This package is written using a [literate programming](https://en.wikipedia.org/wiki/Literate_programming) approach [originally proposed by Yihui Xie](https://yihui.name/rlp/). All the `-GEN.R` suffixed R source code found under [`R/`](R/) is generated from their respective [R Markdown](https://rmarkdown.rstudio.com/) counterparts using [`pkgpurl::purl_rmd()`](https://gitlab.com/salim_b/r/pkgs/pkgpurl/). Always make changes only to the `.Rmd` files -- not the `.R` files -- and then run `pkgpurl::purl_rmd()` to regenerate the R source code.

### Coding Style

This package borrows a lot of the [Tidyverse](https://www.tidyverse.org/) design philosophies. The R code adheres to the principles specified in the [Tidyverse Design Guide](https://principles.tidyverse.org/) wherever possible and is formatted according to the [Tidyverse Style Guide](https://style.tidyverse.org/) (TSG) with the following exceptions:

-   Line width is limited to **160 characters**, double the [limit proposed by the TSG](https://style.tidyverse.org/syntax.html#long-lines) (80 characters is ridiculously little given today's high-resolution wide screen monitors).

-   Usage of [magrittr's compound assignment pipe-operator `%<>%`](https://magrittr.tidyverse.org/reference/compound.html) is desirable[^1].

-   Usage of [R's right-hand assignment operator `->`](https://rdrr.io/r/base/assignOps.html) is not allowed[^2].

As far as possible, these deviations from the TSG plus some additional restrictions are formally specified in the [lintr configuration file](https://github.com/jimhester/lintr#project-configuration) [`.lintr`](.lintr), so lintr can be used right away to check for formatting issues:

``` {.r}
lintr::lint_dir(pattern = "\\.Rmd$",
                exclusions = list.files(path = "vignettes",
                                        recursive = TRUE,
                                        full.names = TRUE))
```

## See also

-   ...

[^1]: The TSG [explicitly instructs to avoid this operator](https://style.tidyverse.org/pipes.html#assignment-1) -- presumably because it's relatively unknown and therefore might be confused with the forward pipe operator `%>%` when skimming code only briefly. I don't consider this to be an actual issue since there aren't many sensible usage patterns of `%>%` at the beginning of a pipe sequence inside a function -- I can only think of creating side effects and relying on [R's implicit return of the last evaluated expression](https://rdrr.io/r/base/function.html). Therefore -- and because I really like the `%<>%` operator -- it's usage is welcome.

[^2]: The TSG [explicitly accepts `->` for assignments at the end of a pipe sequence](https://style.tidyverse.org/pipes.html#assignment-1) while Google's R Style Guide [considers this bad practice](https://google.github.io/styleguide/Rguide.html#right-hand-assignment) because it "makes it harder to see in code where an object is defined". I second the latter.

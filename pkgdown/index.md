# swissmuni

[![CRAN Status](https://r-pkg.org/badges/version/swissmuni)](https://cran.r-project.org/package=swissmuni){.pkgdown-release}

swissmuni provides access to Swiss municipality [snapshots](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/snapshots), [congruences](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/correspondances), [mutations](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/mutations) and their [spatial classifications](https://sms.bfs.admin.ch/WcfBFSSpecificService.svc/AnonymousRest/communes/levels) from the [web services](https://www.bfs.admin.ch/bfs/de/home/dienstleistungen/forschung/api/api-gemeinde.assetdetail.15224054.html) provided by the [Swiss Federal Statistical Office (FSO)](https://www.bfs.admin.ch/bfs/en/home.html). The accessed web services are part of the FSO's *Statistical Metadata System (SMS)*[^1].

Note that there's also an official web application [available](https://www.agvchapp.bfs.admin.ch/de/communes/query) to access Swiss municipality data.

## Installation

To install the latest development version of swissmuni, run the following in R:

``` r
if (!("remotes" %in% rownames(installed.packages()))) {
  install.packages(pkgs = "remotes",
                   repos = "https://cloud.r-project.org/")
}

remotes::install_gitlab(repo = "rpkg.dev/swissmuni")
```

## Usage

The (function) reference is found [here](reference).

## Development

### R Markdown format

This package's source code is written in the [R Markdown](https://rmarkdown.rstudio.com/) file format to facilitate practices commonly referred to as [*literate programming*](https://en.wikipedia.org/wiki/Literate_programming). It allows the actual code to be freely mixed with explanatory and supplementary information in expressive Markdown format instead of having to rely on [`#` comments](https://rstudio.github.io/r-manuals/r-lang/Parser.html#comments) only.

All the `.gen.R` suffixed R source code found under [`R/`](https://gitlab.com/rpkg.dev/swissmuni/-/tree/master/R/) is generated from the respective R Markdown counterparts under [`Rmd/`](https://gitlab.com/rpkg.dev/swissmuni/-/tree/master/Rmd/) using [`pkgpurl::purl_rmd()`](https://pkgpurl.rpkg.dev/dev/reference/purl_rmd.html)[^2]. Always make changes only to the `.Rmd` files -- never the `.R` files -- and then run `pkgpurl::purl_rmd()` to regenerate the R source files.

### Coding style

This package borrows a lot of the [Tidyverse](https://www.tidyverse.org/) design philosophies. The R code is guided by the [Tidy design principles](https://design.tidyverse.org/) and is formatted according to the [Tidyverse Style Guide](https://style.tidyverse.org/) (TSG) with the following exceptions:

-   Line width is limited to **160 characters**, double the [limit proposed by the TSG](https://style.tidyverse.org/syntax.html#long-lines) (80 characters is ridiculously little given today's high-resolution wide screen monitors).

    Furthermore, the preferred style for breaking long lines differs. Instead of wrapping directly after an expression's opening bracket as [suggested by the TSG](https://style.tidyverse.org/syntax.html#long-lines), we prefer two fewer line breaks and indent subsequent lines within the expression by its opening bracket:

    ``` r
    # TSG proposes this
    do_something_very_complicated(
      something = "that",
      requires = many,
      arguments = "some of which may be long"
    )

    # we prefer this
    do_something_very_complicated(something = "that",
                                  requires = many,
                                  arguments = "some of which may be long")
    ```

    This results in less vertical and more horizontal spread of the code and better readability in pipes.

-   Usage of [magrittr's compound assignment pipe-operator `%<>%`](https://magrittr.tidyverse.org/reference/compound.html) is desirable[^3].

-   Usage of [R's right-hand assignment operator `->`](https://rdrr.io/r/base/assignOps.html) is not allowed[^4].

-   R source code is *not* split over several files as [suggested by the TSG](https://style.tidyverse.org/package-files.html) but instead is (as far as possible) kept in the single file [`Rmd/swissmuni.Rmd`](https://gitlab.com/rpkg.dev/swissmuni/-/tree/master/Rmd/swissmuni.Rmd) which is well-structured thanks to its [Markdown support](#r-markdown-format).

As far as possible, these deviations from the TSG plus some additional restrictions are formally specified in [`pkgpurl::default_linters`](https://pkgpurl.rpkg.dev/reference/default_linters), which is (by default) used in [`pkgpurl::lint_rmd()`](https://pkgpurl.rpkg.dev/reference/lint_rmd), which in turn is the recommended way to lint this package.

## See also

-   [Official municipality data web application from the Swiss Federal Statistical Office (FSO)](https://www.agvchapp.bfs.admin.ch/de/communes/query)

[^1]: Publicly accessible information about this system is scarce. A presentation introducing the system at the [4th SDMX Global Conference 2013](https://sdmx.org/?sdmx_events=4th-sdmx-global-conference) is found [here](https://web.archive.org/web/20200615113441/https://www.oecd.org/sdd/SDMX%202013%20Session%203.7%20-%20A%20statistical%20metadata%20system%20based%20on%20SDMX.pdf).

[^2]: The very idea to leverage the R Markdown format to author R packages was originally proposed by Yihui Xie. See his excellent [blog post](https://yihui.org/rlp/) for his point of view on the advantages of literate programming techniques and some practical examples. Note that using `pkgpurl::purl_rmd()` is a less cumbersome alternative to the Makefile approach outlined by him.

[^3]: The TSG [explicitly instructs to avoid this operator](https://style.tidyverse.org/pipes.html#assignment-2) -- presumably because it's relatively unknown and therefore might be confused with the forward pipe operator `%>%` when skimming code only briefly. I don't consider this to be an actual issue since there aren't many sensible usage patterns of `%>%` at the beginning of a pipe sequence inside a function -- I can only think of creating side effects and relying on [R's implicit return of the last evaluated expression](https://rdrr.io/r/base/function.html). Therefore -- and because I really like the `%<>%` operator -- it's usage is welcome.

[^4]: The TSG [explicitly accepts `->` for assignments at the end of a pipe sequence](https://style.tidyverse.org/pipes.html#assignment-2) while Google's R Style Guide [considers this bad practice](https://google.github.io/styleguide/Rguide.html#right-hand-assignment) because it "makes it harder to see in code where an object is defined". I second the latter.

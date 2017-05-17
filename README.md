webmockr
========

[![Build Status](https://travis-ci.org/ropensci/webmockr.svg?branch=master)](https://travis-ci.org/ropensci/webmockr)
[![codecov](https://codecov.io/gh/ropensci/webmockr/branch/master/graph/badge.svg)](https://codecov.io/gh/ropensci/webmockr)

R library for stubbing and setting expectations on HTTP requests.

Port of the Ruby library [webmock](https://github.com/bblimke/webmock)


## Features

* Stubbing HTTP requests at low http client lib level (no need to change tests when you change HTTP library)
* Setting and verifying expectations on HTTP requests
* Matching requests based on method, URI, headers and body
* Support for `testthat` (coming soon via `vcr`)

## Supported HTTP libraries

* [crul](https://github.com/ropensci/crul)

> more to come

## Install


```r
devtools::install_github("ropensci/webmockr")
```


```r
library(webmockr)
```

## Turn on webmockr


```r
webmockr::enable()
```

```
## CrulAdapter enabled!
```

```
## [1] TRUE
```

```r
crul::mock()
```

## Outside a test framework


```r
library(crul)
```

### Stubbed request based on uri only and with the default response


```r
stub_request("any", "https://httpbin.org/get")
x <- HttpClient$new(url = "https://httpbin.org")
x$get('get')
```

### Stubbing requests based on method, uri, query params and headers


```r
stub_request("get", "https://httpbin.org/get") %>%
  wi_th(
    query = list(hello = "world"),
    request_headers = list(`Accept-Encoding` = "gzip, deflate", `User-Agent` = 'R'))
x <- HttpClient$new(url = "https://httpbin.org", headers = list(`User-Agent` = 'R'))
x$get('get', query = list(hello = "world"))
```

## Meta

* Please [report any issues or bugs](https://github.com/ropensci/webmockr/issues).
* License: MIT
* Get citation information for `webmockr` in R doing `citation(package = 'webmockr')`
* Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md).
By participating in this project you agree to abide by its terms.

[![ropensci_footer](https://ropensci.org/public_images/github_footer.png)](https://ropensci.org)

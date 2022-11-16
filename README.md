
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Environmental attitudes: natural language processing of social media posts

<!-- badges: start -->
<!-- badges: end -->

The goal of this hackathon session is to find out how we can use social
media data to find peoples attitudes to different environmental
challenges or aspects of nature.

I am hopeful that the work we do today can inform a peer reviewed paper
on environmental attitudes and social media data.

## Installation

You can install and load the code for this hackathon session from
[GitHub](https://github.com/nfox29/seasHackathon) with:

``` r
devtools::install_github("nfox29/seasHackathon")

library(seasHackathon)
```

## Getting data from Flickr

The first social media website we will look at is Flickr.

``` r
tidytext::get_sentiments("afinn")
#> # A tibble: 2,477 × 2
#>    word       value
#>    <chr>      <dbl>
#>  1 abandon       -2
#>  2 abandoned     -2
#>  3 abandons      -2
#>  4 abducted      -2
#>  5 abduction     -2
#>  6 abductions    -2
#>  7 abhor         -3
#>  8 abhorred      -3
#>  9 abhorrent     -3
#> 10 abhors        -3
#> # … with 2,467 more rows
```

``` r
#search flickr for posts containing the word "nature" in a give place and time
flickr_raw <- photo_search(mindate_taken = "2022-01-01",
                           maxdate_taken = "2021-01-01",
                           bbox = "-134.648443,21.398553,-54.140630,49.925909",
                           text = "nature")

#here we create a new column called text and paste in all the other text from that row
flickr_raw$text <- paste2(flickr_raw$title,
                          flickr_raw$description,
                          flickr_raw$tags)

#use our custom function to add afinn sentiments to the
flickr_afinn <- get_afinn(flickr_data = flickr_raw)
```
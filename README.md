# wikimedia-functions
List of functions and packages in R for Wikimedia data import and tidying

## Packages
```
# Wikipedia
library("WikipediR")
library("WikipediaR")
library("pageviews")

# Wikidata
library("tidywikidatar")
library("WikidataQueryServiceR")
library("WikidataR")
```

### WikipediR package
```R
library("WikipediR")

# User
user_information()
user_contributions()

# Revisions
revision_diff()
revision_content()

# Page content
page_info()
page_content()
page_links()
page_backlinks()
page_external_links()
```

### tidywikipediar package

```R
library("tidywikipediar")

# Get Wikipedia article in given language using Wikidata item
tw_get_wikipedia()
```

### WikipediaR package
```R
library("WikipediaR")

contribs()
userContribs()
userInfo()

# number of contributions for this user
nrow(userContribs(user.name = last.contrib.5636, domain = "en")$contribs)
```

## Get pageviews for multiple articles
The code below returns a dataframe.
```R
library("tidyverse")
library("pageviews")

articles <- c("Donald Trump", "Joe Biden")

pageviews <- map_dfr(articles, ~ pageviews::article_pageviews(article = ., end = "2022100900"))
```

## Get the most viewed wikipedia articles per country
The following script creates a function that retrieves the most viewed wikipedia articles per country. It serves as an API wrapper for the [Wikimedia REST API](https://wikimedia.org/api/rest_v1/).

```R
pageviews_top_per_country <-
  function (country = "CA",
            access = "all-access",
            year = format(Sys.Date(), "%Y"),
            month = format(Sys.Date(), "%m"),
            day = format(Sys.Date()-1, "%d"),
            user_agent = Sys.getenv("WIKIMEDIA_USER_AGENT")) {
    # Get response from API
    request_result <-
      httr::GET(
        url = paste(
          "https://wikimedia.org/api/rest_v1/metrics/pageviews/top-per-country",
          country,
          access,
          year,
          month,
          day,
          sep = "/"
        ),
        config = httr::user_agent(user_agent)
      )
    
    if(httr::http_error(request_result)){
      warning("The request failed")
    } else {
      httr::content(request_result)
    }
    
    # Parse returned text with fromJSON()
    parsed <- jsonlite::fromJSON(httr::content(request_result, as = "text"))
    
    # Create dataframe
    df_untidy <- parsed[["items"]][["articles"]][[1]]
    
    # Clean article names
    df <- df_untidy %>% 
      dplyr::mutate(
        article = gsub("_", " ", article),
        date = as.POSIXct(paste(year, month, day, sep = "-"), tz = "UTC"),
        country = country,
        access = access
      )
    
    # Return dataframe
    df
  }
```

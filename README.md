# wikimedia-functions
List of functions and packages in R for Wikimedia data import and tidying

## Packages
```
library("WikipediR")
library("WikipediaR")
library("WikidataR")
library("tidywikidatar")
library("pageviews")
```

## Functions
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

```R
library("WikipediaR")

contribs()
userContribs()
userInfo()

# number of contributions for this user
nrow(userContribs(user.name = last.contrib.5636, domain = "en")$contribs)
```

## Pageviews
```R
library("tidyverse")
library("pageviews")

# Get pageviews for multiple articles and create a dataframe

articles <- c("Donald Trump", "Joe Biden")

pageviews <- map_dfr(articles, ~ pageviews::article_pageviews(article = ., end = "2022100900"))
```

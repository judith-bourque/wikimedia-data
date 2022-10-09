# wikimedia-functions
List of functions and packages in R for Wikimedia data import and tidying

## Packages
```
library("WikipediR")
library("WikipediaR")
library("WikidataR")
library("tidywikidatar")
```

 ## Functions
```r
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

# wikimedia-functions
List of functions and packages in R for Wikimedia data import and tidying

## Packages
```R
# Wikipedia
library("WikipediR")
library("WikipediaR")
library("pageviews")
library("waxer")

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

---
layout: post
title: "Biggest Star in the world - Donald Trump"
date: 2018-04-19
---

Trump is getting too much attention... 

At least article titles of Washington Post, Wall Street Journal, New York Times, Bloomberg, New Yorker, Cosmopolitan, and Vogue(Yes, fashion magazine Vogue) are giving more and more attention to Trump, only Trump! 

<img src="https://elodielu.github.io/picture/wordcloud.png" width = "1080">

In 2017, here are what are these publishers talking about.

<img src="https://elodielu.github.io/picture/publisher.png" width = "1080">

To show this result is not from photoshop but from data science;
* Next I am going to present some numbers and charts to convince you 
* If you still are not buying the story, please go to last section and check how did I get this result through extract data from [GDELT](https://www.gdeltproject.org/) dataset in Google's BigQuery, data wrangling in R, and fancy charts in R and Tableau.


## Let data speak

**Brief intro of the amazing GDELT project**

GDELT Project monitors the world's broadcast, print, and web news from nearly every corner of every country in over 100 languages and identifies the people, locations, organizations, themes, sources, emotions, counts, quotes, images and events driving our global society every second of every day, creating a free open platform for computing on the entire world.(quote form their webisite) [GDELT schema](https://elodielu.github.io/material/megadata.pdf)

### Data source
<img src="https://elodielu.github.io/picture/data_source.png" width = "1080">

In total I extract 2.9 million records from the US mainstream media starting 2013 to start my analysis. They can be classified into 3 categories for a larger cover of the events;
* Political and general: Wahsington Post, New York Times
* Business: Wall Street Journal, Bloomberg
* Fashion and Culture: Vogue, Cosmopolitan, and New Yorker

### Analysis begins here
<img src="https://elodielu.github.io/picture/wordcount.png" width = "1080">



### Dear presidents
<img src="https://elodielu.github.io/picture/president2.png" width = "1080">

Average “tone” of all documents containing one or more mentions of this event. **Average tone** can be used as a method of filtering the “context” of events as a subtle measure of the importance of an event and as a proxy for the “impact” of that event. When events happended around the world involve Trump or Obama, how positive are they?

<img src="https://elodielu.github.io/picture/tone2.png" width = "1080">

**Goldstein Scale** captures the theoretical potential impact that type of event will have on the stability of a country. When events happended around the world involve Trump or Obama, what's the impact on the country?

<img src="https://elodielu.github.io/picture/gscore.png" width = "500">    <img src="https://elodielu.github.io/picture/gscore2.png" width = "500">

The media is in much favor of Obama, but the events impact of country stability does not seem to be a clear difference big enough to caught by human eyes. Tjerefore, I ran a statistical test. Well the t test show that there is significant difference between the Goldstein Scale of obama-related and trump-related events.
* Mean Goldstein Scale of Obama-related events is **0.88**
* Mean Goldstein Scale of Trump-related events is **0.72**
* 95% confident the true difference in means falls in  0.1301 - 0.1962

## How to make the data speak
### Data Extraction from BigQuery(SQL)

### Data Wrangeling(R)
```r
wsj <- read.csv("wsj.csv")
bloomberg <- read.csv("bloomberg.csv")
nytimes <- read.csv("nytimes.csv")
washingtonpost <- read.csv("washingtonpost.csv")

newyorker <- read.csv("newyorker.csv")
vogue <- read.csv("vogue.csv")
cosmopolitan <- read.csv("cosmopolitan.csv")

washingtonpost <- washingtonpost %>%
  select(-X) %>%
  mutate(publisher = "WashingtonPost")

bloomberg <- bloomberg %>% 
  mutate(publisher = "Bloomberg")

wsj <- wsj %>% 
  mutate(publisher = "WSJ")

nytimes <- nytimes %>% 
  mutate(publisher = "NYtimes")

newyorker <- newyorker %>% 
  mutate(publisher = "NewYorker")

vogue <- vogue %>% 
  mutate(publisher = "Vogue")

cosmopolitan <- cosmopolitan %>% 
  mutate(publisher = "Cosmopolitan")

events <- rbind(washingtonpost,bloomberg) %>%
  rbind(wsj) %>%
  rbind(nytimes) %>%
  rbind(newyorker) %>%
  rbind(vogue) %>%
  rbind(cosmopolitan) %>%  
  filter( Year > 2012)

title <- events %>%
  select(GLOBALEVENTID,SQLDATE,publisher,SOURCEURL) 

#write.csv(events,'events.csv')
#write.csv(washingtonpost,'washingtonpost.csv')
write_rds(title,"title.rda")
write_rds(events,'events.rda')
```
#### Text Processing
Parse url to extrat the article titles
```r
parsed_address <- url_parse(title$SOURCEURL)

title$path  <- parsed_address$path

title <- title %>%
  separate(path,into = c("a","b","c","d","e","f","g","h","i","j"), sep = "/", remove = FALSE, extra = "merge", fill = "right") %>%
  mutate(title = ifelse((publisher != "WashingtonPost") & grepl("-",j),j,
                 ifelse((publisher != "WashingtonPost") & grepl("-",i),i,
                 ifelse((publisher != "WashingtonPost") & grepl("-",h),h,
                 ifelse((publisher != "WashingtonPost") & grepl("-",g),g,
                 ifelse((publisher != "WashingtonPost") & grepl("-",f),f,
                 ifelse((publisher != "WashingtonPost") & grepl("-",e),e,
                 ifelse((publisher != "WashingtonPost") & grepl("-",d),d,
                 ifelse((publisher != "WashingtonPost") & grepl("-",c),c,
                 ifelse((publisher != "WashingtonPost") & grepl("-",b),b,
                 ifelse((publisher != "WashingtonPost") & grepl("-",a),a,
                 ifelse((publisher == "WashingtonPost") & grepl("-",g) & !grepl(".html",g),g,
                 ifelse((publisher == "WashingtonPost") & grepl("-",f) & !grepl(".html",f),f,
                 ifelse((publisher == "WashingtonPost") & grepl("-",e) & !grepl(".html",e),e,
                 ifelse((publisher == "WashingtonPost") & grepl("-",d) & !grepl(".html",d),d,
                 ifelse((publisher == "WashingtonPost") & grepl("-",c) & !grepl(".html",c),c,b
                        
                        
))))))))))))))))

title$title <- gsub("-", " ", title$title, fixed=TRUE)
title$title <- gsub("_", " ", title$title, fixed=TRUE)
title$title <- gsub(".html", "", title$title, fixed=TRUE)
title$title <- gsub("%E2%80%8B", "", title$title, fixed=TRUE)
title$title <- gsub("u s", "us", title$title, fixed=TRUE)

#head(title)
```


**Getting words and bigrams**

Words
```r
title2 <- title %>%
  select(GLOBALEVENTID,SQLDATE, publisher,title) %>%
  separate(title,into = c("X1","X2","X3","X4","X5","X6","X7","X8","X9","X10",
                          "X11","X12","X13","X14","X15","X16","X17","X18","X19","X20"), 
           sep = " ", remove = FALSE, extra = "merge", fill = "right")

title3 <- title2 %>%
  select(-title) %>%
  melt(id=c('GLOBALEVENTID','SQLDATE','publisher'), na.rm = TRUE)
 
title3 <- title3 %>%
  filter(!(value %in% stopwords("en"))) %>%
  filter(value != "s") %>%
  mutate(SQLDATE = as.Date(as.character(SQLDATE), format = "%Y%m%d")) %>%
  mutate(Year = format(SQLDATE, "%Y")) %>%
  select(-variable)
```

## Bigram
```r
title4 <- title %>%
  select(GLOBALEVENTID,SQLDATE, publisher,title) %>%
  mutate(SQLDATE = as.Date(as.character(SQLDATE), format = "%Y%m%d")) %>%
  mutate(Year = format(SQLDATE, "%Y")) %>%
  unnest_tokens(bigram, title, token = "ngrams", n = 2)

title4 <- title4 %>%
  separate(bigram, c("word1", "word2"), sep = " ", remove = FALSE) %>%
  filter(!(word1 %in% stopwords("en"))) %>%
  filter(!(word2 %in% stopwords("en"))) %>%
  select(-word1,-word2) %>%
  filter(!is.na(bigram))

colnames(title4)[which(names(title4) == "bigram")] <- "value" 


title5 <- rbind(title4,title3) #combine the words and bigram

#head(title4,20)
```

### Data Visualization(Tableau and R)

#### Wordcloud of one-word and bigram
```r
title5 %>%
  group_by(Year, value) %>%
  summarise(freq = n()) %>%
  ungroup() %>%
  filter(Year == "2014") %>% #Change year to get all yearly wordcloud
  select(-Year) %>%
  arrange(desc(freq)) %>%
  top_n(200) %>%
  wordcloud2(color = "random-light")

```

**This is just an interesting by-product when I am exploring the GDELT dataset. My plan is to utlize the global event data in foreign exchange prediction with LSTM. Coming soon!**

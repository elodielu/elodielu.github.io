---
layout: post
title: "The American mainstream media is shifting their focus from US/us to Trump"
date: 2018-04-19
---

Trump is getting too much attention... 

At least article titles of Washington Post, Wall Street Journal, New York Times, Bloomberg, New Yorker, Cosmopolitan, and Vogue(Yes, fashion magazine Vogue) are giving more and more attention to Trump, only Trump! 

<img src="https://elodielu.github.io/picture/wordcloud.png" width = "1080">

To show this result is not from photoshop but from data science;
* Next I am going to present some numbers to convince you 
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

<img src="https://elodielu.github.io/picture/president.png" width = "1080">

When events happended around the world involve Trump or Obama, how positive are they?

<img src="https://elodielu.github.io/picture/tone.png" width = "1080">

## How to make the data speak
### Data Extraction from BigQuery(SQL)

### Data Wrangeling(R)

### Data Visualization(Tableau and R)

**This is just an interesting by-product when I am exploring the GDELT dataset. My plan is to utlize the global event data in foreign exchange prediction with LSTM. Coming soon!**

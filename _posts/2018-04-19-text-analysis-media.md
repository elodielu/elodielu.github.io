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
* If you still are not buying the story, please go to [this page(code)](https://github.com/elodielu/FxPrediction/blob/master/text_analysis.md) and check how did I get this result through extract data from  GDELT dataset in Google's BigQuery, data wrangling in R, and fancy charts in R and Tableau.


## Let data speak

**Brief intro of the amazing GDELT project**

[GDELT](https://www.gdeltproject.org/) Project monitors the world's broadcast, print, and web news from nearly every corner of every country in over 100 languages and identifies the people, locations, organizations, themes, sources, emotions, counts, quotes, images and events driving our global society every second of every day, creating a free open platform for computing on the entire world.(quote form their webisite) [GDELT schema](https://elodielu.github.io/material/megadata.pdf)

### Data source
<img src="https://elodielu.github.io/picture/data_source.png" width = "1080">

In total I extract 2.9 million records from the US mainstream media starting 2013 to start my analysis. They can be classified into 3 categories for a larger cover of the events;
* Political and general: Wahsington Post, New York Times
* Business: Wall Street Journal, Bloomberg
* Fashion and Culture: Vogue, Cosmopolitan, and New Yorker

### Deeper look into the data
<img src="https://elodielu.github.io/picture/wordcount.png" width = "1080">

<img src="https://elodielu.github.io/picture/publisher2.png" width = "1080">

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

<br><br>
**This is just an interesting by-product when I am exploring the GDELT dataset. My plan is to utlize the global event data in foreign exchange prediction with LSTM. Coming soon!**

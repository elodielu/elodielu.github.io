---
layout: post
title: "Data Pointed out the Biggest, Negative-Reviewed Star in the World - Donald Trump"
date: 2018-04-24
---

Trump is getting too much attention...Errr, negative ones 

I started my analysis in parsing article titles of the US mainstream publishers to see what the world concerns over the year and found this interesting fact that I would like to dig more and share.  **Washington Post, Wall Street Journal, New York Times, Bloomberg, New Yorker, Cosmopolitan, and Vogue(Yes, fashion magazine Vogue) are giving more and more attention to Trump, only Trump!** 

<img src="https://elodielu.github.io/picture/wordcloud.png" width = "1080">

In 2017, here are what are these publishers talking about.

<img src="https://elodielu.github.io/picture/publisher.png" width = "1080">

To show this result is not from photoshop but from data science;
* Next I am going to present some numbers and charts to convince you 
* If you still are not buying the story, please go to [this page(code)](https://github.com/elodielu/FxPrediction/blob/master/text_analysis.md) and check how did I get this result through extract data from  GDELT dataset in Google's BigQuery, data wrangling in R, and fancy charts in R and Tableau.


## Let data speak

**Brief intro to the amazing GDELT project**

[GDELT](https://www.gdeltproject.org/) Project monitors the world's broadcast, print, and web news from nearly every corner of every country in over 100 languages and identifies the people, locations, organizations, themes, sources, emotions, counts, quotes, images and events driving our global society every second of every day, creating a free open platform for computing on the entire world.(quote from their website) [GDELT schema](https://elodielu.github.io/material/megadata.pdf)

### Data source
<img src="https://elodielu.github.io/picture/data_source.png" width = "1080">

In total, I extract 2.9 million records from the US mainstream media starting 2013 to start my analysis. They can be classified into 3 categories for a larger coverage of the events;
* Political and general: Washington Post, New York Times
* Business: Wall Street Journal, Bloomberg
* Fashion and Culture: Vogue, Cosmopolitan, and New Yorker

### Deeper look into the data

In 2017, Top 10 words for these publishers

<img src="https://elodielu.github.io/picture/publisher2.png" width = "1080">

Top 10 words of the Year

<img src="https://elodielu.github.io/picture/wordcount.png" width = "1080">

The above chart indicates that Trump is getting way more attention than Obama. Using word the US as a reference, which has a constant mention around 30k-40k. To be more relative, we are taking Obama's 2015 mention to compare with Trump's 2017 mentions, as these are the years they are in power and not influenced by election. Well, the chart below gives a clear image of the number of mentions of Trump and Obama over the years as well as the percentage of total articles(2.9 million records I extracted) they appear.

We can see that Trump(2017) is getting as much as **5 times** as Obama(2015). And Obama only gets mention **below 5%** among the newsfeeds, while Trump is reaching **20%**.

<img src="https://elodielu.github.io/picture/president2.png" width = "1080">

### More interesting facts when the presidents are mentioned

Average “tone” of all documents containing one or more mentions of this event. **Average tone** can be used as a method of filtering the “context” of events as a subtle measure of the importance of an event and as a proxy for the “impact” of that event. When events happened around the world involve Trump or Obama, how positive are they?

<img src="https://elodielu.github.io/picture/tone2.png" width = "1080">

* Mean Average tone of Obama-related events is **0.19**
* Mean Average tone of Trump-related events is **-2.01**
* 95% confident  that the true difference in means falls in  -2.2246 to -2.1821

The common range for average tone is from -10 to 10, President Trump is really not doing good in this round.

<br>

**Goldstein Scale** captures the theoretical potential impact that type of event will have on the stability of a country. When events happened around the world involve Trump or Obama, what's the impact on the country?

<img src="https://elodielu.github.io/picture/gscore.png" width = "500">    <img src="https://elodielu.github.io/picture/gscore2.png" width = "500">

The media is in much favor of Obama, but the impact of the event of country stability does not seem to be a clear difference big enough to caught by human eyes. Therefore, I ran a statistical test. Well, the t-test shows that there is a significant difference between the Goldstein Scale of Obama-related and Trump-related events.
* Mean Goldstein Scale of Obama-related events is **0.88**
* Mean Goldstein Scale of Trump-related events is **0.72**
* 95% confident that the true difference in means falls in  0.1301 to 0.1962

Obama is doing slightly better in involving with more good events that bring stability to the related country.

#### We are not sure whether Trump is a good president or not yet, but big data tells us that Trump is definitely not a lovable president, especially compared to Obama!

<br>

[Link to the code](https://github.com/elodielu/FxPrediction/blob/master/text_analysis.md)

<br><br>
**This is just an interesting by-product when I am exploring the GDELT dataset. My plan is to utilize the global event data in foreign exchange prediction with LSTM. Coming soon!**

---
image:
  teaser: 1920px-Python_logo_and_wordmark.svg.png

layout: article
title: FinTech Study (1)
date: 2019-04-02
categories: notes
author: chunyi_hsiao
tags: [Python, FinTech]
share: true
---

Playground Intro: A space where contains following infrastructure.

1. __Data Preprocessing__

Data Preprocessing is the most important part for the project. It includes <sup>**1**</sup>collecting, <sup>**2**</sup>arranging and <sup>**3**</sup>preparing the data for feature engineering section.

 - The collection is to crawl the raw data from the published websites like [TWSE](http://www.twse.com.tw/zh/). Here to worry about is to prevent being as DDOS while visiting the server too frequent. If it went smoothly, then store the data with .csv format or other preferences.

 - The arrangement is to standardizing the stored data by using a common library [Pandas](https://pandas.pydata.org). The raw data is temporal, generally contains date, prices and volume, which is also able to derive other indexes. 

 - The preparation for the next is to orgnize mentioned needs above as methods called: **DataCrawler**, **DataLoader** and **DataHandler**.

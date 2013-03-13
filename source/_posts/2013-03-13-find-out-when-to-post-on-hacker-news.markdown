---
layout: post
title: "Find out when to post on hacker news"
date: 2013-03-13 16:15
comments: true
categories:
  - software
  - python
  - javascript
---

As part of my efforts to [promote this new blog](/blog/2013/02/09/a-blog-is-a-mini-startup/), I've been submitting posts to [hacker news](news.ycombinator.com). Not surprisingly, my initial submissions went roughly nowhere. Less than 100 visitors saw the posts.

Stepping back, I decided to think a little more about timing my submissions to get better results. [HN Pickup Ratio](http://hnpickup.appspot.com/) looked like a nice representation of the relevant factors, but it is sadly defunct, as App Engine has been blocked from scraping hacker news. I liked the concept enough to write my own implementation, which is now available here: [HN Notify](http://hnnotify.leknarf.net).

Timing my [last submission](https://news.ycombinator.com/item?id=5335241) was exceptionally successful: it reached the front page of hacker news and was seen by 3,000 readers.

## Concept

Assuming you want your HN submission to reach the front page, then it's important to post at times when scores on the new page are relatively high compared to the front page.

<!-- more -->

This assumes your goal is to reach the front page. I don't actually know how many people skim over the 'new' links, but it's fairly obvious that a far greater number of people only look at the first 30 links on the home page.

For the purposes of discussion, I'm going to assume a very simplistic model of the HN front page: new stories with more points will outrank older stories with less points. That is, I'm ignoring any effects existing karma has on a user's submission and any factors related to when a story gets upvotes. If we assume that a new story needs to get more points than an existing story in order to replace it on the front page, then the following is straightforward:

  - It's a good time to submit when scores on the front page are low. If the lowest-ranked story has 10 points, it will be much easier to replace than if the lowest-ranked story has 100 points.
  - It's a good time to post when scores on the new page are high. If the highest-ranked story on the new page only has 2 points, it doesn't seem likely that your submission will fare much better.

## Differences from HN Pickup

HN Pickup introduced this concept of comparing the lowest-front-page with the highest-new-page scores. It graphs the mean of the last 6 data points in each category along with the ratio of the two averages. From what I've seen, it's fairly rare for new page scores to exceed those on the front page, so I'm just considering the difference between the two. I also don't think the mean is an appropriate statistic, given how easy it is for extremely popular submissions to skew the results. Instead, I'm using the second-highest and second-lowest scores. This provides some protection against outliers.

I disliked the idea of compulsively watching a graph update, so I added an alert mechanism. If you follow [@HNNotify](https://twitter.com/HNNotify) on twitter, you'll be able to receive notifications of opportune submission times. It won't post more than once an hour and also ignores times when the high score on the front page is less than 10, which reduces the noise in the feed.

When you are compulsively waiting for a submission window, it's nice to see the chart update in real-time. This chart updates automatically, without refreshing the page.

Since HN Pickup was blocked, I don't want to scrape HN directly. Instead, this uses the Unofficial Hacker News API as its data source, which has been reliable so far.

## Architecture & Implementation

This sort of real-time data scraping/representation is a great fit for [Firebase](https://www.firebase.com/), which is a very exciting hosted database service. They provide a REST API that lets you write and read data from anywhere, which means I don't need to run a web server. Instead, the project frontend is an entirely static page running on Github Pages, which fetches updated data directly from Firebase using javascript.

The backend is a simple python script running on Heroku. This handles polling the HN API, writing the data to Firebase, and sending notifications to twitter.

The result is a very maintainable weekend project that doesn't actually require me to run any servers. Firebase, Github Pages, Heroku, and Twitter handle all of the responsibilities I'd usually need a server for, without forcing me to deal with security, scalability, or monitoring.

Source code is available on [Github](https://github.com/leknarf/hn-notify).

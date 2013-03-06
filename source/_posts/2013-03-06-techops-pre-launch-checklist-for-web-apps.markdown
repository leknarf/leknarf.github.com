---
layout: post
title: "TechOps pre-launch checklist for web apps"
date: 2013-03-06 11:49
comments: true
categories:
  - software
  - ops
---

As my startup gears up for our first paid marketing campaign, I've been giving some thought to the necessary preparations a developer should go through before driving some traffic to a web app.

In general, the goal isn't to prevent every possible problem. In addition to being impossible, any attempts to do so would almost certainly involve premature engineering. Instead, my goal is to be adequately prepared for unforeseeable problems. The important thing is to ensure I'll be notified when a problems occur and that I'll have enough information to investigate and fix said problems.

We're hosted on AWS, so this list assumes you're running in a similar environment. Managed platforms like Heroku take care of much of this for you.

In no particular order, the following should be completed before aggressively promoting a new web app:

<!-- more -->

# Prepare for disaster
  - Setup fully automated, zero-downtime deployments: Once people are using your site, you can't bring down the server to make changes. If you haven't already set up a smooth deployment process, this should be your first priority.
  - Automatically collect database backups and store in S3: hourly x 48, daily x 14, weekly x 8, and monthly x forever.
  - Restore the database from these backups to a developer's machine at least once.
  - Ship your log files to a hosted retention service (Splunk, Loggly, Papertrail). Or prepare your own scripts to copy files to S3.
  - Setup application performance monitoring and alerting (New Relic). If your site gets a sudden traffic spike, this should notify you that you've exceeded your capacity.
  - Server monitoring (New Relic): If your server is running out of hard drive space or if an errant process is consuming all the CPU/RAM, you'll want to get an email before the site goes down.
  - Uptime alerting/monitoring (New Relic and Pingdom): If the site does go down, you'll obviously want to know about it. New Relic does this via email, but Pingdom's mobile app is free and excellent.
  - Error alerting (Airbrake, Exceptional): Again, if something goes wrong, you want to find out about it.
  - If your application doesn't require a high level of user privacy, then you should be able to log into your site as a given user. Odd problems will pop up that only affect one user. It's a lot easier to investigate when you can see exactly what that user is seeing.

# Basic security checks
  - Upgrade to the latest versions or install security patches for all the major components of your stack, including your framework (Rails/Django/etc.), web server (nginx, apache, etc.), and OS.
  - Install Fail2Ban on any publicly available servers.
  - Configure firewalls to restrict access to any server that don't need to be publicly available (i.e. your database, message broker, etc.) and block all but the necessary ports.
  - Change any horrendously insecure passwords you may have. Many startups use absurd passwords like "password" or "test123" for their admin accounts when starting out. These should be changed as soon as possible.

# Prep for scaling
  - Serve static assets from S3 or a CDN (CloudFlare, CloudFront)
  - Setup a caching layer (Memcached, Redis, Varish)
  - Point your DNS entry to a load balancer, not an individual server. ELB makes this easy. If you do take on a massive amount of traffic, you can always add more web servers to the load balancer.
  - You should have the ability to scale up to N web servers at any time (Chef).
  - If something odd happens on one of your servers, the two points above make the solution easy: just spin up a new web node, add it to the load balancer, and then remove the failing node. Don't bother trying to fix or even diagnose one-off failures.

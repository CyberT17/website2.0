---
title: "securityblogs.xyz"
summary: "A simple webpage that aggregates security related news and blog posts"
date: 2024-03-16T15:12:26-05:00
draft: false
ShowReadingTime: true
author: ["Kevin Patel"]
ShowToc: false
---

{{< github-repo url="CyberT17/secblogs" >}}

[Security Blogs](https://securityblogs.xyz/) (secblogs) is a simple website that aggregates a bunch of news sites and blogs and displays it on a single page. Original inspiration came from [Engineering blogs](https://engineeringblogs.xyz/) and I ended up using a similar layout for secblogs.

The idea was born out of a necessity to streamline the process of sifting through numerous websites daily to catch up on essential readings. Secblogs is designed to be a one-stop destination that provides an easy way to consume security related articles.

### Some Technical Notes

The page is generated using HTML templating provided by Go. The [Github repo](https://github.com/CyberT17/secblogs) has a Github Action build plan setup which runs the Go code every 30 minutes to fetch and parse the latest articles. It creates the `index.html` and pushes it to Cloudflare Pages where the page is hosted. IMO using github actions for this seems a bit hacky which is why I would eventually like to move the build process out of Github Actions to somewhere else.

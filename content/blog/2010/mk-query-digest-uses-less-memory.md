---
title: mk-query-digest uses less memory
date: "2010-05-19"
url: /blog/2010/05/19/mk-query-digest-uses-less-memory/
categories:
  - Databases
  - Open Source
---
Daniel changed [mk-query-digest](http://www.maatkit.org/) to use much less memory. It parsed and aggregated a 2GB MySQL slow query log file in a few dozen megabytes of memory for me yesterday. Thanks to Facebook for sponsoring this work.



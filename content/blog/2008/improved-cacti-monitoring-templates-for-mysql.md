---
title: Improved Cacti monitoring templates for MySQL
date: "2008-04-27"
url: /blog/2008/04/27/improved-cacti-monitoring-templates-for-mysql/
categories:
  - Monitoring
  - Databases
---

As promised, I've created some improved software for monitoring MySQL via [Cacti](http://www.cacti.net/). I began using the [de facto MySQL Cacti templates](http://faemalia.net/mysqlUtils/) a while ago, but found some things I needed to improve about them. As time passed, I rewrote everything from scratch. The resulting templates are much improved.

You can grab the templates by browsing the source repository on the project's homepage.

In no particular order, here are some things I improved:

*   Standard polling interval and graph size by default.
*   Full captions on every graph; you don't have to guess at how big the values are. Each graph has current, max, and average values printed at the bottom for every value on it.
*   Much more data is captured. I've graphed almost everything I could think of.
*   The graphs are grouped better. Most graphs have only related values. There are some exceptions, but not many.
*   The templates don't hijack your existing installation. They don't depend on or alter anything in your default Cacti installation.
*   The script that gathers the data is totally rewritten from scratch, and much improved. For example, [the math works on 32-bit systems](http://www.mysqlperformanceblog.com/2007/03/27/integers-in-php-running-with-scissors-and-portability/). It has caching built-in so [each poll cycle results in just one request to the server, instead of one request per graph](http://forums.cacti.net/viewtopic.php?t=26448). (This is a weakness of Cacti I'm trying to work around). It also has debugging aids and other good coding stuff.
*   By default, it assumes you have the same username and password across every server you're monitoring, so you don't have to fill in a username and password for every single graph you create.
*   One data template == one graph template. This helps work around another Cacti limitation.
*   Lots more. Honestly I can't really remember everything I've done. I'm sure you'll help me remember by asking me how to get X feature working the way you want, and I'll go "oh, yeah, that's another thing I improved..."

Cacti templates are very laborious to create if they're complex at all; it takes a long time and is very error-prone. Instead of doing it through Cacti's web interface and exporting a huge XML file, I eliminated the redundancies and created a small, easy-to-maintain file from which I generate the XML template with a Perl script. This gives the added benefit of letting me (or you) generate templates with different parameters such as polling interval or graph size. The README file has the full details. However, I've pre-generated a set of templates that matches Cacti's defaults, so you can probably just use that.

This has taken a lot of time. In particular, I spent a lot of time working on it at my former employer, [The Rimm-Kaufman Group](http://www.rimmkaufman.com) (kudos to them for letting me open-source the work) and I just spent most of my weekend writing the scripts to convert from the compact format to XML templates, so it's possible to maintain these beasts. Plus I had to develop the compact format, too. This took a lot of time because I had to understand the Cacti data model, which is pretty complex.

PS: You may also be interested in [Alexey Kovyrin's list of templates for monitoring servers](http://blog.kovyrin.net/2007/10/06/useful-cacti-templates-to-monitor-your-servers/).



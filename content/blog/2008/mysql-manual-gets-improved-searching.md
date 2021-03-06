---
title: MySQL manual gets improved searching
date: "2008-07-28"
url: /blog/2008/07/28/mysql-manual-gets-improved-searching/
categories:
  - Databases
---
Hooray! The [MySQL reference manual](http://dev.mysql.com/doc/) has a new search system. It now uses a [Google Appliance](http://www.google.com/enterprise/search.html) and the results should be a lot better. The old system was not very helpful. It used to break config variables into multiple words and search on them individually and give a billion results I didn't care about. I've just tried to search for some things like `key_buffer_size` and got results I think are very useful.

I love the MySQL manual. It is a great example of quality software documentation. As someone recently mentioned, it is not released under a Free license though---that would be a great improvement, too!

When did this change happen, by the way? Maybe it's been there for a while and I just missed it because I grew accustomed to using Google search instead.

Edit: I actually would suggest a change to this search, too. It's the same change I have suggested in the past: put the document title in front of the manual's title. Instead of "MySQL :: MySQL 5.1 Reference Manual :: 7.4.6.6 Restructuring a Key ..." I would rather see "Restructuring a Key Cache :: MySQL 5.1 Reference Manual". (Note that the title gets truncated as-is, and it's hard to see in the browser's titlebar/tab/system taskbar).



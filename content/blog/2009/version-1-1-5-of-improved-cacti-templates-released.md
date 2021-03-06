---
title: Version 1.1.5 of improved Cacti templates released
date: "2009-12-13"
url: /blog/2009/12/13/version-1-1-5-of-improved-cacti-templates-released/
categories:
  - Monitoring
  - Databases
  - Operations
  - Programming
tags:
  - PostgreSQL
---
I've released version 1.1.5 of my [improved Cacti templates](http://code.google.com/p/mysql-cacti-templates/) for MySQL and other components of a LAMP application. This is a pure bug-fix release. One of the bug fixes prevents spikes in graphs, but requires you to rebuild your RRD files. There are [upgrade instructions](http://code.google.com/p/mysql-cacti-templates/wiki/UpgradingTemplates) on the project wiki for this and all releases. Use the [project issue tracker](http://code.google.com/p/mysql-cacti-templates/issues/list) to view and report issues, and use the [project mailing list](http://groups.google.com/group/better-cacti-templates) to discuss the templates and scripts.

The full changelog follows:

```
2009-12-13: version 1.1.5

  * Support for getting replica lag via mk-heartbeat was broken (issue 87).
  * The memcached stats command hung because it lacked "quit" (issue 65).
  * The COUNTER data type caused spikes; switched to DERIVE instead (issue41).
  * LOCK WAIT in an InnoDB transaction could cause an error (issue 91).
  * The cache file name didn't include the MySQL port (issue 82).
  * Added the -q option to the SSH command to quell missing homedir warnings.
  * The --port option to the MySQL templates could not be null.
  * The log_bytes_flushed and log_bytes_written were renamed (issue 81).
```



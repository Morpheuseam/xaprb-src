---
title: "How to write INSERT IF NOT EXISTS queries in standard  SQL"
date: "2005-09-25"
url: /blog/2005/09/25/insert-if-not-exists-queries-in-mysql/
categories:
  - Databases
---
If necessary, INSERT IF NOT EXISTS queries can be written in a single atomic statement, eliminating the need for a transaction, and without violating standards. In this article I'll explain several ways to write such queries in a platform-independent way.

### Motivation

Suppose a table of urls has a unique index on the url:

```
create table urls(url varchar(200) primary key);
```

Now suppose I want to insert a row in a single statement, without using a transaction, and I only want the row to get inserted if the url isn't already in the table. I don't want any warnings or errors. I just want to issue a normal `INSERT` statement and know the url is now in the table.

Standard SQL provides no means of doing this. There's no syntax like this:

```
insert if not exists into url(url) values(...)
```

In Microsoft SQL Server, I can use an `IF` statement:

```
if not exists (select * from url where url = ...)
   insert into url...
```

This has to be wrapped in a transaction to avoid a race condition, though. Otherwise someone might insert a row between the time I check the table and when I insert the row. I want to do this in a single statement, without a transaction.

### Several solutions

One solution is to use a [mutex table](/blog/2005/09/22/mutex-tables-in-sql/):

```
insert into urls(url)
select '/blog/'
from mutex
    left outer join urls
        on urls.url = '/blog/'
where mutex.i = 1 and urls.url is null;
```

There are more flexible variations on this technique. Suppose there is no unique index on the url column. If desired, it is possible to insert several values in a single statement by changing the `WHERE` clause:

```
insert into urls(url)
select '/blog/'
from mutex
    left outer join urls
        on urls.url = '/blog/'
where mutex.i < 5 and urls.url is null;
```

Now suppose the requirements specify up to three duplicate entries in the table, and each insert should add a single row. It is possible to insert a row at a time while enforcing the requirement with the following query:

```
insert into urls(url)
select '/blog/'
from mutex
    left outer join urls
        on urls.url = '/blog/'
where mutex.i = 1
group by urls.url
having count(*) < 3;
```

This query shows the input to the `INSERT` statement:

```
select '/blog/', count(*)
from mutex
    left outer join urls
        on urls.url = '/blog/'
where mutex.i = 1
group by urls.url;
```

If this article was useful to you, you should [subscribe](/index.xml) to stay current with my upcoming articles. It's free and convenient.

**Edit 2006-02-26** See also my article on using this and other techniques to do [flexible INSERT and UPDATE statements in MySQL](/blog/2006/02/21/flexible-insert-and-update-in-mysql/).



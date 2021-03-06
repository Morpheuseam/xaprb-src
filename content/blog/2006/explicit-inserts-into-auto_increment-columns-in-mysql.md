---
title: How MySQL decides to AUTO_INCREMENT a value
date: "2006-04-23"
url: /blog/2006/04/23/explicit-inserts-into-auto_increment-columns-in-mysql/
categories:
  - Databases
---
It is possible to explicitly insert values into an `AUTO_INCREMENT` in MySQL, but sometimes these inserts cause confusing behavior. In this article I'll explain that behavior.

### Background

Suppose I have the following table:

```
create table number (
    number int not null auto_increment primary key
) ;
```

Now suppose I insert some values into the primary key explicitly, bypassing the `AUTO_INCREMENT` feature:

```
insert into number(number) values (-100);
select * from number;
+--------+
| number |
+--------+
| -100   |
+--------+
```

So far, so good. Now, I'll try to insert the value 0:

```
insert into number(number) values (0);
select * from number;
+--------+
| number |
+--------+
| -100   |
| 1      |
+--------+
```

Why is the value 1? It turns out that, by default, MySQL generates the next `AUTO_INCREMENT` value for the column when either `NULL` or 0 is inserted. The next value is *not* the maximum value plus one; it is the next value larger than an internal counter MySQL maintains, which starts at 0 by default.

This can be configured. It's possible to set the [`NO_AUTO_VALUE_ON_ZERO`](http://dev.mysql.com/doc/refman/5.0/en/server-sql-mode.html) so it allows explicitly inserted zero values, as follows:

> `NO_AUTO_VALUE_ON_ZERO` affects handling of `AUTO_INCREMENT` columns. Normally, you generate the next sequence number for the column by inserting either NULL or 0 into it. `NO_AUTO_VALUE_ON_ZERO` suppresses this behavior for 0 so that only NULL generates the next sequence number.

The MySQL manual also has more detailed information on [`AUTO_INCREMENT` behavior](http://dev.mysql.com/doc/refman/5.0/en/example-auto-increment.html).



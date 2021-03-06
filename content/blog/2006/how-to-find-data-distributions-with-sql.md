---
title: How to find data distributions with SQL
date: "2006-06-10"
url: /blog/2006/06/10/how-to-find-data-distributions-with-sql/
credit: "https://unsplash.com/photos/4Y_bVu4j0cA"
image: "/media/2006/06/unsplash-photos-4Y_bVu4j0cA.jpg"
description: "This article explains how to group data into arbitrarily-sized buckets and count the number of entries in each."
categories:
  - Databases
---
In an earlier article I wrote about [grouping data into ranks with a catch-all bucket](/blog/2005/09/28/grouping-data-with-catch-all-ranks/). In this article I'll show you how to group the data into variable-sized buckets any way you please.

<!--more-->

This query came up when a business partner asked me to send over the distribution of some hierarchical data. It's the same category/subcategory/item data as in my article about [optimizing joins and subqueries](/blog/2006/04/30/how-to-optimize-subqueries-and-joins-in-mysql/). The partner wanted to know, broadly speaking, "how many subcategories have very small and very large numbers of items?"

I could have done a simple query:

```sql
select category, count(*) as num
from item group by category;
```

That would have resulted in one row for every category, which would have been thousands of rows---not very useful for answering the question. I needed just a few rows, showing how many subcategories are large and how many are small. I started by filling a temporary table with my desired size ranges:

```sql
create temporary table ranges (
   s int not null, -- start of range
   e int not null  -- end of range
);

insert into ranges (s, e) values
   (1, 1),
   (2, 10),
   (11, 50),
   (51, 100),
   (101, 200),
   (201, 500),
   (501, 1000),
   (1000, 9999);
```

Then I grouped the data by subcategory, joined it against the ranges by size, and grouped again by range, counting and summing the sizes of each of the subcategories to get totals. In the query below, I analyze the distribution of items in category 14:

```sql
set @category := 14;

select concat(s, '-', e) as range, sum(num) as total, count(*) as num
from ranges
inner join (
   select s.id, count(*) as num
   from subcategory as s
      inner join item as i on i.subcategory = s.id
   where s.category = @category
   group by s.id
) as x on x.num between ranges.s and ranges.e
group by ranges.s, ranges.e;
```

The results look roughly like this:

|     range | total |   num |
|----------:|------:|------:|
|       1-1 | 10038 | 10038 |
|      2-10 |  4032 |  1012 |
|     11-50 |   300 |   123 |
|    51-100 |    72 |     1 |
| 1000-9999 |  3040 |     2 |

The distribution is clearly biased towards single-item categories, with the occasional huge category. Part of the goal was to rewrite our grouping algorithm to chunk things together in groups of 20 to 80 (depending on a variety of complex factors I won't explain here). This query helped us get a realistic picture before and after the algorithm change.



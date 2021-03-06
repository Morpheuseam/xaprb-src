---
title: How to quote and encode XML attribute values
date: "2005-10-21"
url: /blog/2005/10/21/quotes-around-xml-attribute-values/
categories:
  - Programming
---
Attribute values in XML are usually double-quoted, but single-quotes can be used as well, according to the relevant part of the [XML Spec](http://www.w3.org/TR/REC-xml/#NT-AttValue). Here is the production:

```
[10] AttValue ::= '"' ([^<&"] | Reference)* '"'
                  | "'" ([^<&'] | Reference)* "'"
```

In plain English: an attribute consists of

*   a double or single quote
*   any number of the following: 
    *   any character but <, & or " OR
    *   an entity reference
*   the same character that was used to begin the attribute (double or single quote)

What's most interesting about this to me is that a < is forbidden inside attribute values, but a > is not. I always assumed both were illegal.

This is why I love reading specs. The XML spec is a great example of clear and terse writing. There is no chance for confusion when reading the productions themselves! Any secondary source can only obscure the matter, in my opinion.



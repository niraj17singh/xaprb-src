---
title: MySQL kill could be so much more exciting
date: "2012-08-28"
url: /blog/2012/08/28/mysql-kill-could-be-so-much-more-exciting/
categories:
  - Databases
---
When I kill a query or connection, whoever is running it gets a boring message about what happens. Wouldn't it be fun and useful to be able to specify the error message the user should see? Imagine the possibilities:

```
mysql> KILL 10282, "Sorry, no cigar today. Try again tomorrow."
```

Joking aside, relevant error messages would be great for all involved.



---
title: mk-query-digest now supports Postgres logs
date: "2010-02-20"
url: /blog/2010/02/20/mk-query-digest-now-supports-postgres-logs/
categories:
  - Databases
  - Open Source
  - Programming
tags:
  - PostgreSQL
---
Maatkit does more than just MySQL. I've just committed a new version of [mk-query-digest, a powerful log analysis tool](http://www.maatkit.org/doc/mk-query-digest.html), with support for Posgtres logs, in both syslog and stderr format. I'm hoping that people will give this a spin in the real world. I have lots of test cases, but that's never enough; I'm looking for people to crunch their logs and let me know if anything breaks.

A brief tutorial:

```
# Get it
$ wget http://www.maatkit.org/trunk/mk-query-digest

# Run it
$ perl mk-query-digest --type pglog /path/to/log/file

# Learn about it (search for the string "pglog")
$ perldoc mk-query-digest
```


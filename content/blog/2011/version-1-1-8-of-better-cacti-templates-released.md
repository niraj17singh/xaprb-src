---
title: Version 1.1.8 of Better Cacti Templates released
date: "2011-01-22"
url: /blog/2011/01/22/version-1-1-8-of-better-cacti-templates-released/
categories:
  - Monitoring
  - Databases
  - Operations
  - Programming
tags:
  - PostgreSQL
  - MongoDB
---
I've released version 1.1.8 of the [Better Cacti Templates](http://code.google.com/p/mysql-cacti-templates/) project. This release includes a bunch of bug fixes and several important new graphs. There are [graphs](http://code.google.com/p/mysql-cacti-templates/wiki/MySQLTemplates#MySQL_Query_Response_Time_%28Microseconds%29) for the new [response-time statistics exposed in Percona Server](http://www.percona.com/docs/wiki/percona-server:features:response_time_distribution), and a new set of graphs for [MongoDB](http://code.google.com/p/mysql-cacti-templates/wiki/MongoDBTemplates).

> [VividCortex](https://vividcortex.com/) is the startup I founded in 2012. It's the easiest way to monitor what
> your servers are doing in production and I consider it far superior to Cacti. VividCortex offers [MySQL performance
> monitoring](https://vividcortex.com/monitoring/mysql/) and [PostgreSQL
> performance management](https://vividcortex.com/monitoring/postgres/) among many
> other features.

The full changelog follows.

```
2011-01-22: version 1.1.8

  * The cache file names could conflict due to omitting --port (issue 171).
  * Load-average parsing did not work correctly at high load (issue 170).
  * The --mpds option to make-template.pl did not create new inputs (issue 133).
  * The url and port were reversed in the Nginx commandline (issue 149).
  * Added $nc_cmd to ss_get_by_ssh.php (issue 154, issue 152).
  * InnoDB Transactions and other graphs showed NaN instead of 0 (issue 159).
  * Added graphs for Percona Server response-time distribution (issue 158).
  * Added graphs for MongoDB (issue 136).
  * Added a minimum option to the template construction logic (issue 169).
  * Added memtotal for Memory (issue 146).
  * make-template.pl sanity checks were too strict (issue 168).
```



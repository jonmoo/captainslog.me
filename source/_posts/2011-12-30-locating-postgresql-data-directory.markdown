---
layout: post
title: Locating PostgreSQL data directory
tags:
- postgresql
- tips
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
<p>Use a simple psql query to find the location of the data directory
```
postgres=# SHOW data_directory;
data_directory
------------------------------
/var/lib/postgresql/8.4/main
(1 row)
```

Or

```
postgres=# select setting from pg_settings where name = 'data_directory';
           setting
------------------------------
 /var/lib/postgresql/8.4/main
(1 row)
```

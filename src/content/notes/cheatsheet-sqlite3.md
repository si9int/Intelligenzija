---
title: 'SQLite3 Cheatsheet'
description: ''
pubDate: 'Nov 28 2025'
---

## Quick Reference

```
$> sqlite3
$> sqlite3 database.db

sqlite> .help
sqlite> .open database.db
sqlite> .databases
sqlite> .dump [database|table]

sqlite> .tables
sqlite> alter table [table] add column [name] TEXT;
sqlite> alter table [table] rename to [name];
sqlite> drop table [table];

sqlite> select * from [table];
sqlite> select count(*) from [table];
sqlite> select x, y from [table];
sqlite> select * from [table] where [column] > 100 order by [column] ASC limit 10;

sqlite> insert into [table] (x, y) values ('a', 'b');
sqlite> update [table] set x = 'b' where [column] = [value];
sqlite> delete from [table] where [column] = [value];

sqlite> .mode csv
sqlite> .output data.csv
sqlite> .import data.csv [table]
sqlite> .read script.sql

sqlite> .exit 
sqlite> .quit 
```
MonetDB
=======

Reference: [monetdbd](https://www.monetdb.org/Documentation/monetdbd)

## monetdbd
Reference: [monetdbd](https://www.monetdb.org/Documentation/monetdbd)
Each monetdb demon is associated with a **dbfarm**. Only one instance of *monetdbd* can be running on a dbfarm.

1. Create a dbfarm: `monetdbd create ~/my-dbfarm`
2. Show properties: `monetdbd get all ~/my-dbfarm`
3. Start the demon on a dbfarm: `monetdbd start ~/my-dbfarm`
4. Shutdown: `monetdbd stop ~/my-dbfarm`

## monetdb

1. Create a new database: `monetdb create tpch`
2. A newly-created DB is in *locked* state. Need to release it for use: `monetdb release tpch`
3. Show status of all databases in the dbfarm: `monetdb status`

## mclient
Reference: [mclient man-page](https://www.monetdb.org/Documentation/mclient-man-page)

### Start

``mclient -u monetdb -d tpch``


**Pseudo-passwordless start**: put the username and password in a file *.monetdb*:
```bash
$ cat .monetdb
user=monetdb
password=monetdb
```

### Backslash commands


Purpose        | PostgreSql    | MonetDB
---------------|-------------|-----------:
Change DB      | \c tpch     | no way
List all DB    | \l          | no way
Describe table | \d [tpch]   | \d [tpch]
Execute script | \i file.sql | \\\< file.sql
Quit           | \q          | \q

## mclient examples

### Load a table from csv
```sql
COPY INTO customer from '/home/neo/tpch/tpch_2_16_1/dbgen/customer.csv' USING DELIMITERS '|','\n' NULL AS '';
```

### Export a table/query result to csv
```sql
COPY (select encode_date(l_shipdate) from "sys"."lineitem") INTO '/tmp/lineitem.l_shipdate.txt' NULL AS '0';
```
Notice: file path must be **absolute path**.

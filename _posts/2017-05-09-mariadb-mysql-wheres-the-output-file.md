---
layout: post
title: "Missing MySQL / MariaDB output files"
date: 2017-05-09
---
If you ever want to output something from a MySQL database into a file, a query you've cooked up that someone wants in a CSV spreadsheet, here is the SQL command to do that: 
```
SELECT Your_Column_Name
 FROM Your_Table_Name
 INTO OUTFILE 'Filename.csv'
 FIELDS TERMINATED BY ','
 ENCLOSED BY '"'
 LINES TERMINATED BY '\n';
```
Thing is, I did this the other day and couldn't find the output file. The SQL command didn't give any error. I looked in `/var/tmp` & `/tmp`, nothing. 
A quick google search threw up the following command to check where the tmpdir is listed:
```
 MariaDB [my_database]> show variables like 'tmpdir';
+---------------+----------+
| Variable_name | Value    |
+---------------+----------+
| tmpdir        | /var/tmp |
+---------------+----------+
```
I had already checked `/var/tmp` - nothing there. 

I finally found the files in ```/var/lib/mysql/my_database1``` the main DB directory that contains the data files for each table!

This was MariaDB 10.1.21-3, running on Fedora 25. 

Missing MySQL / MariaDB output files. 

Sometimes you'll want to output something from the database, a query you've cooked up that someone wants in a spreadsheet. 
Here's the SQL command to get the data out into a file. 

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

Finally found the files in ```/var/lib/mysql/my_database1``` the main DB directory that contains the data files for each table.

This was MariaDB 10.1.21-3, running on Fedora 25. 

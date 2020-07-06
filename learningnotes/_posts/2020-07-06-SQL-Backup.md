---
image:
  teaser: Bayes.jpeg

layout: article
title: SQL Backup
date: 2020-07-06
categories: notes
author: chunyi_hsiao
tags: [SQL]
share: true
---

I have waseted two days overwrite the data on our production database without backup...

To record how I did for mentioning that the backup is really important before we update/delete.

refer to this [link](https://blog.yowko.com/sql-server-backup-restore/), I choose "**Generate Scripts...**"
- Right click the engine and select **Tasks** and find the "**Generate Scripts...**"  
- Select specific database objects - the target table
- In Advanced, I select "**Script DROP and CREATE**" and "**Data only**"
 
 This process will generate a script that delete your table and then multi-insert your backup data. It's quite simple. 
 
 Hmm... But if we accidently modify all data of one specific column. Luckly you got a teammate to help you to duplicate the data before you did the stupid thing to a temporary server.
 
 But that table cannot be Deleted-then-Insert due to **PRIMARY KEY CONSTRAINT**. What should you do?
 
 Because I can't use SQL to iterate the data from the table in  temporary server then update to target table. 
 
 - So I write and save index and rollback column data into a csv file.
 - And I run a Python script to read the csv file and update to my target table.

```python
import pyodbc 
import pandas as pd
conn = pyodbc.connect('Driver={SQL Server};'
                      'Server=RON\SQLEXPRESS;'
                      'Database=ProdDB;'
                      'Trusted_Connection=yes;')
 
cursor = conn.cursor()
df = pd.read_csv('shit.csv').fillna('NULL')
for row in df.iterrows():
    id = row['id']
    data = row['data']
    if data == 'NULL':
        update = "USE ProdDB GO UPDATE {data} WHERE id = {id}".format(data, id)
    else:
        update = "USE ProdDB GO UPDATE {'" + data + "'} WHERE id = {id}".format(id)
    cursor.execute(update)
    conn.commit()
```

Therefore I successfully rollback the data.


***Reference***  
[3 Ways to Backup](https://blog.yowko.com/sql-server-backup-restore/)  
[Update to SQL in Python](https://datatofish.com/update-records-sql-server/)

---
layout: post
author: Chaz Lee
title: Bug fixing when setting up Django + MySQL cloud
date: 2020-07-06T08:28:20.613Z
thumbnail: /assets/img/posts/hello.jpg
category: Tutorial
summary: Issues & links to fix them
---
#####  __Guides to set up the django?__
#####   Solution: 
-  [Django official doc](https://docs.djangoproject.com/en/2.1/ref/settings/#auth-password-validators)
-  [Google cloud sdk doc](https://cloud.google.com/sdk/docs)
-  [Run Django with flex env](https://cloud.google.com/python/django/flexible-environment)


&nbsp;
&nbsp;
##### 'Ubuntu 18.04 LTS _Bionic Beaver_ - Release amd64 (20180426)' in the drive
  ```'/media/cdrom/' and press [Enter]``` __, [refer link](https://askubuntu.com/questions/1056309/i-cant-install-any-new-software-i-keep-getting-this-message)
#####   Solution: 
1.  Open __Software & Updates__ (or software-properties-gtk from terminal), in the area named __Installable from CD-ROM/DVD__ uncheck the __Cdrom with Ubuntu 18.04 (Bionic Beaver)__.
2.  Then make do not have checked __Cdrom with Ubuntu 18.04 'Bionic Beaver'__ on Other __Software__ tab:
3.  Keep your system secure on Updates tab enable security updates (__bionic-security, bionic-updates, bionic-backports__):

&nbsp;
&nbsp;
##### django.db.utils.OperationalError: (1045:Access denied for user 'root'@'localhost' (using password: YES) __
#####   Solution: 
Add below import to where MySQLdb is import, [refer link](https://stackoverflow.com/questions/55657752/django-installing-mysqlclient-error-mysqlclient-1-3-13-or-newer-is-required)
```python
import pymysql
pymysql.version_info = (1, 3, 13, "final", 0)
pymysql.install_as_MySQLdb()
```

&nbsp;
&nbsp;
##### django.db.utils.OperationalError: (1045:Access denied for user 'root'@'localhost' (using password: YES) __
#####   Solution: 
Tried with below method get next errow below
-  [Stack over1](https://stackoverflow.com/questions/33750895/django-db-utils-operationalerror-1045-access-denied-for-user-userlocalh)
-  [Django offical Doc](https://docs.djangoproject.com/en/2.1/topics/auth/passwords/#password-validation)


&nbsp;
&nbsp;
#####  __ERROR 2003 (HY000): Can't connect to MySQL server on '127.0.0.1' (111) when run ```mysql -h 127.0.0.1 -P 3306 -u root -p``` or ```mysql -u root -p``` __
#####   Solution: 
SQL configuration issue, ~~still need to fix~~. Check blow links for reference
-  [Stack over1](https://stackoverflow.com/questions/11657829/error-2002-hy000-cant-connect-to-local-mysql-server-through-socket-var-run)
__Update__: Reason is we use cloud sql in setting instead of local sql, so need to use below cmd to set up gcloud sql
```bash
	a) $./cloud_sql_proxy -instances="plantdatabase-51026:us-central1:mysql-plant-database"=tcp:3306
```
	b) if this doesn't work, mysqld is probably using port 3306 run 
  ```bash 
  $sudo /etc/init.d/mysql stop
  ```
	c) try a) again

&nbsp;
&nbsp;
#####  pymysql.err.OperationalError: (1045, "Access denied for user 'username'@'cloudipproxy' (using password: YES)") __ after solve above error when run ```python manage.py makemigrations```
#####   Solution: 
Reason is not set up the gcloud sql user or not set correct password, see [Stack over1](https://stackoverflow.com/questions/41645309/mysql-error-access-denied-for-user-rootlocalhost)
In gcloud SQL console page, go to user tab and create a new user name and password or update your existing username and password. Make sure the username and password is the same with what is in the setting.py.

&nbsp;
&nbsp;
#####  django.db.utils.InternalError: (1049, "Unknown database 'databasename'") __ when run ```python manage.py makemigrations``` after solve above error when run ```python manage.py makemigrations```
#####   Solution: 
Reason is not create corresponding database for your data.
In gcloud SQL console page, go to database tab and create a new database and run make migration again.

&nbsp;
&nbsp;
#####  plantsite.EcoRegion.photo: (fields.E210) Cannot use ImageField because Pillow is not installed.``` after solve above error when run ```python manage.py makemigrations```
#####   Solution: 
In bash run ```bash python -m pip install Pillow ``` to install Pillow. (After installing run migration then no error.)

&nbsp;
&nbsp;
#####  Exception Type:	IndexError Exception Value:	list index out of range after solve above error and migration until when run python manage.py runserver. (The server is running but the web give below error)
#####   Solution: 
Seems related to no actual table or data in the database, need to fix it by creating a table. 
- [REF1 codelab creating table with gcloud terminal](https://codelabs.developers.google.com/codelabs/cloud-create-cloud-sql-db/index.html?index=..%2F..index#6)
- [REF2 codelab creating table with MySQL client](https://dataedo.com/docs/connecting-to-google-cloud-sql)
- [REF3 MySQL cmd to create table](https://dev.mysql.com/doc/mysql-tutorial-excerpt/8.0/en/examples.html)
Run following cmd
```bash
mysql>  CREATE TABLE plants_csv(id INT UNSIGNED, PRIMARY KEY(id));
Query OK, 0 rows affected (0.02 sec)
```
then ```select id from plants_csv``` could get id for each row but not able to get other columns. and try to run sever still get out of range error.(Thinking maybe only add one column, so would add all columns and try again).

```sql
CREATE TABLE plants_csv( id INT UNSIGNED, nativeadapted VARCHAR(20), image VARCHAR(500), name VARCHAR(100), nickname VARCHAR(100), planttype VARCHAR(50), lightreq VARCHAR(50), waterdemand VARCHAR(50), landscapeuse VARCHAR(200), ornamentalvalue VARCHAR(50), wildlifevalue VARCHAR(50), season VARCHAR(50), plantform VARCHAR(50), plantspread VARCHAR(20), plantheight VARCHAR(20), deciduousevergreen VARCHAR(50), soil VARCHAR(200), reproduction VARCHAR(500), sciname VARCHAR(50), lat VARCHAR(10), lon VARCHAR(10), econregion VARCHAR(500), statepark VARCHAR(50), lifecycle VARCHAR(20), edibility VARCHAR(500), zone VARCHAR(20), endangered VARCHAR(50), eco
regionids VARCHAR(50), search_times INT UNSIGNED, description CHAR(30), PRIMARY KEY(id));                                                                                                                                  
Query OK, 0 rows affected (0.02 sec)
```
Use above sql to create the table and add the csv, able to query in gcloud terminal but still get index of range error on running server. And try later get below error(~think is django not correctly resolved as django -v not show django: command not found but already satisfied when try to install~, use ```django-admin version```)
    __CR.CR_SERVER_LOST, "Lost connection to MySQL server during query")
pymysql.err.OperationalError: (2013, 'Lost connection to MySQL server during query')__
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
SQL configuration issue, still need to fix. Check blow links for reference
-  [Stack over1](https://stackoverflow.com/questions/11657829/error-2002-hy000-cant-connect-to-local-mysql-server-through-socket-var-run)



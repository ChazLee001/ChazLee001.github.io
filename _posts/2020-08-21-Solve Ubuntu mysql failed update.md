---
layout: post
author: Chaz Lee
title: Bugs fixed for ubuntu mysql crash on updating
date: 2020-08-21T11:47:20.613Z
thumbnail: /assets/img/posts/hello.jpg
categories: Bug
summary: knowledge summary
---
#####  __installation of MySQL is already upgraded to 5.7.31 -> dpkg was interrupted, you must manually run 'sudo dpkg --configure -a' to correct the proble__

This is caused by mysql package not correctly recognize its version, and would introduce the apt-get cmd failed `dpkg was interrupted, you must manually run 'sudo dpkg --configure -a' to correct the proble` the solution is to purge sql and reinstall it. as [this link](https://askubuntu.com/questions/825579/upgrading-to-mysql-5-7-15-crashes-on-ubuntu-16-04)

solved problem, but after installing sql again and cp the backup file, the cp my.cnf said they are are the same file
so use mv but  seems still a link, now seems fine
back up the content incase use it later

<!-- #
# The MySQL database server configuration file.
#
# You can copy this to one of:
# - "/etc/mysql/my.cnf" to set global options,
# - "~/.my.cnf" to set user-specific options.
# 
# One can use all long options that the program supports.
# Run program with --help to get a list of available options and with
# --print-defaults to see which it would actually understand and use.
#
# For explanations see
# http://dev.mysql.com/doc/mysql/en/server-system-variables.html

#
# * IMPORTANT: Additional settings that can override those from this file!
#   The files must end with '.cnf', otherwise they'll be ignored.
#

!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mysql.conf.d/ -->

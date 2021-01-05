# Installing Python Git Repository Viewer on IBM i 

Klause is a Python based git repository viewer for viewing local file system repositories. 

For this use-case we will be viewing repositories stored in the IBM IFS file system.

Slogan from the Github site: 
**klaus: a simple, easy-to-set-up Git web viewer that Just Works**

Github site for Klause

https://github.com/jonashaag/klaus

# Security
There is no user security on the web server component by default. If you need some basic security you will possibly want to implement this with the Gunicorn web server and nginx. 

**TODO:** Gunicorn set up tutorial

# Prerequisites
Make sure all Python 3 yum packages installed on IBM i via IBM ACS.

Install the following Python modules
```
pip3 install klaus
```
**If you get any errors during install, please note them here.**

# Running Klaus git viewer server from qsh/pase/bash

This example runs the Klaus git server over repositories GITTEST123 and GITTEST124 on HTTP port 4646 and is listening on all IP addresses.

```
klaus --host 0.0.0.0 --port 4646 /gitrepostest/GITTEST123 /gitrepostest/GITTEST124
```

# Running Klaus git viewer server from SBMJOB/QSHEXEC

This example runs the Klaus git server over repositories GITTEST123 and GITTEST124 on HTTP port 4646 and is listening on all IP addresses.

The background job is submitted via SBMJOB and the QSHEXEC command. (http://www.github.com/qshoni)

```
SBMJOB CMD(QSHONI/QSHEXEC CMDLINE('klaus --host 0.0.0.0 --port 4646 /gitrepostest/GITTEST123') 
SETPKGPATH(*YES) PRTSPLF(GITVEWER)) JOB(GITVIEWER) JOBQ(QUSRNOMAX) JOBMSGQFL(*WRAP)                                         
```

# Links
See the Klause site for further documentation

https://github.com/jonashaag/klaus
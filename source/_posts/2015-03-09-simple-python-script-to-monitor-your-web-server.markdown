---
layout: post
title: "Simple Python Script To Monitor Your Web Server"
date: 2015-03-09 19:31
comments: true
categories: 
---

Too cheap to get a proper monitoring tool? Here's a simple Python script that I wrote that will send me an email if my webserver isn't returning HTTP 200.

1. `git clone https://github.com/pugnusferreus/py_monitoring.git`
2. Open monitoring.py with your favourite text editor.
3. Change the `EMAIL_LIST` variable, `SERVER` and `FROM` variable.
4. On line 36 and 37, change your webserver address and the email subject and message.
5. Copy monitoring.py to your webserver
6. Add the script to your crontab by typing sudo crontab -e
7. To run the script every 5 minutes, enter `*/5 * * * * /<your path>/monitor.py`

Note: I've only tested this script on Python 2.6 (since my server came with that version of Python). I'm not sure if it'll work on Python 3.
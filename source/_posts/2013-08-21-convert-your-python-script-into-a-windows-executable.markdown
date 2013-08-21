---
layout: post
title: "Convert your python script into a Windows executable"
date: 2013-08-21 14:02
comments: true
categories: 
---

During our migration to Windows Azure, we've found out that one of our script that does video rotation is a python script. 
Of course, when you're on a Windows platform, it'll be better off for you to run the script as a Windows executable file.

What you need:

  *  [py2exe](http://www.py2exe.org/)
  *  [python](http://www.python.org/download/)

&nbsp;

1 .  Install python and py2exe


2 .  Create a simple python script. Name it `hello.py`
```
print "This is a windows executable"
```

3 .  Create a `setup.py` file
```
from distutils.core import setup
import py2exe

setup(console=['hello.py'])
```

4 .  Open `cmd.exe` and go to your working directory.

5 .  We need to install the dependencies that are required by our python script. Run `python setup.py install`

6 .  Then, we convert the python script to an exe with `python setup.py py2exe`

7 .  Your `hello.exe` will be in the dist directory.
```
C:\temp>dist\hello.exe
This is a windows executable
```
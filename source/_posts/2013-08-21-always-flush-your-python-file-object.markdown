---
layout: post
title: "Always flush your Python file object"
date: 2013-08-21 15:19
comments: true
categories: 
---

If you're running Python on Windows and if you're dealing with read and writing files,
remember to do a `file.flush()` after a `file.write()`. 

On POSIX systems, it seems that the `file.read()` method will automatically commit the changes onto the file.
On Windows systems, it'll add a null character instead of the character that you're writing into the file.

So remember kids! Do a `.flush()` after a `.write()`!
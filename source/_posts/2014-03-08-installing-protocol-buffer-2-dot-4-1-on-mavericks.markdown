---
layout: post
title: "Installing Protocol Buffer 2.4.1 on Mavericks"
date: 2014-03-08 09:47
comments: true
categories: 
---

Sure, you can install the latest protocol buffer via [Brew](http://brew.sh/), 
but what happens when your entire organization is still stuck on protocol buffer 2.4.1?

Like me, if you tried to install protocol buffer 2.4.1 on OS X Mavericks, you'll get a compilation error.
This is how I fixed it.

1 .  Open terminal.app and run `brew update`

2 .  Get the hash for ProtoBuf 2.4.1 by running `brew versions protobuf`

3 .  Run cd &#96;brew --prefix&#96;

4 .  Get the 2.4.1 brew installation script by running `git checkout $hash_shown_in_step2 Library/Formula/protobuf.rb`

5 .  Attempt to install protobuf 2.4.1 by running `brew install protobuf` and you'll get the error like the following:
``` 
make[1]: *** [all-recursive] Error 1
make: *** [all] Error 2

READ THIS: https://github.com/Homebrew/homebrew/wiki/troubleshooting
```

6 .  Go to HomeBrew's source directory folder by running `cd /Library/Caches/Homebrew`

7 .  Unzip protobuf-2.4.1.tar.bz2

8 .  Open src/google/protobuf/message.h

9 .  Go to line 115 and change
```
#ifdef __DECCXX
// HP C++'s iosfwd doesn't work.
#include <iostream>
#else
#include <iosfwd>
#endif
```
To
```
#ifdef __DECCXX
// HP C++'s iosfwd doesn't work.
#include <iostream>
#else
#include <sstream>
#endif 
```

10 .  In the protobuf directory, run  `tar -cvjf protobuf-2.4.1.tar.bz2 .`

11 .  Obviously after modifying the code, the SHA sum will be different now. Get the new SHA sum by running `shasum protobuf-2.4.1.tar.bz2` abd then run `brew edit protobuf` and change the SHA1 with the new SHA sum

12 .  Finally run `brew install protobuf` again and enjoy your Protocol Buffer 2.4.1





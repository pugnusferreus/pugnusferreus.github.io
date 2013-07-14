---
layout: post
title: Mocking with Mockito
---

<h3>18 June 2011</h3>

At movideo, we're using <a href="http://mockito.org/">Mockito</a> as our mocking framework.
Mockito provides a clean and simple API to mock your Java objects.

Let's say Class1 has a couple of arguments for it's constructor and you do not want to provide each arguments,
you can simply do:

```
import static org.mockito.Mockito.mock;
```


then, you do

```
Class1 class1 = mock(Class1.class);
```

If you want to mock a certain method call in class1, do the following:

```
import static org.mockito.Mockito.when;
import static org.junit.Assert.assertEquals;
```

then, you do

```
when(class1.methodReturnsString()).thenReturn("foo");
assertEquals("foo", class2.callClass1Method());
```

Assuming that `class2.callClass1Method()` will call
`class1.methodReturnsString()`
the assertion will be successful.

To get a better picture of what Mockito can do for you, you can checkout my Mockito Test project
from my <a href="https://github.com/pugnusferreus/mockito_test">Github Sample Project</a>.

I'll assume that you have Git, Java 1.6 and Ant installed on your machine.

1. `git clone https://github.com/pugnusferreus/mockito_test`
2. `cd mockito_test`
3. `ant`
4. Open docs/unitTest/index.html in your browser

You can see that all the unit tests pass.

Thanks <a href="http://twitter.com/#!/cstrzadala">@cstrzadala</a> for introducing Mockito to all of us!

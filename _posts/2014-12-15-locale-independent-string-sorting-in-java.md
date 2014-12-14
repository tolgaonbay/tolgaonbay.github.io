---
layout: post
title: Locale-Independent String Sorting in Java
description: Locale-Independent String Sorting in Java
keywords: locale-independent string sorting in java
categories: [programming, internationalization]
tags: [java internationalization sorting]
---


In Java programming language, ```Arrays.sort``` or ```Collections.sort```
methods from the Class Library are used to sort a list of strings. These
methods use the ```compareTo``` method of the ```Comparable``` interface for
objects. The standard ```compareTo``` implementation of the String class uses
ASCII codes of the characters, and this works great in English.

When you need to sort strings in languages other than English, or more commonly
you need to write a software for global use, then you can use the
[Collator](https://docs.oracle.com/javase/7/docs/api/java/text/Collator.html)
class.

Below is the Turkish alphabet in order.

{% highlight java %}
abcçdefgğhıijklmnoöprsştuüvyz
{% endhighlight %}

Let's sort the characters of the alphabet with ```Arrays.sort``` method.

{% highlight java %}
String[] alphabet = "abcçdefgğhıijklmnoöprsştuüvyz".split("");

Arrays.sort(alphabet);
{% endhighlight %}

The result is not ordered in Turkish, as expected.

{% highlight java %}
abcdefghijklmnoprstuvyzçöüğış
{% endhighlight %}

Let's try the Collator class.

{% highlight java %}
Arrays.sort(alphabet, Collator.getInstance(Locale.forLanguageTag("tr")));
{% endhighlight %}

This works just in Turkish unsurprisingly. When you need to make your code work
in other languages too, you can use ```getDefault``` instead of
```forLanguageTag```.

{% highlight java %}
Arrays.sort(alphabet, Collator.getInstance(Locale.getDefault()));
{% endhighlight %}

I will write about internationalization in detail, but until then, have a look
at [What's wrong with
Turkey?](http://blog.codinghorror.com/whats-wrong-with-turkey/) by Jeff Atwood

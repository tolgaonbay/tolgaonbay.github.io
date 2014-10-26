---
layout: post
title: Null Object Pattern
description: Null Object Pattern is actually a special form of Special Case pattern. It gives a null meaning to your object and prevents getting null reference error
keywords: null object pattern
categories: [design, software]
tags: [design patterns]
---

A couple of months ago I needed to write a logging mechanism where logs weren't
always necessary to be persisted and log objects had to be transferred between
methods, so each method assigns some specific attributes of the log object
before being persisted. I know the latter seems like a terrible design, but not
everybody can work on a state-of-the-art system like some lucky guys do!

You can get a feeling of the log class below:

{% highlight java %}
public class AuditLog {
	private String id;
	...
	@Override
	public String getId() {
		return id;
	}
	@Override
	public void setId(String id) {
		this.id = id;
	}
	...
	@Override
	public void save() {
		//Persist to database
	}
}
{% endhighlight%}

Standard procedure is of course passing null reference to the methods when
there is no need to log and afterwards checking if the object is not null, so
you can invoke its methods without getting a null reference exception.

{% highlight java %}
public class TransactionHandler {
	public void handle(Transaction transaction, AuditLog log) {
		if (log != null)
			log.setId(id);
		...
	}
	...
	public void log(AuditLog log) {
		if (log != null)
			log.save();
	}
}
{% endhighlight%}

If you are an Objective-C programmer, then you are lucky, you don't need to
worry about checking if the object is null. But if you are using a mainstream
object oriented programming language like me, you need to keep in mind that the
objects can be null.

When you need to check null reference multiple times in more than a
few methods, then your code is going to start smelling. You should start
thinking about something else. Null Object Pattern can be your way out.

## Null Object Pattern

Null Object Pattern is actually a special form of [Special
Case](http://martinfowler.com/eaaCatalog/specialCase.html) pattern. It gives a
null meaning to your object and prevents getting null reference error and the
best part is: invoking its methods does nothing and there's no need to check if
it is null. It will cost you a method call instead of an if statement, but you
will get a cleaner code.

Let's get back to the design. We can transform the AuditLog class to use the
Null Object pattern like below.

![null object pattern]({{ site.url }}/assets/2014/04/nullobjectpattern.png)

The code will simply be changed to:

{% highlight java %}
public interface AuditLog {
	public String getId();
	public void setId(String id);
	...
	public void save();
}

public class AuditLogImpl implements AuditLog {
	private String id;
	...
	@Override
	public String getId() {
		return id;
	}
	@Override
	public void setId(String id) {
		this.id = id;
	}
	...
	@Override
	public void save() {
		//Persist to database
	}
}

public class NullAuditLog implements AuditLog {
	@Override
	public String getId() {
		return null;
	}
	@Override
	public void setId(String id) {
		//Do nothing
	}
	...
	@Override
	public void save() {
		//Do nothing
	}
}
{% endhighlight%}

Invoking the save method with a NullAuditLog instance will do nothing and you
don't need to add a null reference check anymore.

{% highlight java %}
public class TransactionHandler {
	public void handle(Transaction transaction, AuditLog log) {
		log.setId(id);
		...
	}
	...
	public void log(AuditLog log) {
		log.save();
	}
}
{% endhighlight%}

Actually using an interface is the optimal usage. But in my design, I simply
extended AuditLog class as NullAuditLog and made it a private static
class inside of the AuditLog class. With this way null instance may have been
retrieved from the NULL constant defined in AuditLog class. You can have a look
at it on
[github](https://github.com/tolgaonbay/examples/blob/master/src/com/thingstocode/examples/nullobject/AuditLog.java).

There are some downsides of this usage, like when you add new methods to the
class, you should remember to add them into your null class. With an interface
it is clearer to add method definitions into your interface and implement them
in the derived classes.

## Conclusion

Even if it came out because of a [billion dollar
mistake](http://www.infoq.com/presentations/Null-References-The-Billion-Dollar-Mistake-Tony-Hoare),
Null Object Pattern is very handy and makes your code clean. This doesn't mean
that you should apply Null Object Pattern to every single class in your design
- it can make things even more complicated and error-prone. It may be
used when:

*   It is possible to have a null reference and assigning null reference has a
    meaning in the design. For example we used it to not persist a log into the
    database
*   There are many null comparisons for the object across the system

Take a look at the Special Case pattern if you didn't before. I'm sure you will
find it very useful.

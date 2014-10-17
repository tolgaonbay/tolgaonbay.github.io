---
layout: post
title: The Good Enough Software Design
description: Software design is a challenge&#58; hard architectural decisions, change of requirements, lots of tools to use, lack of time. Is perfect design possible?
---
Designing software is a challenge, especially for a perfectionist programmer.
There are tons of decisions to make and lots of problems with many solutions.
It is very likely that some of them will be hard. You can find yourself
searching best practices online, and asking questions at
[stackoverflow.com](http://www.stackoverflow.com). Even if you find practices
and you get the answers you want, it is quite possible that you will end up
with a design that you are not satisfied with. You doubt whether it is a
perfect design or not. Guess what, there is no perfect design!

## Mount of Design

It is impossible to solve the design puzzle as a whole. Every requirement will
pop up in your brain and you will see the biggest challenges in the design like
the choices about the data or the presentation layer. Do I need to use MVC or
MVVM? Which ORM tool do I need to use? How am I supposed to handle multiple
database connections? Every question will make you feel more overwhelmed and
you will start to see the design as an ever growing mountain. Every step you
take will seem worthless to the giant mountain in front of you. Feeling
overwhelmed can make you want to escape from the problem and the
procrastination problem begins. But procrastination won't lead you to the
solution.

The simplest solution to this problem is to [Divide &amp;
Conquer](http://en.wikipedia.org/wiki/Divide_and_rule). You have to stop
thinking about the entire system in your head. You should divide the design
into smaller blocks and see what you can do to those simple blocks one by one.
If possible, choose an iterative development approach like
[XP](http://en.wikipedia.org/wiki/Extreme_programming). This way you can focus
design obstacles iteratively and then you will start to see multiple small
hills in your head.

Also don't spend too much time on choosing tools or APIs to use like a database
or a rule engine. These are just tools to make our lives easier. You should
spend more time on general design principles like [Separation of
Concerns](http://en.wikipedia.org/wiki/Separation_of_concerns). For example SoC
will allow you to change any layer or any tool in your software without
affecting the others. Apply
[TDD](http://en.wikipedia.org/wiki/Test-driven_development), it will pump up
your courage and let you make radical changes in your software.

Don't forget; the time spent on design is never enough. As Steve McConnell said
in his masterpiece, [Code
Complete](http://www.amazon.com/gp/product/0735619670/ref=as_li_ss_tl?ie=UTF8&amp;camp=1789&amp;creative=390957&amp;creativeASIN=0735619670&amp;linkCode=as2&amp;tag=thin0f5-20),

> When are you done [designing]? Since design is open-ended, the most common
> answer to that question is “When you're out of time."

## Requirements Change

Your client or your company has to adapt changes in the business to survive.
This means that requirements will change. You can't write a software to cover
all the possible requirements that could come up in the future. There will
always be some requirements that didn't even pop up in your brain. So don't try
to cover future requirements because [You Aren't Gonna Need
It](http://en.wikipedia.org/wiki/You_aren). It is like reserving and decorating
a room for a baby when you aren't even expecting one. Try to write a software
that covers the current requirements.

## Don't Overengineer

If you work on a specific feature for days that will reduce the work of your
client just 5 minutes in a year, then your work is actually useless. I know
sometimes we can't stop ourselves making that particular change, because it
might feel us like a better programmer or we might do it just for fun, but you
need to consider the cost/benefit ratio. Your time is precious, spend your time
on something better.

[![Overengineering problem](http://imgs.xkcd.com/comics/the_general_problem.png)](https://xkcd.com/974)

## Simplify

When you just need to store the state of an object into the file system, no
time-intensive job or anything special, it is pointless to write a custom
object serializer. I saw some designs that look like masterpieces from an
engineering point of view, but they made everything overcomplicated. It takes
weeks for newcomers to adapt to the system. You shouldn't make your design
overcomplicated. Sometimes the best solution is the simplest one. So keep in
mind the [KISS principle](http://en.wikipedia.org/wiki/KISS_principle).

## Courage

The design actually is the outcome of the programmer's experience. It is quite
likely that different programmers can come up with different design ideas. This
might result in you searching for the best possible way to design a feature
since there is no single solution to a design problem. Don't do that. It
doesn't mean you should stop learning, listening or reading other people's
ideas, of course you should. But design phase is not the time to learn all the
best practices in the world that could possibly be applied to your problem.
Have some courage, do your best design and start implementing your design
ideas.

In the design, you might give a class more responsibility than it should have,
or you might not see the inheritance relationship between two classes, or you
might miss a clearly visible pattern. When you start coding, you will see some
similar flaws in your design.
[Refactoring](http://en.wikipedia.org/wiki/Code_refactoring) is a really good
practice to make your design better. Don't try to make a perfect design, start
coding and refactor when your [code
smells](http://en.wikipedia.org/wiki/Code_smell). You will learn from your
mistakes and they will be helpful for your future designs.

## No Perfect Sofware

Whatever you do you will end up with a piece of software that won't satisfy
you. As Hunt and Thomas wrote in [The Pragmatic
Programmer](http://www.amazon.com/gp/product/020161622X/ref=as_li_ss_tl?ie=UTF8&amp;camp=1789&amp;creative=390957&amp;creativeASIN=020161622X&amp;linkCode=as2&amp;tag=thin0f5-20);

> ... perfect software doesn't exist. No one in the brief history of computing
> has ever written a piece of perfect software. It's unlikely that you'll be
> the first. And unless you accept this as a fact, you'll end up wasting time
> and energy chasing an impossible dream.

I'm sorry, but they are right. Instead of chasing an impossible dream, try to
make your design "good enough" and start coding!

---
title: Avoid using tail
layout: article
linters:
  - name: wartremover
    rules:
      - name: TraversableOps
        url:  http://www.wartremover.org/doc/warts.html#traversableops
---

> When retrieving everything but the first element of a sequence, do not use [`tail`]. [`drop(1)`] is often what you want to use.

# Reason

Some collections are empty, and [`tail`] deals with them by throwing an exception:

```scala mdoc:crash
Seq.empty[Int].tail
```

[`drop(1)`], on the other hand, will yield a reasonable value: the empty list.

```scala mdoc
Seq(1, 2, 3).drop(1)

Seq.empty[Int].drop(1)
```

# Exceptions to the rule

Note that this is not *always* what you want to do. There are scenarios in which you must deal with the empty case explicitly - as a stop condition in a recursive function, say.
It's just that, often, getting the empty list when you ask for everything but the first element of an empty list is perfectly reasonable.

[`tail`]:https://www.scala-lang.org/api/2.12.8/scala/collection/Seq.html#tail:A
[`drop(1)`]:https://www.scala-lang.org/api/2.12.8/scala/collection/Seq.html#drop(n:Int):Repr

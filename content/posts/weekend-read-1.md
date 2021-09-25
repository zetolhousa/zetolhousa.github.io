---
title: "Weekend Read 1"
date: 2021-09-25T01:48:04+05:30
---

### Articles
* [Thread pools in JVM](https://gist.github.com/djspiewak/46b543800958cf61af6efa8e072bfd5c)
    * CPU bound, Blocking and Non-blocking
    * **CPU bound** should have threads at max equal to no of CPU
        * **Blocking IO** operations should never be allowed on the CPU bound pool
            * They need to go to separate pool
    * **Async IO** polls (non blocking) should be handled by very small number of fixed, pre-allocated threads
        * These just sit idle asking kernel continually if any new async IO notification is available then forward to rest of application
        * Never do any work on this thread pool. NEVER!
* [Code convention: java comments](https://www.oracle.com/java/technologies/javase/codeconventions-comments.html)
    * Code block (note: this is not a javadoc comment) - snippet#1
    * Single line comments - snippet#2
    * Trailing comments - snippet#3
    * End of line comments - snippet#4
    * Java doc comments
        * After `/**` the next line follows a one space indent to align all subsequent `*`
        * These should **NOT** be placed inside contructors/methods
        * [Annotations supported in javadoc](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html)
* [Mockito verify cookbook](https://www.baeldung.com/mockito-verify)
    * `verify(x)`
    * `verify(x, y)`
    * `verifyZeroInteractions(x)`
    * `verifyNoMoreInteractions(x)`
    * `inOrder.verify(x)`
* [Git rebase explained visually](https://dev.to/joemsak/git-rebase-explained-and-eventually-illustrated-5hlb)
* [Deep stubs in mockito](https://www.javadoc.io/doc/org.mockito/mockito-core/2.2.9/org/mockito/Mockito.html#RETURNS_DEEP_STUBS)
    * `Mockito.RETURNS_DEFAULTS`
* [Reverse/foward proxies explained](https://www.haskellforall.com/2021/09/forward-and-reverse-proxies-explained.html)
* [10x engineer myth](https://www.swarmia.com/blog/busting-the-10x-software-engineer-myth)
    * tl;dr such engineers ultimately slow company down and drags scalability.

### Code snippets
Snippet#1
```java
/*
 * Here is a block comment.
 */
```

Snippet#2
```java
if (condition) {
    /* Handle the condition. */
    ...
}
```

Snippet#3
```java
if (a == 2) {
    return TRUE;            /* special case */
} else {
    return isPrime(a);      /* works only for odd a */
}
```

Snippet#4
```java
if (foo > 1) {

    // Do a double-flip.
    ...
}
else {
    return false;          // Explain why here.
}
```

Snippet#4
```java
/**
 * The Example class provides ...
 */
public class Example {
...
}
```

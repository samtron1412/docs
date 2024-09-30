# Overview

# Virtual Threads

- https://en.wikipedia.org/wiki/Green_thread
- https://medium.com/@genchilu/concurrency-paradigms-golang-v-s-java-1c71cbdb57de
- https://openjdk.org/jeps/444
- https://docs.oracle.com/en/java/javase/21/core/virtual-threads.html
- https://stackoverflow.com/questions/72116652/what-exactly-makes-java-virtual-threads-better
- https://news.ycombinator.com/item?id=29236375
    + Ron Pressler
        * https://www.youtube.com/watch?v=KmMU5Y_r0Uk
        * https://www.youtube.com/results?search_query=ron+pressler
        * https://inside.java/u/RonPressler/
- Continuation-passing style
    + https://en.wikipedia.org/wiki/Continuation-passing_style

```
There is a spectrum of solutions for dealing with slow I/O in
programming languages (well, all I/O is best assumed to be slow I/O). At
the two ends of the spectrum are:
- continuation-passing style (CPS), hand-coded or compiler
- preemptive threading / processes

In between lie various solutions, like async/await (closer to CPS), and
green threads (closer to preemptive threading).

The key difference between the two ends of this spectrum is memory
footprint. With CPS you manually compress state into tuned
structures. With threads you store state all over the stack in very
inefficient ways because all those stack frames take extra space.

Any solution towards the thread side of the spectrum will yield
significantly larger memory footprints than solutions towards the CPS
side of the spectrum.

On the other hand, solutions towards the CPS side of the spectrum can
require writing application-specific schedulers if fairness issues
arise.

On the whole, solutions on the CPS side of the spectrum are better, IMO.

Java is kinda stuck with threads, so green threads make some sense. Of
course, you can get pathological issues in M:N threading, so be careful
about that.
```

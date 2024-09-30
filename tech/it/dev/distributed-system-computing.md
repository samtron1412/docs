# Overview

## Books, Papers and Resources to read and learn

+ https://en.wikipedia.org/wiki/Distributed_computing
+ https://en.wikipedia.org/wiki/Leslie_Lamport
    * https://en.wikipedia.org/wiki/Leslie_Lamport#Distributed_systems
- https://github.com/systemdesignfightclub/sdfc
- Distributed computing courses
    + https://pdos.csail.mit.edu/6.824/schedule.html
    + https://people.eecs.berkeley.edu/~alig/cs294-91/
    + Parallel computing
        * https://gfxcourses.stanford.edu/cs149/fall21
        * http://15418.courses.cs.cmu.edu/spring2016/
- Books
    + Is Parallel Programming Hard, And, If So, What Can You Do About It?
        * https://mirrors.edge.kernel.org/pub/linux/kernel/people/paulmck/perfbook/perfbook.html
        * https://arxiv.org/abs/1701.00854
    + LMAX disruptor
        * https://lmax-exchange.github.io/disruptor/
    + Sophomoric Parallelism and Concurrency
        * https://homes.cs.washington.edu/~djg/teachingMaterials/spac/

# Concepts

- A program, algorithm, or problem can be decomposed into units of
  computation: tasks or components.
    + `Concurrent`: multiple tasks are executed at the same time by
      interleaving (T1, T2, T1, T2, ..., T2-end, T1-end).
        * `Sequential`: tasks are executed one at a time and no task
          begins until the prior task ends (without interleaving).
        * Single processor.
    + `Parallel`: multiple tasks are executed at the same time on multiple
      processors (each task is executed on a separate processor).
        * `Serial`: tasks are executed one at a time without interleaving.
        * Multiple processors: P1: T1; P2: T2
- Concurrency
    + https://www.youtube.com/watch?v=oV9rvDllKEg
    + A `composition / structure` of independently executing things /
      processes (not Linux processes, the most abstract meaning) /
      tasks.
        * The ability of different parts or units of a program,
          algorithm, or problem to be executed out-of-order or in
          partial order, without affecting the outcome.
        * In more technical terms, concurrency refers to the
          `decomposability` of a program, algorithm, or problem into
          order-independent or partially-ordered components or units of
          computation.
        * Paper to read: Tony Hoare - Communicating Sequential Processes
    + Note that in computer science, `parallelism` and `concurrency` are
      two different things:
        * a parallel program uses multiple CPU cores, each core
          performing a task independently.
        * On the other hand, concurrency enables a program to deal with
          multiple tasks even on a single CPU core; the core switches
          between tasks (i.e. threads) without necessarily completing
          each one.
    + A program can have `both`, `neither` of or a `combination` of
      parallelism and concurrency characteristics.
        * Concurrent and Parallel
        * Concurrent and Parallel
- Parallelism
    + The simultaneous `execution` of multiple things / processes /
      tasks.
- Concurrent computing
    + Java Concurrency in Practice (book)
- Concurrent computing vs. Parallel computing vs distributed computing
    + In parallel computing, all processors may have access to a shared
      memory to exchange information between processors.
    + In distributed computing, each processor has its own private
      memory (distributed memory). Information is exchanged by passing
      messages between the processors.
- Consistency models

# Correctness, Formal Languages, Model checking

- Writing correct software (correctness for software)
    + https://pron.github.io/page2/
    + Formal languages (for model checking):
        * Model checking
            - Conceptually checking all possible executions of the
              program on a very small model.
        * https://en.wikipedia.org/wiki/List_of_model_checking_tools
        * Temporal Logic of Actions - TLA+ (Leslie Lamport)
            - Leslie Lamport talks:
                + https://www.youtube.com/watch?v=-4Yp3j_jk8Q
                + Slide: https://www.microsoft.com/en-us/research/wp-content/uploads/2016/07/leslie_lamport.pdf
                + Conclusion:
                    * People tends to think that they are thinking about
                      problems and solutions.
                    * However, you are not truly thinking without
                      writing. Writing is to solidify your thinking.
                    * Writing specifications for programs are a way to
                      think about the problems and solutions before
                      coding.
                    * TLA+ / PlusCal and other tools help you with
                      writing specifications, and then you can use model
                      checkers to verify the correctness of the
                      systems.
            - https://en.wikipedia.org/wiki/TLA%2B
            - https://www.reddit.com/r/tlaplus/comments/ki4ufh/why_i_dont_use_tla_for_my_current_work/
        * Comunicating Sequential Processes - CSP (Tony Hoare)
            - https://en.wikipedia.org/wiki/Communicating_sequential_processes
            - Paper: https://www.cs.cmu.edu/~crary/819-f09/Hoare78.pdf
            - Book: http://www.usingcsp.com/cspbook.pdf
            - Examples:
                + Goroutines
                + JavaScript example
                    * https://github.com/dvlsg/async-csp
                    * https://www.quora.com/Is-async-await-in-Node-js-similar-to-Goroutines

# Concurrency

## Communicating Sequential Processes (CSP)

### Go language

I'm far from being an expert at Go, but I will try: goroutines are green threads (very light threads, if you prefer). The main difference between async calls and threads is that threads remove the distinction between synchronous and asynchronous code.
In C# or Python 3, each function is colored as either sync or async. You can quite easily call an async function from a sync context, but doing a blocking sync call from an async context is forbidden (although possible).

In Go there is no such distinction: you just write your functions in a straightforward fashion, as if everything was synchronous, and then wrap whatever you want to run in the background in a goroutine. If you don't need the return value from that function, it is has simple as issuing:

  go my_func(param_a, param_b, ...)
Note that goroutines are green threads, not OS threads, so you can easily spawn many tens of thousands of them without bringing your system to a halt.

---
layout: post
title:  "Java util.concurrent package"
date:   2022-12-03 22:00:00 +0700
categories: [java]
mermaid: true
---

# JAVA concurrent
java.util.concurrent is package that provides classes/interfaces that related to concurrent execution

## Important interfaces/classes
### Respresent the object that can execute the given task(either current therad or another thread)
- Executor : Object that can run a given task(Runnable).
- ExecutorService : More useful method than Executor. It provides methods to summit task, then give back Future.
- ScheduledExecutorService : Can execute task given delay in future or execute periodically.
- ForkJoinPool : An ExecutorService that implement work-stealing algorithms. Thread in the pool can steal work which in the pending queue of another thread.
- Executors : The class that contains factory methods use for create Thread pool.

### Wrapper of task execution result
- Future : The wrapper of execution result that may success or fail.
- CompletableFuture : Provide more extensive usecase than Future(for example Composition)
```java
// Create executorService with single thread using factory method from Executors
var executorService = Executors.newSingleThreadExecutor();

Callable<Integer> task = () -> {
    System.out.println("Perform something and return value");
    return 2;
};

// summit task to executorService
Future<Integer> future = executorService.submit(task);

try {
    // blocking the current thead until result is done
    var result = future.get();
    System.out.println("the result of computation is " + result);
} catch (InterruptedException | ExecutionException e) {
    System.out.println("Exception!!! " + e);
}
```

### Syscronizations
- CountDownLatch : Block with await method until count reach zero.
- Phaser : Extended functionality version of CountDownLatch. 
- CyclicBarrier : Extended functionality version of CountDownLatch.

### Memory Synchronization
- Lock : More extensive locking mechanism that synchronized keyword
- Semaphore : Respresent the resource counting that can be acquired and released. 

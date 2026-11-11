# Multithreading basics

<details><summary>

## [Easy] What is the need for Threads in Java?
</summary>

In Java, threads are used to achieve concurrent execution of tasks within a program. A thread is a lightweight unit of execution that can run concurrently with other threads, allowing multiple tasks to be performed simultaneously.

There are several reasons why threads are used in Java:

**1. Responsiveness:** Threads enable responsiveness in programs by allowing tasks to run concurrently. For example, if you have a graphical user interface (GUI) application, you can use threads to perform time-consuming operations in the background without freezing the user interface. This ensures that the application remains responsive to user interactions.

**2. Parallelism:** Threads can be used to achieve parallelism, where multiple tasks are executed simultaneously on different processor cores. This can lead to improved performance and efficiency in certain scenarios. For instance, in a multi-core system, you can divide a large computational task into smaller sub-tasks and execute them concurrently on different threads, effectively utilizing the available processing power.

**3. Asynchronous Operations:** Threads are useful for performing asynchronous operations. For example, if you need to fetch data from a remote server, you can create a thread to handle the network communication while the main thread continues to execute other tasks. This allows your program to continue functioning without waiting for the network operation to complete.

Here's a simple example to illustrate the use of threads in Java:

```java
    public class ThreadExample {
        public static void main(String[] args) {
            Thread thread1 = new Thread(new Task("Task 1"));
            Thread thread2 = new Thread(new Task("Task 2"));
            
            thread1.start(); // Start executing Task 1 in a separate thread
            thread2.start(); // Start executing Task 2 in a separate thread
            
            // Perform other tasks in the main thread
            System.out.println("Main thread is performing other tasks...");
        }
    }

    class Task implements Runnable {
        private String name;
        
        public Task(String name) {
            this.name = name;
        }
        
        public void run() {
            System.out.println("Executing " + name);
            
            // Simulate some work
            try {
                Thread.sleep(2000); // Sleep for 2 seconds
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            
            System.out.println(name + " completed");
        }
    }
```

In this example, two instances of the Task class are created, representing two different tasks. Each task is executed in a separate thread using the Thread class. The run() method of the Task class contains the code that will be executed in each thread. The Thread.sleep() method is used to simulate some work being done. While the tasks are being executed in separate threads, the main thread continues to perform other tasks concurrently.
</details>

<details><summary>

## [Easy] How do you create a thread?
</summary>

In Java, you can create a thread by following one of the two approaches: extending the Thread class or implementing the Runnable interface. Here's how you can create a thread using both approaches:

1. Extending the Thread class:

```java
    public class MyThread extends Thread {
        public void run() {
            // Code to be executed in the thread
        }
    }
```

To start the thread, you create an instance of your MyThread class and call the start() method:

```java
    MyThread thread = new MyThread();
    thread.start();
```

The run() method contains the code that will be executed in the thread. You can override this method to define the behavior of your thread.

2. Implementing the Runnable interface:

```java
    public class MyRunnable implements Runnable {
        public void run() {
            // Code to be executed in the thread
        }
    }
```

To start the thread, you create an instance of your MyRunnable class and pass it to the Thread constructor. Then, you call the start() method on the Thread object:

```java
    MyRunnable runnable = new MyRunnable();
    Thread thread = new Thread(runnable);
    thread.start();
```

The run() method in the Runnable implementation contains the code that will be executed in the thread.

Both approaches allow you to define the behavior of the thread in the run() method. When the start() method is called, a new thread is created, and the run() method is executed concurrently in that thread. It's important to note that you should not call the run() method directly; instead, use the start() method, which handles the thread creation and execution for you.

By creating threads, you can achieve concurrent execution of tasks, enabling responsiveness, parallelism, and asynchronous operations in your Java programs.
</details>

<details><summary>

## [Easy] What are the different states of a Thread?
</summary>

`Thread.getState()` returns one of **six** states defined in `Thread.State`:

| State | Meaning |
|---|---|
| `NEW` | Created, `start()` not called yet |
| `RUNNABLE` | Running **or** ready to run (waiting for CPU). Java has no separate "Running" state |
| `BLOCKED` | Waiting to acquire a monitor lock (entering a `synchronized` block/method) |
| `WAITING` | Waiting indefinitely for another thread: `wait()`, `join()`, `LockSupport.park()` |
| `TIMED_WAITING` | Waiting with a timeout: `sleep(ms)`, `wait(ms)`, `join(ms)`, `parkNanos` |
| `TERMINATED` | `run()` finished normally or with an uncaught exception |

Transitions: `NEW → RUNNABLE` (start), `RUNNABLE ↔ BLOCKED/WAITING/TIMED_WAITING`, `RUNNABLE → TERMINATED`. A terminated thread can't be restarted; calling `start()` twice throws `IllegalThreadStateException`.

Note: a thread blocked on I/O (e.g. a socket read) still shows `RUNNABLE`.

**Example:**

```java
Object lock = new Object();
Thread t = new Thread(() -> {
    synchronized (lock) {
        try { lock.wait(); } catch (InterruptedException ignored) {}
    }
});
System.out.println(t.getState());  // NEW
t.start();
Thread.sleep(100);
System.out.println(t.getState());  // WAITING (inside wait())
synchronized (lock) { lock.notify(); }
t.join();
System.out.println(t.getState());  // TERMINATED
// Other states: RUNNABLE, BLOCKED (waiting for a monitor lock), TIMED_WAITING (sleep/wait with timeout)
```

</details>

<details><summary>

## [Easy] What is priority of a thread? How do you change the priority of a thread?
</summary>

In Java, the priority of a thread is an integer value that determines the relative importance or scheduling preference of the thread. Thread priorities range from 1 (lowest) to 10 (highest), where the default priority is 5. The thread scheduler uses the thread's priority to decide which thread should be executed when multiple threads are in the "Runnable" state.

You can change the priority of a thread using the setPriority() method provided by the Thread class. Here's an example that demonstrates how to change the priority of a thread:

```java
      public class PriorityExample {
          public static void main(String[] args) {
              Thread thread1 = new Thread(new Task(), "Thread 1");
              Thread thread2 = new Thread(new Task(), "Thread 2");
              
              thread1.setPriority(Thread.MAX_PRIORITY); // Set Thread 1 priority to maximum
              thread2.setPriority(Thread.MIN_PRIORITY); // Set Thread 2 priority to minimum
              
              thread1.start();
              thread2.start();
          }
      }

      class Task implements Runnable {
          public void run() {
              System.out.println("Executing task in " + Thread.currentThread().getName());
          }
      }
```

In this example, two instances of the Task class are created, representing two different tasks to be executed in separate threads. The setPriority() method is used to set the priority of each thread.

The Thread.MAX_PRIORITY and Thread.MIN_PRIORITY constants represent the maximum and minimum thread priorities, respectively. You can also use values between 1 and 10 to set a specific priority.

When the threads are started using the start() method, the thread scheduler will take the thread priorities into account when deciding which thread to execute. However, it's important to note that thread priorities are platform-dependent and might not have a significant impact on thread scheduling on all systems.

It's generally recommended to use thread priorities judiciously and rely on other synchronization mechanisms, such as locks or semaphores, to ensure correct and reliable thread coordination. Thread priorities are typically used as hints to the scheduler, but the final decision is ultimately determined by the underlying platform and JVM implementation.
</details>

<details><summary>

## [Easy] What is ExecutorService?
</summary>

ExecutorService is an interface in Java that provides a way to manage and control the execution of tasks in a multithreaded environment. It is part of the Java Concurrency framework and is used to create and manage a pool of threads, allowing you to submit tasks for execution and retrieve the results when they are completed.

The ExecutorService interface extends the Executor interface and adds additional methods to manage the execution of tasks. It provides a high-level API for working with threads, abstracting away the complexities of thread creation, management, and synchronization.

Here's an example that demonstrates the usage of ExecutorService:

```java
        import java.util.concurrent.ExecutorService;
        import java.util.concurrent.Executors;

        public class ExecutorServiceExample {
            public static void main(String[] args) {
                // Create an ExecutorService with a fixed thread pool of size 5
                ExecutorService executorService = Executors.newFixedThreadPool(5);

                // Submit tasks for execution
                for (int i = 0; i < 10; i++) {
                    int taskId = i;
                    executorService.submit(() -> {
                        System.out.println("Task " + taskId + " is being executed by thread: " + Thread.currentThread().getName());
                    });
                }

                // Shutdown the ExecutorService to reject any new tasks and wait for the previously submitted tasks to complete
                executorService.shutdown();
            }
        }
```

In this example, we create an ExecutorService using the Executors.newFixedThreadPool() method, which creates a thread pool with a fixed number of threads (in this case, 5). We then submit 10 tasks for execution using the submit() method of the ExecutorService. Each task is a lambda expression that prints a message indicating the task ID and the name of the thread executing it.

Finally, we call the shutdown() method on the ExecutorService to initiate a graceful shutdown. This will cause the ExecutorService to reject any new tasks and wait for the previously submitted tasks to complete before terminating the threads in the pool.

By using ExecutorService, you can efficiently manage the execution of tasks in a concurrent environment, allowing for better utilization of system resources and improved performance.
</details>

<details><summary>

## [Easy] What is Callable? How do you execute a Callable from ExecutionService?
</summary>

Callable is a functional interface in Java that represents a task that can be executed by a thread and returns a result. It is similar to the Runnable interface, but Callable tasks can return a result and throw checked exceptions.

The Callable interface has a single method call() that you need to implement. This method contains the task's logic and returns a result of a specified type.

To execute a Callable from an ExecutorService, you can use the submit() method, which accepts a Callable instance and returns a Future object representing the task's execution.

Here's an example that demonstrates how to create a Callable and execute it using an ExecutorService:

```java
        import java.util.concurrent.Callable;
        import java.util.concurrent.ExecutorService;
        import java.util.concurrent.Executors;
        import java.util.concurrent.Future;

        public class CallableExample {
            public static void main(String[] args) {
                ExecutorService executorService = Executors.newFixedThreadPool(5);

                // Create a Callable task
                Callable<Integer> task = () -> {
                    // Simulating some computation
                    Thread.sleep(2000);
                    return 42;
                };

                // Submit the task for execution
                Future<Integer> future = executorService.submit(task);

                // Do other tasks or operations while the Callable is executing

                try {
                    // Retrieve the result of the Callable task
                    Integer result = future.get();
                    System.out.println("Task result: " + result);
                } catch (Exception e) {
                    System.err.println("An error occurred while retrieving the task result: " + e.getMessage());
                }

                // Shutdown the ExecutorService
                executorService.shutdown();
            }
        }
```

In this example, we create a Callable task using a lambda expression. The Callable returns an Integer result after a simulated computation. We then submit the Callable task to the ExecutorService using the submit() method, which returns a Future object.

While the Callable task is executing, you can perform other tasks or operations. Later, when you need the result of the Callable task, you can call the get() method on the Future object. The get() method blocks until the task completes and returns the result. If an exception occurred during the task execution, it will be thrown when calling get(), so it's important to handle potential exceptions.

By using Callable and Future together with an ExecutorService, you can execute tasks that return results and retrieve those results at a later point in time, providing more flexibility and control over concurrent operations.
</details>

<details><summary>

## [Easy] What is Synchronization of threads ?
</summary>

Synchronization of threads refers to the coordination and control of multiple threads to ensure that they access shared resources in a mutually exclusive manner. It is used to prevent race conditions and maintain data consistency when multiple threads are concurrently accessing and modifying shared data.

In Java, synchronization can be achieved using the synchronized keyword and intrinsic locks. When a block of code or a method is marked as synchronized, only one thread can execute that block or method at a time, while other threads must wait until the lock is released.

Here's a simple example that demonstrates synchronization:

```java
        public class Counter {
            private int count;

            public synchronized void increment() {
                count++;
            }

            public synchronized int getCount() {
                return count;
            }
        }
```

In this example, the Counter class has two methods: increment() and getCount(). Both methods are marked as synchronized, which means only one thread can execute these methods at a time.

Suppose multiple threads are concurrently calling the increment() method to increment the count variable. With synchronization, each thread will acquire the intrinsic lock associated with the Counter object before executing the increment() method. This ensures that only one thread can modify the count variable at any given time, preventing data corruption or inconsistencies.

Similarly, if a thread calls the getCount() method, it will also acquire the intrinsic lock before retrieving the value of count. This guarantees that the thread will see the most up-to-date value of count and avoids reading stale or inconsistent data.

By synchronizing critical sections of code or methods, you can enforce mutual exclusion and ensure thread-safe access to shared resources, maintaining data integrity and preventing race conditions in multi-threaded environments.
</details>

<details><summary>

## [Easy] Can you give an example of a Synchronization block ?
</summary>

```java
        public class Counter {
            private int count;
            private Object lock = new Object();

            public void increment() {
                synchronized (lock) {
                    count++;
                }
            }

            public int getCount() {
                synchronized (lock) {
                    return count;
                }
            }
        }
```

In this example, the Counter class has two methods: increment() and getCount(). Instead of marking the entire methods as synchronized, we use synchronization blocks to achieve thread-safety.

A synchronization block is denoted by the synchronized keyword followed by an object that serves as the lock. In this case, we create an instance variable lock of type Object to use as the lock.

Within the increment() method, the critical section of code that modifies the count variable is enclosed within a synchronization block using the lock object. This ensures that only one thread can enter the block and execute the code at a time.

Similarly, within the getCount() method, the critical section that retrieves the value of count is synchronized using the same lock object. This guarantees that only one thread can access the count variable and retrieve its value at any given time.

By using synchronization blocks, you can achieve fine-grained control over synchronization and ensure that only the necessary sections of code are synchronized, rather than the entire methods. This can improve performance by allowing concurrent access to non-shared parts of the code while still ensuring thread-safety for shared resources.
</details>

<details><summary>

## [Easy] What is the use of join methods in threads ?
</summary>

The join() method in Java is used to pause the execution of a thread until the thread it is called on completes its execution. It allows one thread to wait for the completion of another thread before proceeding further.

Here's a simple example that demonstrates the use of the join() method:

```java
        public class JoinExample {
            public static void main(String[] args) throws InterruptedException {
                Thread thread1 = new Thread(() -> {
                    System.out.println("Thread 1 started");
                    try {
                        Thread.sleep(2000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println("Thread 1 completed");
                });

                Thread thread2 = new Thread(() -> {
                    System.out.println("Thread 2 started");
                    try {
                        Thread.sleep(3000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println("Thread 2 completed");
                });

                thread1.start();
                thread2.start();

                // Wait for thread1 to complete before proceeding
                thread1.join();

                // Wait for thread2 to complete before proceeding
                thread2.join();

                System.out.println("All threads completed");
            }
        }
```

In this example, we have two threads: thread1 and thread2. Each thread performs some tasks and then completes after a certain delay using Thread.sleep().

After starting both threads, we call the join() method on thread1, which causes the main thread to wait until thread1 completes its execution. Similarly, we call join() on thread2 to wait for it to complete as well.

By using join(), we ensure that the main thread waits for the completion of both thread1 and thread2 before continuing further. This allows for synchronization and coordination among threads, ensuring that certain tasks are completed before proceeding with subsequent operations.
</details>

<details><summary>

## [Easy] What is the use of yield method?
</summary>

The yield() method in Java is used to voluntarily give up the current thread's turn of execution to allow other threads of the same priority to run. It is a hint to the scheduler that the current thread is willing to yield its use of the CPU.

When a thread calls yield(), it may be moved to the runnable state, allowing other threads to be scheduled for execution. However, there is no guarantee that the yield request will be honored by the scheduler.

The main use of the yield() method is to improve the fairness and responsiveness of thread scheduling in situations where multiple threads with the same priority are contending for CPU resources.

Here's a simple example that demonstrates the use of the yield() method:

```java
        public class YieldExample {
            public static void main(String[] args) {
                Thread thread1 = new Thread(() -> {
                    for (int i = 1; i <= 5; i++) {
                        System.out.println("Thread 1 - " + i);
                        Thread.yield(); // Yield the execution to other threads
                    }
                });

                Thread thread2 = new Thread(() -> {
                    for (int i = 1; i <= 5; i++) {
                        System.out.println("Thread 2 - " + i);
                        Thread.yield(); // Yield the execution to other threads
                    }
                });

                thread1.start();
                thread2.start();
            }
        }
```

In this example, we have two threads: thread1 and thread2. Each thread prints a message with a sequence number and then calls yield() to give other threads a chance to run.

When you run this example, you will notice that both threads take turns executing, but the exact interleaving of their output may vary between different runs. The yield() method allows the scheduler to switch between threads more frequently, enhancing the fairness of execution.
</details>

<details><summary>

## [Easy] What is Deadlock ?
</summary>

Deadlock is a situation in concurrent programming where two or more threads are blocked indefinitely, waiting for each other to release resources that they hold. In other words, it's a state in which the execution of threads becomes permanently halted because each thread is waiting for a resource that can only be released by another thread, resulting in a deadlock.

A deadlock occurs when the following four conditions are met:

- **Mutual Exclusion:** At least one resource must be held in a non-sharable mode, meaning only one thread can access the resource at a time.
- **Hold and Wait:** A thread must be holding at least one resource and waiting to acquire additional resources that are currently held by other threads.
- **No Preemption:** Resources cannot be forcibly taken away from a thread; they can only be released voluntarily by the thread holding them.
- **Circular Wait:** There must be a circular chain of two or more threads, where each thread is waiting for a resource held by another thread in the chain.
When a deadlock occurs, the threads involved are unable to make progress, leading to a system freeze or unresponsiveness.

Here's a simplified example that illustrates a deadlock scenario:

```java
        public class DeadlockExample {
            private static final Object resource1 = new Object();
            private static final Object resource2 = new Object();

            public static void main(String[] args) {
                Thread thread1 = new Thread(() -> {
                    synchronized (resource1) {
                        System.out.println("Thread 1 acquired resource 1");
                        try {
                            Thread.sleep(1000);
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }

                        synchronized (resource2) {
                            System.out.println("Thread 1 acquired resource 2");
                            // Perform operations using both resources
                        }
                    }
                });

                Thread thread2 = new Thread(() -> {
                    synchronized (resource2) {
                        System.out.println("Thread 2 acquired resource 2");
                        try {
                            Thread.sleep(1000);
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }

                        synchronized (resource1) {
                            System.out.println("Thread 2 acquired resource 1");
                            // Perform operations using both resources
                        }
                    }
                });

                thread1.start();
                thread2.start();
            }
        }
```

In this example, two threads, thread1 and thread2, attempt to acquire two resources, resource1 and resource2. However, they acquire the resources in different orders, leading to a potential deadlock situation.

If thread1 acquires resource1 and thread2 acquires resource2 simultaneously, both threads will be blocked indefinitely waiting for the other resource to be released. This forms a circular wait condition, resulting in a deadlock.

Preventing deadlocks involves careful design and the use of strategies like resource ordering, avoiding circular wait, and implementing timeouts or deadlock detection mechanisms.

Handling deadlocks requires identifying and resolving the circular wait condition by breaking the circular chain, forcibly releasing resources, or using techniques like resource allocation graphs or deadlock detection algorithms to detect and recover from deadlocks.
</details>

<details><summary>

## [Medium] Explain different ways of creating Executor Services?
</summary>

Factory methods in `Executors`:

| Factory | What you get | Watch out |
|---|---|---|
| `newFixedThreadPool(n)` | n threads, **unbounded** queue | Queue can grow until OOM under overload |
| `newCachedThreadPool()` | Creates threads on demand, reuses idle ones (60 s keep-alive) | **Unbounded thread count** under load |
| `newSingleThreadExecutor()` | One thread, tasks run sequentially in order | Unbounded queue |
| `newScheduledThreadPool(n)` | Returns a **`ScheduledExecutorService`** for delayed/periodic tasks | |
| `newWorkStealingPool()` | `ForkJoinPool` sized to CPU cores | For CPU-bound, splittable work |
| `newVirtualThreadPerTaskExecutor()` (Java 21) | A new virtual thread per task | For blocking IO; don't pool virtual threads |

```java
ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(2);
scheduler.scheduleAtFixedRate(() -> System.out.println("heartbeat"), 0, 10, TimeUnit.SECONDS);
```

For production services, create a **`ThreadPoolExecutor` directly** so you control the queue size and what happens when it's full:

```java
ExecutorService pool = new ThreadPoolExecutor(
	4, 8,                                      // core and max threads
	60, TimeUnit.SECONDS,                      // keep-alive for extra threads
	new ArrayBlockingQueue<>(100),             // bounded queue
	new ThreadPoolExecutor.CallerRunsPolicy()  // back-pressure when full
);
```

Always `shutdown()` executors you create (or use try-with-resources on Java 19+, since `ExecutorService` is `AutoCloseable`).

</details>

<details><summary>

## [Medium] How do you check whether an ExecutionService task executed successfully?
</summary>

`submit()` returns a `Future`. Call `get()` (ideally with a timeout): it returns the result if the task succeeded, or throws:
- `ExecutionException` – the task threw; the real cause is `e.getCause()`
- `TimeoutException` – not finished within the timeout
- `CancellationException` – the task was cancelled
- `InterruptedException` – the waiting thread was interrupted

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
Future<String> future = executor.submit(() -> {
	Thread.sleep(2000);
	return "Task completed successfully";
});

try {
	String result = future.get(5, TimeUnit.SECONDS);   // waits up to 5 seconds
	System.out.println(result);
} catch (ExecutionException e) {
	System.err.println("Task failed: " + e.getCause());
} catch (TimeoutException e) {
	future.cancel(true);                               // interrupt it
	System.err.println("Task timed out");
} catch (InterruptedException e) {
	Thread.currentThread().interrupt();
} finally {
	executor.shutdown();
}
```

`isDone()` only tells you the task finished (successfully, with an error, or cancelled); checking it right after `submit()` will almost always be `false`. Java 19 added `future.state()` (`SUCCESS`, `FAILED`, `CANCELLED`, `RUNNING`) plus `resultNow()` and `exceptionNow()`. For non-blocking callbacks, use `CompletableFuture`.

</details>

<details><summary>

## [Medium] Can a static method be synchronized ?
</summary>

Yes. A `static synchronized` method locks on the **`Class` object** (`Counter.class`), not on an instance. So:
- Only one thread at a time can run *any* static synchronized method of that class.
- It does **not** block threads calling *instance* `synchronized` methods, because those lock on `this`, a different monitor.

```java
public class Counter {
	private static int count;

	public static synchronized void increment() {   // same as synchronized (Counter.class) { ... }
		count++;
	}

	public static synchronized int getCount() {
		return count;
	}
}
```

Use it to protect **static shared state**. If static and instance methods touch the same data, they must use the same lock, otherwise you still have a race.

</details>
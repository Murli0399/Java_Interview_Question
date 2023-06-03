<details><summary>

## What is the need for Threads in Java?
</summary>
In Java, threads are used to achieve concurrent execution of tasks within a program. A thread is a lightweight unit of execution that can run concurrently with other threads, allowing multiple tasks to be performed simultaneously.

There are several reasons why threads are used in Java:

**1. Responsiveness:** Threads enable responsiveness in programs by allowing tasks to run concurrently. For example, if you have a graphical user interface (GUI) application, you can use threads to perform time-consuming operations in the background without freezing the user interface. This ensures that the application remains responsive to user interactions.

**2. Parallelism:** Threads can be used to achieve parallelism, where multiple tasks are executed simultaneously on different processor cores. This can lead to improved performance and efficiency in certain scenarios. For instance, in a multi-core system, you can divide a large computational task into smaller sub-tasks and execute them concurrently on different threads, effectively utilizing the available processing power.

**3. Asynchronous Operations:** Threads are useful for performing asynchronous operations. For example, if you need to fetch data from a remote server, you can create a thread to handle the network communication while the main thread continues to execute other tasks. This allows your program to continue functioning without waiting for the network operation to complete.

Here's a simple example to illustrate the use of threads in Java:

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

In this example, two instances of the Task class are created, representing two different tasks. Each task is executed in a separate thread using the Thread class. The run() method of the Task class contains the code that will be executed in each thread. The Thread.sleep() method is used to simulate some work being done. While the tasks are being executed in separate threads, the main thread continues to perform other tasks concurrently.

</details>
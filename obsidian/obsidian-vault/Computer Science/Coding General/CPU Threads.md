
Threads are the **virtual components or codes**, which **divides** the physical core of a [[Central Processing Unity (CPU)]] into **virtual multiple cores**. A single CPU core can have **up-to 2 threads per core**. For example, if a CPU is dual core (i.e., 2 cores) it will have 4 threads. And if a CPU is Octal core (i.e., 8 core) it will have 16 threads and vice-versa.

- **Threads** are virtual sequences of instructions given to a CPU. 
- **Multithreading** allows for better utilization of available system resources by dividing tasks into separate threads and running them in parallel.
- **Hyperthreading** further increases performance by allowing processors to execute two threads concurrently.

A thread is *a sequence of instructions* given to the CPU by a program or application. The more threads a CPU can execute at once, the more tasks it can complete.

Threading in a CPU is a technique that can increase the *speed and efficiency* of multitasking. It enables *multiple threads of execution to run simultaneously* on one or more cores in a single processor, allowing for quicker response times and more efficient use of resources.

*When multiple threads are running simultaneously, it’s called multithreading.*

Multithreading also *helps reduce latency* by allowing different processes to run in parallel rather than one at a time. It can also be used to help increase the number of tasks that can be executed in any given period of time.

The main difference between CPU cores and threads is that a core is an individual physical processing unit, while threads are virtual sequences of instructions.

*The performance of a computer depends on the number of cores **AND** the threading technique.*

A hyperthreading technique can further increase the number of threads that can be active by splitting a single core into two virtual cores, allowing them to run multiple threads.

**The trade-off to such strength is that it often comes with a cost, consumes more power, and may only sometimes result in an overall improvement in performance.**

**The thread is created by a process.**

Every time you open an application, it itself creates a thread which will handle all the tasks of that specific application. Like-wise the more application you open more threads will be created.

They are always created by the operating system for performing a task of a specific application.

There is single thread (code of that core which performs the computations also known as primary thread) on the core which when gets the information from the user, creates another thread and allocates the task to it. Similarly, if it gets another instruction it forms second thread and allocates the task to it. Making a total of two threads.

*The only fact that will limit the creation of the threads will be the number of the threads provided by the physical CPU, and it varies from CPU to CPU.*

#### Use Cases for Multi-Threading:

- Web Browsing: Modern web browsers with multiple open tabs and extensions benefit from multi-threaded CPUs, as each tab or process can be handled by a separate thread.
- Software Development: Compilers, integrated development environments (IDEs), and other development tools often use multiple threads to compile code, perform tests, and manage resources simultaneously.
- Virtualization: Running multiple virtual machines on a single physical server is made more efficient with multi-threading, as each VM can be allocated its own set of threads.

#### Manufacturers and Their Technologies:

- **Intel**: Known for its `Hyper-Threading technology`, which allows each core to process two threads simultaneously. Intel’s CPUs, such as the `Core i7` and `Core i9`, are designed for high-performance computing with multiple cores and threads.
- **AMD**: Famous for its `Ryzen` and `EPYC` processors, AMD uses `Simultaneous Multi-Threading (SMT) `technology, which also enables two threads per core. AMD’s processors are highly regarded in both consumer and enterprise markets for their excellent multi-threading capabilities.

---

## Unreal Engine Render Threads

In Unreal Engine, the entire renderer operates in its own thread that is a frame or two behind the game thread.

Multithreading is a powerful technique in game development that allows *multiple tasks* to run *concurrently*, leveraging the full potential of modern multi-core processors. In a game, numerous processes such as rendering, physics calculations, AI, and input handling need to be executed simultaneously. Properly implemented multithreading can significantly improve the performance and responsiveness of your game by ensuring these processes run smoothly without blocking each other.

The engine uses *several threading models* and provides various tools and classes to manage threads and tasks efficiently. Here’s an overview of Unreal Engine’s multithreading capabilities:

- **Game Thread**: The main thread where *most gameplay logic runs*. It processes input, updates game objects, and handles most of the game’s logic.
- **Render Thread**: A separate thread responsible for *rendering graphics*. It works in *tandem with the game thread* to ensure smooth and efficient rendering.
- **Task Graph System**: A powerful system for managing asynchronous tasks and parallel execution. It helps in efficiently scheduling and running tasks across multiple threads.

The combination of these threads and systems allows Unreal Engine to handle complex and demanding games with high performance and scalability.

#### Why Use Multithreading in Unreal Engine?

1. **Improved Performance**: By distributing tasks across multiple threads, you can take full advantage of multi-core processors, resulting in faster and more efficient execution of tasks.
2. **Smooth Gameplay**: Multithreading helps maintain a smooth gameplay experience by ensuring that resource-intensive tasks like rendering and physics calculations do not block the game thread.
3. **Scalability**: Properly implemented multithreading allows your game to scale efficiently with hardware advancements, ensuring better performance on modern systems.

#### Game Thread

The **Game Thread** is the primary thread in Unreal Engine where most of the gameplay logic runs. It handles:

- Input processing
- Actor updates
- Game state management
- Logic execution

The Game Thread operates on a variable time step, meaning the time elapsed between frames (`DeltaTime`) can vary. This ensures consistent gameplay updates by adjusting calculations based on the actual time elapsed. While it is responsible for most of the core game logic, offloading certain tasks to other threads can improve performance and responsiveness.  
  
Certain subsystems, such as `physics simulations`, often operate on a `fixed time step`. This approach ensures `stable and deterministic physics` behavior by updating at consistent intervals, independent of the variable frame times of the Game Thread.

#### Render Thread

The **Render Thread** is dedicated to rendering graphics. It works closely with the Game Thread to process rendering commands and *draw the game world*. Key responsibilities include:

- Preparing rendering data
- Communicating with the [[Graphics Processing Unity (GPU)]]
- Executing draw calls

By separating rendering from the game logic, Unreal Engine can achieve smoother frame rates and better performance.

#### Task Graph System

The **Task Graph System** is a powerful system for managing asynchronous tasks and parallel execution in Unreal Engine. It allows developers to schedule and execute tasks concurrently, making full use of multi-core processors.

- **FGraphEventRef**: Represents a reference to a graph event, used to track the completion of tasks.
- **FFunctionGraphTask**: Allows you to define and schedule tasks.

#### Worker Threads

Unreal Engine utilizes **Worker Threads** to perform background tasks that do not require immediate attention. These threads handle tasks such as:

- Asset loading
- Physics calculations
- AI processing

Worker threads help offload work from the Game Thread and Render Thread, ensuring smoother gameplay and responsiveness.



## **Further Reading** 
* [**Thread in Operating System](https://www.geeksforgeeks.org/thread-in-operating-system/)
* [Thread (Wiki)](https://en.wikipedia.org/wiki/Thread_(computing))
* [How to improve game thread CPU performance in Unreal Engine](https://www.unrealengine.com/es-ES/blog/how-to-improve-game-thread-cpu-performance)
* [Multithreading in Unreal Engine 5](https://inoland.net/unreal-engine-5-multithreading/)
* [Threaded Rendering](https://dev.epicgames.com/documentation/en-us/unreal-engine/threaded-rendering-in-unreal-engine)
  
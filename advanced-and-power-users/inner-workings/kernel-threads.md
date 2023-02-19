---
description: Threading at its best!
---

# 📞 Kernel Threads

Threads are a great way to asynchronously do things in your mod! They play a huge role on preventing the block from happening on the main thread. Single-threaded aplications usually get blocked by long operations, but threads solve this problem.

Nitrocid KS manages the threads that are created by the `KernelThread` instances. It allows the kernel to manipulate with these threads more efficiently, and they stop each time the kernel is requested to shut down or restart by any power management functions, either locally or br remotely by RPC.

`ThreadManager` provides you a whole set of functions and properties to efficiently manage your threads from listing all active threads to sleeping to benchmarking the sleep function.

## How to make your thread

To make your `KernelThread`, just call its constructor with the following parameters:

* `ThreadName`
  * Thread name
* `Background`
  * Whether the thread is a background thread
* `Executor`
  * A function to execute in the thread
  * It can be either of the type `ThreadStart` or of the type `ParameterizedThreadStart`

You can then start the thread using the `Start()` function for normal threads or the `Start(object)` function for parameterized threads.

{% hint style="warning" %}
You can't start the kernel thread once it's stopped by `Stop(false)` until it's regenerated either automatically by `Stop()` or manually by `Regen()`, and you can't call `Regen()` before calling the `Stop(false)` function.
{% endhint %}

## Task manager

The task manager can be called by `taskman` in the normal shell. It allows you to list both the Nitrocid KS threads and the unmanaged operating system threads, and it provides you with their information.

The left pane of the task manager shows you a list of threads, and the right pane shows you the selected thread info.

### Controls

* `F1`
  * Kills a Nitrocid KS thread and regenerates it
  * This can't be used on unmanaged OS threads
* `Tab`
  * Switches between the Nitrocid KS thread listing and the unmanaged OS thread listing
* `ESC`
  * Exits the program

### Thread information

The selected thread information can be found on the right pane of your task manager. However, depending on the type of the thread you're currently at, it might show different information.

#### Nitrocid KS threads

The below information are shown:

* `Task name`
  * The kernel thread name
* `Alive`
  * Whether the kernel thread is running or not
* `Background`
  * Whether the kernel thread is running in the background or not
* `Critical`
  * Threads that are crucial to the kernel is usually set to `True` and thus can't be killed
* `Ready`
  * Whether the thread is ready to be started or not

#### Unmanaged OS threads

The below information are shown:

* `Task ID`
  * Unmanaged OS thread number assigned by the operating system
* `Privileged processor time`
  * Amount of work a processor is completing while executing in privileged mode
* `User processor time`
  * Amount of work a processor is completing while executing in user space
* `Total processor time`
  * Total amount of work a processor is completing
* `Task state`
  * The thread state holding one of the [ThreadState](https://learn.microsoft.com/en-us/dotnet/api/system.diagnostics.threadstate) values
* `Priority level`
  * The unmanaged thread priority level
* `Task memory address`
  * A hexadecimal representation of the memory address for an unmanaged thread assigned by the operating system that points to the thread entry point (start) in this format: `0x00000000`

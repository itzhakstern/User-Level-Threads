The project provides functions for the user to manage thrades as well as Mutex.
the files Threads.h and Threads.cpp are the file of the class threads.
the file uthread.cpp responsible for management and scheduling the threads.

In thus project I used in the Round-Robin scheduling policy should work as follows:
  • Every time a thread is moved to RUNNING state, it is allocated a predefined number of microseconds to run. This time interval is called a quantum.
  • A thread is preempted if any of the following occurs:
      a) Its quantum expires.
      b) It changed its state to BLOCKED and is consequently waiting for an event (i.e. some other
         thread that will resume it – more details below).
      c) It is terminated.
      
  • Every time a thread moves to the READY state from any other state, it is placed at the end of the
    list of READY threads.
    
  • If the RUNNING thread is preempted, do the following:
      1. If the RUNNING thread is preempted because its quantum is expired, move the preempted
         thread to the end of the READY threads list.
      2. Move the next thread in the list of READY threads to RUNNING state.
      
  • When a thread doesn't finish its quantum (as in the case of a thread that blocks itself), the next
    thread should start executing immediately as if the previous thread finished its quota.
    In the following illustration the quantum was set for 2 seconds, Thread 1 blocks itself after running
    only for 1 second and Thread 2 immediately starts its next quantum.
    
  • You are required to manage a READY threads list. You can use more lists for other purposes.
  
  • On each quantum the READY top-of-list thread is moved to RUNNING.
  
  • There is one mutex in this library. Mutex is simply a lock. The lock can be acquired by only one
    thread at a time. If the lock is already locked by one thread, while another thread tries to lock it, it
    changes its state to BLOCK and wait for the mutex to be released. Only the thread which locked
    the mutex can release it. After the mutex is released, one of the waiting threads will change its
    state from BLOCK to READY and will try to acquire the mutex again next time it will be RUNNING.
    
    <img width="766" alt="צילום מסך 2021-11-09 ב-13 44 29" src="https://user-images.githubusercontent.com/83215154/140918318-d3b1127c-86a9-49dd-a186-fe8bf59afec9.png">
    
    

The project provides functions for the user to manage thrades as well as Mutex.
the files Threads.h and Threads.cpp are the file of the class threads.
the file uthread.cpp responsible for management and scheduling the threads.

# Algorithm

In thus project I used in the Round-Robin scheduling policy should work as follows:

- Every time a thread is moved to RUNNING state, it is allocated a predefined number of microseconds to run. This time interval is called a quantum.
- A thread is preempted if any of the following occurs:
  1. Its quantum expires.
  2. It changed its state to BLOCKED and is consequently waiting for an event (i.e. some other thread that will resume it – more details below).
  3. It is terminated.
      
- Every time a thread moves to the READY state from any other state, it is placed at the end of the
    list of READY threads.
    
- If the RUNNING thread is preempted, do the following:

  1. If the RUNNING thread is preempted because its quantum is expired, move the preempted thread to the end of the READY threads list.
  2. Move the next thread in the list of READY threads to RUNNING state.
      
- When a thread doesn't finish its quantum (as in the case of a thread that blocks itself), the next
    thread should start executing immediately as if the previous thread finished its quota.
    In the following illustration the quantum was set for 2 seconds, Thread 1 blocks itself after running
    only for 1 second and Thread 2 immediately starts its next quantum.
    
- On each quantum the READY top-of-list thread is moved to RUNNING.
  
- There is one mutex in this library. Mutex is simply a lock. The lock can be acquired by only one
    thread at a time. If the lock is already locked by one thread, while another thread tries to lock it, it
    changes its state to BLOCK and wait for the mutex to be released. Only the thread which locked
    the mutex can release it. After the mutex is released, one of the waiting threads will change its
    state from BLOCK to READY and will try to acquire the mutex again next time it will be RUNNING.
    
- for example:

    <img width="569" alt="צילום מסך 2021-11-09 ב-14 11 01" src="https://user-images.githubusercontent.com/83215154/140922121-355ae436-3ede-48c6-a932-c7e5273cf679.png">

    
# Thread State Diagram

At any given time during the running of the user's program, each of the threads in the program is in one of
the states shown in the following state diagram. Transitions from state to state occur as a result of calling
one of the library functions, or from elapsing of time,

 <img width="766" alt="צילום מסך 2021-11-09 ב-13 50 21" src="https://user-images.githubusercontent.com/83215154/140919365-b6aa2de7-c33f-476c-8215-dd79086a0ec5.png">
    

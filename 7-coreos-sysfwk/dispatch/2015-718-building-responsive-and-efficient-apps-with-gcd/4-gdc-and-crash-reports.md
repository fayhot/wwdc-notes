
[GCD and Crash Reports](4-gdc-and-crash-reports.md) | | | 



Reading the Tea Leaves
Manager thread

```text
Thread 1:: Dispatch queue: com.apple.libdispatch-manager
0   libsystem_kernel.dylib      0x00007fff8967e08a kevent_qos + 10
1   libdispatch.dylib           0x00007fff8be05811 _dispatch_mgr_invoke + 251
2   libdispatch.dylib           0x00007fff8be05465 _dispatch_mgr_thread + 52
```


Idle GCD thread

```text
Thread 6:
0   libsystem_kernel.dylib      0x00007fff8967d772 __workq_kernreturn + 10
1   libsystem_pthread.dylib     0x00007fff8fd317d9 _pthread_wqthread + 1283
2   libsystem_pthread.dylib     0x00007fff8fd2ed95 start_wqthread + 13
```




### Active GCD thread


```text
Thread 3 Crashed:: Dispatch queue: <queue name>
                                             <my code>
7   libdispatch.dylib
8   libdispatch.dylib
9   libdispatch.dylib
10  libdispatch.dylib
11  libdispatch.dylib
12  libdispatch.dylib
13  libsystem_pthread.dylib  0x07fff93c17637 _pthread_wqthread + 729
14  libsystem_pthread.dylib  0x07fff93c1540d start_wqthread + 13

```


### Idle main thread

```text
Thread 0 Crashed:: Dispatch queue: com.apple.main-thread
0   libsystem_kernel.dylib      0x00007fff906614de mach_msg_trap + 10
1   libsystem_kernel.dylib      0x00007fff9066064f mach_msg + 55
2   com.apple.CoreFoundation    0x00007fff9a8c1eb4 __CFRunLoopServiceMachPort
3   com.apple.CoreFoundation    0x00007fff9a8c137b __CFRunLoopRun + 1371
4   com.apple.CoreFoundation    0x00007fff9a8c0bd8 CFRunLoopRunSpecific + 296
...
10  com.apple.AppKit            0x00007fff8e823c03 -[NSApplication run] + 594
11  com.apple.AppKit            0x00007fff8e7a0354 NSApplicationMain + 1832
12  com.example                 0x00000001000013b4 start + 52
```


### Main queue

```text
Thread 0 Crashed:: Dispatch queue: com.apple.main-thread
                                                 <my code>
12  com.apple.Foundation        0x00007fff931157e8 __NSBLOCKOPERATION_IS_CALLING_OUT_TO_A_BLOCK__ + 7
13  com.apple.Foundation        0x00007fff931155b5 -[NSBlockOperation main] + 9
14  com.apple.Foundation        0x00007fff93114a6c -[__NSOperationInternal _start:] + 653
15  com.apple.Foundation        0x00007fff93114543 __NSOQSchedule_f + 184
16  libdispatch.dylib
17  libdispatch.dylib
18  com.apple.CoreFoundation  0x00007fff8d9223f9 __CFRUNLOOP_IS_SERVICING_THE_MAIN_DISPATCH_QUEUE__
19  com.apple.CoreFoundation  0x00007fff8d8dd68f __CFRunLoopRun + 2159
20  com.apple.CoreFoundation  0x00007fff8d8dcbd8 CFRunLoopRunSpecific + 296
...
26  com.apple.AppKit
27  com.apple.AppKit
28  libdyld.dylib

```
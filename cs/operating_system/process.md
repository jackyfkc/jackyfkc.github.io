Process
---
a program in execution 运行中的程序


In _UNIX 6th Edition Commentary_, it said

`Processes` can be introduced into discussions of operating systems at two levels.

操作系统中的进程可以分二个层面来理解

At the upper level, `process` is an important organising concept for describing `the activity of a computer system as a whole`. It is often expedient to view the latter as the combined activity of a number of processes, each associated with a particular program such as the `shell`, or the `editor`.

At this level the processes themselves are considered to be the `active entities` in the system, while the identities of the true active elements, the processor and the peripheral devices, are submerged: the processes are born, live and die; they exist in varying numbers; they may acquire and release resources; they may interact, cooperate, conflict, share resources; etc.

在上层, 进程是一个重要的组织概念, 用于描述计算机系统的整体活动. 可以认为它们是系统中活动的实体, 而真正的活动实体, 比如处理器, 硬盘则被雪藏了. 进程可以被创建, 进行计算活动, 死亡; 它们可以获取, 释放资源. 它们可以交互, 协作, 冲突, 共享资源等等.

At the lower level, `processes` are `inactive entities` which are acted on by active entities such as the processor. By allowing the processor to switch frequently from the execution of one process image to another, the impression can be created that each of the process images is developing continuously and this leads to the upper level interpretation.

在下层, 进程是非活动实体. 通过处理器在不同进程间切换(上下文切换)来实现上层的假象


### Daemon

A `deamon` is a process that runs in the background and is not associated with a controlling terminal.



### Zombie
...



### Signal

Signals allow the manipulation of a process from outside its domain, as well as allowing the process to manipulate itself or copies of itself (children).

There are two general types of signals: those that cause termination of a process and those that do not.  Signals which cause termination of a program might result from an irrecoverable error or might be the result of a user at a terminal typing the `interrupt' character.

Signals are used when a process is stopped because it wishes to access its control terminal while in the background.  Signals are optionally generated when a process resumes after being stopped, when the status of child processes changes, or when input is ready at the control terminal.  Most signals result in the termination of the process receiving them, if no action is taken; some signals instead cause the process receiving them to be stopped, or are simply discarded if the process has not requested otherwise.

Except for the `SIGKILL` and `SIGSTOP` signals, the `signal()` function allows for a signal to be caught, to be ignored, or to generate an interrupt.


These signals are defined in the file <signal.h>:

     No    Name         Default Action       Description
     1     SIGHUP       terminate process    terminal line hangup
     2     SIGINT       terminate process    interrupt program
     3     SIGQUIT      create core image    quit program
     4     SIGILL       create core image    illegal instruction
     5     SIGTRAP      create core image    trace trap
     6     SIGABRT      create core image    abort program (formerly SIGIOT)
     7     SIGEMT       create core image    emulate instruction executed
     8     SIGFPE       create core image    floating-point exception
     9     SIGKILL      terminate process    kill program
     10    SIGBUS       create core image    bus error
     11    SIGSEGV      create core image    segmentation violation
     12    SIGSYS       create core image    non-existent system call invoked
     13    SIGPIPE      terminate process    write on a pipe with no reader
     14    SIGALRM      terminate process    real-time timer expired
     15    SIGTERM      terminate process    software termination signal
     16    SIGURG       discard signal       urgent condition present on socket
     17    SIGSTOP      stop process         stop (cannot be caught or ignored)
     18    SIGTSTP      stop process         stop signal generated from keyboard
     19    SIGCONT      discard signal       continue after stop
     20    SIGCHLD      discard signal       child status has changed
     21    SIGTTIN      stop process         background read attempted from control terminal
     22    SIGTTOU      stop process         background write attempted to control terminal
     23    SIGIO        discard signal       I/O is possible on a descriptor (see fcntl(2))
     24    SIGXCPU      terminate process    cpu time limit exceeded (see setrlimit(2))
     25    SIGXFSZ      terminate process    file size limit exceeded (see setrlimit(2))
     26    SIGVTALRM    terminate process    virtual time alarm (see setitimer(2))
     27    SIGPROF      terminate process    profiling timer alarm (see setitimer(2))
     28    SIGWINCH     discard signal       Window size change
     29    SIGINFO      discard signal       status request from keyboard
     30    SIGUSR1      terminate process    User defined signal 1
     31    SIGUSR2      terminate process    User defined signal 2

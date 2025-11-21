# Intro to Operating Systems

So what happens when a programs runs?

- According to the Von Neumann model of computation (heavily influenced by Turing's notion of a "universal machine"), a running program executes instructions.
- The fetch-decode-execute instruction cycle

Yet, a lot of things go on "behind the scences", while a program is running.
Enter the operating system...

Informally, what does an operating system (OS) do?

- The OS allows you, the user, to "seemingly" run many programs at the same time.
  - The OS virtualizes the CPU and memory.
- It allows programs to share system resources (e.g memory, disk, I/O, network, etc...).

So how does the OS do its thing?

- Through a general, powerful technique called **virtualization**

Recall the subtitle of this OSTEP, **Three Easy Pieces**...
Well, virtualization is the first piece of the puzzle!

So the OS "transforms" a **physical** resource (e.g the processor) into a **virtual** form of itself. Sometimes, you'll hear people refer to the OS as a **virtual machine**

So how does a OS virtualize system resources?

- Asking _why_ is silly (it makes the system to use from the user's POV)
- **Mechanisms** and **policies** are implemented by the OS to attain virtualization

An OS provides the user with application programming interfaces (API) to make use of the features of the virtual machine (e.g reading from or writing to a file, allocating memory, running a program). These are formally called **system calls**

So if two programs want to run at a particular time, which _should_ run?
That is decided by the OS via a scheduling **policy**

Ch. 2 of OSTEP introduces the subtle distinction between a process and a program in the two sections **2.1 Virtualizing the CPU** and **2.2 Virtualizing memory**
The process identifier (PID) is unique per running process. Two processes may be running the same program. For example, `$ ./mem & mem` runs two instances of _mem_ in the background.

Each process has its own private memory, formally known as the **address space**. The OS maps the virtual address space to the physical memory of the machine.

The second piece of the OSTEP puzzle is **concurrency**

Informally, **concurrency** is just juggling many things at once (ie. concurrently). Multi-threaded programs (more on that in a later post) must resolve the problems of concurrency (aka. race hazards or conditions)

I like the authors' preliminary definition of a thread: "a function running within the same memory space as other functions, with more than one of them active at a time"

## Homework 1

The end of chapter 4 questions are all about seeing how a process state changes while a program is running.
I highly recommend [forking](<https://en.wikipedia.org/wiki/Fork_(software_development)>) the GitHub repo (short for repository) remzi-arpacidusseau/ostep-homework. To those unitiaited with version control, I might write up a blog post to give a quick and dirty guide on using [git](https://git-scm.com/).
Forking a repo allows you to duplicate and modify an existing codebasse without affecting the original code.

In the ostep-homework repo, take a look at cpu-intro/README.md for more information.

1. Run `./process-run.py -l 5:100,5:100`.
   What should the CPU utilization be (i.e the percent of time the CPU is in use)? Why do you know this? Check your answer with the -c and -p flags.
   HINT: the comma-seperated values after the `-l` flag is the PROCESS_LIST (see the README.md file). For this particular commmand prompt, we are running two processes each have 5 instructions (the number before the colon) and each instruction has a 100% chance of using the CPU (the number after the colon).

   The CPU utilization is 100%, as both process 0's and process 1's instructions are all "CPU-bound" (i.e no I/O requests) and the CPU is always busy.

2. Now run `./process-run.py -l 4:100,1:0` This command prompt specifies two processes to run: one process with 4 CPU-bound instructions and another process that simply issues and I/O request.
   How long does it take to complete both proceses? Use `-c` and `-p` to check you answer

   TIME_CPU = 6 ticks = 4 (from process 0) + 2 (initiating and completing the I/O request for process 1)
   TIME_IO = 5 ticks (The default period of an I/O request is 5 clock ticks. This can be changed by appending `-L IO_LENGTH` flag.

   So it takes 11 clock ticks to complete both processes.

3. What happens when you switch the order of process in question 2? i.e run `./process-run.py -l 1:0,4:100`.
   Does the switching order matter? Why or why not?

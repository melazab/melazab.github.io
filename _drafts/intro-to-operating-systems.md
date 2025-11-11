# Intro to Operating Systems

So what happens when a programs runs?

- According to the Von Neumann model of computation (heavily influenced by Turing's notion of a "universal machine"), a running program executes instructions.
- The fetch-decode-execute instruction cycle

Yet, a lot of things go on "behind the scences", while a program is running.
Enter the operating system...

Informally, what does an operating system (OS) do?

- The OS allows you, the user, to "seemingly" run many programs at the same time.
- It allows programs to share system resources (e.g memory, disk, I/O, network, etc...)

So how does the OS do its thing?

- Through a general, powerful technique called **virtualization**

Recall the subtitle of this OSTEP, **Three Easy Pieces**...
Well, virtualization is the first piece of the puzzle!

So the OS "transforms" a **physical** resource (e.g the processor) into a **virtual** form of itself. Sometimes, you'll hear people refer to the OS as a **virtual machine**

So how does a OS virtualize system resources?

- Asking _why_ is silly (it makes the system to use from the user's POV)
- **Mechanisms** and **policies** are implemented by the OS to attain virtualization

An OS provides the user with an application programming interfaces (API) to make use of the features of the virtual machine (e.g reading from or writing to a file, allocating memory, running a program). These are formally called **system calls**

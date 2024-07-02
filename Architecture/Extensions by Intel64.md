<h2>Intel 64 incorporates multiple extensions of von Neumann’s architecture. The most important are:</h2>
<h3>Registers</h3>
These are memory cells placed directly on the CPU chip. Circuit-wise they are much faster,
but they are also more complicated and expensive. Register accesses do not use the bus. The response time
is quite small and usually equals a couple of CPU cycles.

<h3>Hardware stack</h3>
A stack in general is a data structure. It supports two operations: pushing an element
on top of it and popping the topmost element. A hardware stack implements this abstraction on top of
memory through special instructions and a register, pointing at the last stack element. A stack is used not
only in computations but to store local variables and implement function call sequence in programming
languages.

<h3>Interrupts</h3>
This feature allows one to change program execution order based on events external to
the program itself. After a signal (external or internal) is caught, a program’s execution is suspended, some
registers are saved, and the CPU starts executing a special routine to handle the situation. Following are
exemplary situations when an interrupt occurs (and an appropriate piece of code is executed to handle it):

- A signal from an external device.
- Zero division.
- Invalid instruction (when CPU failed to recognize an instruction by its binary
representation).
- An attempt to execute a privileged instruction in a non-privileged mode.

<h3>Protection rings</h3>
A CPU is always in a state corresponding to one of the so-called protection rings. Each
ring defines a set of allowed instructions. The zero-th ring allows executing any instruction from the entire
CPU’s instruction set, and thus it is the most privileged. The third allows only the safest ones. An attempt to
execute a privileged instruction results in an interrupt. Most applications are working inside the third ring
to ensure that they do not modify crucial system data structures (such as page tables) and do not work with
external devices, bypassing the OS. The other two rings (first and second) are intermediate, and modern
operating systems are not using them.

<h3>Virtual memory</h3>
This is an abstraction over physical memory, which helps distribute it between
programs in a safer and more effective way. It also isolates programs from one another.

<h3>Shadow register</h3>
This is a register devised within the microcontroller for purpose of holding certain data to be used later. The name "Shadow" implies to duplicate some value and use it again - so it wont get lost.
The shadow registers save the program's context by capturing several core registers when an interrupt occurs. The core registers are restored when a Return From Interrupt (RETFIE) instruction is executed.

<h3>Cache</h3>
A CPU cache is a hardware cache used by the central processing unit (CPU) of a computer to reduce the average cost (time or energy) to access data from the main memory.
A cache is a smaller, faster memory, located closer to a processor core, which stores copies of the data from frequently used main memory locations. Most CPUs have a hierarchy of multiple cache levels (L1, L2, often L3, and rarely even L4), with different instruction-specific and data-specific caches at level 1.
The cache memory is typically implemented with static random-access memory (SRAM), in modern CPUs by far the largest part of them by chip area, but SRAM is not always used for all levels (of I- or D-cache), or even any level, sometimes some latter or all levels are implemented with eDRAM.
Other types of caches exist (that are not counted towards the "cache size" of the most important caches mentioned above), such as the translation lookaside buffer (TLB) which is part of the memory management unit (MMU) which most CPUs have.

<h2>Modern extentions for von Neumann Architecture</h2>

| Problem                                                            | Solution      |
| ------------------------------------------------------------------ | ----------------- |
| Nothing is possible without querying slow memory                   | Registers, caches |
| Lack of interactivity                                              | Interrupts        |
| No support for code isolation in procedures, or for context saving | Hardware stack    |
| Multitasking: any program can execute any instruction              | Protection rings  |
| Multitasking: programs are not isolated from one another           | Virtual memory    |

This is a computer consisting of one processor and one memory bank, connected to a common
bus. A central processing unit (CPU) can execute instructions, fetched from memory by a control unit.
The arithmetic logic unit (ALU) performs the needed computations. The memory also stores data.
Key features of this architecture:
• Memory stores only bits (a unit of information, a value equal to 0 or 1).
• Memory stores both encoded instructions and data to operate on. There are no means
to distinguish data from code: both are in fact bit strings.
• Memory is organized into cells, which are labeled with their respective indices in
a natural way (e.g., cell #43 follows cell #42). The indices start at 0. Cell size may
vary (John von Neumann thought that each bit should have its address); modern
computers take one byte (eight bits) as a memory cell size. So, the 0-th byte holds the
first eight bits of the memory, etc.
• The program consists of instructions that are fetched one after another. Their
execution is sequential unless a special jump instruction is executed.


Architecture overview:

| CPU          |       |        |
| ------------ | ----- | ------ |
| Control Unit | <---> | MEMORY |
| ALU          |       |        |

Memory model:

|      | MEMORY |          |
| ---- | ------ | -------- |
| 0000 | 0000   | 11011100 |
| 0000 | 0001   | 11011110 |
| 000  | 0002   | 11011001 |
|      | ...    |          |
| FFFF | FFFF   | 00110010 |

Memory state and values of registers fully describe the CPU state (from a programmer’s point of
view). understanding an instruction means understanding its effects on memory and registers
<h2>Registers</h2>

<h3>Overview</h3>

Crucial part of von Neumann computer is data exchanging beetwen CPU and memory. Instructions have to be fetched from memory, operands have to be fetched from memory, somy instructions store results also in memory.
It creates a bottleneck and CPU time wasting when we are waiting from data from memory.
That's why CPU are equipped in own memory, called registers. There are only few of them, but fast.
Registers are based on transistors, while main memory uses condensers. We could have implemented
main memory on transistors and gotten a much faster circuit. There are several reasons engineers prefer
other ways of speeding up computations.

- Registers are more expensive.
- Instructions encode the register’s number as part of their codes. To address more
registers the instructions have to grow in size.
- Registers add complexity to the circuits to address them. More complex circuits are
harder to speed up. It is not easy to set up a large register file to work on 5 GHz.

<h3>Data locality</h3>

In worst case, registers slowdown processor. If everything has to be fetched into registers before the computations are made and flushed into memory after, where’s the profit?
The programs are usually written in such a way which is called **locality of reference** and there are two main types of it: temporal and spatial.
- Temporal locality means that accesses to one address are likely to be close in time.
- Spatial locality means that after accessing an address X the next memory access will likely to be close
to X, (like X − 16 or X + 28).

These properties are not binary: you can write a program exhibiting stronger or weaker locality.
Typical programs are using the following pattern: the data working set is small and can be kept inside registers. After fetching the data into registers once we will work with them for quite some time, and then the results will be flushed into memory.
The data stored in memory will rarely be used by the program. In case we need to work with this data we will lose performance because
- We need to fetch data into the registers.
- If all registers are occupied with data we still need later on, we will have to spill some of
them, which means save their contents into temporally allocated memory cells.

<h3>General Purpose Registers</h3>

Most of the time, we work with **general purpose registers**. These are 64bits registers called *r0, r1, …, r15*.
The first eight of them can be named alternatively; these names represent the meaning they bear for some special instructions.
For example, *r1* is alternatively named *rcx*, where *c* stands for “cycle.” There is an instruction loop, which uses *rcx* as a cycle counter but accepts no operands explicitly.

<h2>64-bit General Purpose Registers</h2>

| Name         | Alternative name (alias) | Description |
| ------------ | ------------------------ | ----------- |
| r0           | rax                      | Kind of an “accumulator,” used in arithmetic instructions. For example, an instruction div is used to divide two integers. It accepts one operand and uses rax implicitly as the second one. After executing div rcx a big 128-bit wide number, stored in parts in two registers rdx and rax is divided by rcx and the result is stored again in rax. |
| r3           | rbx                      | Base register. Was used for base addressing in early processor models. |
| r1           | rcx                      | Used for cycles (e.g., in loop). |
| r2           | rdx                      | Stores data during input/output operations. |
| r4           | rsp                      | Stores the address of the topmost element in the hardware stack. |
| r5           | rbp                      | Stack frame’s base. |
| r6           | rsi                      | Source index in string manipulation commands (such as movsd). |
| r7           | rdi                      | Destination index in string manipulation commands (such as movsd). |
| r8, r9...r15 | no                       | Appeared later. Used mostly to store temporal variables (but sometimes used implicitly, like r10, which saves the CPU flags when syscall instruction is executed. |

You usually do not want to use *rsp* and *rbp* registers because of their very special meaning. However, you can perform arithmetic operations on them directly, which makes them general purpose.

<h3>Registers sorted by their names following an indexing convention</h3>

| r0  | r1  | r2  | r3  | r4  | r5  | r6  | r7  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| rax | rcx | rdx | rbx | rsp | rbp | rsi | rdi |

Addressing a part of a register is possible. For each register you can address its lowest 32 bits, lowest 16
bits, or lowest 8 bits.
When using the names *r0,...,r15* it is done by adding an appropriate suffix to a register’s name:
- d for double word—lower 32 bits;
- w for word—lower 16 bits;
- b for byte—lower 8 bits

For example:
- r7b is the lowest byte of register r7;
- r3w consists of the lowest two bytes of r3; and
- r0d consists of the lowest four bytes of r0.

The naming convention for accessing parts of *rax, rbx, rcx*, and *rdx* follows the same pattern; only the middle letter (*a* for *rax*) is changing. The other four registers do not allow an access to their second lowest
bytes (like rax does by the name of ah). The lowest byte naming differs slightly for rsi, rdi, rsp, and rbp.
- The smallest parts of rsi and rdi are sil and dil.
- The smallest parts pf rsp and rbp are spl and bpl.

In practice, the names *r0-r7* are rarely seen. Usually programmers stick with alternate names for the **first eight general purpose registers**. It is done for both legacy and semantic reasons: *rsp* relates a lot more information, than *r4*. The other eight (*r8-r15*) can only be named using an indexed convention.

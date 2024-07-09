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

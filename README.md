# -Mixed-Signal-Physical-Design-Flow-with-Sky130
 This directory describes how the PNR of an analog IP, 2:1 analog multiplexer is carried out by opensource EDA tools, OpenLANE. It also discusses the steps to modify the current IP layouts in order to ensure its acceptance by the EDA tools.


**Chapter 1: Generating hard-macro LEF for basic analog block**

**1.a Introduction to mixed-signal flow & EDA tools**

**What is mixed signal?**

Mixed signal is a design which consists of both analog as the digital components in the same packageas you can see in the traditional mixed signals, consist of a separate digital and a separate analog component.

Both of them combine, including a chip, whereas in the modern mixed signal you can see that the digital

analog components are present as it was in the traditional ones.

But along with that of mixed signal, block is also present.

Now, what is this mixed signal?

Mixed Signals Block is a block which consists of both digital analog component inside a single component,

unlike the one the traditional which would separate.

So first, why is there a need for mixed signals nowadays, the analog component is rapidly increasing,

which requires us for mixed signals the same.

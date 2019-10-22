# Chapter 2: MapReduce and the New Software Stack
- Nowadays, data analysis might require processing terabytes or petabytes of data. Fortunately, it's possible to exploit parallelism to perform such computations in a reasonable amount of time
- We get parallelism from **compute clusters** consisting of multiple **compute nodes**, which themselves are collections of commidity hardware connected by ethernet or switches.
- Data storage also looks different in this context, where we will have **distributed filesystems** to redundantly store chunks of files across compute nodes.
- Distributed programming systems like **MapReduce** provide a simple, fault-tolerant model for efficiently performing common calculations across distributed datasets.
  - Writing good MapReduce programs looks different from writing parallelized code which runs on a supercomputer because of the issue of **network bandwidth**

## 2.1 Distributed Filesystems
- Distributed computing leverages collections of commidity hardware, rather than specialized supercomputers, making it more cost-effective
  
### 2.1.1 Physical Organization of Compute Nodes
- Typically, a datacenter will consist of racks, each containing 8-64 servers
- Each server can communicate with the other servers in the same rack through a **gigabit Ethernet** connection
- Communication *between racks* is done through a **network switch** which has higher bandwidth than the aforementioned ethernet
- Node failures are inevitable with massive compute clusters, so if a node crashes we might have two issues:
  - The data on the node becomes unavailable, either temporarily or permanently
  - The computation has to be started all over again
- To mitigate these issues, distributed computing systems will:
  - Store **redundant** copies of data, such that it is accessible even if the primary node it's on fails
  - Define computations with more discrete chunks, or **tasks**, each of which can be started/restarted independently from the rest
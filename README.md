[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: 
### Student Id: 
### Email: 

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

I used Phoronix Test Suite (PTS) as the measurement tool, which is a widely used open-source benchmarking framework for Linux platforms. It can measure both CPU and memory performance.<br>

Configuration Parameters:<br>
Benchmark Suite: pts/cpu and pts/memory<br>
    pts/cpu was selected to evaluate processor computing capabilities, including integer and floating-point performance.<br>
    pts/memory was chosen to assess system memory bandwidth and access latency.<br>
Test Iterations: 3 times<br>
    Three test iterations were performed to minimize random errors and improve measurement stability.<br>
    
Meaning of Measurement Results:<br>
CPU Performance Results:<br>
    Possible metrics include FLOPS (Floating Point Operations Per Second), integer operations per second, or execution time for scientific computing tasks.<br>
    Higher values indicate better CPU computational performance.<br>
Memory Performance Results:<br>
    Possible metrics include memory bandwidth (MB/s) and latency (ns).<br>
    Higher memory bandwidth indicates faster data read/write speeds, while lower latency means more efficient data access.<br>

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` | Compression Rating: Average: 3685 MIPS ; Deviation: 2.27%<br> Decompression Rating: Average: 3101 MIPS ; Deviation: 0.31% | Type: Copy - Benchmark: Integer: Average: 10939.35 MB/s ; Deviation: 0.28% |
    | `t2.medium`  | Compression Rating: Average: 9796 MIPS ; Deviation: 1.86%<br> Decompression Rating: Average: 5911 MIPS ; Deviation: 1.07% | Type: Copy - Benchmark: Integer: Average: 19552.74 MB/s ; Deviation: 1.40% |
    | `c5d.large` | Compression Rating: Average: 7557 MIPS ; Deviation: 0.39%<br> Decompression Rating: Average: 4960 MIPS ; Deviation: 0.86% | Type: Copy - Benchmark: Integer: Average: 14151.21 MB/s ; Deviation: 0.39% |

    The CPU performance does not increase proportionally with the increase in resources. For example:<br>
    t2.medium (which has more resources than t2.micro) shows a significant improvement in both compression and decompression performance (compression increased by approximately 2.66x, and decompression by 1.9x).<br>
    However, c5d.large (with more resources than t2.medium) does not show a proportional increase in performance. In fact, its CPU performance is lower than that of t2.medium in both compression and decompression. This may be due to the specific architecture and configuration of the instances.<br>
    Memory Performance:<br>
    Similarly, memory performance increases with the size of the instance but is not strictly proportional. The t2.medium outperforms the c5d.large in memory bandwidth (19552 MB/s vs. 14151 MB/s), despite c5d.large having more resources. This suggests that t2.medium might have better memory access or configuration for certain workloads.
    

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |                |          |
    | `m5.large` - `m5.large`   |                |          |
    | `c5n.large` - `c5n.large` |                |          |
    | `t3.medium` - `c5n.large` |                |          |
    | `m5.large` - `c5n.large`  |                |          |
    | `m5.large` - `t3.medium`  |                |          |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |                |          |
    | N. Virginia - N. Virginia |                |          |
    | Oregon - Oregon           |                |          |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.

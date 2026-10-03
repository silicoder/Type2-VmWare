# Type-2 Hypervisor – VMware Workstation

This folder contains the screenshots, configuration details, procedure, commands, and benchmark results for the **Type-2 Hypervisor – VMware Workstation** part of the Hypervisor Performance Analysis experiment.

---

## 1. Experiment Title

**Performance Evaluation of a Type-2 Hypervisor using VMware Workstation**

---

## 2. Objective

To create and configure an Ubuntu Virtual Machine (VM) using **VMware Workstation**, a Type-2 hypervisor, and evaluate the VM's CPU, memory, storage, and system performance using Linux system monitoring commands and the **Sysbench CPU benchmark**.

---

## 3. Hypervisor

| Parameter              | Details                    |
| ---------------------- | -------------------------- |
| Hypervisor             | VMware Workstation         |
| Hypervisor Type        | Type-2 / Hosted Hypervisor |
| Guest Operating System | Ubuntu                     |
| Network Mode           | NAT                        |

VMware Workstation is a Type-2 hypervisor that runs on top of a host operating system and provides an environment for creating and running virtual machines.

---

## 4. Requirements

The following were required for the experiment:

* PC with VMware Workstation installed
* Ubuntu ISO image
* Internet connection
* Sufficient CPU and RAM resources
* Sysbench installed inside the Ubuntu VM

---

## 5. Machine Specification

The Ubuntu virtual machine was configured with the following specifications:

| Parameter         | Configuration          |
| ----------------- | ---------------------- |
| VM Name           | `CC-Experiment1-Type2` |
| Guest OS          | Ubuntu                 |
| CPU               | 2 vCPU                 |
| CPU Configuration | 1 Processor, 2 Cores   |
| RAM               | 2048 MB (2 GB)         |
| Disk              | 20 GB                  |
| Network Adapter   | NAT                    |
| Computer Name     | `cc-type2-vm`          |

---

## 6. Procedure

### Step 1: Open VMware Workstation

Opened **VMware Workstation** and selected:

**Create a New Virtual Machine**

---

### Step 2: Select Virtual Machine Configuration

Selected:

**Typical (recommended)**

configuration.

---

### Step 3: Select Ubuntu ISO

Selected:

**Installer disc image file (ISO)**

and browsed to the downloaded Ubuntu ISO file.

---

### Step 4: Select Guest Operating System

Configured the guest operating system as:

```text
Guest OS: Linux
Version: Ubuntu 64-bit
```

---

### Step 5: Configure Virtual Machine Name

Set the VM name as:

```text
CC-Experiment1-Type2
```

---

### Step 6: Configure Virtual Disk

Configured the virtual disk with:

```text
Disk Size: 20 GB
```

---

### Step 7: Customize Hardware

Opened **Customize Hardware** and configured:

```text
Memory: 2048 MB (2 GB)

Processors:
    Number of processors: 1
    Number of cores per processor: 2
    Total vCPU: 2

Network Adapter:
    NAT
```

---

### Step 8: Install Ubuntu

Powered on the VM and completed the Ubuntu installation.

The computer name was configured as:

```text
cc-type2-vm
```

---

### Step 9: Login to Ubuntu

Restarted the virtual machine after installation and logged in to the Ubuntu operating system.

---

### Step 10: Check System Information

The following commands were executed to inspect the VM's system configuration and resource usage.

#### Hostname and OS Information

```bash
hostnamectl
```

#### CPU Information

```bash
lscpu
```

#### Memory Usage

```bash
free -h
```

#### Disk Usage

```bash
df -h
```

#### Real-Time System Monitoring

```bash
top
```

---

## 7. Installing Sysbench

Updated the Ubuntu package repository:

```bash
sudo apt update
```

Installed Sysbench:

```bash
sudo apt install sysbench -y
```

Checked the installed Sysbench version:

```bash
sysbench --version
```

---

## 8. CPU Benchmark

The CPU benchmark was performed using:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

This benchmark measures the CPU processing performance of the virtual machine by performing prime-number calculations.

---

## 9. VM Hardware Verification

After running the benchmark, the VMware virtual machine hardware configuration was checked through:

**VM → Settings**

The following settings were verified:

* Memory allocation
* Processor configuration
* Virtual disk capacity
* Network adapter configuration

---

## 10. Sysbench CPU Benchmark Result

The following result was obtained from:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

### CPU Performance

```text
Events per Second: 951.38
```

### General Statistics

```text
Total Time: 10.0011 s
Total Number of Events: 9517
```

### Latency

```text
Minimum:          0.95 ms
Average:          1.04 ms
Maximum:          4.24 ms
95th Percentile:  1.10 ms
```

---

## 11. Result Summary

| Metric            |        Result |
| ----------------- | ------------: |
| CPU Events/Second |    **951.38** |
| Total Time        | **10.0011 s** |
| Total Events      |      **9517** |
| Minimum Latency   |   **0.95 ms** |
| Average Latency   |   **1.04 ms** |
| Maximum Latency   |   **4.24 ms** |
| 95th Percentile   |   **1.10 ms** |

---

## 12. Screenshots

The following screenshots are included as evidence of the experiment.

### 12.1 CPU Information

**Files:**

* `lspu.jpg`
* `lspu1.jpg`

These screenshots show the output of:

```bash
lscpu
```

and provide CPU and processor information of the Ubuntu VM.

---

### 12.2 Memory Information

**File:**

* `free -h.jpg`

This screenshot shows the output of:

```bash
free -h
```

and displays the memory allocation and usage of the VM.

---

### 12.3 Sysbench CPU Benchmark

**Files:**

* `Sysbench.jpg`
* `sysbenchjpg.jpg`

These screenshots show the output of:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

and contain the CPU performance and latency measurements.

---

## 13. Commands Used

The complete set of commands used during the experiment is listed below:

```bash
sudo apt update

sudo apt install sysbench -y

sysbench --version

sysbench cpu --cpu-max-prime=20000 run

hostnamectl

lscpu

free -h

df -h

top

sudo poweroff
```

---

## 14. VM Shutdown

After completing the experiment, the Ubuntu VM was safely shut down using:

```bash
sudo poweroff
```

---

## 15. Result

An Ubuntu virtual machine was successfully created and executed using **VMware Workstation**, a Type-2 hypervisor.

The VM was configured with:

* **2 vCPUs**
* **2 GB RAM**
* **20 GB disk**
* **NAT networking**

The Sysbench CPU benchmark produced the following results:

```text
Events per Second: 951.38

Total Time:         10.0011 s
Total Events:       9517

Minimum Latency:    0.95 ms
Average Latency:    1.04 ms
Maximum Latency:    4.24 ms
95th Percentile:    1.10 ms
```

These measurements provide a performance baseline for the Ubuntu VM running on VMware Workstation.

---

## 16. Conclusion

The experiment successfully demonstrated the creation, configuration, and performance evaluation of an Ubuntu virtual machine using **VMware Workstation** as a Type-2 hypervisor.

The VM was configured with 2 vCPUs, 2 GB RAM, 20 GB storage, and NAT networking. System information was collected using Linux monitoring commands, and CPU performance was evaluated using Sysbench.

The collected benchmark data can be used along with the Type-1 Proxmox VE results for the overall **Hypervisor Performance Analysis** experiment.

---

## 17. Folder Structure

The experiment folder can be organized as follows:

```text
Type-2-VMware/
│
├── README.md
│
├── Screenshots/
│   ├── lspu.jpg
│   ├── lspu1.jpg
│   ├── free -h.jpg
│   ├── Sysbench.jpg
│   └── sysbenchjpg.jpg
│
└── Results/
    └── Sysbench_CPU_Result.txt
```

---

## 18. Experiment Summary

| Category        | Details                       |
| --------------- | ----------------------------- |
| Experiment      | Type-2 Hypervisor Performance |
| Hypervisor      | VMware Workstation            |
| Hypervisor Type | Type-2                        |
| Guest OS        | Ubuntu                        |
| CPU             | 2 vCPU                        |
| RAM             | 2 GB                          |
| Storage         | 20 GB                         |
| Network         | NAT                           |
| Benchmark       | Sysbench CPU                  |
| CPU Events/sec  | **951.38**                    |
| Average Latency | **1.04 ms**                   |
| Maximum Latency | **4.24 ms**                   |

# Performance Analysis of Type-1 and Type-2 Hypervisors

Cloud Computing Lab experiment - Proxmox VE vs VMware Workstation

---

## Objective

In this experiment I made the same Ubuntu VM on a Type-1 hypervisor and a Type-2 hypervisor. Then I ran a Sysbench CPU test on both and compared the results.

## Hypervisors Used

* Type-1: Proxmox VE
* Type-2: VMware Workstation

Proxmox VE runs on a physical server and I used it from the browser. VMware Workstation runs on top of a host operating system.

## VM Configuration

I used the same configuration on both:

* OS: Ubuntu
* CPU: 2 vCPU
* RAM: 2 GB
* Disk: 20 GB
* Benchmark: Sysbench

Sysbench command:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

---

## Type-1: Proxmox VE

### Login

* Opened `https://<PROXMOX_SERVER_IP>:8006` in the browser
* A security warning came because of the self-signed certificate, so I clicked Advanced and then Proceed
* Logged in with the given credentials

### VM Settings

I clicked Create VM and used these settings:

* Name: `CC-Experiment1-Type1`
* OS: Ubuntu ISO, storage `local`
* Disk: 20 GB (`local-lvm`)
* CPU: 1 socket, 2 cores (2 vCPU)
* Memory: 2048 MiB (2 GB)
* Network: bridge `vmbr0`
* System tab: left as default

### After Creating the VM

* Started the VM and opened the Console
* Installed Ubuntu and logged in
* Checked the VM with `hostnamectl`, `lscpu`, `free -h`, `df -h` and `top`
* Installed Sysbench and ran the benchmark:

```bash
sudo apt update
sudo apt install sysbench -y
sysbench --version
sysbench cpu --cpu-max-prime=20000 run
```

* Checked CPU, memory, network and disk usage in the Summary page of the VM
* Shut down the VM using `sudo poweroff`

### Screenshots

More screenshots and details are in the [Type-1-Proxmox](Type-1-Proxmox) folder.

---

## Type-2: VMware Workstation

### VM Settings

I opened VMware Workstation, clicked Create a New Virtual Machine and used these settings:

* Configuration: Typical (recommended)
* Installer disc image file (iso): Ubuntu ISO
* Guest OS: Linux, Ubuntu 64-bit
* Name: `CC-Experiment1-Type2`
* Disk: 20 GB
* In Customize Hardware:

  * Memory: 2048 MB (2 GB)
  * Processors: 1 processor, 2 cores (2 vCPU)
  * Network Adapter: NAT

### After Creating the VM

* Powered on the VM and installed Ubuntu (computer name `cc-type2-vm`)
* Restarted and logged in
* Checked the VM with `hostnamectl`, `lscpu`, `free -h`, `df -h` and `top`
* Installed Sysbench and ran the benchmark:

```bash
sudo apt update
sudo apt install sysbench -y
sysbench --version
sysbench cpu --cpu-max-prime=20000 run
```

* Checked the hardware settings under VM, then Settings
* Shut down the VM using `sudo poweroff`

### Screenshots

More screenshots and details are in the [Type-2-VMware](Type-2-VMware) folder.

---

## Results

### Type-1: Proxmox VE

* Total Execution Time: 10.0030s
* Total Events: 14548
* Events per Second: 1453.98
* Minimum Latency: 0.57 ms
* Average Latency: 0.69 ms
* Maximum Latency: 1.24 ms
* 95th Percentile: 0.74 ms

### Type-2: VMware Workstation

* Total Execution Time: 10.0011s
* Total Events: 9517
* Events per Second: 951.38
* Minimum Latency: 0.95 ms
* Average Latency: 1.04 ms
* Maximum Latency: 4.24 ms
* 95th Percentile: 1.10 ms

## Performance Comparison Table

| **Metric**           | **Type-1 (Proxmox VE)** | **Type-2 (VMware Workstation)** |
| -------------------- | ----------------------: | ------------------------------: |
| Total Execution Time |                10.0030s |                        10.0011s |
| Total Events         |                   14548 |                            9517 |
| Events per Second    |                 1453.98 |                          951.38 |
| Minimum Latency      |                 0.57 ms |                         0.95 ms |
| Average Latency      |                 0.69 ms |                         1.04 ms |
| Maximum Latency      |                 1.24 ms |                         4.24 ms |
| 95th Percentile      |                 0.74 ms |                         1.10 ms |

Comparison graphs and full details are in the [Comparison](Comparison) folder.

**Observation:** In this test, Proxmox VE (Type-1) gave a higher events per second (1453.98) than VMware Workstation (Type-2) (951.38), and also had lower average latency (0.69 ms vs 1.04 ms). Both VMs had the same configuration (2 vCPU, 2 GB RAM, 20 GB disk).

---

## Metric Explanations & Visualizations

* **Total Execution Time**: how long the Sysbench test ran for. Both tests ran for approximately 10 seconds.
* **Total Events**: total number of events completed during the test.
* **Events per Second**: how many events were completed per second (throughput). Higher values indicate more events completed during the benchmark.
* **Average Latency**: the average time taken per event. Lower values indicate less average processing time per event.

### Chart: CPU Throughput Comparison (Events per Second)

The graph below compares the number of Sysbench events completed per second by the two hypervisors.

**Graph file:** `Comparison/cpu_throughput.png`

> Graph will be added to the repository after generation.

---

### Chart: Average Latency Comparison (ms)

The graph below compares the average Sysbench latency between Proxmox VE and VMware Workstation.

**Graph file:** `Comparison/average_latency.png`

> Graph will be added to the repository after generation.

---

### Chart: Total Events Comparison

The graph below compares the total number of Sysbench events completed by each virtual machine.

**Graph file:** `Comparison/total_events.png`

> Graph will be added to the repository after generation.

---

### Chart: Total Execution Time Comparison

The graph below compares the total execution time of the Sysbench benchmark.

**Graph file:** `Comparison/execution_time.png`

> Graph will be added to the repository after generation.

---

## Technical Analysis & Discussion

Proxmox VE is a Type-1 hypervisor, while VMware Workstation is a Type-2 hypervisor.

In this experiment, Proxmox VE recorded **1453.98 events per second**, while VMware Workstation recorded **951.38 events per second**.

The average latency recorded for Proxmox VE was **0.69 ms**, compared with **1.04 ms** for VMware Workstation.

Both virtual machines used the same basic configuration of 2 vCPU, 2 GB RAM, and 20 GB disk. The measured difference in benchmark results represents the performance observed under the specific experimental conditions and hardware used for this test.

---

## Commands Used

```bash
hostnamectl
lscpu
free -h
df -h
top
sudo apt update
sudo apt install sysbench -y
sysbench --version
sysbench cpu --cpu-max-prime=20000 run
sudo poweroff
```

---

## Conclusion

I made the same VM (2 vCPU, 2 GB RAM, 20 GB disk, Ubuntu) on Proxmox VE and VMware Workstation and ran the same Sysbench CPU test on both.

In this test, Proxmox VE recorded **1453.98 events per second** with an average latency of **0.69 ms**, while VMware Workstation recorded **951.38 events per second** with an average latency of **1.04 ms**.

The results show the performance measured for both hypervisors under the configuration and test conditions used in this experiment.

---

## Repository Structure

```text
Hypervisor-Performance-Analysis/
│
├── README.md
│
├── LAB_REPORT.md
│
├── Type-1-Proxmox/
│   ├── README.md
│   └── Screenshots/
│       ├── lspuT.jpg
│       ├── free -h (2).jpg
│       └── SysbenchT1.jpg
│
├── Type-2-VMware/
│   ├── README.md
│   └── Screenshots/
│       ├── lspu.jpg
│       ├── lspu1.jpg
│       ├── free -h.jpg
│       ├── Sysbench.jpg
│       └── sysbenchjpg.jpg
│
└── Comparison/
    ├── cpu_throughput.png
    ├── average_latency.png
    ├── total_events.png
    └── execution_time.png
```

To reproduce this experiment: create an Ubuntu VM with the same configuration (2 vCPU, 2 GB RAM, 20 GB disk) on both a Type-1 and a Type-2 hypervisor, install Sysbench, and run:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

on both.

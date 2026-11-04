# Project 1: My Custom PC

My interest in building a custom PC started because I was dissatisfied with console gaming and wanted more performance, flexibility, and a better overall experience.

At the time, I had little to no knowledge about PC hardware or how to build a computer. Instead of buying a prebuilt system, I decided to learn how to build one myself. I spent about a year researching components, comparing parts, watching build guides, and learning how everything worked together.

I also decided to go big with my first PC and choose higher-end components that would give me room to upgrade and keep the system relevant for years. Rather than stopping at a standard air- or AIO-cooled setup, I challenged myself to install a full custom water-cooling loop on my very first PC.

In 2023, I completed the build successfully. Since then, I have continued upgrading, maintaining, and troubleshooting the system, which has helped me gain hands-on experience with computer hardware, cooling, system configuration, performance, and problem-solving.

<p align="center">
  <img width="60%" alt="Original PC" src="https://github.com/user-attachments/assets/7b27f50d-fe16-443a-9dbd-58c4b690e003" />
</p>

<p align="center">
  <em>My completed first custom PC in 2023.</em>
</p>

## Specifications

### Original System Specifications

- **CPU:** Intel Core i9-13900K
- **GPU:** NVIDIA GeForce RTX 4080 Founders Edition
- **Motherboard:** MSI MAG Z690 Tomahawk
- **Memory:** 32GB DDR5-6000
- **Storage:** 2TB NVMe SSD
- **Case:** HYTE Y60
- **Cooling:** Custom water-cooling loop
- **Power Supply:** Gigabyte 1000W PSU
- **Networking:** 2.5GbE + Wi-Fi 6E
- **Operating System:** Windows 11 Home

> Current system photo coming soon.

### Current System Specifications

- **CPU:** Intel Core i9-13900K
- **GPU:** NVIDIA GeForce RTX 4080 Founders Edition
- **Motherboard:** NZXT N7 Z790
- **Memory:** 32GB DDR5-6000
- **Storage:** 2 × 2TB NVMe SSDs (4TB total)
- **Case:** HYTE Y70
- **Cooling:** Custom water-cooling loop
- **Power Supply:** 1000W PSU
- **Networking:** 10GbE + Wi-Fi 7
- **Operating System:** Windows 11 Pro

## Custom Water-Cooling Loop

One of the biggest challenges I took on with my first PC was installing a full custom water-cooling loop. Since I had never built a PC before, this added another layer of difficulty to the project and required me to learn much more than basic component installation.

I researched how custom loops work, including pumps, reservoirs, radiators, tubing, fittings, coolant flow, leak testing, and maintenance. After planning the loop and choosing the components, I successfully assembled and tested the cooling system as part of my first PC.

Since completing the original loop, I have continued improving the cooling setup by upgrading the fans and fan-control system, pump/reservoir, CPU water block, tubing, and fittings. Maintaining the loop has also given me hands-on experience with draining and refilling the system, replacing components, checking connections, and troubleshooting cooling-related issues.

## Upgrades

### Motherboard Upgrade

I replaced my original MSI MAG Z690 Tomahawk with an NZXT N7 Z790 after finding a good deal on the board. I also preferred the cleaner design of the N7 and felt that it matched the overall aesthetics of my PC better.

After installing the new motherboard, I updated the BIOS and went through the necessary system configuration to make sure the hardware was recognized and operating correctly.

The upgrade gave me more experience with fully disassembling and rebuilding the system, reconnecting components, updating firmware, checking BIOS settings, and verifying that everything was working correctly after the swap.

### GPU Overclocking & Performance Tuning

I also experimented with overclocking my NVIDIA GeForce RTX 4080 Founders Edition to improve performance and learn more about GPU tuning.

Using MSI Afterburner, I increased the core clock by +170 MHz and the memory clock by +800 MHz while raising the power limit to 110%. I tested the GPU under gaming and benchmark workloads while monitoring temperatures, stability, clock behavior, and overall performance.

The goal was to find a stable overclock that improved performance without introducing crashes, visual artifacts, or excessive temperatures.

This gave me hands-on experience with GPU performance tuning, thermal monitoring, stability testing, power limits, and understanding the relationship between clock speed, power consumption, temperature, and system stability.

<p align="center">
  <img width="60%" alt="RTX 4080 FE Overclock Settings" src="https://github.com/user-attachments/assets/cb2d0b8b-ef1f-4761-8086-1e3b67d1e0a4" />
</p>

<p align="center">
  <em>MSI Afterburner settings used for my RTX 4080 Founders Edition overclock.</em>
</p>

### Networking Upgrades

I upgraded the networking capabilities of my PC after my household moved to a 7Gbps internet plan. At that point, the system's built-in 2.5GbE connection became a limitation because it could not fully take advantage of the available bandwidth. I wanted the PC to better match the speed of the new connection, so I upgraded both the wired and wireless networking.

For wired networking, I installed a 10GbE PCIe network adapter. This gave the system significantly more bandwidth than the motherboard's built-in 2.5GbE port and also provided additional headroom for future local network upgrades. After installing the adapter, I configured the required drivers, checked the network settings, and verified that the system was negotiating at the expected link speed.

The motherboard originally supported Wi-Fi 6E, but I decided to upgrade the wireless connection to Wi-Fi 7 for improved wireless performance and newer networking capabilities.

During the Wi-Fi 7 upgrade, I ran into a more complicated hardware issue. One of the motherboard's internal antenna wires had broken near the connector, which prevented the new wireless hardware from working correctly.

To fix the problem, I had to partially disassemble the motherboard so I could access the wireless module and antenna connections. I replaced the damaged antenna connection, reassembled the motherboard, and then tested the wireless connection again to confirm that the repair was successful and that the Wi-Fi 7 upgrade was functioning properly.

The networking upgrades gave me hands-on experience with PCIe network adapters, wireless networking hardware, driver installation, link-speed verification, connectivity troubleshooting, and careful motherboard disassembly and repair. It also helped me better understand how hardware limitations can create bottlenecks even when the internet connection itself is much faster.

<p align="center">
  <img width="49%" alt="10GbE Wired Speed Test" src="https://github.com/user-attachments/assets/a5532e6e-2f8e-4a61-9cd5-8bf324ce2ff4" />
  <img width="49%" alt="Wi-Fi 7 Speed Test" src="https://github.com/user-attachments/assets/5b55076d-20cf-4449-9e22-8fd89337e594" />
</p>

<p align="center">
  <em>10GbE wired and Wi-Fi 7 performance after the networking upgrades.</em>
</p>

## Troubleshooting

### Intel Core i9-13900K RMA

Over time, my original Intel Core i9-13900K began developing serious stability issues. I experienced crashes, reduced benchmark performance, and instability even when the processor was running at default settings. Because the symptoms could have been caused by several different parts of the system, I did not immediately assume that the CPU was the problem.

I worked through multiple troubleshooting steps to isolate the issue. This included updating the BIOS, returning the motherboard to default CPU settings, testing different memory configurations, reinstalling Windows, reseating hardware, checking power delivery, and verifying that the custom cooling loop was operating properly. I also monitored temperatures and benchmark performance to see whether the problem changed under different conditions.

Even after those steps, the system continued to experience instability. The fact that the processor was still unstable at default settings, combined with the performance degradation I was seeing, strongly pointed toward the CPU itself.

I submitted the i9-13900K to Intel for RMA and temporarily purchased an Intel Core i5-14600KF, so I could continue using the system while the 13900K was away. This also gave me another way to verify that the rest of the system was functioning properly. With the 14600KF installed, the system was usable while I waited for the replacement processor.

Intel approved the RMA and sent me a replacement i9-13900K. After reinstalling the replacement chip in the same system, the crashes and instability were resolved, and performance returned to normal. This confirmed that the original processor had degraded.

After receiving the replacement CPU, I took additional steps to reduce the risk of the same problem happening again. I updated the motherboard BIOS to include the newer Intel stability fixes, configured controlled CPU power limits instead of allowing unrestricted motherboard settings, and continued monitoring temperatures, power consumption, and stability under load. I also used benchmarks and stress tests to verify that the replacement CPU was operating consistently and within the limits I wanted.

I kept the i5-14600KF as a spare processor, which also gives me a known-working CPU that I can use in the future if I ever need to isolate a processor or motherboard-related issue again.

**Root Cause:** CPU degradation related to the Intel 13th-generation desktop instability issue.

This experience taught me a lot about systematic hardware troubleshooting, isolating variables, BIOS configuration, CPU power management, warranty replacement, and the value of having known-good spare hardware available when diagnosing a system.

### SSD Troubleshooting & Repurposing

At the time, my 2TB NVMe SSD was being used as my primary Windows boot drive. Following one of the system crashes, the PC stopped booting normally and would instead enter the BIOS or Windows Automatic Repair. Attempts to boot from the drive resulted in Automatic Repair failing and eventually produced a `BAD_SYSTEM_CONFIG_INFO` blue screen. Because of these symptoms, I initially suspected that the SSD itself was the source of the problem.

To get the system running again, I purchased a second NVMe SSD, installed a fresh copy of Windows on it, and began using it as my new primary boot drive.

With both drives installed at the same time, the motherboard detected both of them, and I was able to boot into the fresh Windows installation while keeping the original SSD connected as a secondary drive. From there, I was able to access the original SSD and read the data stored on it.

This showed that the original SSD hardware was still functional and that the issue was instead with the Windows installation on the drive.

Since I did not have any important data that needed to be recovered from the original drive, I wiped and reformatted it, then repurposed it for additional storage.

**Root Cause:** System instability from my degrading Intel Core i9-13900K caused Windows to crash and corrupt part of the operating system responsible for booting.

This experience taught me the importance of isolating variables during troubleshooting and not assuming that the component showing the symptoms is necessarily the root cause.

<p align="center">
  <img width="49%" alt="Troubleshooting Screenshot 1" src="https://github.com/user-attachments/assets/96827de0-944a-4008-94a7-c53483bd044a" />
  <img width="49%" alt="Troubleshooting Screenshot 2" src="https://github.com/user-attachments/assets/72b43517-c6ad-4e80-846c-03ca07a12814" />
</p>

<p align="center">
  <em>Windows boot errors encountered during SSD troubleshooting.</em>
</p>

### PSU Cable Failure

While running a benchmark, I noticed a strong burning-plastic smell coming from the system. I immediately stopped the test, shut the PC down, and inspected the hardware to find the source of the issue.

During the inspection, I discovered that one of the CPU power extension cables had melted. I removed the damaged cable and checked the surrounding connectors for any obvious signs of additional damage.

To be safe, I replaced the power supply before using the system again. After installing the new PSU, I powered the system back on and tested it to confirm that everything was operating normally.

**Root Cause:** Failure of a CPU power extension cable under heavy system load, which caused the cable to overheat and melt.

This experience taught me the importance of recognizing physical warning signs such as unusual smells, excessive heat, or discoloration during high-load testing. It also gave me more hands-on experience with diagnosing power-related hardware issues and responding cautiously when there is a risk of component damage.

## Skills Practiced

- **PC hardware:** choosing components, assembling a full system, and upgrading parts like the motherboard, storage, and case
- **Custom water cooling:** planning and assembling a loop, leak testing, draining and refilling, and replacing components
- **BIOS and firmware:** BIOS updates, default settings, and CPU power limits
- **Hardware troubleshooting:** isolating issues, swapping known-good parts, and handling a warranty RMA
- **Windows and storage:** fresh Windows installs, NVMe SSD boot drives, and repurposing drives
- **Performance tuning:** GPU overclocking, stress testing, and monitoring temperatures and stability
- **Networking hardware:** installing a 10GbE PCIe adapter, upgrading to Wi-Fi 7, drivers, and link-speed checks

---

[← Back to portfolio](../README.md)

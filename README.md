# High-Availability Enterprise Infrastructure Lab (GNS3)

Welcome to my production-ready, highly redundant enterprise topology built completely from scratch inside the GNS3 laboratory. This project represents an intensive 3-month hands-on engineering architecture designed to eliminate any Single Point of Failure (SPOF) while enforcing rigorous zero-trust security.

## 🚀 Core Architectural Features

* **Perimeter Security Tier:** 2x FortiGate Firewalls configured in Active-Passive High Availability (HA) mode to guarantee uninterrupted gateway traffic and seamless failover.
* **Core & Network Nucleus:** 2x Multilayer Layer 3 Switches. The `Main-Switch` acts as the root bridge and routing nucleus, while `BCKP-Main` acts as a hot-standby unit using PVST+ to eliminate Layer 2 loops.
* **The DMZ (Demilitarised Zone):** Dedicated tier servers (Web, Client, Email) isolated from the internal network. Every DMZ server is multi-homed and dual-connected to survive physical link failures.
* **The Quorum Data Centre:** A 3-Node Backend Server Cluster engineered explicitly to eliminate the catastrophic Split-Brain scenario.
* **Link Aggregation:** LACP Dynamic EtherChannel (802.3ad) configured across core switches and firewalls to automate link bundling and maximise throughput.

## 🔒 Layer 4 Microsegmentation & Hardening

* **Least Privilege Access:** The public Web Server in the DMZ can query the production database cluster strictly via **TCP Port 3306 (MySQL)**. Any other lateral movement is dropped at the kernel level (Implicit Deny).
* **Stealth Topology Design (ICMP Silent Target):** The database environment silently drops all ICMP echo requests to prevent unauthorised asset discovery via network sweeps.
* **Banner Grabbing Mitigation:** Service application headers and OS release signatures are masked to deny intelligence during attacker reconnaissance.

## 🛠️ Real-World Incident Management Logs

* **Case 1: Cisco IOU Kernel Crash (Segfault -11):** Resolved an offline memory allocation bug by modifying the `startup-config.cfg` file via NVRAM, bypassing the faulty dynamic negotiation phase during boot.
* **Case 2: EtherChannel Port Mismatch (Po10 Stuck in RD mode):** Forced physical/logical interfaces into pure Layer 2 mode, cleared stale channel-group blocks, and stabilised the EtherChannel into an `SU` (In Use) state.
* **Case 3: DHCP IP Allocation Failure:** Fixed trunk encapsulation restrictions on the Port-channel link between Core and Access layers using `switchport trunk allowed vlan all` to restore flawless 802.1Q tag propagation.

---
*Note: Full Low-Level Design (LLD) document and configuration files are available directly inside this repository.*# Enterprise-HA-Infrastructure-Simulation

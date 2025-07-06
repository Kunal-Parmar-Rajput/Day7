# System & Networking Cheat‑Sheet

<details>
<summary>Table of Contents</summary>

1. [Safe Mode](#1-safe-mode)
2. [Recovery Tools & OS Repair](#2-recovery-tools--os-repair)
3. [Virus & Malware Hygiene](#3-virus--malware)
4. [Storage & Backup Strategies](#4-storage--backup)
5. [Physical Networking Hardware](#5-networking-basics)
6. [Cabling Standards](#6-types-of-cables-in-networking)
7. [Hosts & Networks Fundamentals](#7-hosts--networks-fundamentals)
8. [IP Addressing Basics](#8-ip-addressing-basics)
9. [IPv4 vs IPv6](#9-ipv4-vs-ipv6)
10. [Networking Notations](#10-notations-in-networking)
11. [Classful Addressing](#11-ip-classes-classful-addressing)
12. [Address Types & Reserved Blocks](#12-address-types--reserved-ip-addresses)
13. [DNS, MAC & Gateways](#13-dns-mac-address--default-gateway)
14. [Subnetting Essentials](#14-subnetting-essentials)
15. [Bandwidth vs Latency](#15-bandwidth-and-latency)
16. [Quick Reference Summary](#16-final-summary)
</details>

---

## 1. Safe Mode
### Purpose
* Load Windows with a minimal set of drivers/services so problems caused by third‑party software or drivers don’t interfere.

### When to Use
* BSOD or boot loops after a new driver/app install
* Suspected malware infection
* Driver rollback or uninstall
* Removing stubborn software

### Types of Safe Mode
| Mode | Boot Configuration | Networking | Typical Use‑Case |
| --- | --- | --- | --- |
| **Safe Mode** | Minimal drivers & services | ❌ | Core driver issues, malware clean‑up |
| **Safe Mode with Networking** | Safe Mode + network stack | ✔️ | Download patches/tools while troubleshooting |
| **Safe Mode with Command Prompt** | CLI only | ❌ | Advanced repairs, scripting, DISM/SFC |

### How to Access Safe Mode (Win 10/11)
1. **Settings › System › Recovery › Advanced startup › Restart now**
2. **Shift + Restart** from Start menu > Power > Restart
3. Interrupt boot 3× to launch **WinRE** › *Troubleshoot* › *Advanced options* › *Startup Settings* › *Restart* › Choose option (4–6).

---

## 2. Recovery Tools & OS Repair
* **Windows Recovery Environment (WinRE)** – graphical repair console
* **Startup Repair** – fixes boot files/BCD
* **System Restore** – rolls back system files & registry
* **System Image Recovery** – restore from full image
* **Command Prompt** – manual fix via CLI

### OS Repair Methods
| Method | Tool | Scenario |
| --- | --- | --- |
| **In‑place upgrade** | Windows Setup USB | Corrupted OS but data intact |
| **SFC /scannow** | CMD (admin) | Missing/altered system files |
| **DISM /RestoreHealth** | CMD (admin) | Damaged component store |
| **Reset this PC** | Settings › Recovery | Severe OS problems, keep/delete files |

### Plugins (Add‑ons for WinRE)
* **Microsoft DaRT** – Diagnostics & Recovery Toolset
* **AOMEI Backupper** or **Macrium PE** plug‑ins

---

## 3. Virus & Malware

### Common Symptoms
| Symptom | Likely Cause |
| --- | --- |
| Endless pop‑ups/ads | Adware/PUP |
| CPU/GPU spikes at idle | Crypto‑miner |
| Browser homepage changes | Browser hijacker |
| Unknown processes & services | Trojan/rootkit |
| Files renamed with *.locked* extension | Ransomware |

### Basic Malware Removal Steps
1. Disconnect from internet/LAN.
2. Boot to **Safe Mode with Networking** (download updates only if needed).
3. Update & run trusted scanner (e.g., Windows Defender Offline, Malwarebytes).
4. Quarantine/delete detections.
5. Clear %TEMP% and browser caches.
6. Check startup entries (Task Manager › Startup, `shell:` locations, `msconfig`).
7. Run **SFC** and **DISM** to repair OS files.
8. Patch OS/apps & change passwords once clean.

---

## 4. Storage & Backup

### Where Should You Keep Your Windows Storage?
* **System Drive (C:) on SSD** – OS + apps for speed.
* **Separate Data Partition (D:)** – isolate personal files from OS.
* **External SSD/HDD** – offline backups & system images.

### Various Ways of Backing Up Important Files
| Method | Tool | Frequency | Pros | Cons |
| --- | --- | --- | --- | --- |
| File History | Built‑in | Hourly/Daily | Versioning, auto | Same‑PC risk |
| Cloud Sync | OneDrive, Google Drive | Continuous | Off‑site, easy | Bandwidth, cost |
| System Image | wbAdmin, Macrium | Weekly | Bare‑metal restore | Large size |
| Disk Clone | Macrium, Clonezilla | Monthly | Fast fail‑over | Manual process |
| 3‑2‑1 Rule | — | Strategy | 3 copies, 2 media, 1 off‑site | More planning |

### Summary (OS Troubleshooting)
| Task | Recommended Tool | Notes |
| --- | --- | --- |
| Boot loop fix | Startup Repair | WinRE automatic |
| Replace DLLs | `sfc /scannow` | Run twice if needed |
| Component store repair | `DISM /RestoreHealth` | Needs internet/ISO |
| Driver rollback | Device Manager | Use Safe Mode |

---

## 5. Networking Basics

### RJ45
* 8‑position, 8‑contact modular connector used for Ethernet.
* Locks with a plastic tab; careful not to break it.

### CAT Cable (Ethernet)
| Category | Max Bandwidth | Max Length (1 Gbps) | Shielding |
| --- | --- | --- | --- |
| CAT5e | 1 Gbps | 100 m | UTP/STP |
| CAT6 | 10 Gbps* (37‑55 m) | 100 m @ 1 Gbps | UTP/STP |
| CAT6a | 10 Gbps | 100 m | F/UTP, S/FTP |
| CAT7 | 10 Gbps | 100 m | S/FTP only |

\*10 Gbps over CAT6 limited by alien crosstalk.

### Crimping Tool
* Attaches RJ45 plugs to bulk twisted‑pair cable.
* Ratcheting action ensures full termination.
* Use cable tester after crimping.

#### Networking Summary Table
| Component | Purpose |
| --- | --- |
| RJ45 Plug | Terminate cable ends |
| Keystone Jack | Patch panel/outlet termination |
| Punch‑down Tool | Seat wires into IDC terminals |
| Cable Tester | Validate pinout & continuity |

### T568B Wiring Standard (Straight‑through)
| Pin | Color | Pair | Signal |
| --- | --- | --- | --- |
| 1 | White‑Orange | 2 | TX+ |
| 2 | Orange | 2 | TX‑ |
| 3 | White‑Green | 3 | RX+ |
| 4 | Blue | 1 | — |
| 5 | White‑Blue | 1 | — |
| 6 | Green | 3 | RX‑ |
| 7 | White‑Brown | 4 | — |
| 8 | Brown | 4 | — |

---

## 6. Types of Cables in Networking
| Cable | Medium | Typical Use |
| --- | --- | --- |
| **Twisted Pair (UTP/STP)** | Copper | LAN up to 100 m |
| **Coaxial** | Copper w/ shield | Cable internet, CCTV |
| **Fiber Optic** | Glass/Plastic | Backbone, long‑distance |

### Twisted Pair Cable
* Paired conductors twisted to reduce EMI.
* Shielded variants (STP, FTP) for high‑noise areas.

### Coaxial Cable
* Single copper core + braided shield.
* 75 Ω (RG‑6) for DOCSIS broadband, CCTV.

### Fiber Optic Cable
* Transmits light—immune to EMI.
* **Single‑mode (OS2)**: 1310/1550 nm lasers, >10 km.
* **Multi‑mode (OM3/OM4)**: 850 nm LEDs, 10 Gbps ≈ 300 m.

---

## 7. Hosts & Networks Fundamentals
### What is a **Host** in Networking?
A **host** is any device with an IP stack capable of sending/receiving data on a network.

#### Examples of Hosts
* Desktop, laptop, smartphone
* IoT devices (smart bulbs, thermostats, IP cameras)
* Virtual machines & containers
* Network printers / NAS

> **In IP addressing:** every host has at least **one unique IP address** within a subnet.

**Example:** Your phone (host) with IP `192.168.1.25/24` on Wi‑Fi.

---

### What is a **Network**?
A **network** is two or more hosts connected to exchange data.

#### Why Networks are Useful
* Resource sharing (files, printers)
* Communication (email, VoIP, video calls)
* Centralised management & security
* Internet access

#### Examples of Networks & Types
| Type | Scale | Typical Tech |
| --- | --- | --- |
| **PAN** | <10 m | Bluetooth, NFC |
| **LAN** | Building | Ethernet, Wi‑Fi |
| **CAN** | Campus | Fiber backbone |
| **MAN** | City | Metro‑Ethernet |
| **WAN** | Country/Global | MPLS, Internet |
| **GAN** | Worldwide | Satellite |
| **SAN** | Storage | Fibre Channel |
| **VPN** | Virtual overlay | IPSec, SSL |

---

## 8. IP Addressing Basics
### What is an **IP Address**?
A logical identifier for a host or interface on a network.

#### Key Properties
* **Uniqueness** within its scope (subnet/global)
* **Hierarchical**: network + host portions
* **Two versions:** IPv4 (32‑bit) & IPv6 (128‑bit)

#### Types of IP Address
* **Public vs Private**
* **Static vs Dynamic (DHCP)**
* **Unicast, Multicast, Broadcast, Anycast**

#### IP Address Format
* **IPv4:** dotted decimal (e.g., `192.0.2.146`)
* **IPv6:** hexadecimal hextets (e.g., `2001:0db8:85a3::8a2e:0370:7334`)

---

## 9. IPv4 vs IPv6
| Feature | IPv4 | IPv6 |
| --- | --- | --- |
| Address size | 32‑bit | 128‑bit |
| Address space | ~4.3 billion | 3.4×10^38 |
| Notation | Dotted decimal | Colon‑hex (compressed) |
| Header size | 20–60 bytes | Fixed 40 bytes |
| Broadcast | Supported | Replaced by multicast |
| Security | Optional (IPsec) | Built‑in (IPsec mandatory) |
| Auto‑config | DHCP | SLAAC/DHCPv6 |

### IPv4 Features
* Variable‑length header, checksum
* Fragmentation by routers
* Widespread legacy support

### IPv6 Features
* Extension headers – clean processing
* No NAT required (ample space)
* Simplified routing, anycast native

---

## 10. Notations in Networking
### Binary Notation
```
11000000 10101000 00000001 00010110  =>  192.168.1.22
```

### Dotted Decimal Notation
Human‑friendly decimal form for IPv4.

### Conversion Trick: Binary ➝ Decimal
Split byte (8 bits) → calculate 128 64 32 16 8 4 2 1 → sum positions with 1.

### CIDR Notation (Bonus)
`192.168.1.0/24` – the `/24` indicates 24 network bits; replaced classful masks.

---

<img width="715" height="375" alt="Image" src="https://github.com/user-attachments/assets/4987ee8f-25e0-41a9-85f1-80362163746b" />

## 11. IP Classes (Classful Addressing)
### What is Classful Addressing?
Original 1981 scheme dividing IPv4 into fixed‑size classes.

| Class | Leading Bits | Range (1st Octet) | Default Mask | Hosts/Subnet | Use |
| --- | --- | --- | --- | --- | --- |
| **A** | 0 | 1‑126 | 255.0.0.0 (/8) | 16 M | Large orgs |
| **B** | 10 | 128‑191 | 255.255.0.0 (/16) | 65 K | Mid‑sized |
| **C** | 110 | 192‑223 | 255.255.255.0 (/24) | 254 | Small LANs |
| **D** | 1110 | 224‑239 | – | – | Multicast |
| **E** | 1111 | 240‑255 | – | – | Experimental |

#### Limitations
* Wasted address space
* No aggregation – huge routing tables
* Led to exhaustion → **CIDR** & **IPv6**

#### Example Q&A
* **Q:** What class is `14.23.8.5`? **A:** ‑> 1‑126 ⇒ Class A.
* **Q:** Default mask for Class B? 255.255.0.0.

#### How to Remember
> **ABC = 8,16,24 masks** & first bits `0,10,110`.

---

## 12. Address Types & Reserved IP Addresses
| Range | Purpose |
| --- | --- |
| `10.0.0.0/8` | Private A |
| `172.16.0.0/12` | Private B |
| `192.168.0.0/16` | Private C |
| `127.0.0.0/8` | Loopback |
| `169.254.0.0/16` | APIPA/Link‑local |
| `0.0.0.0/32` | Default route / “any” |
| `255.255.255.255/32` | Limited broadcast |

### Network vs Host ID
* **Network ID:** bits locked by subnet mask
* **Host ID:** bits free for device addresses (cannot be all 0s or all 1s)

### Unicast vs Broadcast vs Multicast
| Type | Destination | Example Address |
| --- | --- | --- |
| **Unicast** | Single host | 192.168.1.10 |
| **Broadcast** | All hosts in subnet | 192.168.1.255 |
| **Multicast** | Group of hosts | 224.0.0.9 (RIPv2) |

---

## 13. DNS, MAC Address & Default Gateway
### DNS vs MAC (Quick Diff)
| Aspect | DNS | MAC |
| --- | --- | --- |
| Layer | Application | Data Link |
| Purpose | Resolve names → IP | Frame delivery on LAN |
| Format | `example.com` | `00‑1A‑2B‑3C‑4D‑5E` |

### Default Gateway
* Router IP where off‑subnet traffic is sent.
* **Importance:** Enables Internet or inter‑subnet comms.

> **Example:** Host 192.168.1.50/24, gateway 192.168.1.1 → traffic to 8.8.8.8 forwarded via 1.1.

#### Gateway vs Host IP
* Gateway has its **own** IP inside the subnet (**part of host address space**).

---

## 14. Subnetting Essentials
### Why We Need It
* Reduce broadcast domains
* Improve security & performance
* Efficient IP allocation

### Subnet Mask
`255.255.255.0` → `/24` – 24 network bits, 8 host bits.

| Mask | Hosts/Subnet |
| --- | --- |
| /30 | 2 |
| /29 | 6 |
| /28 | 14 |
| /27 | 30 |

### Network IP & Broadcast IP
For `/29` (`255.255.255.248`) block starting `192.168.1.0`:
* Network: **192.168.1.0**
* Usable: 192.168.1.1‑6
* Broadcast: **192.168.1.7**

---

## 15. Bandwidth and Latency
* **Bandwidth:** maximum data rate (e.g., 100 Mbps)
* **Latency:** time delay for a packet (e.g., 20 ms)

High bandwidth ≠ low latency; both matter for performance.

---
<img width="1160" height="628" alt="Image" src="https://github.com/user-attachments/assets/97156174-4820-4fc8-a102-bc31e2876fdb" />


## 16. Final Summary
| Topic | Takeaway |
| --- | --- |
| Host | Device with IP stack |
| Network | Interconnected hosts |
| IP Addr | Logical identifier (v4/v6) |
| Classful | Legacy A‑E scheme |
| CIDR | Variable‑length masks (e.g., /24) |
| Unicast | 1→1 traffic |
| Broadcast | 1→All in subnet |
| Multicast | 1→Many group |
| DNS | Name → IP |
| MAC | NIC hardware addr |
| Gateway | Exit point of subnet |
| Subnet Mask | Separates network/host bits |

> **Mnemonic:** **"Some Beautiful Networks Include Dedicated Super Guardians"**
(Safe‑mode, Backup, Networking, IP, DNS, Subnet, Gateway)

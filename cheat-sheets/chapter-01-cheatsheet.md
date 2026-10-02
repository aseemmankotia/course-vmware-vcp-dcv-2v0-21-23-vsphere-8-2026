# Chapter 1 Cheat Sheet — vSphere 8 Architecture & ESXi Installation

## Core Components
| Component | Role |
|---|---|
| ESXi | Bare-metal hypervisor host |
| vCenter Server | Centralized management (clusters, DRS, HA, vMotion) |
| vSphere Client (HTML5) | Manages vCenter inventory (multi-host) |
| ESXi Host Client | Manages ONE standalone host, no vCenter needed |
| DCUI | Console-level initial config (root pwd, mgmt network, restart agents) |

## Installation Methods
| Method | Automation Level | Key Detail |
|---|---|---|
| Interactive | Manual, per-host | Boot from ISO/USB, answer prompts |
| Scripted (Kickstart) | Fully automated | Uses ks.cfg via ks=usb/cdrom/nfs/http/ftp boot option |
| Auto Deploy | Fully automated, network boot | Needs DHCP (opt 66/67), TFTP, Auto Deploy server, PowerCLI rules |

## Auto Deploy Modes
| Mode | Local Storage Used? | Behavior if Auto Deploy server unreachable |
|---|---|---|
| Stateless | No | Fails to boot (fully dependent on server) |
| Stateless Caching | Yes (cache only) | Boots from local cache |
| Stateful Install | Yes (full install) | Boots normally like a standard install after first PXE boot |

## Boot Device Requirements (ESXi 8)
- Boot bank (USB/SD): 8 GB minimum
- ESX-OSData partition: SEPARATE persistent device, 32 GB min / 128 GB+ SSD-NVMe recommended
- Local disk install: single device can host both boot bank + OSData
- Boot from SAN: supported, requires HBA config in server BIOS

## Hardware Prerequisites
- CPU: 64-bit x86, 2+ cores, NX/XD bit enabled, CPU generation ≥ 2016 (older CPUs dropped in v8)
- RAM: 8 GB minimum
- Always verify via **VMware Compatibility Guide** (vmware.com/compatibility) — checks server model, CPU, storage controller, NIC

## Licensing
| Mode | Duration | Behavior at Expiry |
|---|---|---|
| Evaluation | 60 days, full features | Running VMs continue; new VMs can't power on until licensed |
| Assigned key | Per license terms | Feature set matches edition purchased |

- Per-CPU license cap: **32 cores**; CPUs >32 cores need additional license units

## Time Sync
| Protocol | Accuracy | Use Case |
|---|---|---|
| NTP | Milliseconds | Standard for all clusters, port 123/UDP |
| PTP | Microsecond/nanosecond | Hardware-assisted, latency-sensitive workloads |

- esxcli system ntp set --server=<server> / --enabled=true
- esxcli system ntp get (verify)
- Clock drift breaks: HA reference checks, vMotion, certificate validity

## Common Exam Traps
1. Thinking SD/USB alone can host OSData in ESXi 8 — it cannot; needs separate persistent storage ≥32 GB
2. Confusing Stateless (no local storage) with Stateless Caching (uses local cache)
3. Assuming DCUI can fully configure NTP/licensing — it cannot; use Host Client
4. Forgetting Auto Deploy Stateless still requires the Auto Deploy server reachable at EVERY boot
5. Believing evaluation mode has feature restrictions — it does not, only a 60-day timer

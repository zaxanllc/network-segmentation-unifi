# Network Segmentation – Real Infrastructure

This repository documents a real-world implementation of a secure, VLAN-segmented network architecture using UniFi gear.

## 🌐 WAN Topology

```
[ISP Dual Copper] → [Wattbox Rebooter] → [Bridged Modem] → [UDM (Core Router)]
```

- Wattbox monitors power and reboots modem if offline
- Bridged modem passes public IP to UDM (Core, VLAN 1)

## 🔀 VLANs Used

| VLAN | Subnet       | Purpose              | Notes                           |
|------|--------------|----------------------|----------------------------------|
| 1    | 10.0.1.0/24  | Core                 | UDM, Switches, Ubuntu Server     |
| 2    | 10.0.2.0/24  | Business Network     | Office PCs, Shop PC              |
| 3    | 10.0.3.0/24  | KidsNetwork          | Child devices (Wi-Fi only)       |
| 4    | 10.0.4.0/24  | VOIP                 | VOIP ATA                         |
| 5    | 10.0.5.0/24  | Security             | Cameras, DVR                     |
| 6    | 10.0.6.0/24  | IoT Devices          | Music Player, Wattbox, BRN       |
| 7    | 10.0.7.0/24  | Guest Network        | Open Wi-Fi, 2 APs only           |

## 📶 Wireless Layout

SSID-to-VLAN broadcast map across multiple APs:

- All APs: **Zaxanllc (VLAN 2)**, **MacKenna (VLAN 3)**, **IoT (VLAN 6)**
- Guest: 2 APs only, 2.4 GHz
- UID (WPA2 Enterprise): VLAN 1, Core (admin)

## 📎 Files Included

- `unifi-vlan-config.md`: VLAN breakdown with devices
- `firewall-rules.md`: Segmentation and routing rules
- `zero-trust-principles.md`: Isolation policy design
- `topology-diagram.png`: Visual map of the network

---
This configuration is live-tested and powering a segmented, redundant home + business hybrid network.

# Zero Trust Enforcement in Real-World VLAN Segmentation

## 🔐 Core Principles

- **Least Privilege by VLAN**: IoT, KidsNetwork, Guest, VOIP, and Security are all isolated by default.
- **Explicit Routing Only**: Only Core VLAN (admin) has access to other VLANs as needed (e.g., for backups, print servers).
- **Gateway Protection**: All non-core VLANs are denied access to the UDM interface (no HTTP/SSH access).
- **DNS Isolation**: All DNS routed through Pi-hole with VLAN-aware resolution.
- **Logging**: Firewall logs are exported for DPI analysis.

## 📶 SSID Rules

- Guest Wi-Fi (VLAN 7) cannot communicate with any local subnets.
- IoT and KidsNetwork denied inter-VLAN traffic; only allowed outbound to Internet or DNS.
- VOIP VLAN is isolated from all other VLANs except allowed SIP proxy (if configured).
- Core VLAN is only reachable by UID SSID or wired admin devices.

---
Zero Trust in this setup ensures that even if a guest, child, or compromised IoT device joins the network, they are **contained** by strict firewall rules and monitored traffic flows.

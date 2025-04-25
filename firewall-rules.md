
### 🔐 Firewall Rules Overview (Real Network)

This document summarizes the firewall rules active across the following key interfaces on your UniFi setup:
- LAN In / LAN Out
- Internet In / Internet Local / Internet Out
- IPv6 interfaces
- Domain and App filtering

---

## 🔧 LAN In Rules

| Action | Source            | Destination        | Purpose                                | Rule Name                   |
|--------|-------------------|--------------------|----------------------------------------|-----------------------------|
| Accept | Any               | Pi-hole DNS        | Allow DNS to Pi-hole                   | pihole                     |
| Accept | Guest             | Pi-hole DNS        | Allow Guest DNS to Pi-hole             | Allow Guest piehole        |
| Accept | IoT               | Pi-hole DNS        | Allow IoT DNS to Pi-hole               | Allow IOT pihole           |
| Accept | KidsNetwork       | Pi-hole DNS        | Allow KidsNetwork DNS to Pi-hole       | Allow KidsNetwork pihole   |
| Accept | Any               | RFC1918 (VLANs)    | Core VLAN access to other VLANs        | allow default to vlans     |
| Drop   | RFC1918           | RFC1918            | Block all inter-VLAN traffic           | block inter vlan and routing |
| Drop   | IoT               | IoT                | Isolate IoT traffic                    | Block IOT to All           |
| Drop   | Guest             | Guest              | Isolate Guest traffic                  | Block Guest to All         |
| Drop   | KidsNetwork       | KidsNetwork        | Isolate KidsNetwork traffic            | Block KidsNetwork to All   |
| Drop   | VOIP              | VOIP               | Isolate VOIP traffic                   | Block VOIP to All          |
| Accept | KidsNetwork       | 10.0.1.235         | Allow KidsNetwork to access Printer    | Printer to KidsNetwork     |

---

## 🌐 Internet In / Local Rules

| Action | Source            | Destination        | Protocol/Ports | Purpose                        | Rule Name                  |
|--------|-------------------|--------------------|----------------|--------------------------------|----------------------------|
| Drop   | 144.6.197.157     | 192.168.1.136      | Any            | IPS Deny inbound               | IPS Block 1                |
| Drop   | 144.6.197.157     | Any                | Any            | IPS Deny list global block     | IPS Deny List              |
| Accept | Any (established) | Any                | Any            | Allow related traffic          | Allow Established          |
| Drop   | Any               | Any                | Any            | Block invalid traffic          | Block Invalid              |
| Drop   | Any               | Any                | Any            | Block all other                | Block All Other            |

### 🛡️ Local Interface Blocking (to UDM)

| Action | Source     | Destination | Ports | Rule Name                      |
|--------|------------|-------------|-------|-------------------------------|
| Drop   | IoT        | Gateway     | HTTP/HTTPS/SSH | Block IOT to UDM         |
| Drop   | Guest      | Gateway     | HTTP/HTTPS/SSH | Block Guest to UDM       |
| Drop   | KidsNetwork| Gateway     | HTTP/HTTPS/SSH | Block KidsNetwork to UDM |

### 🔐 VPN/Access Services Allowed

- IPsec (UDP, ESP)
- L2TP (UDP 1701)
- OpenVPN Server (TCP 1194)
- UID VPN (UDP 10118)

---

## 🌐 Internet Out / LAN Out Rules

- Block outbound traffic to/from specific IPs via IPS deny list
- Allow outbound for all VLANs explicitly by subnet (10.0.x.0/24)

---

## 📡 IPv6 and Other Rules

- Allow Neighbor Solicitations/Advertisements
- Drop all invalid/unwanted IPv6 traffic
- Allow LAN v6 outbound traffic

---

## 🎯 App/Domain Filtering Rules

| Action | Type     | Target        | Rule Name           |
|--------|----------|----------------|---------------------|
| Block  | App      | WhatsApp       | Block WhatsApp      |
| Allow  | Domain   | s2.bl-1.com    | Allow s2.bl-1.com   |

---

### 🌐 WAN Architecture Note

- ISP connects to Wattbox (power monitor + auto-reboot failover)
- Wattbox feeds **modem**, which is **bridged** to UDM
- UDM (VLAN 1 - Core) serves as the **network gateway/router** to the entire internal VLAN system
- Dual copper ISP feed for redundancy

This document will be exported to your GitHub `network-segmentation-unifi` project as `firewall-rules.md` and updated to match your current UniFi deployment.

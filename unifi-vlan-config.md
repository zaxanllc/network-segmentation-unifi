# UniFi VLAN Configuration (Live)

| VLAN ID | Name            | Subnet         | Purpose                          | Example Devices               |
|---------|------------------|----------------|----------------------------------|-------------------------------|
| 1       | Core             | 10.0.1.0/24    | UDM, switches, Ubuntu server     | Dream Machine, USW-24, Server |
| 2       | Business Network | 10.0.2.0/24    | Office and shop PCs              | Office-2023, Shop PC          |
| 3       | KidsNetwork      | 10.0.3.0/24    | Kids’ Wi-Fi devices              | Tablets, phones               |
| 4       | VOIP             | 10.0.4.0/24    | Voice devices                    | OBi200 ATA                    |
| 5       | Security         | 10.0.5.0/24    | Surveillance and DVR             | Wyze Cam, DVR                 |
| 6       | IoT              | 10.0.6.0/24    | Smart devices + Wattbox          | Music Player, Wattbox, BRN    |
| 7       | Guest            | 10.0.7.0/24    | Open Wi-Fi for guests            | Phones/laptops (2.4 GHz only) |

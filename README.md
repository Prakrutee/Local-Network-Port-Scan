# Local Network Port Scanning with Nmap and Wireshark

## Objective
Using nmap to discover open ports and services in the local network. Understanding potential security risks and practice recon techniques, and using Wireshark to capture and analyze packet-level network activity.

---

## Tools Used
- Nmap v7.97 (for port scanning, host discovery) 
- Windows 10 Command Prompt (Admin mode)
- Wireshark (for packet capture and network traffic analysis)

---

## Task Steps

### 1. Find Local IP Range
- Used `ipconfig` to determine local IP
- IP Info:
- IPv4: `192.168.0.103`
- Gateway: `192.168.0.1`
- Subnet: `255.255.255.0` → CIDR `/24`

### 2. Run Nmap TCP SYN Scan
```bash
nmap -sS 192.168.0.0/24 -oN local_scan.txt

Saved scan results in local_scan.txt

### 3. Capture Packets using Wireshark
Ran Nmap while capturing packets in Wireshark
Observed:
- ARP requests
- TCP SYN (port scan attempts)
- SYN-ACK (open ports) or RST (closed ports)
- Saved as: scan_capture.pcapng

## Wireshark Filters Used

| Filter                                      | Purpose                            |
| ------------------------------------------- | ---------------------------------- |
| `tcp.flags.syn == 1 and tcp.flags.ack == 0` | Shows SYN packets (Nmap scanning)  |
| `tcp.flags.syn == 1 and tcp.flags.ack == 1` | Shows SYN-ACK replies (open ports) |
| `tcp.flags.reset == 1`                      | Shows RST replies (closed ports)   |
| `arp`                                       | Shows ARP IP → MAC discovery       |


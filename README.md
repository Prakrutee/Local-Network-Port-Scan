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
''' bash
nmap -sS 192.168.0.0/24 -oN local_scan.txt

This performs a TCP SYN scan on all devices in the local network.

### 3. Capture Packets using Wireshark
While the Nmap scan was running, Wireshark was used to capture the packet exchange between the scanner and local devices.
Observed:
- ARP Requests – for resolving IP addresses to MAC addresses
- TCP SYN Packets – used by Nmap to scan ports
- SYN-ACK Packets – received from open ports
- RST Packets – from closed ports rejecting the connection

The capture was saved as: scan_capture.pcapng

## Wireshark Filters Used
Filter	Purpose
tcp.flags.syn == 1 and tcp.flags.ack == 0	Displays SYN packets (scanning)
tcp.flags.syn == 1 and tcp.flags.ack == 1	Displays SYN-ACK replies (open)
tcp.flags.reset == 1	Displays RST packets (closed)
arp	Displays ARP requests and replies

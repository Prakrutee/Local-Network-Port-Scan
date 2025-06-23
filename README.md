# Local Network Port Scanning with Nmap

## Objective
Use `nmap` to discover open ports and services in the local network. Understand potential security risks and practice recon techniques.

---

## Tools Used
- Nmap v7.97
- Windows 10 Command Prompt (Admin mode)
- Optional: Wireshark (for packet analysis)

---

## Scanning Details

### IP Info:
- IPv4: `192.168.0.103`
- Gateway: `192.168.0.1`
- Subnet: `255.255.255.0` → CIDR `/24`

### Scan Command Used:
```bash
nmap -sS 192.168.0.0/24 -oN local_scan.txt

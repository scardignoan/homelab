# homelab
Documentation of current homelab configuration.


# Cybersecurity Home Lab

A personal homelab built around a Proxmox VE hypervisor, designed to simulate 
a segmented enterprise-style network for practicing offensive security, defensive 
monitoring, and self-hosted infrastructure management.

## Hardware

| Device | Role |
|--------|------|
| Mini PC (Proxmox node) | Hypervisor — 16GB RAM, 1TB SSD |
| Mini PC (daily driver) | Fedora Linux management workstation |
| 10" rack | Physical enclosure with managed switch and patch panel |

## Network Architecture
ISP
│
Router
│
WAN bridge (Proxmox)
│
pfSense VM ── firewall / router / DHCP / DNS
│
LAN bridge
├── Management VM (Ubuntu 24.04)
├── Attacker VM (Kali Linux)
└── Target VM (Metasploitable 2)



Remote access managed via **Tailscale VPN** — no services exposed to the public internet.

## Virtual Machines

| Role | OS | Purpose |
|------|----|---------|
| Firewall | pfSense | Network segmentation, DHCP, DNS |
| Management | Ubuntu 24.04 | Lab administration |
| Attacker | Kali Linux | Offensive security practice |
| Target | Metasploitable 2 | Intentionally vulnerable target |

## Security Lab Work

### Network Reconnaissance
- Performed `nmap` service scans against Metasploitable 2, identifying vulnerable 
  services including an open backdoor shell, unauthenticated VNC, and a 
  misconfigured FTP daemon

### Exploitation
- Exploited a backdoor service to obtain an unauthenticated root shell via netcat
- Identified VNC running with no authentication as a critical misconfiguration

### Planned
- Wazuh SIEM for log aggregation and alert monitoring across lab VMs
- Windows Server with Active Directory to simulate a corporate domain environment
- VLAN segmentation to isolate attacker/target traffic from management network

## Self-Hosted Services

- **Media automation stack** — Sonarr, Radarr, Prowlarr, SABnzbd, and Jellyfin 
  running via Docker Compose on a dedicated VM with isolated storage
- **Self-hosted password manager** — Vaultwarden, accessible only over VPN

# 🔐 pfSense SOC Homelab

![SOC Homelab Topology](screenshots/Topology.png)

## Purpose

This project sets up a segmented network using pfSense to support my SOC-focused homelab.

The goal is to create a realistic environment where I can:

- Monitor traffic
- Generate logs
- Practice detection and investigation
- Simulate internal and external activity

This serves as the foundation for future SIEM and IDS projects.

---

## Overview

pfSense is used as the firewall and gateway between three networks:

- WAN (external / attacker side)
- LAN (internal systems)
- DMZ (monitored traffic segment)

The dashboard confirms interface status, gateway health, and core services like DHCP and DNS.

![pfSense Dashboard](screenshots/pfsense-dashboard.png)

---

## Interface Assignments

Each pfSense interface is mapped to a specific network segment.

![Interface Assignments](screenshots/pfsense-interface-assignments.png)

### Network Segments

- **WAN** – Simulated external network (Kali attacker + internet)
- **LAN** – Internal systems (Windows, Ubuntu, Wazuh, Security Onion management)
- **DMZ** – Monitoring interface for Security Onion

pfSense handles:

- Default gateway routing
- DHCP for internal devices
- DNS resolution
- NAT for outbound internet access
- Firewall rules between segments

---

## LAN Configuration

The LAN interface uses a static IPv4 address to act as the default gateway for internal machines.

![LAN Interface Configuration](screenshots/pfsense-lan-interface.png)

Outbound traffic from LAN is allowed, while inbound WAN traffic is blocked by default.

This setup allows me to safely simulate:

- External scans
- Normal user traffic
- Restricted communication between zones

---

## DHCP & DNS

pfSense provides DHCP to LAN clients:

![DHCP Server Configuration](screenshots/pfsense-dhcp-server-lan.png)

DNS is handled by the built-in resolver (Unbound):

![DNS Resolver Configuration](screenshots/dns-resolver.png)

This ensures that:

- All DNS queries pass through the firewall
- DNS activity can later be analyzed in SIEM tools

---

## Connectivity Verification

Internal clients were tested to confirm proper configuration.

![Client Connectivity Test](screenshots/windows10pro-ping-google.png)

Validation steps included:

- Confirming DHCP lease assignment
- Verifying default gateway
- Testing outbound internet access
- Confirming DNS resolution

---

## Why This Matters for SOC Work

This environment generates useful telemetry such as:

- Firewall logs
- DNS queries
- DHCP lease data
- Internal-to-external traffic flows

These logs will be used in future projects involving:

- Wazuh SIEM integration
- Security Onion alert analysis
- Detection testing
- Incident investigation scenarios

---

## Current Status

- Network segmentation implemented
- Internet access verified
- DNS functioning correctly
- Environment ready for SIEM and IDS integration

This project serves as the network foundation for the rest of my SOC homelab.

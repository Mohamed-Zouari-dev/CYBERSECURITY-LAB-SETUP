<img width="1917" height="976" alt="image" src="https://github.com/user-attachments/assets/7dac444e-a01a-4348-ab67-5e5f766ff850" /># Cybersecurity Lab Environment Setup
### VirtualBox & Kali Linux | Project Module 1

## 1. Project Overview

This project focuses on designing and deploying a virtual cybersecurity laboratory using Oracle VirtualBox and Kali Linux on a Windows 11 host machine.

The primary objective is to establish a controlled and isolated environment for cybersecurity learning, network analysis, and authorized security testing.

By leveraging virtualization and a dedicated NAT Network, the laboratory provides a foundation for experimenting with cybersecurity tools, conducting network reconnaissance, performing vulnerability assessments, and eventually integrating additional virtual machines as testing targets.

## 2. Objectives

The main objectives of this project were:

- Install and configure Oracle VirtualBox.
- Deploy Kali Linux as a virtual machine.
- Establish a dedicated NAT Network using the `10.0.0.0/24` subnet.
- Configure a static IPv4 address for Kali Linux.
- Establish internet connectivity and DNS resolution.
- Configure virtual machine integration features.
- Enable shared folders for host-to-VM file exchange.
- Create clean virtual machine snapshots for recovery.
- Prepare an extensible environment for future cybersecurity exercises.

## 3. Lab Architecture

The laboratory consists of a Windows 11 host machine running VirtualBox, with Kali Linux operating as a virtual machine.

A dedicated NAT Network allows virtual machines connected to the same network to communicate with one another while retaining internet connectivity.

### Infrastructure Configuration

| Component | Configuration |
|---|---|
| Host OS | Windows 11 |
| Hypervisor | Oracle VirtualBox 7.2 |
| Security VM | Kali Linux 2026.2 |
| VM Memory | 2048 MB |
| Network Mode | NAT Network |
| Network Name | NatNetwork |
| Network Subnet | 10.0.0.0/24 |
| Kali IP | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |
| Additional Target | Metasploitable (planned configuration: 10.0.0.3) |

### Network Architecture

The laboratory uses the following addressing scheme:

- `10.0.0.1` – Default gateway.
- `10.0.0.2` – Kali Linux virtual machine.
- `10.0.0.3` – Planned Metasploitable target machine.

This architecture provides a foundation for building a multi-machine cybersecurity laboratory.


## 4. Implementation

### Step 1 – Installing the Prerequisites

Installed 7-Zip to extract the Kali Linux virtual machine archive and Oracle VirtualBox to provide the virtualization infrastructure.

### Step 2 – Configuring the Virtual Network

Created a dedicated NAT Network in VirtualBox with the following parameters:

- Network name: NatNetwork
- IPv4 prefix: 10.0.0.0/24
- DHCP: Enabled
- IPv6: Disabled

This network serves as the communication infrastructure for the laboratory.

### Step 3 – Deploying Kali Linux

Downloaded the official Kali Linux VirtualBox image and imported it into VirtualBox.

Configured the virtual machine with:
- 2048 MB of RAM.
- A network adapter attached to the custom NatNetwork.
- Intel PRO/1000 MT Desktop network adapter.

### Step 4 – Configuring Network Connectivity

Configured Kali Linux with a static IPv4 configuration to ensure consistent network addressing.

| Parameter | Value |
|---|---|
| IPv4 Address | 10.0.0.2 |
| Netmask | 255.255.255.0 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |
<img width="1917" height="976" alt="image" src="https://github.com/user-attachments/assets/83f17a9f-e0f7-469d-8bb0-965573a23182" />


### Step 5 – Creating a Recovery Snapshot

Created a clean virtual machine snapshot named:

`Kali - Network Setup`

This provides a recovery point that can be restored whenever an experiment or configuration change affects the virtual machine.

## 5. Network Verification

After completing the configuration, several connectivity checks were performed.

| Test | Command |
|---|---|
| Verify IP configuration | `ip a` |
| Test gateway connectivity | `ping 10.0.0.1` |
| Test internet connectivity | `ping 8.8.8.8` |
| Verify DNS resolution | `nslookup networkwalks.com` |
| Verify Nmap installation | `nmap --version` |
| Test target connectivity | `ping 10.0.0.3` |

These checks help validate the network configuration, internet access, DNS resolution, and readiness for future laboratory exercises.

## 6. Troubleshooting

### Issue: Kali Linux Network Connectivity Failure

Following the initial deployment, Kali Linux did not receive the expected network configuration and could not communicate with the default gateway.

**Diagnostic process:**

Used the following commands to investigate the problem:

- `ip a`
- `ping -c 4 10.0.0.1`

**Resolution:**

1. Verified that the VirtualBox network adapter was attached to the correct NAT Network.
2. Opened the Kali Linux network connection settings.
3. Selected the Wired connection.
4. Changed the IPv4 configuration from Automatic (DHCP) to Manual.
5. Applied the static IP address, subnet mask, gateway, and DNS configuration.

This resolved the network configuration issue and established the intended addressing scheme.

## 7. Technical Knowledge Acquired

Throughout this project, I developed practical knowledge in several areas:

**Virtualization**
- Understanding virtual machines and hypervisor configuration.
- Deploying and managing virtual operating systems.
- Using snapshots for recovery and environment management.

**Networking**
- Understanding the difference between NAT and NAT Network.
- Configuring private IPv4 networks.
- Working with subnet masks, gateways, and DNS.
- Troubleshooting virtual network connectivity.

**Linux Administration**
- Configuring network interfaces.
- Using terminal commands for network diagnostics.
- Understanding basic Linux network management.

**Cybersecurity Lab Management**
- Preparing controlled environments for security experimentation.
- Understanding the importance of network isolation.
- Establishing a reproducible testing environment.

**Technical Documentation**
- Documenting infrastructure configurations.
- Recording troubleshooting procedures.
- Maintaining a reproducible laboratory setup.


## 8. Conclusion

This project established the infrastructure required for a practical cybersecurity learning environment.

Beyond installing and configuring Kali Linux, it provided hands-on experience with virtualization, network architecture, Linux administration, IP configuration, and troubleshooting.

The laboratory will serve as a foundation for progressively more advanced cybersecurity exercises and practical security projects.

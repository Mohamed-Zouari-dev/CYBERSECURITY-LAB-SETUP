<img width="1917" height="976" alt="image" src="https://github.com/user-attachments/assets/7dac444e-a01a-4348-ab67-5e5f766ff850" /># Cybersecurity Lab # Cybersecurity Lab Environment Setup
### Week 1 – Project Module 1 | Networkwalks Cybersecurity Program

## 1. Project Overview

This project involves building a virtual cybersecurity laboratory using Oracle VirtualBox and Kali Linux on a Windows 11 host machine.

The objective is to establish a dedicated virtual environment for cybersecurity learning, network configuration, and authorized security testing.

The laboratory uses a custom NAT Network to provide communication between virtual machines while maintaining internet connectivity. It is designed to be expandable, allowing additional virtual machines to be introduced for future practical exercises.

## 2. Project Objectives

- Install and configure Oracle VirtualBox.
- Deploy Kali Linux as a virtual machine.
- Create a dedicated NAT Network using the `10.0.0.0/24` subnet.
- Configure a static IPv4 address for Kali Linux.
- Establish internet connectivity.
- Enable clipboard sharing and drag-and-drop functionality.
- Configure a shared folder between the host and virtual machine.
- Create a clean virtual machine snapshot.
- Document the configuration process and troubleshooting experience.

## 3. Lab Architecture

The environment consists of a Windows 11 host machine running Oracle VirtualBox, with Kali Linux deployed as a virtual machine.

The NAT Network provides a dedicated virtual network for communication between laboratory machines and internet connectivity.

### Infrastructure Configuration

| Component | Configuration |
|---|---|
| Host OS | Windows 11 |
| Hypervisor | Oracle VirtualBox 7.2 |
| Security VM | Kali Linux 2026.2 |
| Host RAM | 8 GB |
| Processor | Intel Core i5 |
| Kali VM RAM | 2048 MB |
| Network Mode | NAT Network |
| Network Name | NatNetwork |
| Network Subnet | 10.0.0.0/24 |
| Kali IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

### Network Topology

The laboratory uses the following addressing scheme:

- Default gateway: 10.0.0.1
- Kali Linux: 10.0.0.2
- Future target VM: 10.0.0.3

The additional target machine is planned for a future extension of the laboratory.

## 4. Implementation Procedure

### Step 1 – Install 7-Zip

Installed 7-Zip to extract the Kali Linux virtual machine archive.

### Step 2 – Install Oracle VirtualBox

Installed Oracle VirtualBox to provide the virtualization environment for running and managing virtual machines.

### Step 3 – Configure the NAT Network

Created a dedicated NAT Network through VirtualBox network settings.

Configuration:

| Parameter | Value |
|---|---|
| Network Name | NatNetwork |
| IPv4 Prefix | 10.0.0.0/24 |
| DHCP | Enabled |
| IPv6 | Disabled |

This configuration provides the network infrastructure for the laboratory.

**Screenshot:** VirtualBox NAT Network configuration.

### Step 4 – Import Kali Linux

Downloaded the official Kali Linux VirtualBox image and imported it into VirtualBox.

Configured the virtual machine with:

- Memory allocation: 2048 MB.
- Network adapter: Adapter 1.
- Attached to: NAT Network.
- Network: NatNetwork.
- Adapter type: Intel PRO/1000 MT Desktop.

**Screenshot:** Kali Linux virtual machine running in VirtualBox.

### Step 5 – Configure Kali Linux Networking

Configured a static IPv4 address to ensure consistent network addressing.

| Parameter | Value |
|---|---|
| IPv4 Address | 10.0.0.2 |
| Subnet Mask | 255.255.255.0 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |

**Screenshot:** Kali Linux IPv4 configuration.

### Step 6 – Configure Virtual Machine Integration

The assignment requires the following VirtualBox integration features:

- Shared clipboard.
- Drag-and-drop functionality.
- Shared folders.

The designated shared folder is `/downloads` on the host machine.

**Verification checklist:**

- [ ] Shared clipboard enabled.
- [ ] Drag-and-drop enabled.
- [ ] Host `/downloads` folder configured as a shared folder.
- [ ] Shared folder accessible from Kali Linux.

### Step 7 – Create a Virtual Machine Snapshot

Created a clean snapshot of the Kali Linux virtual machine named:

`Clean Kali - Network Setup`

The snapshot provides a recovery point that can be restored if subsequent experiments or configuration changes affect the environment.

**Screenshot:** VirtualBox snapshot configuration.

## 5. Network Verification

The following commands are used to validate the laboratory configuration.

| Test | Command | Expected Result |
|---|---|---|
| IP configuration | `ip a` | Configured static IP displayed |
| Gateway connectivity | `ping 10.0.0.1` | Successful replies |
| Internet connectivity | `ping 8.8.8.8` | Successful replies |
| DNS resolution | `nslookup networkwalks.com` | Domain resolves |
| Nmap installation | `nmap --version` | Version information displayed |
| Snapshot recovery | Restore snapshot | Previous configuration restored |

These checks provide a basic validation of network configuration and virtual machine readiness.

## 6. Problems Encountered and Troubleshooting

### Problem: Kali Linux Network Connectivity Failure

After importing Kali Linux and connecting it to the custom NAT Network, the virtual machine did not initially receive the expected network configuration.

As a result, communication with the default gateway and internet connectivity were unavailable.

**Diagnosis**

Used the following commands to investigate the issue:

```bash
ip a
ping -c 4 10.0.0.1
```

The network interface did not have the expected laboratory IP configuration, and communication with the gateway failed.

**Solution**

1. Checked VirtualBox Settings → Network.
2. Confirmed that Adapter 1 was attached to the correct NAT Network.
3. Opened the Kali Linux network connection settings.
4. Selected Wired connection 1.
5. Opened IPv4 Settings.
6. Changed the configuration method from Automatic (DHCP) to Manual.
7. Configured the required IP address, subnet mask, gateway and DNS server.

After applying the configuration, connectivity was tested again.

## 7. Technical Knowledge Acquired

### Virtualization
- Deploying and managing virtual machines.
- Understanding hypervisor configuration.
- Using snapshots for environment recovery.

### Networking
- Understanding NAT and NAT Network configurations.
- Configuring IPv4 addresses and subnet masks.
- Working with gateways and DNS.
- Troubleshooting network connectivity.

### Linux Administration
- Managing network interfaces.
- Configuring static IP addressing.
- Using command-line networking utilities.

### Cybersecurity Lab Management
- Building controlled testing environments.
- Preparing infrastructure for security exercises.
- Understanding the importance of authorized testing and isolation.

## 8. Future Improvements

This initial laboratory configuration provides a foundation for future practical exercises.

Planned improvements include:

- Integrating additional virtual machines.
- Adding vulnerable target environments.
- Practicing network reconnaissance and security assessment within the laboratory.
- Exploring packet analysis and network monitoring.
- Documenting future security exercises and findings.

## 9. Tools and Resources

- **7-Zip:** https://www.7-zip.org/
- **Oracle VirtualBox:** https://www.virtualbox.org/
- **Kali Linux:** https://www.kali.org/

## 10. Conclusion

This project established the foundation of a virtual cybersecurity laboratory using VirtualBox and Kali Linux.

Through this implementation, I gained practical experience with virtualization, network configuration, Linux administration, and troubleshooting.

The laboratory will serve as a starting point for future cybersecurity exercises and the development of practical technical skills.

---

**Project:** Week 1 – Project Module 1  
**Program:** Networkwalks Cybersecurity Program  
**Author:** Mohamed ZOUARI  

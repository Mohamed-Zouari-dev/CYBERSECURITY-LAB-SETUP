<img width="1917" height="976" alt="image" src="https://github.com/user-attachments/assets/e8b624e0-8eeb-40fd-a385-d8b68778a246" />
<img width="1917" height="997" alt="image" src="https://github.com/user-attachments/assets/62749751-9f53-472b-adef-44ab6e943a8a" />
<img width="1031" height="858" alt="image" src="https://github.com/user-attachments/assets/039f99fd-db9c-42b9-8524-0964f1783ce9" />

# Cybersecurity Lab Environment Setup

A practical cybersecurity lab built with Oracle VirtualBox, Kali Linux, and Windows 10. The project focuses on creating an isolated virtual network, configuring communication between virtual machines, and learning network traffic analysis with Wireshark.

## Project Objectives

- Build a virtual cybersecurity lab using VirtualBox.
- Configure a NAT Network shared by multiple virtual machines.
- Establish communication between Kali Linux and Windows 10.
- Verify connectivity between virtual machines and internet access.
- Analyze network traffic using Wireshark.
- Understand how HTTP communicates and why unencrypted authentication is a security risk.

## Lab Environment

| Component | Configuration |
|---|---|
| Virtualization | Oracle VirtualBox |
| Network type | NAT Network |
| Network subnet | `10.0.0.0/24` |
| Kali Linux | `10.0.0.2/24` |
| Windows 10 | `10.0.0.10/24` |
| Default gateway | `10.0.0.1` |
| DNS | `8.8.8.8` |

*The Windows 10 configuration is the additional lab extension described in the project guide.*

---

## Part 1 — Kali Linux Virtual Machine

The initial lab consists of installing Kali Linux in VirtualBox and connecting it to a dedicated NAT Network.

Main configuration tasks:

1. Install Oracle VirtualBox.
2. Create a NAT Network with the required subnet.
3. Import and configure the Kali Linux virtual machine.
4. Configure the Kali network interface.
5. Verify network connectivity and internet access.
6. Create a clean VM snapshot.

**Kali Linux network configuration**

- Network: VirtualBox NAT Network
- IP address: `10.0.0.2/24`
- Gateway: `10.0.0.1`
- DNS: `8.8.8.8`

## Part 2 — Windows 10 Lab Extension

The second lab extends the environment by introducing a Windows 10 virtual machine connected to the same NAT Network as Kali Linux.

### Requirements

- VirtualBox already installed.
- At least 40 GB of available disk space.
- At least 4 GB of RAM available for the VM.
- Kali Linux already configured on the NAT Network.

### VM configuration

| Setting | Value |
|---|---|
| VM name | `Windows10-Lab` |
| Operating system | Windows 10 (64-bit) |
| Memory | 4096 MB |
| Virtual disk | VDI, dynamically allocated |
| Disk capacity | At least 40 GB |
| Network adapter | NAT Network |
| Network | Same NAT Network as Kali |

### Network configuration

Configure the Windows 10 network adapter with:

- IP address: `10.0.0.10`
- Subnet mask: `255.255.255.0`
- Default gateway: `10.0.0.1`
- Preferred DNS: `8.8.8.8`

### Connectivity verification

From Windows Command Prompt:

```cmd
ping 10.0.0.2
ping 8.8.8.8
```

From Kali Linux:

```bash
ping 10.0.0.10
```

These tests are intended to verify communication between the two virtual machines and internet connectivity.

---

## Part 3 — Lab 1: Wireshark Traffic Analysis

This exercise focuses on inspecting captured TCP traffic and identifying the details of an HTTP login exchange.

### 1. Finding the relevant TCP stream

Start by applying the following Wireshark display filter:

```text
tcp
```

Select the first packet, right-click it, and choose:

`Follow → TCP Stream`

Navigate through the available streams using the arrows in the Follow TCP Stream window.

The relevant stream is **Stream 2**, which contains a staff portal login page.

The other streams contain normal page traffic.

### 2. Identifying the login protocol

Apply:

```text
tcp.stream eq 2
```

The login request uses **HTTP**.

This means the login exchange is transmitted without HTTPS transport encryption.

### 3. HTTP version

The login request begins with:

```http
POST /login HTTP/1.1
```

Identified version: **HTTP/1.1**

### 4. Browser identification

The request contains a User-Agent header identifying:

- Browser: Google Chrome
- Platform: Windows 10 (64-bit)

### 5. Hostname

The HTTP Host header identifies the destination as:

```text
portal.company.local
```

### 6. Web server identification

The server response contains:

```text
Server: Apache/2.4.57 (Ubuntu)
```

Identified web server: **Apache**

### 7. HTTP request method

The login submission uses:

```http
POST /login
```

Identified method: **POST**

The login page itself was initially requested using GET.

### 8. Number of login attempts

Apply this Wireshark filter:

```text
http.request.method == "POST"
```

Two matching POST requests are present in the exercise capture.

Identified login attempts: **2**

### 9. Authentication analysis

Both requests use the same username.

The first authentication attempt receives an unsuccessful login response. The second receives a successful response.

**Security note:** The captured authentication values are intentionally omitted from this public report. The important finding is that the credentials were visible in the HTTP traffic because the authentication exchange was not protected by HTTPS.

### 10. Main security observation

The capture demonstrates the risk of transmitting authentication data over unencrypted HTTP.

An observer with access to the relevant network traffic could inspect the HTTP request and response contents.

**Recommended security improvements:**

- Enforce HTTPS for authentication pages.
- Redirect HTTP requests to HTTPS.
- Use valid TLS certificates.
- Enable HSTS where appropriate.
- Avoid transmitting sensitive authentication data over unencrypted connections.

---

## Tools Used

- Oracle VirtualBox
- Kali Linux
- Windows 10
- Wireshark
- TCP/IP networking
- HTTP protocol analysis

## Learning Outcomes

Through these exercises, the project covers:

- Virtual machine deployment and configuration.
- NAT Network configuration.
- Static IPv4 addressing.
- Communication between different operating systems.
- Basic connectivity troubleshooting.
- TCP stream inspection.
- HTTP request and response analysis.
- Identification of browser and web server information.
- Understanding the security implications of unencrypted authentication.

## Future Improvements

- Add more virtual machines to expand the lab.
- Introduce additional network services.
- Practice packet analysis with different protocols.
- Explore network monitoring and detection.
- Document further security exercises in the isolated lab environment.

## Disclaimer

This project is intended for educational purposes and authorized cybersecurity practice only. All testing and analysis should be performed on systems you own or have explicit permission to assess.

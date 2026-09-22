# Suricata IDS/IPS Network Security Lab

A virtualized network security laboratory designed to analyze network traffic, detect suspicious patterns, and demonstrate the difference between intrusion detection and intrusion prevention using Wireshark and Suricata.

## Objectives

The main objectives of this project are:

- Build an isolated virtual network for security testing
- Capture and analyze network traffic with Wireshark
- Deploy Suricata as an Intrusion Detection System (IDS)
- Analyze network events and suspicious traffic patterns
- Create and test custom Suricata rules
- Deploy Suricata as an Intrusion Prevention System (IPS)
- Demonstrate the difference between detection and active prevention
- Document tests, alerts, packet captures, and results

## Lab Environment

### Host System

- Fedora Linux 43 KDE
- Oracle VirtualBox 7.2.16
- AMD Ryzen 5 5500U
- Hardware virtualization: AMD-V

## Virtual Machines

The laboratory uses two virtual machines.

### Kali Linux

**Purpose**

- Traffic generation
- Network testing
- Packet analysis
- Controlled security testing

**Resources**

- 4 GB RAM
- 2 vCPUs
- VirtualBox virtual disk

**Network interfaces**

- `eth0` — VirtualBox NAT
- `eth1` — VirtualBox Internal Network (`LAB-SEC`)

Current NAT address:

```text
10.0.2.15/24
```

Planned laboratory address:

```text
10.10.10.10/24
```

### Ubuntu Server

**Planned purpose**

- Protected server
- Nginx web service
- Suricata IDS/IPS
- Security event logging
- Traffic inspection and prevention

Planned laboratory address:

```text
10.10.10.20/24
```

## Network Architecture

Each virtual machine uses two network adapters.

```text
                         Internet
                            |
                      VirtualBox NAT
                            |
                +-----------+-----------+
                |                       |
             Kali VM               Ubuntu Server
             eth0 NAT               NAT interface
                |                       |
             eth1                    LAB interface
                |                       |
                +------ LAB-SEC --------+
                       10.10.10.0/24
```

### LAB-SEC

`LAB-SEC` is configured as a VirtualBox **Internal Network**.

The security testing traffic remains isolated from the host's physical network.

The NAT adapters are used separately for:

- System updates
- Package installation
- Internet access

The Internal Network is used for:

- Packet capture
- IDS testing
- IPS testing
- Controlled traffic generation
- Communication between the laboratory VMs

Bridged networking is intentionally avoided for security testing.

## Planned Traffic Flow

```text
Kali Linux
10.10.10.10
     |
     | Test Traffic
     |
     v
LAB-SEC
     |
     v
Ubuntu Server
10.10.10.20
     |
     +-- Nginx
     |
     +-- Suricata
```

## IDS Scenario

Suricata will initially operate as an Intrusion Detection System.

The expected workflow is:

```text
Traffic generated
       |
       v
Suricata inspection
       |
       v
Suspicious pattern detected
       |
       v
Alert generated
       |
       v
Traffic continues
```

In IDS mode, Suricata observes and reports suspicious activity without actively blocking the connection.

## IPS Scenario

After the IDS tests, Suricata will be configured as an Intrusion Prevention System.

The same controlled traffic will be generated again.

Expected behavior:

```text
Traffic generated
       |
       v
Suricata inspection
       |
       v
Suspicious pattern detected
       |
       +--> Alert generated
       |
       v
Traffic blocked
```

This allows a practical comparison between:

```text
IDS
Detect -> Alert -> Allow

IPS
Detect -> Alert -> Block
```

## Tools

The laboratory uses or will use:

- Fedora Linux
- VirtualBox
- Kali Linux
- Ubuntu Server
- Wireshark
- Suricata
- Nginx
- Git
- GitHub
- Linux networking tools

## Repository Structure

```text
suricata-ids-ips-lab/
|
├── README.md
|
├── docs/
│   ├── architecture.md
│   ├── network.md
│   ├── ids-tests.md
│   └── ips-tests.md
|
├── rules/
│   └── local.rules
|
└── screenshots/
    ├── virtualbox/
    ├── wireshark/
    ├── suricata/
    └── tests/
```

## Project Progress

- [x] Fedora 43 host installed and updated
- [x] Hardware virtualization verified
- [x] VirtualBox installed
- [x] VirtualBox kernel module configured
- [x] Kali Linux VM deployed
- [x] Kali VM configured with 4 GB RAM and 2 vCPUs
- [x] NAT adapter configured
- [x] Internal `LAB-SEC` network created
- [x] Kali network interfaces identified
- [ ] Configure static IPv4 address on Kali `eth1`
- [ ] Deploy Ubuntu Server VM
- [ ] Configure Ubuntu `LAB-SEC` interface
- [ ] Validate communication between both VMs
- [ ] Capture baseline traffic with Wireshark
- [ ] Install and configure Suricata
- [ ] Perform IDS detection tests
- [ ] Create custom Suricata rules
- [ ] Configure IPS mode
- [ ] Perform IPS prevention tests
- [ ] Compare IDS and IPS behavior
- [ ] Document results and evidence

## Security and Isolation

All security tests in this project are performed in a controlled and isolated virtual environment.

The `LAB-SEC` network is separated from the physical local network to prevent laboratory traffic from reaching unrelated systems.

## Disclaimer

This project is intended exclusively for educational purposes and authorized security testing.

All traffic generation, detection, and prevention experiments are performed inside an isolated virtual laboratory.

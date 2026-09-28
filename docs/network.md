## Kali Linux

| Interface | Purpose | Address |
|---|---|---|
| eth0 | Internet access via NAT | 10.0.2.15/24 |
| eth1 | Internal LAB-SEC network | 10.10.10.10/24 |

The LAB-SEC interface has no default gateway or DNS configured.
This prevents laboratory traffic from being used as the VM's Internet route.

## Network Topology

| VM | Interface | Purpose | Address |
|---|---|---|---|
| Kali Linux | eth0 | NAT / Internet | 10.0.2.15/24 |
| Kali Linux | eth1 | LAB-SEC | 10.10.10.10/24 |
| Ubuntu Server | enp0s3 | NAT / Internet | 10.0.2.15/24 |
| Ubuntu Server | enp0s8 | LAB-SEC | 10.10.10.20/24 |

`LAB-SEC` is a VirtualBox Internal Network used exclusively for laboratory traffic.

## Kali Linux

| Interface | Purpose | Address |
|---|---|---|
| eth0 | Internet access via NAT | 10.0.2.15/24 |
| eth1 | Internal LAB-SEC network | 10.10.10.10/24 |

The LAB-SEC interface has no default gateway or DNS configured.
This prevents laboratory traffic from being used as the VM's Internet route.

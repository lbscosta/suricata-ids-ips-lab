## ICMP Detection

Rule:

```text
alert icmp 10.10.10.10 any -> 10.10.10.20 any (msg:"LAB ICMP detected from Kali"; sid:1000001; rev:1;)

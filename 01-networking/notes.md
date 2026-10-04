# Chapter 1 notes

## Lesson 1: Test01 network settings

| Setting | Value |
| --- | --- |
| IPv4 address | 172.25.162.128 |
| Subnet mask | 255.255.240.0 |
| Default gateway | 172.25.160.1 |
| DNS server | 172.25.160.1 |
| DHCP server | 172.25.160.1 |

## Test ladder

| Step | Command | Result |
| --- | --- | --- |
| 1 | ping (gateway) | Failed |
| 2 | ping 1.1.1.1 | Succeeded   |
| 3 | Resolve-DnsName github.com | Succeeded |

## HV01

Shows the same IP address as the DHCP Server on Test01

IPAddress         : 172.25.160.1 

Step 1 failed most likely due to the firewall blocking ping requests.
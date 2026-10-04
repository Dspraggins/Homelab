# Chapter 1: Networking - lab notes

These are my working notes for the networking chapter of my homelab. Each lesson has a goal, what I did, what I recorded, and what I learned from it.

## The environment

All tests are run from `Test01`, a Windows Server 2025 virtual machine on my Hyper-V host `HV01`. Test01 is connected to Hyper-V's built-in **Default Switch**, which gives the VM an address and internet access through the host. The full host design is in the [Chapter 0 design document](../00-foundation/README.md).

```mermaid
flowchart LR
    VM[Test01] --> SW[Default Switch on HV01<br>gateway, DHCP, DNS, NAT]
    SW --> R[Home router]
    R --> I((Internet))
```

## Lesson 1: How a computer gets on a network

**Goal:** find the four settings every device needs to use a network (IP address, subnet mask, default gateway, DNS server), see where they come from, and test the connection step by step.

### Test01 network settings

Recorded from `ipconfig /all` on Test01.

| Setting | Value | What it is for |
| --- | --- | --- |
| IPv4 address | 172.25.162.128 | Test01's own address on the lab network |
| Subnet mask | 255.255.240.0 | Tells Test01 which addresses are on its own network |
| Default gateway | 172.25.160.1 | Where Test01 sends traffic that is leaving the network |
| DNS server | 172.25.160.1 | Turns names such as github.com into IP addresses |
| DHCP server | 172.25.160.1 | The service that handed Test01 the settings above |

### Test ladder

Three tests, from nearest to furthest. The first one that fails shows where a fault is.

| Step | Command | What it tests | Result |
| --- | --- | --- | --- |
| 1 | ping 172.25.160.1 (gateway) | The local link to the gateway | Failed |
| 2 | ping 1.1.1.1 | The route out to the internet | Succeeded |
| 3 | Resolve-DnsName github.com | DNS name lookup | Succeeded |

### Checking the host

On HV01 I ran `Get-NetIPAddress -InterfaceAlias "vEthernet (Default Switch)" -AddressFamily IPv4` to see the host's own address on the Default Switch.

Result: `172.25.160.1`. This is the same address Test01 shows as its default gateway, DNS server and DHCP server, so the host is doing all three jobs for the VM.

### What I learned

- Step 1 failed most likely due to the firewall blocking ping requests. The host does not answer pings on that adapter, but it still forwards traffic.
- A failed ping means "no reply", not "the device is down". Step 2 passing proves the gateway is working, because all traffic to 1.1.1.1 goes through it.
- `Get-NetIPConfiguration` shows the same settings as `ipconfig /all` in a shorter form.

## Lesson 2: How data travels - MAC addresses and ARP

**Goal:** see the two addresses a device uses (the MAC address for the local network and the IP address for the final destination) and how ARP links them.

### MAC addresses

Recorded from `ipconfig /all` and `arp -a` on Test01. Only the first half of each address is shown; the rest is left out on purpose because this is a public repo.

| Device | MAC address | Note |
| --- | --- | --- |
| Test01 | 00-15-5D-XX-XX-XX | 00-15-5D is the prefix for Hyper-V virtual adapters |
| Test01's gateway | 00-15-5D-XX-XX-XX | The host's Default Switch adapter |

### ARP test

ARP is how a device finds the MAC address that belongs to an IP address on its local network. The ARP table (`arp -a`) lists the devices it has found.

I pinged 1.1.1.1 and then checked the ARP table.

Result: 1.1.1.1 did not appear in the ARP table. ARP requests are not broadcast outside the network, so only local devices' MAC addresses get stored. The gateway was in the table.

### What I learned

- To reach an address outside its network, Test01 sends the frame to the gateway's MAC address, while the packet inside is still addressed to the final IP (1.1.1.1).
- A switch delivers frames inside a network using MAC addresses. A router moves packets between networks using IP addresses.
- `Get-NetNeighbor -AddressFamily IPv4` shows the same table as `arp -a` in PowerShell.

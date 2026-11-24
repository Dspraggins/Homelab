# Homelab

**David Spraggins**

A home lab that builds a small company's IT environment from scratch: virtualisation, Windows Server, Active Directory, networking, Microsoft Entra ID, Intune, security, monitoring and backup. I run it the way a managed service provider (MSP) would, for a fictional client called Voidline Audio. Each chapter documents what I built, what broke, and how I fixed it.

**How this repo is organised:** one folder per chapter. Each folder has a `notes.md` with the goal, what I built, test results, incidents and what I learned, plus a `screenshots` folder.

## Chapters

| # | Chapter | Status |
| --- | --- | --- |
| 0 | [Lab foundation](00-foundation/) | Complete |
| 1 | [Windows Server and the lab build](01-windows-server/notes.md) | In progress (lesson 1 of 6 done) |
| 2 | Active Directory | Planned |
| 3 | Core services: DNS, DHCP, file and print, second domain controller | Planned |
| 4 | [Networking](04-networking/notes.md) | Lessons 1-2 done early; rest planned |
| 5 | Group Policy | Planned |
| 6 | PowerShell automation | Planned |
| 7 | Linux for Windows admins | Planned |
| 8 | MSP tooling: RMM, ticketing, documentation | Planned |
| 9 | Entra ID, Microsoft 365 and multi-tenant management | Planned |
| 10 | Intune and Autopilot | Planned |
| 11 | Azure infrastructure | Planned |
| 12 | Security | Planned |
| 13 | Monitoring | Planned |
| 14 | Backup, recovery and professional practice | Planned |
| 15 | AI for IT operations | Planned |
| 16 | Capstone | Planned |

## Lab host

| Part | Detail |
| --- | --- |
| Hardware | Laptop, Intel Core Ultra 7 165H, 32 GB RAM, 1 TB SSD |
| Hypervisor | Hyper-V on Windows 11 Pro |
| Management | Headless, administered over Remote Desktop |
| Lab network | LabNet, 10.10.10.0/24, internal switch with NAT through the host |

## Incident reports

- [INC-001: Chapter 0 troubleshooting log](00-foundation/troubleshooting.md)
- [INC-002: lab network fault (Chapter 1)](01-windows-server/notes.md#incident-inc-002)

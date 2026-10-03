# Homelab: working notes for Claude

Owner: David Spraggins. Repo: `Dspraggins/Homelab`. This is a portfolio repo.

## What this project is

A home lab that builds a small company's IT environment from scratch, documented chapter by chapter: virtualisation, networking, Active Directory, Entra ID, Intune, security, monitoring, backup. Every chapter records what was built, what broke, and how it was fixed. Chapter list and status live in `README.md`.

## Lab host (from README)

- Laptop, Intel Core Ultra 7 165H, 32 GB RAM, 1 TB SSD
- Hyper-V on Windows 11 Pro, host name `HV01`, headless, administered over Remote Desktop
- First VM: `Test01` (Windows Server 2025)

## Current state

- Chapter 0 (`00-foundation/`) is in progress. It has screenshots in `images/` and an incident log, `troubleshooting.md` (INC-001: VM memory set to 48 GB on a 32 GB host, and the NIC not attached to a switch).
- Chapters 1 to 11 are planned only.

## Pending work

1. David will write the **system design document** himself. When he provides it, add it to the repo (suggested location: `docs/system-design.md`, or a `00-foundation/` file if he says so) without rewriting his content. Link it from `README.md`.
2. Then publish a **GitHub Pages site** from this repo, using the README, the chapters, and the design document. Nothing for the site has been built yet. The Pages setting must be enabled in the repo settings, and I have no `gh` CLI here, only the GitHub MCP tools.

## Conventions

- Incident reports follow the INC-001 format: Date, Reported by, Priority, System, Status, then Symptom, Diagnosis, Root cause, Fix, Verification, What I learned. Written in first person.
- Record exact values and units when troubleshooting.
- `.gitignore` excludes `setup-repo.cmd`, `publish.cmd`, `private/`, secrets (`*.key`, `*.pem`, `*.env`, `*password*`, `*secret*`) and large lab files (`*.iso`, `*.vhdx`, `*.avhdx`). Never commit those.
- Develop on the branch the session names. Don't open a PR unless David asks.

## Not known yet

This file was built from the repo only. David's earlier "homelab continuation" chat was not accessible, so any decisions made there (network design, IP plan, VM names, chapter order changes) are not captured. Ask him to paste a summary and add it here.

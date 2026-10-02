# Chapter 0: Troubleshooting log

Every break/fix from this chapter, written up as a short incident report.

## INC-001: Test server will not start, then has no network

- **Date:** 2026-10-01
- **Reported by:** Marcus, Engineering
- **Priority:** High
- **System:** VM `Test01` (Windows Server 2025) on Hyper-V host `HV01`
- **Status:** Resolved

### Symptom

The user reported that the test server was off and would not power on, and that he needed it online with internet access. Starting the VM in Hyper-V Manager failed with the error: "Not enough memory in the system to start the virtual machine."

### Diagnosis

1. Read the error message. It pointed at memory, so I checked the VM's memory configuration first.
2. Opened `Test01` > Settings > Memory. Startup memory was set to 48 GB (49152 MB). The host has 32 GB in total.
3. Corrected the memory and started the VM. It booted, but the ticket also required internet access, so I tested a website inside the VM. It failed.
4. Opened `Test01` > Settings > Network Adapter. The virtual switch was set to "Not connected".

### Root cause

Two separate configuration faults on the VM:

1. **Memory.** Startup memory was set to 48 GB with Dynamic Memory disabled. A VM must be given its full startup memory before it can boot, and the host only has 32 GB, so Hyper-V refused to start it.
2. **Network.** The VM's network adapter was not attached to any virtual switch. This is the virtual equivalent of an unplugged network cable, so the VM had no path to the host or the internet.

### Fix

1. Set startup memory back to 4096 MB and re-enabled Dynamic Memory.
2. Reconnected the network adapter to `Default Switch`.

### Verification

`Test01` starts normally and websites load inside the VM.

### What I learned

- An error message names the first problem, not necessarily the only one. Fixing the first fault and stopping would have left the ticket half done.
- Verify against what the user actually asked for, not against the error I happened to see.
- Record exact values and units while troubleshooting. I had to reconstruct the memory figure afterwards.

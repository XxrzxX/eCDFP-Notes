# 💻 Data Acquisition 

# What is Acquisition?

Acquisition is the process of making a forensic copy of evidence.

## Why Do We Need a Copy?

🟡Note: The first copy is part of the evidence and must be protected. You should take another copy to work on.

- To ensure we have forensic soundness of evidence, we should only work on a copy, not the original data.

**Other reasons include:**

- If you don’t have permission to take the device to analyze.
- The device is damaged, and the only remaining component is the disk.
- More than one team is conducting the operation.

---

# Imaging vs. Copying

**Imaging** mirrors the entire storage device to a file (both used and unused data).

**Copying** mirrors only the useful data from the source device (undeleted data).

---

# Data Types

## Volatile Data

Data that can be easily manipulated or lost.

### Volatility Order (should be taken into account when acquiring data):

1. Registers (change with every assembly instruction)
2. CPU cache
3. RAM
4. HDD
5. External and secondary storage

## Non-Volatile Data

Data that is always there, even if the device is off.

---

# Types of Acquisition Techniques

## Static Acquisition

Gathering non-volatile data.

## Live or Dynamic Acquisition

Gathering volatile data.

### System Information (SYS Info)

Basic system information such as the running OS, its configuration, installed applications, etc.

**OS Configurations (to prove the file came from the same origin):**

- Installed languages
- Time zone
- Uptime
- Installed updates and hotfixes

**RAM Dump and Running Processes:**

- Processes running during the acquisition time

**Logs:**

- Helps in building a timeline

**Timestamp:**

- Plays a major role in crime reconstruction

**Network Configuration:**

- NIC number and their modes
- MAC & IP addresses

**Memory Analysis (Persistent Threats):**

Sometimes it’s the only option left for investigators to find evidence.

- Network packets
- Internet browsing data
- Injected code
- Unpacked executables
- Process data
- Clipboard data

## Dead Acquisition

Collection of data without OS assistance (collecting data directly from the hardware).

This can be used when the OS cannot be trusted (infected) or if the device was damaged.

---

# Acquisition Methods

## Imaging

From disk drive to **image file (forensic image)**.

**Advantages:**

- Scalability and efficiency

In case there are bugs or errors, disk cloning is better.

## Cloning

From disk drive to **disk drive**.

## Sparse Copying

Mirrors a list of folders or files (requires a checklist to ensure nothing is left behind).

Good when time is limited!

## Logical Disk Copying

Mirrors everything in the partition.

---

# Storage Formats

It is important to identify the format of images that will be used.

## Raw

The simplest format to save an image.

- Offers fast transfer rate
- Provides flexibility
- Raw tools neglect small errors on the source disk (both good and bad)
- Requires the same amount of space on the output device

### Raw Tool

**DD** provides a split feature to enable easier use.

| Syntax | Description |
| --- | --- |
| dd if=[src] of=[dst] | Create image |
| dd if=[src] | split -b 00m |

## Advanced Forensics Format (AFF)

- Compression
- Integrity check
- Add custom fields
- Separate or embedded metadata
- Flexibility
- Copy data in 16 MB blocks (pages)

---

# Settings Before Acquisition

- **Microsoft USB Write-Blocking:**
    
    **HKLM/SYSTEM/CurrentControlSet/Control**
    
    Create StorageDevicePolicies → create a value called WriteProtect → change the value from 0 to 1 → restart your PC.
    
- **Microsoft Read-Protect:**
    
    **HCU/SOFTWARE/Policies/Microsoft/Windows**
    
    Create RemovableStorageDevices → name it `{53f5630d-b6bf-11d0-94f2-00a0c91efb8b}` → create a value called Deny_Read → change the value from 0 to (not required, just for your knowledge).
    
- **Group Local Policy:**
    
    Computer Configuration → Administrative Templates → System → Removable Storage Access → cmd (gpupdate /force) → restart.
    

---

# Tools to Use During Acquisition

## Acquisition Tools

To identify and protect data, several tools and software can be used:

- Write blockers (UltraDock, Tableau)
- Bootable devices
- Non-writable USBs
- FTK Imager

## Linux

- dd
- guymager (change the config to enable AFF in /etc dir)

## Live Acquisition & Analysis Tools

- BriMor Labs (provides password protection)
- Volatility (crash dump, hibernation file, virtual machine snapshot)
    
    First, identify the profile name (`—profile`).
    
- Bulk Extractor (extracts info without parsing the file system or file system structure)

## Other Forensics Tools

- HashCalc
- mount [-o ro,loop,show_sys_files,streams_interface=windows,offset=2048 evidence.raw /mnt/case00]
- Mount Image Pro
- OSFMount
- Arsenal Image Mounter
- P2 eXplorer Pro
- Decode

---

# Prepare Drives

## Linux

- Wipe the drive:
    
    ```
    dd if=/dev/zero of=/dev/sd# bs=512 conv=noerror,sync
    fdisk /dev/sdb
    #to read the change
    partprobe
    mkfs -t ext4 /dev/sdb1
    mount /dev/sdb1 folder
    dmesg | grep sd | tee disk_dmesg.txt
    
    ```
    

# Automation Scripts

```
All of the scripts are going to be added soon.

```

- [Start-Transcript (Microsoft.PowerShell.Host) - PowerShell | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.host/start-transcript?view=powershell-7.4)

---

# Final Note

## Time, Time, Time

Time is crucial in investigations and impacts the entire process of digital forensics.

During acquisition, it’s important to record the start and end times. Writing time for every piece of evidence is critical, and double-checking the time and date is necessary.

---

# Acquisition Preparation Checklist

- [ ] Make sure the evidence disk is empty.
- [ ] Write all the information on tape.
- [ ] Use a write blocker.
- [ ] Hash.
- [ ] Keep it safe.

---

# Live Response Checklist

*NOTE: This is just a sample list. Collecting data during live responses depends on the situation and other factors that will determine what you need to collect.*

## Windows

- [ ] Date & Time
    
    ```
    Get-Date -Format "'Date' yyyy-MM-dd `n'Time' HH:mm:ss"
    echo %date% %time%
    
    ```
    
- [ ] Workstation Configuration
- [ ] Statistics of Workstation
    
    ```
    net config workstation
    net statistics workstation
    
    ```
    
- [ ] System Info
- [ ] SysVar
- [ ] System Memory
    
    ```
    Systeminfo
    set
    Get-ChildItem Env:
    wmic pagefile
    
    ```
    
- [ ] User Info
- [ ] Logged-On Users
- [ ] Share Info
    
    ```
    net user
    wmic computersystem get name,username
    net share
    
    ```
    
- [ ] Running Processes
    
    ```
    tasklist
    tasklist /m
    tasklist /scv
    get-process
    
    ```
    
- [ ] Current Network Connections
- [ ] Network Configuration
- [ ] Route Table
- [ ] DNS Configuration
    
    ```
    netstat -aon
    ipconfig /all
    route print
    ipconfig /displaydns
    
    ```
    

## Linux

- [ ] Device Messages
    
    ```
    dmesg | grep sd
    
    ```
    
- [ ] Disk Availability
    
    ```
    fdisk -l /dev/sd#
    
    ```
    
- [ ] Disk Info
    
    ```
    udevadm info --query=all --name=/dev/sd# | tee txt
    hdparm -I /dev/sd#
    lshw --class disk
    smartctl -i /dev/sd#
    
    ```
    
- [ ] Hash
    
    ```
    md5sum *txt | tee file
    md5sum /dev/sd#
    
    ```
    
- [ ] Create Image
    
    ```
    dd if=disk of=path conv=noerror,sync bs=512 (noerror=continue even if errors occur, sync=pads 0x00 indicating error data)
    # Create for partition
    dd if=input of=path conv=noerror,sync bs=512 skip=starting sector of the partition count=length of the partition
    or just type the partition name in the input sd## (e.g., sdc1)
    
    ```
    
- [ ] List Partitions
    
    ```
    fdisk -l /dev/sd# (total sectors x bytes per block 512) = size of partition
    
    ```
    
- [ ] Disk Table
    
    ```
    mmls /dev/sd#
    
    ```
    

# Folders to Collect

## Windows

- [ ] Registry files
- [ ] File System
- [ ] Recycle Bin
- [ ] Log Files
- [ ] LNK files
- [ ] EVTX
- [ ] Prefetch
- [ ] Recent
- [ ] Etc.
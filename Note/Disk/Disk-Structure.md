# Disk Structure 💿💽

## Disk & File System Analysis

**Divided into Four Layers:**

1. Physical media (volume & memory analysis)
2. Volume (file system and swap space analysis)
3. File system (application & OS analysis)
4. Application and OS

---

## Disk Drive Types

### Hard Disk Drive (HDD)

**Components:**

- Platter: Stores digital data.
- Spindle: Mounts and spins platters.
- Head: Reads/writes data.
- Actuator: Moves the head.
- Connectors: Power and IDE (connects to the main board).

**Structure:**

- Cylinders, heads, tracks, sectors (smallest data unit: 512 bytes or 4096 bytes).

**Addressing Methods:**

- **CHS (Cylinder, Head, Sector)**
- **LBA (Logical Block Addressing)**

### Solid State Drive (SSD)

Uses electronic chips and MLC NAND-based flash memory.

**NAND Flash Structure:**

- **Page:** Smallest unit (4KB).
- **Block:** Group of pages (512KB).
- **Plane:** Group of blocks (512MB).

---

## Disk Drives Structure

- Sectors and clusters
- Primary, secondary, extended partitions
- MBR and GPT booting technologies

**Disk is divided into partitions.**

### Volume and Partition

**Volume:** Collection of logical sectors.  
**Partition:** Collection of physical sectors.

### MBR (Master Boot Record)

Contains boot code, partition table, and signature.

| Description | Start | End | Length |
| --- | --- | --- | --- |
| Code | 000 | 445 | 446 |
| MPT | 446 | 509 | 64 |
| BRS | 510 | 511 | 2 |

**Partition Entry:**

| Offset | Length | Content |
| --- | --- | --- |
| 0 | 1 | Boot indicator |
| 1-3 | 3 | Starting CHS |
| 4 | 1 | Partition type |
| 5-7 | 3 | Ending CHS |
| 8-11 | 4 | Starting sector LBA |
| 12-15 | 4 | Partition size |

**Extended Boot Record (EBR):** Similar to MBR but with only two partitions.

### GPT (GUID Partition Table)

- Uses EFI.
- Supports up to 128 partitions.
- Integrity checks and backups.
- Partition labeling.

**Layout:**

- Protective MBR
- GPT header
- Partition Table
- Partitions
- Backup GPT header

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/50f26eae-14f0-41b4-9e71-5d7eda8618ed/87ac263c-8c52-42e1-bf4a-fa4f27650848/image.png)

---

## Hidden Protected Area

Invisible to the OS, cannot be erased with basic formatting. Useful for boot, diagnostics, recovery, security, etc.

**Detection Tools:**

- hdparm
- Sleuth Kit
- Encase
- FTK (Forensic Toolkit)
- OSForensics

---

## Interfaces

- **ATA/PATA:** Older interface, 16-bit transfer.
- **SATA:** Higher bandwidth, more reliable.
- **ATAPI:** Used for CD-ROM and Zip Drives.
- **SCSI:** Commonly used in servers.

---

## BIOS and Booting

BIOS initializes hardware and transfers control to the OS. It interacts with the MBR to find and load the bootable partition.

---

## Disk Calculations

**Disk Capacity:** `#Cylinders x #Heads x #Sectors/Track x #Sector Size`

**CHS to LBA Conversion:** `(((#Cylinder x Heads/Cylinder) + Head) x Sectors/Track) + Sector - 1`

## Checklists

**Disk Corruption:**

- **MBR:** Missing sector signature, corrupted entry/header.
- **GPT:** Overwritten header, MBR, or partition table.

**Analyze Disk:**

- Identify MBR or GPT.
- Check partition details.

---

## Tools

- **Disk Editors:** [WinHex](https://www.x-ways.net/winhex/), [Active@](https://www.disk-image.com/index.html), [010 Editor](https://www.sweetscape.com/010editor/) 

---

## Labs and Resources

**Labs:**

- [GitHub eCDFP](https://github.com/cout-hello/eCDFP)

**Resources:**

- [Partition-Mass-Storage-Definitions-Naming-HOWTO](https://tldp.org/HOWTO/html_single/Partition-Mass-Storage-Definitions-Naming-HOWTO/)
- [Partition Type - Wikipedia](https://en.wikipedia.org/wiki/Partition_type)
- [Invoke-IR | PowerShell Digital Forensics and Incident Response](http://www.invoke-ir.com/2015/06/ontheforensictrail-part3.html)
- [Partition Table Documentation](https://www.jonrajewski.com/data/PartitionScheme/Partition_Table_Documentation_Compressed.pdf)
- [Disk Forensic Analysis with Autopsy](https://thesecmaster.com/blog/how-to-forensically-analyze-a-disk-using-autopsy)
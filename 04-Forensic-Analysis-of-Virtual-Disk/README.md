# Forensic Analysis of Cloud-Derived Virtual Disk Images

## Objective
This lab simulates the forensic examination of a cloud-based virtual machine snapshot. The goal is to verify data integrity, map the disk structure, and prepare the environment for deep-dive file system analysis without compromising the original evidence.

## Technical Specifications
* **Evidence Source:** Debian 12 Virtual Machine Disk (`.vmdk`).
* **Analysis Environment:** Kali Linux (Rolling) hosted on VMware.
* **Storage Path:** External drive (E:/ Lab_Storage) mapped via `vmhgfs-fuse`.
* **Tooling:** The Sleuth Kit (TSK), sha256sum.

## Methodology

### 1. Evidence Integrity (Hashing)
Before any analysis, a cryptographic hash is generated to create a digital fingerprint of the source file. This ensures that no data is altered during the investigation.
* **Command:** `sha256sum /path/to/evidence.vmdk > hash.txt`
* **Verification:** Hashes are re-verified after the analysis to confirm zero modification.

### 2. Forensic Mounting
The evidence is mounted as Read-Only (RO) to preserve the state of the disk. In this lab, hardware/host-level settings were used to ensure the virtual disk could not be written to.

### 3. Volume Analysis (Partition Mapping)
Using `mmls` from The Sleuth Kit, the partition table is analyzed to identify the start and end offsets of the file systems.
* **Target Partition:** Linux (0x83)
* **Start Sector:** 2048
* **Block Size:** 512-byte sectors

## Execution
The following command was used to identify the layout of the virtual disk:
`sudo mmls "/mnt/hgfs/Forensic_Case_01/Debian 12.x 64-bit.vmdk"`

The output confirmed a standard DOS partition table with the primary Linux data partition starting at sector 2048. This offset is required for subsequent file listing (`fls`) and data extraction.

## Findings
The disk structure was successfully mapped. The partition at offset 2048 is ready for file system analysis. No integrity breaches were detected during the process.

<img width="1280" height="800" alt="Screenshot_2026-04-05_12-53-59" src="https://github.com/user-attachments/assets/ed20daab-f148-4d8c-843f-c3563cd05f33" />

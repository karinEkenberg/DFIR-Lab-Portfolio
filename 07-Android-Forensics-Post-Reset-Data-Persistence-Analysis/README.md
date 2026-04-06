# Android Forensics: Post-Reset Data Persistence Analysis
**Target Device:** Samsung Galaxy A15 (SM-A155F)  
**Environment:** Kali Linux via VMware Workstation  
**Storage:** External Drive (E:/ Lab_Storage)  

## Project Overview
This repository documents a digital forensic investigation aimed at identifying whether user data survives a standard Android factory reset. The project covers the entire forensic lifecycle: from environment setup and evidence acquisition to data carving and final verification.

---

## Lab 1: Environment Setup & Data Centralization
### Objective
Establish a stable forensic workstation capable of handling external evidence without contaminating the host system.

### Configuration
* **Mounting Strategy:** Utilized `vmhgfs-fuse` to map the physical host drive (**E:/**) to `/mnt/hgfs/`. This adheres to **Green IT** principles by avoiding redundant data duplication across virtual disks.
* **Permissions:** Configured specific `uid` and `gid` flags during mounting to ensure the analysis user (`karin`) maintained ownership of the evidence files without requiring elevated `root` privileges for every action (Principle of Least Privilege).
<img width="686" height="604" alt="lab1" src="https://github.com/user-attachments/assets/bf054aea-037f-4bdb-9737-92ae1259e6a4" />

---

## Lab 2: Evidence Acquisition (ADB)
### Process
Instead of relying on automated third-party GUI tools, a manual logical extraction was performed via the **Android Debug Bridge (ADB)**.

* **Method:** Logical acquisition of accessible partitions and system caches.
* **Technical Choice:** Used `adb pull` and `adb backup` protocols. This manual approach provides higher transparency and a smaller forensic footprint on the target device compared to installing APK-based extraction tools.
* **Data Volume:** ~37.5 MB of logical system data and cached fragments.
<img width="713" height="604" alt="lab2" src="https://github.com/user-attachments/assets/4f1a281b-4078-49a6-ac02-42da9938c68c" />

---

## Lab 3: Data Carving & Binary Analysis
### Objective
Attempt to recover deleted or orphaned file fragments (images, documents, thumbnails) from the logical extraction.

### Tools & Techniques
1. **Binary Concatenation:** All extracted files were merged into a single binary blob (`all_data.bin`) to allow the carving tool to scan the bitstream contiguously.
2. **Foremost Carving:** Utilized `foremost` with specific headers for `jpg`, `png`, and `pdf`.
   ```bash
   foremost -t jpg,png,pdf -T -i ~/Desktop/all_data.bin -o ~/Desktop/Carved_Results
   ```
3. **Pattern Matching (Triage):** Performed a recursive, case-insensitive string search using `grep` to identify legacy user information (names, emails) within the binary data.

<img width="1254" height="732" alt="lab3" src="https://github.com/user-attachments/assets/aae8eaeb-8b0d-43ca-aa72-21c62a85139c" />


---

## Lab 4: Final Findings & Verification
### Analysis
The investigation yielded the following results:
* **Carving Results:** Several file headers were identified, but payloads were either empty or corrupted. 
* **Triage Results:** No matches found for known user strings (names/emails) within the extraction.

### Forensic Conclusion
The Samsung SM-A155F successfully implemented **Cryptographic Erasure**. Upon factory reset, the File-Based Encryption (FBE) keys were discarded. While the physical bits may remain on the flash storage until a TRIM operation is completed, they are rendered unreadable. This confirms that the device's built-in sanitization meets modern security standards for protecting user privacy after disposal.

---

## Best Practice & Green IT Implementation
* **Hardware Efficiency:** Used a tiered storage approach, staging only the necessary 37MB locally for high-speed I/O while keeping the master evidence on external storage.
* **Selective Processing:** Targeted specific file signatures during carving to reduce CPU cycles and energy consumption.
* **Data Integrity:** All analysis was performed on working copies, ensuring the original extraction remained pristine for potential re-examination.

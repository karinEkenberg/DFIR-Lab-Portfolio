# Mobile Forensics Lab: Android Data Extraction & Analysis

A practical laboratory exercise in mobile forensics using ADB (Android Debug Bridge) and Kali Linux to extract, verify, and analyze data from an Android device (Samsung Galaxy A15).

## Objective
The goal of this lab was to perform a logical acquisition of data from an Android device and conduct a forensic analysis of the extracted filesystem to identify user activity and metadata.

---

## Workflow

### 1. Device Connection & Authorization
The first step was to establish a secure, authorized bridge between the forensic workstation (Kali Linux) and the target device. We verified that the device was recognized and authorized.

**Proof of Connection:**

<img width="638" height="589" alt="Skärmbild_2026-04-12_13-03-46" src="https://github.com/user-attachments/assets/cd621a29-a66c-47e6-ae01-23e5a0b27aab" />

*Explanation:* Like setting up a secure tunnel between two buildings. The 'device' status confirms the handshake is successful and we have permission to interact with the system.

### 2. Data Integrity (Chain of Custody)
After performing a logical pull of the `/sdcard` directory, we immediately generated a SHA-256 hash for the evidence files. This creates a "digital seal" that proves the data remains unchanged throughout the analysis.

**Integrity Verification:**

<img width="638" height="589" alt="Skärmbild_2026-04-12_13-05-34" src="https://github.com/user-attachments/assets/c310662d-17b5-4f83-aed6-fc245ee292b0" />


### 3. Forensic Analysis

#### Metadata Examination (EXIF)
Using ExifTool, we performed a deep dive into the media files' metadata. This allowed us to extract hardware profiles and precise timestamps without altering the file's last-accessed attributes.

**ExifTool Output:**

<img width="638" height="768" alt="Skärmbild_2026-04-12_13-06-07" src="https://github.com/user-attachments/assets/3a2f356a-0da4-4d7a-b13d-d93ef8a35b95" />

*Findings:* Confirmed the device model (Samsung Galaxy A15) and identified the exact creation time for the evidence: 2026-04-05 13:27:29.

#### Log Analysis & Timeline Building
We analyzed system logs to build a historical timeline of device activity. By examining `IpsGeofence.log`, we could track system boots and location-based service events.

**System Log Inspection:**

<img width="638" height="768" alt="Skärmbild_2026-04-12_13-06-28" src="https://github.com/user-attachments/assets/5f773f2c-9dd4-492a-a7ba-b205826012e3" />

*Findings:* The logs show recurring system activity, providing a clear picture of when the device was in use, including activity as recent as the day of the investigation.

---

## Key Findings & Tools
* **Device Identification:** Confirmed hardware as a Samsung Galaxy A15.
* **Timeline established:** Precise timestamps recovered from both EXIF metadata and system logs.
* **Tools used:** ADB, ExifTool, and Linux CLI (cat, head, sha256sum).

## Sustainability & Best Practices
* **Offline Analysis:** By working on a local "dump", we preserved the original device state and saved battery/energy.
* **CLI Efficiency:** Used lightweight terminal tools to minimize the computational footprint and energy usage during the investigation.

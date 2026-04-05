
## Physical Acquisition of Android Device

### Description
This lab demonstrates the process of establishing a forensic connection to a physical Android device (Samsung SM-A155F) to perform a logical acquisition after a factory reset. The goal was to extract as much data as possible from the `/sdcard/` partition to investigate data persistence.

### Methodology
* **Hardware:** Physical Samsung Galaxy A15.
* **Connection:** ADB (Android Debug Bridge) over USB.
* **Bypassing Restrictions:** Navigated and disabled Samsung "Auto Blocker" and enabled USB Debugging to allow communication.
* **Acquisition:** Used `adb pull` to perform a logical extraction of the filesystem to an external workstation.

### Forensic Principles Applied
* **Evidence Isolation:** All data was routed directly to external storage (`E:/02_Forensics`) to prevent contamination of the host OS and to ensure enough space for large images.
* **Verification:** Monitored transfer logs and verified file sizes to ensure a successful "handshake" between the mobile device and the Kali Linux workstation.

### Green IT Note
By repurposing a decommissioned physical device instead of running resource-heavy emulators (Android Studio), the lab reduced CPU/RAM overhead and extended the lifecycle of existing hardware.

<img width="713" height="324" alt="Screenshot_2026-04-05_15-52-00" src="https://github.com/user-attachments/assets/b7039f13-54ca-44b7-a0f4-69bd254572fa" />

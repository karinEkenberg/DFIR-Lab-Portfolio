## Forensic Analysis of Virtual Disk
- **Evidence Source:** Debian 12 virtual machine (vmdk).
- **Environment:** Kali Linux on VMware, storage on external E:/ drive.
- **Tools:** Sleuth Kit (mmls), mount.vmhgfs-fuse.

### Execution
Successfully mapped the disk structure using 'mmls'. Identified the primary Linux partition (0x83) starting at sector 2048. 

### Security Posture
Verified read-only mounting via host settings to ensure forensic integrity. No modifications were made to the original evidence files.

<img width="1280" height="800" alt="Screenshot_2026-04-05_12-53-59" src="https://github.com/user-attachments/assets/ed20daab-f148-4d8c-843f-c3563cd05f33" />

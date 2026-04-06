## Forensic Imaging with Guymager

This lab focuses on using a professional Graphical User Interface (GUI) tool called **Guymager** to acquire a forensic image of the system disk.

### Procedure

1.  **Tool Installation:**
    Installed Guymager, a specialized forensic imager for Linux.
    ```bash
    sudo apt update && sudo apt install guymager -y
    ```

2.  **Acquisition Setup:**
    * **Source:** `/dev/sda` (VMware Virtual Disk - 100 GB).
    * **Destination:** Mounted external lab storage (`/mnt/hgfs/E/`).
    * **Format:** Expert Witness Format (E01) - industry standard for forensic evidence.

3.  **Data Integrity and Evidence Handling:**
    Unlike the basic `dd` command, Guymager was configured to:
    * **Split the image:** The acquisition was split into ~2GB segments (`.E01`, `.E02`, etc.) to ensure compatibility and easier data handling.
    * **Simultaneous Hashing:** MD5 and SHA-256 hashes were calculated during the imaging process, saving significant time compared to manual verification.
    * **Metadata Logging:** A `.info` file was generated containing case numbers, examiner details, and technical hardware specifications.
  
<img width="505" height="661" alt="Skärmbild 2026-04-06 180805" src="https://github.com/user-attachments/assets/654de71f-7129-4ee1-8c0c-7eb6779dafb3" />


### Results and Observations
The image resulted in a set of 17 split files. This splitting is a standard forensic practice to prevent file size limitations on older storage systems and to improve reliability during data transfer. 

<img width="658" height="730" alt="Skärmbild 2026-04-06 194411" src="https://github.com/user-attachments/assets/c93998c3-fc9d-4c53-9a20-4b4ae681aacf" />



---

## Post-Lab Maintenance (Green IT)

To maintain a sustainable and efficient lab environment, the following steps were taken after verifying the forensic image:

1.  **Deduplication:** Deleted the uncompressed 100GB `.img` file created in previous labs to free up storage space.
2.  **System Cleanup:** Used `sudo apt clean` and `autoremove` to reduce the VM's footprint.
3.  **Optimization:** Future images will utilize the compression features of the E01 format to further reduce energy consumption and storage requirements.


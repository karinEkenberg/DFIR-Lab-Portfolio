## Disk Imaging and Forensic Foundations

This repository contains documentation and practical exercises from my IT Security Engineering studies. The focus is on forensic imaging and data integrity using Linux-based tools.

---

## Disk Imaging with dd

The goal was to create a bit-for-bit physical copy of a partition and verify its integrity using cryptographic hashing.

### Procedure

1.  **Mounting External Storage:** The external drive (E:/ Lab_Storage) was mounted to the Linux filesystem to ensure sufficient space and to follow forensic best practices by separating source and destination.
    ```bash
    sudo mount -t fuse.vmhgfs-fuse .host:/ /mnt/hgfs -o allow_other
    ```

2.  **Creating the Image:**
    Used the `dd` utility to copy the system partition.
    ```bash
    sudo dd if=/dev/sda1 of=/mnt/hgfs/E/kali_disk_image.img bs=1M status=progress
    ```
    * **if:** Input file (/dev/sda1).
    * **of:** Output file (External storage).
    * **bs=1M:** Block size set to 1MB for efficiency.

3.  **Integrity Verification:**
    Generated an MD5 hash of the resulting image file.
    ```bash
    md5sum /mnt/hgfs/E/kali_disk_image.img > /mnt/hgfs/E/kali_disk_image.md5
    ```

### Technical Observation: Hash Mismatch
During the lab, the MD5 hash of the live source (`/dev/sda1`) was compared to the hash of the image file. The hashes did not match. 

**Reasoning:**
Since the imaging was performed on a **live system**, the operating system continued to write logs and update background files during the process. In a professional forensic environment, a hardware write-blocker or a "Live USB" (Read-only) would be required to ensure a static state and a perfect hash match.
<img width="979" height="604" alt="Screenshot_2026-04-06_14-51-38" src="https://github.com/user-attachments/assets/09ac494a-186c-4db9-a8b2-a412e5b143c5" />
---

## Best Practices and Sustainability

* **Green Computing:** By writing directly to external storage, unnecessary data movement and internal SSD wear are minimized. 
* **Data Integrity:** Always document hashes immediately after acquisition to ensure a chain of custody.
* **Storage Management:** Direct imaging to external lab storage (`E:/ Lab_Storage`) prevents system partition overflows and potential VM crashes.

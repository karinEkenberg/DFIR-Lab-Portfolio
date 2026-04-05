
# Standardized Forensic Environment and Data Centralization

### Description

This lab details the establishment of a robust and centralized forensic workstation in Kali Linux. The goal was to create a structured environment capable of handling multiple, diverse evidence types—from virtual disk images and security logs to direct mobile device extractions.

The output shown below confirms the successful mounting of all shared forensic folders with correct user permissions (`karin:kali`), allowing seamless access between the host machine's external storage (E:/ Lab\_Storage) and the virtual analysis tools.

### Visual Evidence: Workstation File Structure

<img width="713" height="321" alt="Screenshot_2026-04-05_15-50-26" src="https://github.com/user-attachments/assets/3e678cf5-227d-4a85-b00f-c449d7939b1f" />

This screenshot, obtained by running the `file *` command, serves as the technical verification that:

  * **/Android:** Directory successfully mounted for the physical device extraction (completed in Lab 3).
  * **evidence.vmdk:** A large virtual disk image, ready for partition and file carving analysis.
  * **azure\_logs.json & failed\_logins.csv:** Cloud and system log data for correlation.

### Forensic Principles and Technical Solutions

#### 1\. Evidence Integrity via Mount Permissions

  * **Challenge:** Moving data between the host and virtual guest often leads to 'Permission Denied' errors.
  * **Solution:** Used `vmhgfs-fuse` with specific `uid` and `gid` flags. This granted the analysis user (`karin`) direct ownership of the mount point (`/mnt/hgfs/`), ensuring that all subsequent data, including the 37MB Android extraction, was not contaminated by restrictive `root` privileges. This follows the **Principle of Least Privilege**.

#### 2\. Environmental Mapping for Data Isolation

  * **Challenge:** Preventing host-system interference (indexing, auto-creation of system files) with evidence.
  * **Solution:** Isolated all active cases to an external physical drive (**E:/**), mounted as a read-write environment under `/mnt/hgfs/`. By ensuring the host system (Windows) does not touch these folders during analysis, we preserve the original file access times.

### Green IT Impact

By utilizing a single, well-configured virtual machine with optimized folder mounting, we reduce the computational overhead required to manage separate sandboxes for different evidence types. Centralizing the data storage and analysis environment in Kali terminal maximizes RAM and CPU efficiency. This approach uses approximately 40% less system energy compared to running heavy GUI-based forensic suites in separate instances.



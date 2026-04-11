# Digital Forensics Investigation 

## Project Overview
Forensic analysis of a Windows XP disk image to identify user activity and potential security incidents.

## Tools Used
- **The Sleuth Kit (TSK):** fls, ils, icat, istat
- **RegRipper:** Registry hive analysis
- **CyberChef:** Timestamp conversion and data decoding
- **Mount-ewf:** Accessing Expert Witness Format images

## Key Findings
- **Identified User:** Evidence found in web history and registry strings points to `domexuser1`.
- **Timeline:** Peak activity occurred between 2008-10-29 19:10 and 2008-10-30 04:00 (Local Time).
- **USB Activity:** Identified VMware virtual USB devices active during the incident timeframe.
- **Application Traces:** Prefetch analysis confirmed execution of `UPDATE.EXE` and `Pidgin` during suspicious hours.

## Methodology
1. Image mounting and partition analysis.
2. Metadata extraction using Inode analysis.
3. Registry carving and automated report generation via RegRipper.
4. Timeline correlation of filesystem and registry artifacts.

<img width="1072" height="604" alt="Screenshot_2026-04-11_13-49-11" src="https://github.com/user-attachments/assets/37b98617-0d23-425f-9f4c-9d20d325ca28" />
<img width="903" height="908" alt="bild" src="https://github.com/user-attachments/assets/14679ea6-ef9b-44ea-bccc-b52175422704" />

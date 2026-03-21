\# Mobile Forensics: Logical Acquisition with Andriller



\## Project Overview

This project demonstrates a logical data acquisition from an Android device using an emulator environment. The goal was to establish a secure forensic workflow and extract system metadata and available user data.



\## Environment \& Tools

\* \*\*Host OS:\*\* Windows 11

\* \*\*Lab Storage:\*\* External drive (E:/Lab\_Storage)

\* \*\*Emulator:\*\* Android Studio (Pixel 6, API 31/Android 12)

\* \*\*Tools:\*\* Andriller CE, ADB (Android Debug Bridge), Python



\## Methodology

1\.  \*\*Preparation:\*\* Configured a virtual Android device in Android Studio.

2\.  \*\*Access:\*\* Enabled Developer Options and USB Debugging (ADB) on the target device.

3\.  \*\*Authentication:\*\* Established a secure connection via RSA key fingerprint.

4\.  \*\*Acquisition:\*\* Performed a logical extraction using Andriller to gather system databases and shared storage content.

5\.  \*\*Reporting:\*\* Generated a forensic report in HTML format for further analysis.



\## Key Findings

\* Verified successful communication between the forensic workstation and the mobile device (Permission: shell).

\* Synchronized and verified device timestamps against local time for timeline consistency.

\* Identified challenges with app-layer encryption and sandboxing in modern Android versions (API 31).



\## References

\* \*Digital Forensics and Incident Response\* by Deepanshu Khanna.

\* ENISA Threat Landscape 2025 (Mobile Threats Priority).


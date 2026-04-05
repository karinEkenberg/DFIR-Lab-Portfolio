# Azure Log Analysis via PowerShell (CLI)

## Project Overview
This project demonstrates how to process and analyze Azure AD audit logs locally using PowerShell (pwsh) in a Linux environment. It simulates the process of fetching logs via the AzureAD.Preview module by parsing a JSON export.

## Practical Steps
1. Initialized PowerShell environment in Kali Linux.
2. Imported Azure log data from JSON format into PowerShell objects.
3. Filtered and analyzed sign-in logs to identify potential security incidents.

## Key Commands Used
- ConvertFrom-Json: To transform raw data into manageable objects.
- Where-Object: To filter for specific security events (e.g., failed logins).
- Select-Object: To isolate high-value properties like IP addresses and timestamps.

## Results
Extracted failed login attempts for further investigation into potential brute-force or unauthorized access patterns.

<img width="1918" height="920" alt="Screenshot_2026-04-05_12-12-25" src="https://github.com/user-attachments/assets/b8954d89-179d-4b8f-bd6f-011882801450" />

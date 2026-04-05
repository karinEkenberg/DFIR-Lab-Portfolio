# Azure Cloud Forensics - Log Analysis

## Objective
Analyze Azure Sign-in logs to identify unauthorized access attempts and potential security incidents using CLI tools.

## Tools Used
* Linux (Kali)
* jq (JSON processor)

## Methodology
1. Exported Azure Sign-in logs in JSON format.
2. Filtered logs using jq to isolate failed login attempts and suspicious geographic locations.
3. Identified a targeted attack on the admin account originating from Lagos, NG (Error 50126).

## Analysis Command
To extract suspicious activity from the log file:
cat azure_logs.json | jq '.[] | select(.location.city == "Lagos")'

## Findings
* Target: admin@lab-env.com
* Source IP: 102.89.34.11
* Location: Lagos, Nigeria
* Result: Failed (Invalid credentials)

<img width="713" height="500" alt="Screenshot_2026-03-28_09-24-49" src="https://github.com/user-attachments/assets/3f58ef90-09a4-49ac-af4c-bade58a7ed73" />

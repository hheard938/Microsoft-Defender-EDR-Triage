# SOC Investigation Report: Microsoft Defender EICAR Detection
## Case Information
- **Analyst:** Harold Heard
- **Date:** September 10, 2026
- **Tool:** Microsoft Defender Antivirus
- **Alert Type:** Malware Detection
- **Detected Threat:** Virus:DOS/EICAR_Test_File
- **Initial Severity:** Severe
- **Final Status:** Closed – Test File Removed
## Executive Summary
Microsoft Defender Antivirus was tested using the harmless EICAR antivirus test file. EICAR is an industry-standard test signature used to verify that endpoint security tools can detect and respond to simulated malware without using real malicious software.
Defender detected the test file, assigned a Severe rating, quarantined the item, and later removed it. Windows Defender Operational logs were reviewed to verify the detection, remediation, and removal timeline.
## Objective
- Validate Microsoft Defender real-time protection
- Generate a controlled endpoint-security alert
- Review the threat details and severity
- Confirm quarantine and removal
- Correlate the alert with Windows Defender event logs
- Document the incident using a SOC triage workflow
## Tools Used
- Microsoft Defender Antivirus
- Windows Security
- Windows PowerShell
- Windows Event Viewer
- EICAR antivirus test file
## Detection Timeline
- **10:59:31 PM – Event ID 1116:** Microsoft Defender detected the EICAR test file.
- **10:59:48 PM – Event ID 1117:** Microsoft Defender took remediation action.
- **11:08:51 PM – Event ID 1011:** Microsoft Defender deleted the item from quarantine.
## Alert Details
- **Threat name:** Virus:DOS/EICAR_Test_File
- **Category:** Virus
- **Severity:** Severe
- **Affected file:** EICAR.txt
- **Initial response:** Quarantined
- **Final response:** Removed
- **User impact:** None
- **Business impact:** None
## Analysis
The detection was generated intentionally as part of an authorized cybersecurity lab. Microsoft Defender recognized the EICAR signature and prevented the test file from remaining active on the endpoint.
The threat was placed into quarantine, which isolated the file from the operating system. The item was then removed from quarantine. Event Viewer confirmed the detection and response sequence through Event IDs 1116, 1117, and 1011.
No evidence of actual malware execution, persistence, lateral movement, credential access, or data exfiltration was observed.
## Analyst Verdict
**Classification:** Benign positive  
**Severity after investigation:** Informational  
**Disposition:** Closed – Authorized security test  
**Containment:** Successful  
**Remediation:** Test file removed
## Recommended Production Actions
If this detection occurred unexpectedly in a production environment:
1. Confirm the threat name, file path, hash, user, and detection time.
2. Determine how the file entered the environment.
3. Review associated processes and command-line activity.
4. Check the endpoint for related alerts and indicators.
5. Search other endpoints for the same file or hash.
6. Isolate the endpoint if additional malicious activity is present.
7. Remove or quarantine the file.
8. Perform a follow-up scan and document the incident.
## MITRE ATT&CK Relevance
If a similar file were delivered and opened maliciously, the activity could relate to:
- **T1204.002 – User Execution: Malicious File**
This mapping is contextual only. The EICAR file was harmless, intentionally created, and did not represent a real attack.
## Skills Demonstrated
- Endpoint protection monitoring
- Malware-alert triage
- Quarantine and remediation
- Windows Defender event-log analysis
- Event-ID correlation
- PowerShell use
- Incident classification
- SOC investigation documentation
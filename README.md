# Microsoft Defender Antivirus Detection and SOC Triage
## Project Overview
This project documents an authorized endpoint-security lab using Microsoft Defender Antivirus. A harmless EICAR antivirus test file was used to validate detection, quarantine, removal, and Windows event-log correlation.
I investigated the alert, verified the recorded response, and documented the findings using a SOC triage workflow.
**Lab scope:** This project used Microsoft Defender Antivirus and local Windows logs. It did not use Microsoft Defender for Endpoint enterprise EDR capabilities, device isolation, or advanced hunting.
## Objectives
- Verify Microsoft Defender Antivirus protection status
- Investigate an authorized EICAR test-file detection
- Review the threat name, severity, affected file, and response
- Confirm quarantine and removal through event logs
- Correlate detection and remediation timestamps
- Verify the test detection is no longer active
- Document the investigation and final disposition
## Tools Used
- Microsoft Defender Antivirus
- Windows Security
- Windows PowerShell
- Windows Event Viewer
- EICAR antivirus test file
## Detection Summary
| Field | Finding |
|---|---|
| Threat name | Virus:DOS/EICAR_Test_File |
| Defender category | Virus |
| Initial Defender severity | Severe |
| Affected file | EICAR.txt |
| Detection source | Real-Time Protection |
| Associated process | powershell.exe |
| Initial response | Quarantined |
| Final response | Deleted from quarantine |
| Analyst classification | Benign positive — authorized antivirus test |
| Analyst severity | Informational |
| Disposition | Closed — authorized test handled |
The Severe rating was assigned by Defender to the test signature. The analyst classification reflects the authorized lab context. No real malware was used.
## Investigation Workflow
1. Reviewed the detection in Windows Security Protection history.
2. Identified the EICAR signature and affected lab file.
3. Reviewed Defender Operational logs for detection and response events.
4. Confirmed the quarantine action completed successfully.
5. Correlated the detection, quarantine, and deletion timeline.
6. Used PowerShell to verify current protection status and the EICAR threat record.
7. Documented the evidence, conclusions, and limitations.
## Incident Timeline — September 10, 2026
Times are displayed in the endpoint’s local time.
| Time | Evidence | Activity |
|---|---|---|
| 10:59:30 PM | PowerShell detection history | InitialDetectionTime recorded |
| 10:59:31 PM | Event ID 1116 | Defender logged detection of the EICAR test file |
| 10:59:48 PM | Event ID 1117 | Defender successfully quarantined the test file |
| 11:08:51 PM | Event ID 1011 | Defender logged deletion of the item from quarantine |

The detection-history timestamp and Event ID 1116 timestamp differ by one second. Both are retained as recorded.
## PowerShell Investigation Commands
### Verify Antivirus Protection Status
```powershell
Get-MpComputerStatus |
   Select-Object AMRunningMode, AntivirusEnabled, RealTimeProtectionEnabled

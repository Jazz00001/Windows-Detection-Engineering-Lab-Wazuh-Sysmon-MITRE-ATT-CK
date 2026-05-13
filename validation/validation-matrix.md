# Detection Validation Matrix

| ID | Detection | Log Source | Test Method | Custom Rule | MITRE Technique | Status | Evidence |
|---|---|---|---|---|---|---|---|
| DET-001 | PowerShell encoded command execution | Sysmon / Windows process telemetry | `powershell.exe -EncodedCommand` | 100100 | T1059.001 | Detected | `screenshots/evidence/04-powershell-alert.png` |
| DET-002 | Local user account creation | Windows Security logs | Local user creation test | 100101 | T1136.001 | Detected | `screenshots/evidence/05-local-user-created-alert.png` |
| DET-003 | Windows service creation/modification | Windows service / process telemetry | `sc.exe create` test | 100102 | T1543.003 | Detected | `screenshots/evidence/06-service-creation-alert.png` |
| DET-009 | EICAR malware-test file detection | Windows Defender Operational | EICAR test file creation | 100108 | T1204.002 | Detected | `screenshots/evidence/13-eicar-defender-alert.png` |
| DET-010 | Atomic Red Team framework activity | Sysmon Event ID 1 | `Invoke-AtomicTest -ShowDetailsBrief` | 100109 | T1059.001 | Detected | `screenshots/evidence/14-atomic-red-team-alert.png` |

## Notes

This validation matrix only includes detections that were tested and supported with evidence screenshots. Additional detections may be added later after full validation.

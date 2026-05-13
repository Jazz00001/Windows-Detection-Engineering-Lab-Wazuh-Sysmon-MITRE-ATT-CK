# Test Commands

These commands were executed only inside a controlled Windows 10 lab VM. No real malware, credential theft, ransomware, or unauthorized testing was performed.

## DET-001: PowerShell Encoded Command

Run in Windows PowerShell:

```powershell
$Command = 'whoami'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($Command)
$EncodedCommand = [Convert]::ToBase64String($Bytes)
powershell.exe -NoProfile -EncodedCommand $EncodedCommand
```

Expected result:

- Sysmon / Windows telemetry records PowerShell execution.
- Wazuh receives the event.
- Custom rule `100100` fires.

## DET-002: Local User Account Creation

Run in PowerShell as Administrator:

```powershell
New-LocalUser -Name "lab_t1136_test" -NoPassword
Remove-LocalUser -Name "lab_t1136_test"
```

Expected result:

- Windows logs account creation activity.
- Wazuh receives the event.
- Custom rule `100101` fires.

## DET-003: Windows Service Creation / Modification

Run in Command Prompt as Administrator:

```cmd
sc.exe create WazuhLabSvc binPath= "C:\Windows\System32\cmd.exe /c whoami" start= demand
sc.exe delete WazuhLabSvc
```

Expected result:

- Windows logs service creation activity.
- Wazuh receives the event.
- Custom rule `100102` fires.

## DET-009: EICAR Malware-Test File Detection

Run in PowerShell as Administrator:

```powershell
mkdir C:\Users\Public\WazuhMalwareSim
Set-Content -Path "C:\Users\Public\WazuhMalwareSim\eicar.com.txt" -Value 'X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*'
```

Expected result:

- Windows Defender detects or remediates the EICAR test file.
- Wazuh receives the Windows Defender Operational event.
- Custom rule `100108` fires.

## DET-010: Atomic Red Team Framework Activity

Run in PowerShell as Administrator:

```powershell
Install-Module -Name invoke-atomicredteam,powershell-yaml -Scope CurrentUser
Import-Module Invoke-AtomicRedTeam
Invoke-AtomicTest T1059.001 -ShowDetailsBrief
```

Expected result:

- PowerShell/Sysmon telemetry is generated.
- Wazuh captures Atomic Red Team framework activity.
- Custom rule `100109` fires.

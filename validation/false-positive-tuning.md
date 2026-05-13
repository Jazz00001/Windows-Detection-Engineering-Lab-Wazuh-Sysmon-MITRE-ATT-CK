# False Positive Tuning Notes

## DET-001: PowerShell Encoded Command

### Why it matters

PowerShell encoded commands are commonly used by administrators and attackers. Encoded commands can hide script content from casual review.

### Possible false positives

- Administrative scripts
- Software deployment tools
- IT automation

### Tuning approach

- Review parent process.
- Decode and inspect the command.
- Check the user account and endpoint role.
- Tune known approved admin scripts only after verification.

---

## DET-002: Local User Account Creation

### Why it matters

Local account creation can be legitimate administration or attacker persistence.

### Possible false positives

- Helpdesk account setup
- Lab testing
- Local admin maintenance

### Tuning approach

- Review the creator account.
- Check whether the account was added to privileged groups.
- Confirm whether account creation was approved.

---

## DET-003: Windows Service Creation / Modification

### Why it matters

Windows services can be used for persistence and privilege escalation.

### Possible false positives

- Software installation
- Driver updates
- Endpoint management tools

### Tuning approach

- Review service name.
- Review binary path.
- Check parent process.
- Confirm whether service creation occurred during expected maintenance.

---

## DET-009: EICAR Malware-Test File Detection

### Why it matters

EICAR validates whether endpoint malware-detection telemetry is reaching Wazuh from Windows Defender.

### Possible false positives

- Antivirus testing
- SOC validation
- Lab testing

### Tuning approach

- Treat EICAR as test-only activity.
- Keep real Defender detections high priority.
- Exclude approved lab paths only if required.

---

## DET-010: Atomic Red Team Framework Activity

### Why it matters

Atomic Red Team is commonly used by blue teams and purple teams to validate detection coverage. Unexpected use outside approved testing may indicate unauthorized adversary-emulation activity.

### Possible false positives

- Internal SOC testing
- Purple-team exercises
- Detection engineering validation

### Tuning approach

- Allow only approved tester accounts and lab systems.
- Alert when Atomic Red Team activity appears outside approved testing windows.
- Review command line, user account, host, and technique ID.

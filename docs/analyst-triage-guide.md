# Analyst Triage Guide

## General Triage Questions

For every alert, an analyst should ask:

1. Which host generated the alert?
2. Which user account was involved?
3. What command or process triggered the alert?
4. Was this expected administrative or lab activity?
5. Are there related alerts from the same host?
6. Does the activity match a known MITRE ATT&CK technique?

---

## DET-001: PowerShell Encoded Command

### Questions

- Who executed PowerShell?
- What was the parent process?
- Can the encoded command be decoded?
- Was this expected admin activity?

### Triage Steps

1. Review command line.
2. Decode the command if possible.
3. Check parent process.
4. Check user account.
5. Escalate if command appears suspicious or unauthorized.

---

## DET-002: Local User Account Creation

### Questions

- Who created the user?
- What was the created username?
- Was the account added to privileged groups?
- Was the action approved?

### Triage Steps

1. Review account creation event.
2. Check creator account.
3. Check group membership changes.
4. Review later logon activity from the new account.

---

## DET-003: Windows Service Creation / Modification

### Questions

- What service was created?
- What binary path was used?
- What process created the service?
- Was it part of software installation or suspicious persistence?

### Triage Steps

1. Review service name.
2. Review service binary path.
3. Check parent process.
4. Confirm whether software installation was expected.

---

## DET-009: EICAR Malware-Test File Detection

### Questions

- Was EICAR testing expected?
- Which user created or downloaded the file?
- Did Defender detect or remediate it?
- Did Wazuh receive the Defender event?

### Triage Steps

1. Review Wazuh alert.
2. Confirm Defender event ID.
3. Check file path.
4. Confirm whether this was lab testing.
5. Escalate if this appears outside approved testing.

---

## DET-010: Atomic Red Team Framework Activity

### Questions

- Was Atomic Red Team testing approved?
- Which command was executed?
- Which user executed it?
- Was it run on an approved lab endpoint?

### Triage Steps

1. Review command line.
2. Identify technique ID if present.
3. Check user and host context.
4. Confirm whether testing was authorized.
5. Escalate if Atomic Red Team activity appears outside approved scope.

# Tested Environment



This detection engineering project was tested in a local VirtualBox SOC lab.



## Wazuh Server



- Wazuh version: 4.7.5

- OS: Ubuntu Server

- Role: Wazuh manager, dashboard, indexer

- Network: VirtualBox host-only network



## Windows Endpoint



- OS: Windows 10

- Logging: Windows Event Logs + Sysmon

- Agent: Wazuh Windows agent

- Sysmon channel: Microsoft-Windows-Sysmon/Operational



## Linux Endpoint



- OS: Ubuntu 22.04.5

- Agent: Wazuh Linux agent

- Used in the parent SOC lab, but this project focuses mainly on Windows detection engineering.



## Scope



This project validates custom Wazuh detection logic against controlled activity in a lab environment. It is not intended for blind production deployment without tuning.


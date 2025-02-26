# HoneyPot aka Mini Home SOC (Security Operations Center) in Azure

A simple honeypot that logs attacks in real time. I built it by Azure’s free tier resources. Feel free to adapt or improve any part of this!

---

## What This Is

- **Purpose**: Spin up a Windows VM in Azure, intentionally open it to the internet, and watch real attackers try to log in.
- **Key Tools**:
  - **Azure VM**: Our main honeypot (Windows machine).
  - **Log Analytics Workspace**: Collects and stores logs from the VM.
  - **Azure Sentinel**: Acts as a SIEM (Security Information and Event Management) solution, allowing me to visualize and query logs.

---

## Architecture (Simplified)

```text
[Public Internet] 
       |
       v
[ Azure Network Security Group ] -- (Opened Ports) 
       |
       v
[ Windows VM ]  <-- Logs --> [ Log Analytics Workspace ] <---> [ Azure Sentinel ]

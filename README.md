# Honey Pot aka Mini Home SOC (Security Operations Center) in Azure

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


```

## Resource Group & Virtual Network

   - Created a new Resource Group and a new Virtual Network

![Screenshot 2025-02-26 183917](https://github.com/user-attachments/assets/953eba59-623a-4ea0-883c-46a34b9a9ed6)

![Screenshot 2025-02-26 184307](https://github.com/user-attachments/assets/edf86b2e-0e05-4ddf-8b1b-4fe11d9e6a19)

## Windows VM (Honeypot)

   - Deployed a Windows 10 inside the Resource Group and Virtual Network.
   - Disabled the Windows Firewall inside the VM.
   - Modified the Network Security Group to allow **all inbound traffic** (definitely not for production!).

![Screenshot 2025-02-26 184730](https://github.com/user-attachments/assets/7c1b2b10-8f9e-4b26-996e-555109fc5a1a)

![Screenshot 2025-02-26 184553](https://github.com/user-attachments/assets/bd1c334c-7700-47aa-ae92-76234932b34d)

![Screenshot 2025-02-26 184620](https://github.com/user-attachments/assets/264d46c0-6b43-489b-bbe6-a2706f6d16fb)

![Screenshot 2025-02-26 185241](https://github.com/user-attachments/assets/7041eb0a-4e13-427f-a488-25e30b7d496d)

## Log Analytics Workspace

   - Created a new Log Analytics Workspace in the same Resource Group.
   - Installed the Azure Monitoring Agent on the VM (via Sentinel’s Data Connector) to forward security logs.
   - Used a KQL query to output only failed logon attempts (EventID: 4625)

![Screenshot 2025-02-26 185241](https://github.com/user-attachments/assets/a2cd326e-bd86-440a-bee1-10b833ea360a)


## Azure Sentinel (SIEM)

   - Attached Sentinel to the Log Analytics Workspace.
   - Connected Windows Security Events data via **Azure Monitoring Agent**.
   - Used an open source .csv file and .json query to map the location of the attacks on Sentinal Workbooks.

![Screenshot 2025-02-26 185604](https://github.com/user-attachments/assets/514f7084-fe24-42f8-b089-51e54f333008)



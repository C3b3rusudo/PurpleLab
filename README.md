PurpleLab: Enterprise Cyber Range & Automated Detection Sandbox

Summary
PurpleLab is a self-contained, enterprise-grade Purple Team simulation environment built within an isolated virtual network. The project bridges the gap between infrastructure engineering, automated adversary emulation (Red Team), and high-fidelity detection engineering (Blue Team). 

By building this range, I simulated the entire lifecycle of a cyber attack—from initial endpoint intrusion to centralized SIEM log detection.

Network 
The environment consists of a segregated Class C private subnet (`10.0.0.0/24`) running inside Oracle VirtualBox:

* **Domain Controller (DC01):** Windows Server (`10.0.0.4`) running Active Directory Domain Services (AD DS) and centralized DNS for the `lab.local` enterprise domain.
* **Adversary Emulation (Caldera-Svr):** Ubuntu Linux (`10.0.0.11`) hosting the MITRE Caldera Command and Control (C2) framework.
* **SIEM & Logging (Splunk-Svr):** Ubuntu Linux (`10.0.0.10`) running Splunk Enterprise for centralized security telemetry aggregation.
* **Target Endpoint (Win-Victim-01):** Windows workstation (`10.0.0.100`) joined to the `lab.local` domain, monitored via advanced telemetry, with defenses intentionally modified for simulation testing.

##Key Technical Achievements & Engineering Highlights

### 1. Source Code Refactoring (Python 3.14 Compatibility Patch)
During the deployment of the MITRE Caldera C2 framework on a cutting-edge Python 3.14 backend, I encountered a critical upstream event-loop lifecycle conflict with the `asyncio` library. 
* **Solution:** Programmatically refactored and patched the core framework source code (`rest_svc.py`) utilizing a custom fallback block to dynamically spawn loops, bypassing the environment-breaking changes and stabilizing the C2 engine.
* **Environment Management:** Isolated the entire application layer using a Python Virtual Environment (`venv`) to ensure strict dependency control.

### 2. End-to-End Log Pipeline Engineering
* Deployed **Microsoft Sysmon** across domain endpoints using a customized security baseline configuration to capture high-definition process and network telemetry.
* Configured and deployed the **Splunk Universal Forwarder** to securely stream Windows Event Logs and Sysmon data across the internal network into the Splunk indexing tier.

## Simulated Attack Campaigns & Detection Use Cases

### Use Case 1: Local Discovery & Reconnaissance Detection
* **Red Team Operation:** Automated an initial access campaign via Caldera utilizing the `Sandcat` agent to run system discovery commands (`whoami`, `net user`, `ipconfig /all`).
* **Blue Team Detection:** Authored custom Splunk Search Processing Language (SPL) queries to flag non-administrative user accounts executing binary profiling utilities.

## Competencies Demonstrated
* **Systems & Identity Administration:** Active Directory, DNS management, Group Policy Object (GPO) structure, Windows Server management.
* **DevOps & Scripting:** Python source code modification, virtual environments (`venv`), network port-forwarding mapping.
* **Security Operations:** SIEM engineering (Splunk), advanced endpoint logging (Sysmon), Command & Control (C2) frameworks (MITRE Caldera).

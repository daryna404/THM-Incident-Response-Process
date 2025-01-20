# THM-Incident-Response-Process

**Objective**
To simulate the role of an Incident Response Team (IRT) member by investigating and resolving a potential security incident on a Windows workstation. The scenario involved a suspected crypto miner impacting system performance and making unauthorized outbound connections.

**Scenario Overview**
A user reported their laptop had become extremely slow, prompting the IT team to identify unusual CPU usage. After further investigation, the SOC team observed anomalous outbound connections from the workstation's IP address to a suspicious destination. The incident was escalated to the Incident Response Team for analysis and remediation.

**Skills and Tools Utilized**

**Skills:** Incident analysis, malware identification, IoC documentation, remediation planning.

**Tools:** Windows Task Manager, netstat, Microsoft Edge, Registry Editor, Microsoft VBA Editor.

# Step-by-Step Process
**Step 1: Detection**
Verified the user's report by logging into the affected machine and observing performance degradation.

Opened Task Manager to check for processes consuming high CPU resources.

Identified an unusual process with a random name (3d33es454e.exe) consuming most of the CPU.
Checked the process's properties and found that it was running from the temporary folder—a common sign of malware.

<img width="331" alt="image" src="https://github.com/user-attachments/assets/cc6912c5-9ac6-471f-bef6-fb4fecd521a0" />

Process properties window confirming its temporary folder location.

**Step 2: Analysis**

Retrieved the Process ID (PID) of the suspicious process using Task Manager.

Used the netstat command in Command Prompt to identify outbound connections from the process.

Discovered frequent connections to a suspicious IP address and random port.

<img width="358" alt="image" src="https://github.com/user-attachments/assets/a9a3d39d-edbd-46ac-8649-c06924e7cfcb" />

Reviewed browser download history in Microsoft Edge:

<img width="466" alt="image" src="https://github.com/user-attachments/assets/b3ecafd9-9a5a-479d-9cd0-5d64efcb15d9" />

Identified a suspicious macro-enabled Word document downloaded from a questionable link.
Opened the document and analyzed the embedded macro using the Microsoft VBA Editor:

<img width="370" alt="image" src="https://github.com/user-attachments/assets/d2397f33-cc58-4552-bdac-435efa12a915" />

Found malicious code that downloaded and executed the suspicious process.
Identified registry modifications to ensure persistence.

**Step 3: Containment**

Disconnected the workstation from the organizational network to prevent malware spread.

Ended the suspicious process using Task Manager.

**Step 4: Eradication**

Deleted the malicious executable (3d33es454e.exe) from the temporary folder.

Removed the malicious macro-enabled document from the downloads folder.

Cleared the browser download history to avoid re-execution.

Opened the Registry Editor to locate and delete the persistence entry under the Run registry key.

<img width="462" alt="image" src="https://github.com/user-attachments/assets/22b2ac7b-8ff2-45fc-9587-23a4b9d60563" />

**Step 5: Post-Incident Activities**

**Documented Indicators of Compromise (IoCs):**
Malicious IP address and port.
URL of the downloaded macro-enabled document.
Hash of the malware executable.

**Recommended updates to the Incident Response Plan:**

Implementing Endpoint Detection and Response (EDR) to detect threats like crypto miners.
Introducing web-browsing controls to prevent access to malicious sites.
Conducting mandatory employee training on the dangers of macro-enabled files and phishing attacks.

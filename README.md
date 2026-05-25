# Project-Network-Traffic-Incident-Analysis
Objective: Identify an infected Windows host and attribute it to a specific user account using packet-level analysis.
Link to lab: https://www.malware-traffic-analysis.net/2026/02/28/index.html
1. Scenario Background
I acted as a SOC analyst investigating NetSupport Manager RAT activity. The traffic, originating from 45.131.214.85 on TCP port 443, was detected starting at 19:55 UTC. My goal was to identify the internal host responsible for this traffic to stop the ongoing communication.

2. Investigation Workflow
A. Network Traffic Analysis
I used the following Wireshark display filter to isolate malicious traffic: (http.request or tls.handshake.type eq 1) and !(ssdp) and ip.addr eq 45.131.214.85.
The analysis revealed multiple POST requests to http://45.131.214.85/1, confirming consistent communication between the internal host and the malicious server.<img width="1941" height="1263" alt="Screenshot 2026-05-25 195049" src="https://github.com/user-attachments/assets/833de01a-8e10-4313-9799-f8e696be6044" />


B. Victim Host Identification
I pivoted the investigation to the internal IP address 10.2.28.88, which was the source of the malicious traffic.
By filtering for nbns traffic, I identified the following host details:
  Host Name: DESKTOP-TEYQ2NR
  MAC Address: 00:19:d1:b2:4d:ad
  <img width="1936" height="1197" alt="Screenshot 2026-05-25 201143" src="https://github.com/user-attachments/assets/51059482-7731-44a2-97f4-ec810410504d" />

C. User AttributionI filtered for kerberos.CNameString to extract user account information.  
The analysis identified the account brolf.  
I used the Find Packet... function to search for the string "Rolf" within the packet details to confirm the full user name: Becka Rolf.  
<img width="1934" height="1244" alt="Screenshot 2026-05-25 201328" src="https://github.com/user-attachments/assets/6c273898-a2f8-4ae3-b9d7-7d1b49b688e2" />
<img width="1107" height="1268" alt="Screenshot 2026-05-25 201358" src="https://github.com/user-attachments/assets/071ac32a-7df4-4ab4-a18d-5bd0bc5f3943" />
<img width="1914" height="1237" alt="Screenshot 2026-05-25 201402" src="https://github.com/user-attachments/assets/4093ef2a-e980-42c5-91c3-a029bdc4d480" />
<img width="1919" height="1238" alt="Screenshot 2026-05-25 201416" src="https://github.com/user-attachments/assets/c96f0c40-2283-4ba1-b5ba-496ec5701af3" />
<img width="1892" height="1188" alt="Screenshot 2026-05-25 201537" src="https://github.com/user-attachments/assets/21b3d381-9ad5-4cdd-a1f9-8f61418f44b8" />

3. Summary of Findings
Infected IP: 10.2.28.88
Hostname: DESKTOP-TEYQ2NR
MAC Address: 00:19:d1:b2:4d:ad
Account Name: brolf
User Name: Becka Rolf

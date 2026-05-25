# Project-Network-Traffic-Incident-Analysis
Objective: Identify an infected Windows host and attribute it to a specific user account using packet-level analysis.
<img width="1892" height="1188" alt="Screenshot 2026-05-25 201537" src="https://github.com/user-attachments/assets/2063fc2a-4def-400f-946e-ff062dbfe490" />

1. Scenario Background
I acted as a SOC analyst investigating NetSupport Manager RAT activity. The traffic, originating from 45.131.214.85 on TCP port 443, was detected starting at 19:55 UTC. My goal was to identify the internal host responsible for this traffic to stop the ongoing communication.

2. Investigation Workflow
A. Network Traffic Analysis
I used the following Wireshark display filter to isolate malicious traffic: (http.request or tls.handshake.type eq 1) and !(ssdp) and ip.addr eq 45.131.214.85.
The analysis revealed multiple POST requests to http://45.131.214.85/1, confirming consistent communication between the internal host and the malicious server.

B. Victim Host Identification
I pivoted the investigation to the internal IP address 10.2.28.88, which was the source of the malicious traffic.
By filtering for nbns traffic, I identified the following host details:
  Host Name: DESKTOP-TEYQ2NR
  MAC Address: 00:19:d1:b2:4d:ad

C. User AttributionI filtered for kerberos.CNameString to extract user account information.  
The analysis identified the account brolf.  
I used the Find Packet... function to search for the string "Rolf" within the packet details to confirm the full user name: Becka Rolf.  

3. Summary of Findings
Infected IP: 10.2.28.88
Hostname: DESKTOP-TEYQ2NR
MAC Address: 00:19:d1:b2:4d:ad
Account Name: brolf
User Name: Becka Rolf
<img width="1919" height="1238" alt="Screenshot 2026-05-25 201416" src="https://github.com/user-attachments/assets/bfe88dff-0d03-4c2e-8686-1ff3ce11993d" />
<img width="1914" height="1237" alt="Screenshot 2026-05-25 201402" src="https://github.com/user-attachments/assets/b1da85d9-093c-4c8f-a184-0ad62826b742" />
<img width="1107" height="1268" alt="Screenshot 2026-05-25 201358" src="https://github.com/user-attachments/assets/5b9bfcc5-a047-4195-a44a-15f46364126b" />
<img width="1934" height="1244" alt="Screenshot 2026-05-25 201328" src="https://github.com/user-attachments/assets/05f02f8d-6a64-4823-9ed2-a3ebe44faad6" />
<img width="1936" height="1197" alt="Screenshot 2026-05-25 201143" src="https://github.com/user-attachments/assets/e8695d42-9c53-447d-887a-a157703711f9" />
<img width="1924" height="1252" alt="Screenshot 2026-05-25 195830" src="https://github.com/user-attachments/assets/fb2d9f71-c514-4498-b5fb-df87d080367c" />
<img width="1941" height="1263" alt="Screenshot 2026-05-25 195049" src="https://github.com/user-attachments/assets/7e16a1f4-a168-4e51-9a90-951b7985500f" />

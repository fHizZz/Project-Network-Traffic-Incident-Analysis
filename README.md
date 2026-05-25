# Project-Network-Traffic-Incident-Analysis
Objective: Identify an infected Windows host and attribute it to a specific user account using packet-level analysis.

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

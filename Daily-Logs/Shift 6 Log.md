![alt text](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/ed374f0c351733e2dc3441614a35c0bba4949763/Daily-Logs/Shift%20Review/Shift%20Recap.png)

# Shift 6 Report: Multi-Stage Malware Analysis
### Date: May 13th, 2026
### Shift: Extended


### **Executive Summary**
- Week 2 involved intensive static, dynamic analysis of `unknown.exe` (knwon as SikoMode). The mission successfully deconstructed a multi-stage infection, leveraging process injection, QUIC protocol for C2, and memory payload delivery. Overcoming technical hurdles, the full second-stage PowerShell C2 client wa captured. This week was a successful completion of Incident Report #2 and one BTLO investigation.

### Technical Engineering & Analysis Wins
1. Splunk Correlation & Lookups
- Advacne spunk skills throuhg Udemy Modules 5 through 6. Applied `transaction` commands for host/network telemetry correlation and preapre for threat intelligence intergration.

2. Controlled Internet Leak (SikoMode)
- Successfully executed the high-risk procedure to temporarily enable internet access via pfSense for `unknown.exe` (Siko Mode).
- Firewall rule surgically adapted new C2 IPs (dynamic ip addresses) and protocol (QUIC/UDP 443).

3. Second-Stage Payload Capture & Decryption
**In-Memory Identification** 
- Located the Base64 encoded, compressed PowerShell script in the `CommandLine` of `powershell.exe` (Sysmon EventID 1) in Splunk.

**QUIC Extraction**
- Overcame Wireshark dissector failures by performing raw UDP stream extraction and reassembly.

**Encryption Identification**
- Successfully identified the encryption of the payload (Base64 then Gzip) using CyberChef.
- Need the XOR key to fully decrypt the second-stage payload.

### Obstacles & Resolutions
**QUIC Payload Extraction** 
- Wireshark's QUIC dissector failed to reassemble the fragmented payload.
  
**Resolution** 
- Pivoted to raw UDP stream extraction, followed by manual Base64 and Gzip decompression in CyberChef.

**pfSense Firewall Adaptation**
- Malware's dynamic C2 IP pivots (`142.250.100.94`, etc.) required rapid adaptation of pfSense rules for multi-protocol (TCP/UDP) and multi-port (443, 53) access to new C2 IPs.

**Resolution**
- Implemented granular `Pass` rules for specific C2 IPs and ports, ensuring payload capture while maintaining overall isolation.

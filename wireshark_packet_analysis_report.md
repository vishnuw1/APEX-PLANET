# Wireshark Network Analysis and Attack Simulation Report

**Date:** September 19, 2025
**Analyst:** Pratham Khairmode
**Objective:** To capture and analyze common network protocols (HTTP, DNS, FTP), identify security vulnerabilities in unencrypted protocols, and simulate and analyze a TCP SYN Flood Denial-of-Service (DoS) attack.

---

## 1. Tools Used 

* **Wireshark:** A network protocol analyzer used for capturing and inspecting network traffic.
* **hping3:** A command-line packet crafting tool used for network testing and attack simulation.
* **Operating System:** Kali Linux (running in a VirtualBox VM).

---

## 2. Methodology and Procedures

The analysis was conducted in three distinct phases.

### ### Phase 1: Basic Protocol Capture and Filtering

1.  **Capture Initiation:** A live packet capture was started in Wireshark on the primary network interface (`eth0`).
2.  **Traffic Generation:**
    * **DNS & HTTP:** A web browser was used to visit `http://http.net` to generate DNS query/response and HTTP GET/response traffic.
    * **FTP:** An FTP client was used to connect to a public FTP server (`ftp.debian.org`) to generate FTP command and control traffic.
3.  **Filtering:** The capture was stopped, and display filters were applied to isolate and inspect the traffic for each protocol individually:
    * `dns`: Revealed the domain-to-IP resolution process.
    * `http`: Showed the plaintext requests for web content.
    * `ftp`: Displayed the command channel for the FTP session.

### ### Phase 2: FTP Credential Analysis

1.  **Objective:** To demonstrate the insecurity of unencrypted protocols.
2.  **Procedure:**
    * The `ftp` display filter was applied to the capture from Phase 1.
    * The packet list was inspected to locate the user authentication sequence, specifically the `USER` and `PASS` commands.
    * Wireshark's **"Follow > TCP Stream"** feature was used on a relevant packet.
3.  **Findings:** The TCP stream view displayed the entire FTP session in raw text, **exposing the username and password in plaintext**. This successfully demonstrated the critical vulnerability of transmitting credentials over an unencrypted channel.

### ### Phase 3: SYN Flood Simulation and Analysis

1.  **Objective:** To simulate a SYN flood DoS attack and identify its signature on the network.
2.  **Simulation:**
    * A new Wireshark capture was initiated with the display filter `tcp.flags.syn == 1 and tcp.flags.ack == 0` pre-applied to isolate incoming connection requests.
    * The `hping3` tool was used from the terminal to launch the attack against the local machine's IP (`10.0.2.15`).
    * **Command Used:** `sudo hping3 -S --flood -V 10.0.2.15`
3.  **Analysis of Captured Data:** The Wireshark capture presented a clear and definitive signature of the attack:
    * **High Volume of SYN Packets:** The packet list was saturated with TCP packets flagged as `[SYN]`, indicating a flood of new connection requests.
    * **Single Destination IP:** All malicious packets were directed to the target IP address, `10.0.2.15`.
    * **Spoofed Source IPs:** A key finding was that the source IP address for each packet was randomized. This is a classic attack technique to hide the attacker's origin and prevent the target from completing the three-way handshake, as its `SYN-ACK` replies are sent to non-existent or incorrect hosts.

---

## 3. Conclusion and Key Takeaways

This exercise successfully demonstrated fundamental network analysis techniques and highlighted critical security concepts.

1.  **Protocol Insecurity:** The FTP analysis serves as a powerful reminder that any data, especially credentials, sent over unencrypted protocols is easily intercepted. **Secure alternatives like SFTP or FTPS are mandatory for secure file transfer.**
2.  **DoS Attack Signature:** The SYN flood simulation showed a clear, identifiable pattern in Wireshark. Understanding this signature (a flood of SYN packets from varied, spoofed source IPs to a single destination) is crucial for network defenders in identifying and mitigating DoS attacks.
3.  **Value of Packet Analysis:** Wireshark proves to be an indispensable tool for network troubleshooting, performance analysis, and, most importantly, cybersecurity defense by providing direct visibility into network activity.
# Task 2: Nmap Scan Analysis - Metasploitable2

This document details the Nmap port and service scan performed on the Metasploitable2 virtual machine as part of Task 2: Network Security & Scanning for the ApexPlanet internship program. The objective was to identify open ports, running services, and the operating system of the target.

* **Target IP Address:** 192.168.56.4 (Metasploitable2 VM)
* **Scanning Machine:** Kali Linux VM (your Kali machine's IP, e.g., 192.168.56.x)

The Nmap command executed was: nmap -sS -sV -O 192.168.56.4

-sS: Performed a TCP SYN Stealth Scan. This method is faster and less likely to be logged by non-IDS firewalls.
-sV: Attempted to determine service/version info for open ports.
-O: Enabled OS detection.

 **Raw Nmap Output**

──(kali㉿kali)-[~]
└─$ nmap -sS -sV -O 192.168.56.4
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-17 11:54 EDT
Nmap scan report for 192.168.56.4
Host is up (0.025s latency).
Not shown: 976 closed tcp ports (reset)
PORT      STATE SERVICE     VERSION
21/tcp    open  ftp         vsftpd 2.3.4
22/tcp    open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp    open  telnet      Linux telnetd
25/tcp    open  smtp        Postfix smtpd
53/tcp    open  domain      ISC BIND 9.4.2
80/tcp    open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp   open  rpcbind     2 (RPC #100000)
139/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp   open  exec        netkit-rsh rexecd
513/tcp   open  login
514/tcp   open  shell       Netkit rshd
1099/tcp  open  java-rmi    GNU Classpath grmiregistry
1524/tcp  open  bindshell   Metasploitable root shell
2049/tcp  open  nfs         2-4 (RPC #100003)
2121/tcp  open  ftp         ProFTPD 1.3.1
3306/tcp  open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp  open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp  open  vnc         VNC (protocol 3.3)
6000/tcp  open  X11         (access denied)
6667/tcp  open  irc         UnrealIRCd
8009/tcp  open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp  open  http        Apache Tomcat/Coyote JSP engine 1.1
44176/tcp open  status      1 (RPC #100024)
MAC Address: 08:00:27:EF:74:9B (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6
OS details: Linux 2.6.9 - 2.6.33
Network Distance: 1 hop
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 32.97 seconds

## Analysis of Findings

The Nmap scan against Metasploitable2 (192.168.56.4) successfully identified numerous open ports and services, confirming its intentionally vulnerable nature.

### **Key Open Ports and Services:**

The scan revealed a significant number of open TCP ports, indicating various services running on the target. Notable findings include:

* **Port 21 (FTP):** Running `vsftpd 2.3.4`. This specific version is known to have a backdoor vulnerability, making it a prime target for exploitation.
* **Port 22 (SSH):** Running `OpenSSH 4.7p1 Debian 8ubuntu1`. This is an older version of OpenSSH, which might contain exploitable vulnerabilities.
* **Port 23 (Telnet):** Running `Linux telnetd`. Telnet transmits data, including credentials, in plaintext, posing a significant security risk.
* **Port 80 (HTTP):** Running `Apache httpd 2.2.8 ((Ubuntu) DAV/2)`. An outdated version of Apache, likely susceptible to various web server vulnerabilities.
* **Ports 139 & 445 (SMB/NetBIOS):** Running `Samba smbd 3.X - 4.X`. Samba services are often targeted for vulnerabilities like remote code execution.
* **Port 1524 (Bindshell):** Identified as `Metasploitable root shell`. This is a critical vulnerability, as it provides a direct root-level shell access if exploited.
* **Port 3306 (MySQL):** Running `MySQL 5.0.51a-3ubuntu5`. An older version of MySQL, potentially vulnerable to known exploits and weak authentication.
* **Port 5432 (PostgreSQL):** Running `PostgreSQL DB 8.3.0 - 8.3.7`. Another outdated database service.
* **Port 8180 (HTTP):** Running `Apache Tomcat/Coyote JSP engine 1.1`. An older Tomcat version, likely having web application vulnerabilities.

### **Operating System Detection:**

Nmap successfully identified the target's operating system as `Linux 2.6.9 - 2.6.33`, which is consistent with the Metasploitable2 environment. This information is crucial for selecting appropriate exploits during later phases.

### **Security Implications:**

The presence of numerous outdated and insecure services (like vsftpd 2.3.4, old OpenSSH, Telnet, and the Metasploitable root shell) highlights the severe vulnerability posture of the target machine. These findings suggest multiple potential entry points for attackers, ranging from credential sniffing to remote code execution.

This scan provides a solid foundation for further vulnerability assessment and penetration testing.

## Conclusion

The Nmap scan was highly effective in enumerating the services and identifying the operating system of the Metasploitable2 target. The findings clearly illustrate the various vulnerabilities inherent in this intentionally insecure system, setting the stage for the next phase of vulnerability analysis using tools like OpenVAS.

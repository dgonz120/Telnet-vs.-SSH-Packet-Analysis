# Telnet vs. SSH Packet Analysis

## Lab Overview
Telnet and Secure Shell (SSH) are network protocols used to remotely access and manage systems over a network. Telnet operates over TCP port 23 and transmits all data, including usernames and passwords, in clear text, making it vulnerable to interception and eavesdropping attacks. In contrast, SSH operates over TCP port 22 and uses encryption to secure all data transmitted between a client and a server.

This lab demonstrates the security differences between clear-text and encrypted remote administration protocols by capturing and analyzing live traffic in Wireshark.

## Lab Objectives & Environment
* **Course:** NWIT 291 (Instructor: Christopher Foster)
* **Objectives:** Establish Telnet and SSH connections to a vulnerable system, capture network traffic using Wireshark, observe clear-text credentials in Telnet traffic, and analyze encrypted traffic in SSH sessions.
* **Tools & Environment:** Kali Linux, Metasploitable, PuTTY, Wireshark, VirtualBox NAT Network.

| Machine | Operating System | Interface | IP Address |
| :--- | :--- | :--- | :--- |
| Kali Linux (Attacker) | Kali Linux | eth0 | 10.0.2.15 |
| Metasploitable (Target) | Metasploitable | — | 10.0.2.3 |

Both machines were configured on the same virtual network to allow communication.

---

## Part 1 – Setup & Network Verification
PuTTY was installed on the Kali Linux system using the Advanced Package Tool (APT) to establish remote connections.

```bash
sudo apt update
sudo apt install putty -y

```
<img width="747" height="588" alt="image" src="https://github.com/user-attachments/assets/4a5b65a2-21bd-416d-b887-8b3f1566d582" />

Connectivity between Kali Linux and Metasploitable was verified using the `ping` command to ensure both machines were on the same subnet. Wireshark was then launched on the `eth0` interface to capture packets across both sessions.

---

## Part 2 – Telnet Session Analysis

A Telnet connection was initiated from Kali Linux to the Metasploitable machine using PuTTY over TCP port 23.

PuTTY configured for Telnet on port 23 targeting 10.0.2.3

> *PuTTY Configuration for Telnet Connection.*
<img width="728" height="671" alt="image" src="https://github.com/user-attachments/assets/424309e1-d601-41d6-aa4c-c71c32de52bb" />

After logging in with valid credentials, the traffic was captured and analyzed in Wireshark by following the TCP stream, exposing the unencrypted username and password.

> *Telnet TCP Stream (Clear-Text Credentials).*
<img width="881" height="430" alt="image" src="https://github.com/user-attachments/assets/990ddc7e-f992-4717-9fc5-7df5682dd424" />
---

## Part 3 – SSH Session Analysis

An SSH connection was initiated from Kali Linux to the Metasploitable machine using PuTTY over TCP port 22.

PuTTY configured for SSH on port 22 targeting 10.0.2.3

> *PuTTY Configuration for SSH Connection.*
<img width="632" height="583" alt="image" src="https://github.com/user-attachments/assets/571fc93d-8b6e-4a08-a671-ea5febb60183" />

The SSH traffic was analyzed in Wireshark by following the TCP stream, confirming that all communication was securely encrypted with no readable credentials visible.


> *SSH TCP Stream (Encrypted Traffic).*
<img width="770" height="658" alt="image" src="https://github.com/user-attachments/assets/1e92f193-69c6-4c15-81bb-1b55ca09386c" />
---

## Results & Conclusion

The lab clearly demonstrated the severe vulnerabilities associated with legacy unencrypted protocols. The Telnet session exposed sensitive authentication data in plain text, whereas the SSH session successfully protected data confidentiality and integrity through encryption.

* **Key Takeaway:** Verified protocol security differences using Wireshark packet capture; demonstrated that Telnet transmits credentials in clear-text while SSH secures all remote administrative sessions.

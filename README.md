# Wireshark Network Traffic Analysis

## Project Overview

This project documents practical network traffic analysis performed using Wireshark on PCAP files containing suspicious and malicious network activity.

The investigations involved analysing network packets, applying Wireshark display filters, identifying suspicious communication patterns and interpreting network behaviour to determine potential security threats.

Two packet captures were investigated:

1. TCP/IP reconnaissance and port scanning activity
2. FTP brute-force authentication activity

Each investigation contains detailed findings, Wireshark filters, security analysis and screenshot evidence from the packet captures.

---

## Tools & Technologies

- Wireshark
- PCAP network captures
- TCP/IP
- ICMP
- FTP
- Wireshark display filters
- Network traffic analysis
- Network security analysis

---

# Investigations

## 1. PCAP 1 — Reconnaissance and TCP Port Scan

[View full PCAP 1 investigation](pcap1-port-scan/README.md)

Analysis of the first packet capture identified network reconnaissance activity followed by TCP port scanning.

### Key Findings

- ICMP Echo traffic consistent with host discovery
- Large numbers of TCP SYN packets targeting multiple destination ports
- TCP RST/ACK responses associated with closed ports
- Traffic patterns consistent with systematic network reconnaissance

### Techniques Used

- ICMP traffic analysis
- TCP flag analysis
- SYN packet filtering
- TCP reset analysis
- Source and destination IP analysis
- Wireshark display filtering

### Example Wireshark Filters

```text
ip.addr == 192.168.56.104 && ip.addr == 192.168.56.101
```

```text
ip.src == 192.168.56.104 && ip.dst == 192.168.56.101 && tcp.flags.syn == 1 && tcp.flags.ack == 0
```

```text
tcp.flags.reset == 1
```

📁 **Full investigation and evidence:**  
[PCAP 1 — Reconnaissance and TCP Port Scan Analysis](pcap1-port-scan/README.md)

---

## 2. PCAP 2 — FTP Brute Force Attack

[View full PCAP 2 investigation](pcap2-ftp-brute-force/README.md)

Analysis of the second packet capture identified repeated FTP authentication attempts consistent with automated password guessing or brute-force activity.

### Key Findings

- Repeated FTP `USER` commands
- Large numbers of different password attempts
- Repeated FTP `530 Login incorrect` responses
- Authentication behaviour consistent with automated password guessing
- Identification of the suspected attacking host and FTP server

### Techniques Used

- FTP protocol analysis
- Authentication traffic analysis
- FTP response-code filtering
- Source and destination IP analysis
- Wireshark display filtering
- Correlation of requests and server responses

### Example Wireshark Filters

```text
ftp.request.command == USER or ftp.request.command == PASS
```

```text
ftp.response.code == 530
```

📁 **Full investigation and evidence:**  
[PCAP 2 — FTP Brute Force Attack Analysis](pcap2-ftp-brute-force/README.md)

---

# Skills Demonstrated

Through these investigations, I developed practical experience in:

- Analysing PCAP files using Wireshark
- Investigating suspicious network traffic
- Applying Wireshark display filters
- Analysing TCP/IP communication
- Interpreting TCP flags
- Identifying ICMP host discovery
- Detecting TCP port scanning
- Analysing FTP authentication traffic
- Identifying brute-force and password-guessing behaviour
- Correlating network requests and responses
- Identifying attacker and target systems
- Documenting network security findings

---

# Security Concepts Demonstrated

These investigations demonstrate practical understanding of several cybersecurity concepts, including:

- Network reconnaissance
- Port scanning
- TCP connection behaviour
- Network protocol analysis
- Authentication attacks
- Brute-force attacks
- Network-based threat detection
- Indicators of suspicious network activity

---

# Repository Structure

```text
Wireshark-network-traffic-analysis/
│
├── pcap1-port-scan/
│   ├── evidence/
│   │   ├── pcap1-icmp-reconnaissance.png
│   │   ├── pcap1-syn-port-scan.png
│   │   └── pcap1-tcp-resets.png
│   └── README.md
│
├── pcap2-ftp-brute-force/
│   ├── evidence/
│   │   ├── pcap2-ftp-user-pass-attempts.png
│   │   └── pcap2-ftp-530-failures.png
│   └── README.md
│
└── README.md
```

---

# Key Learning

This project strengthened my ability to investigate network traffic from a cybersecurity perspective rather than simply inspecting individual packets.

By analysing communication patterns across the packet captures, I was able to identify reconnaissance, port scanning and repeated authentication attempts and use network evidence to explain why the behaviour was potentially malicious.

The investigations also improved my understanding of how Wireshark filters can be used to isolate relevant traffic and support structured network security investigations.

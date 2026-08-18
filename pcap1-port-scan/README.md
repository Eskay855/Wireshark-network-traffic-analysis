# PCAP 1 — Reconnaissance and TCP Port Scan Analysis

## Overview

This investigation involved analysing network traffic in Wireshark to identify potentially suspicious or malicious behaviour within a packet capture.

Analysis identified ICMP host discovery activity followed by TCP SYN packets targeting numerous destination ports, consistent with network reconnaissance and TCP port scanning.

## Tools

- Wireshark
- PCAP network capture
- Wireshark display filters
- TCP/IP and ICMP protocol analysis

## Key Hosts

| Role | IP Address |
|---|---|
| Scanning host | 192.168.56.104 |
| Target host | 192.168.56.101 |

## Finding 1 — ICMP Reconnaissance

ICMP Echo requests were observed from `192.168.56.104` to `192.168.56.101`, with the target responding with ICMP Echo replies.

This traffic is consistent with host discovery activity occurring before the subsequent port scan.

### Wireshark Filter

```text
icmp && ip.addr == 192.168.56.104 && ip.addr == 192.168.56.101
```

## Finding 2 — TCP SYN Port Scan

A large number of TCP SYN packets were observed from `192.168.56.104` to `192.168.56.101`.

The packets targeted numerous destination ports while using the same source port. The SYN flag was set without the ACK flag, showing repeated attempts to initiate TCP connections across different ports.

This traffic pattern is consistent with TCP SYN port scanning used to identify accessible services on a target system.

### Wireshark Filter

```text
ip.src == 192.168.56.104 && ip.dst == 192.168.56.101 && tcp.flags.syn == 1 && tcp.flags.ack == 0
```

## Finding 3 — TCP Reset Responses

The target returned numerous TCP `RST, ACK` responses to the scanning host. These responses indicate that many of the probed TCP ports rejected the connection attempts.

### Wireshark Filter

```text
tcp.flags.reset == 1
```

## Conclusion

The packet capture contains network reconnaissance activity originating from `192.168.56.104` and targeting `192.168.56.101`.

ICMP communication was observed before repeated TCP SYN probes were sent across numerous destination ports. The target returned TCP reset responses for many of these probes.

Taken together, the traffic pattern is consistent with host discovery followed by TCP SYN port scanning.

## Skills Demonstrated

- Network traffic analysis
- Wireshark
- PCAP analysis
- TCP/IP analysis
- ICMP analysis
- Wireshark display filtering
- Network reconnaissance detection
- Port scan identification
- Evidence-based security analysis

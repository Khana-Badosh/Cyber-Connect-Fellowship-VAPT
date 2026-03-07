# Snort - Network Intrusion Detection & Prevention System

<br/>

## Introduction
Snort is a widely deployed open-source Network Intrusion Detection and Prevention System (NIDS/NIPS). It was created by Martin Roesch in 1998 as a packet sniffer, that eventually evolved into an IDS/IPS which was later acquired by Cisco in 2013. It works by performing real-time traffic analysis and packet logging, using a rule-based language to identify malicious activity.

## Objectives
The goal of this project is to move beyond theory and gain hands-on experience with industry-standard security tools. My specific objectives are:
- **System Deployment:** Successfully install and configure Snort on a Linux Virtual Machine.
- **Environment Setup:** Define and monitor a specific network to capture traffic.
- **Rule Engineering:** Write and test custom detection rules to identify unauthorized network activity.
- **Log Analysis:** Generate and analyze real-time alerts.
- **Validation:** Confirm the deployment works by triggering alerts through simulated network.


## What are IDS and IPS
In the world of cybersecurity, IDS (Intrusion Detection System) and IPS (Intrusion Prevention System) are the "security guards" of a network. Both use three primary methods to identify threats. Most modern systems use a hybrid of these.
1. Signature-Based Detection: 
   > It compares network traffic against a database of signatures, which are essentially digital fingerprints of known malware or attack patterns. Although its fast and accurate this approach often fails against new or zero-day attacks.
2. Anomaly-Based Detection: 
   > The system builds a baseline of what normal network traffic looks like (e.g., typical bandwidth usage, common protocols). This approach can detect new unknown attacks based on them being novel but ends up being prone to false positives (e.g. a large file backup might look like a data breach to it).
3. Policy-Based Detection: 
   > Security administrators define specific rules (e.g. "No Telnet traffic allowed on the internal network"). If the rule is broken, an alert or block is triggered regardless of whether the traffic is actually malicious.

While both IDS and IPS monitor network traffic for threats, they differ in action and placement. 

**Intrusion Detection System (IDS)** is a passive monitoring tool designed to provide visibility into network traffic by alerting administrators to suspicious activity without interfering with the data flow. While it is highly effective at identifying potential threats, it lacks the native ability to intercept or block them; this is because an IDS is typically deployed out-of-band (it sits outside the direct path of data, analyzing a mirrored copy of the traffic via a TAP or SPAN port). Consequently, an IDS is considered a reactive security measure, primarily used for post-event analysis and forensic reporting.

**Intrusion Prevention System (IPS)** is an active control tool designed to identify and immediately block malicious activity in real-time. Unlike a passive system, an IPS has the authority to drop packets or terminate connections because it is placed inline (it sits directly in the path of network traffic, acting as a gateway through which all data must pass). This positioning allows the IPS to catch a threat before it reaches its destination, making it a proactive security measure (real-time mitigation).

## Snort Architecture & Detection Logic
https://www.youtube.com/watch?v=RzF5-fVz7Oc
https://cymulate.com/cybersecurity-glossary/snort-rules/
https://www.scribd.com/document/322400421/SnortCP-02-Introduction-to-Snort-Technology
https://www.scribd.com/document/494639517/20-Snort


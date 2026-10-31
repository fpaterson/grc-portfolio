# DNS and ICMP Traffic Analysis

## Project Overview

This repository contains a cybersecurity incident report based on the analysis of DNS and ICMP traffic captured with `tcpdump`. The report identifies the affected protocols, the port involved, and the likely cause of an incident that prevented users from accessing the website `www.yummyrecipesforme.com`.

## Scenario

Several customers reported they could not access the client company's website and received a **"destination port unreachable"** error after waiting for the page to load. A cybersecurity analyst reproduced the error and used `tcpdump` to capture and analyze the network traffic.

## Key Findings

- The user's computer (`192.51.100.15`) sent DNS queries via **UDP** to the DNS server (`203.0.113.2`) on **port 53**.
- The DNS server responded with **ICMP** packets indicating **"udp port 53 unreachable"**.
- Port 53 is the standard port for **DNS service**; the error indicates that no service was listening on that port.
- The same error was received two more times, confirming the issue was consistent.
- **Likely cause:** The DNS service was unavailable on UDP port 53, possibly due to a Denial-of-Service (DoS) attack.

## Repository Contents

| File | Description |
|---|---|
| `README.md` | General repository description and instructions |
| `cybersecurity-incident-report.md` | Complete incident report in Markdown format |




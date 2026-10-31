# Cybersecurity Incident Report: Network Traffic Analysis

## Part 1: Provide a summary of the problem found in the DNS and ICMP traffic log.

The UDP protocol reveals that:

A user's computer (192.51.100.15) sent UDP packets to the DNS server (203.0.113.2) on port 53 to resolve the domain name www.yummyrecipesforme.com to an IP address. The DNS request used the UDP protocol. In response, the DNS server returned ICMP error packets containing the message "udp port 53 unreachable."

This is based on the results of the network analysis, which show that the ICMP echo reply returned the error message:

udp port 53 unreachable

The port noted in the error message is used for:

DNS service

The most likely issue is:

A DoS attack.

## Part 2: Explain your analysis of the data and provide at least one cause of the incident.

**Time incident occurred:**

13:24:32.192571 (1:24 p.m. and 32.192571 seconds), based on the timestamps in the first sequence of the tcpdump log.

**Explain how the IT team became aware of the incident:**

Several customers reported they could not access www.yummyrecipesforme.com and received the error "destination port unreachable." An analyst attempted to visit the site and received the same error.

**Explain the actions taken by the IT department to investigate the incident:**

The analyst loaded tcpdump and reloaded the webpage, capturing the DNS query and response traffic to identify which protocols were involved and where the failure occurred.

**Note key findings of the IT department's investigation (i.e., details related to the port affected, DNS server, etc.):**

- The DNS request was sent via UDP from 192.51.100.15 to the DNS server 203.0.113.2 on port 53 (query ID 35084, "A?" flag for an A record).
- The DNS server returned ICMP errors stating "udp port 53 unreachable."
- Port 53 is the standard DNS port; the error means no service was listening on it.
- The same error was received two more times, confirming it was consistent.

**Note a likely cause of the incident:**

The DNS service on 203.0.113.2 was not running or was unavailable on UDP port 53, so the domain name could not be resolved and the website could not be reached. The most likely cause is a denial-of-service attack.

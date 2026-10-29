# Cybersecurity Incident Report: SYN Flood Attack

## Section 1: Identify the type of attack that may have caused this network interruption

One potential explanation for the website's connection timeout error message is a **SYN flood attack**, which is a type of Denial of Service (DoS) attack.

In a SYN flood, the attacker sends a massive volume of TCP SYN (synchronization) requests to the web server, flooding it with connection requests that are never completed (the attacker never sends the final ACK to complete the TCP three-way handshake). This overwhelms the server's ability to handle legitimate connection requests, causing it to become unresponsive.

### What the logs show

The Wireshark TCP/HTTP log captures a large number of TCP SYN requests coming from an unfamiliar/suspicious IP address directed at the web server. The server receives an abnormally high volume of SYN packets and appears unable to respond to all of them, causing it to become overwhelmed.

Legitimate users attempting to access the website experience connection timeouts because the server's resources are consumed by the flood of bogus connection requests. The server's ability to complete the TCP three-way handshake is disrupted, interrupting service.

### This event could be

A **DoS attack**, because it comes from a single source. Specifically, a **SYN flood**.

---

## Section 2: Explain how the attack is causing the website to malfunction

### The TCP three-way handshake

When website visitors try to establish a connection with the web server, a three-way handshake occurs using the TCP protocol:

1. The client sends a **SYN** (synchronization) packet to the server to request a connection.
2. The server responds with a **SYN-ACK** (synchronization-acknowledgment) packet, acknowledging the client's request and sending its own synchronization request.
3. The client sends an **ACK** (acknowledgment) packet back to the server, completing the handshake and establishing the connection.

### What happens when a malicious actor sends a large number of SYN packets at once

The server responds to each SYN with a SYN-ACK and allocates resources for each half-open connection. But the attacker never sends the final ACK, so these connections stay incomplete. The server's connection queue fills up, and it can no longer process legitimate requests.

### What the logs indicate and how that affects the server

The log shows a single unfamiliar IP address (`203.0.113.0`) repeatedly sending TCP SYN packets to the web server (`192.0.2.1`) on port 443 (HTTPS). These SYN requests come in rapid succession, roughly every 0.3 seconds, for the entire duration of the capture, totaling well over 150 SYN packets from the same source.

The server attempts to respond with SYN-ACK packets, but the attacker never completes the handshake with a final ACK. Meanwhile, the log shows legitimate users (`198.51.100.x`) beginning to experience failures: they receive RST-ACK responses instead of normal connections, and in one case an `HTTP/1.1 504 Gateway Time-out` error.

The server's connection table and resources are consumed by the attacker's incomplete SYN requests, leaving no capacity to handle normal traffic.

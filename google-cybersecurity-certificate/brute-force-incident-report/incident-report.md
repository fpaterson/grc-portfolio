Security Incident Report

## Section 1: Identify the network protocol involved in the incident

**HTTP (Hypertext Transfer Protocol).**

Looking at the tcpdump log, the packets show HTTP traffic on port 80. You can see lines like:

- `yummyrecipesforme.com.http`: the browser connected to the website using HTTP
- `HTTP: GET / HTTP/1.1`: the browser requested the webpage using HTTP

The same happened again for `greatrecipesforme.com.http`.

So the protocol used to load the webpage and download the malicious file was HTTP, which works at the application layer of the TCP/IP model.

DNS also appears in the log (to look up IP addresses), but the protocol that carried the actual web content and the malware download was HTTP.

---

## Section 2: Document the incident

A former employee attacked the website's web host using a brute force attack. They tried known default passwords until they guessed the admin password. Then they changed the website's source code, added JavaScript that told visitors to download an executable file, and changed the admin password so the owner could not log in.

Hours later, customers emailed the helpdesk. They said the site asked them to download a file, the website address changed, and their computers became slower.

### How it was found

The owner could not log in to the admin panel and contacted the hosting provider. Analysts used a sandbox and ran tcpdump. The site asked them to download a file. After running it, the browser redirected to `greatrecipesforme.com`.

### Log evidence

1. DNS request for `yummyrecipesforme.com`
2. DNS reply (`203.0.113.22`)
3. HTTP GET request
4. Malware download
5. DNS request for `greatrecipesforme.com`
6. DNS reply (`192.0.2.17`)
7. HTTP GET request

### Confirmation

Confirmation was achieved when a senior analyst found the JavaScript in the source code. The downloaded file contained a script that redirects visitors to the fake site. The team confirmed a brute-force attack.

### Sources

tcpdump log, sandbox test, source code review, file analysis, customer emails.

---

## Section 3: Recommend one remediation for brute force attacks

**Limit the number of login attempts.**

This way, the account locks after a few failed tries. The attacker guessed the password only by trying many times. Limiting attempts would have stopped the attack. It also creates logs that help analysts detect attacks.

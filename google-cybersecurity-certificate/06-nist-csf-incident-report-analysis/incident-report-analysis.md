# NIST CSF Incident Report Analysis: ICMP Flood (DoS) Attack

Incident report analysis applying the NIST Cybersecurity Framework (CSF) to a denial of service attack on a company's internal network.

## Summary

A denial of service (DoS) attack disrupted the company's internal network for approximately two hours. A malicious actor sent a flood of ICMP ping packets through an unconfigured firewall, overwhelming network services so that normal internal traffic could not access any network resources.

The incident management team responded by blocking incoming ICMP packets, taking non-critical network services offline, and restoring critical services. The cybersecurity team's investigation identified the root cause as an unconfigured firewall that allowed the ICMP flood to pass through.

In response, the network security team implemented:

- A new firewall rule to rate-limit incoming ICMP packets
- Source IP address verification to detect spoofed addresses
- Network monitoring software to detect abnormal traffic patterns
- An IDS/IPS to filter suspicious ICMP traffic

## Identify

The security event was a denial-of-service (DoS) attack, specifically an ICMP flood, in which a malicious actor overwhelmed the network with ICMP ping packets. The systems affected included the organization's internal network and network services, which became unresponsive for about two hours.

The cause was an unconfigured firewall that lacked rules to limit or filter incoming ICMP traffic, allowing the flood to overwhelm network resources. The attack source was an external malicious actor sending ICMP packets into the internal network.

**Impact:** temporary loss of availability of internal network resources and non-critical services, which were taken offline during the response.

## Protect

To protect against future incidents, the company should:

- Maintain and regularly review firewall rules
- Implement source IP address verification
- Conduct regular audits of firewall configurations, network devices, and access privileges to identify gaps before they are exploited
- Develop and enforce policies and procedures for firewall configuration and change management, ensuring no device is deployed without proper configuration
- Provide security awareness training to staff and ensure the incident response plan is documented, communicated, and rehearsed
- Keep systems and network devices patched and updated

## Detect

The company should:

- Deploy and maintain network monitoring software to continuously monitor traffic and alert on abnormal patterns
- Monitor firewall and device logs for unusual activity, including repeated connection attempts or traffic from spoofed addresses

## Respond

The organization blocked incoming ICMP packets, took non-critical network services offline, and restored critical network services first. Management was informed of the event and will communicate with stakeholders and inform law enforcement and other organizations as required by local laws. The incident timeline, actions taken, and lessons learned were documented, and response procedures will be updated.

## Recover

Immediately restore critical network services first, then bring non-critical services back online once the threat is contained and verified.

## Reflections

This exercise demonstrated how the NIST CSF provides a structured way to analyze a security incident across Identify, Protect, Detect, Respond, and Recover. The DoS attack was possible because of a simple configuration gap (an unconfigured firewall), showing that basic hardening and regular audits are critical. The layered defenses implemented reflect the principle of defense in depth.

# Security Risk Assessment Report

## Part 1: Select up to three hardening tools and methods to implement

I would recommend implementing these three network hardening tools and methods:

1. Multifactor authentication (MFA)
2. Password policies
3. Firewall maintenance (including port filtering)

## Part 2: Explain your recommendations

### 1. Multifactor authentication (MFA)

The organization isn't using MFA at all, which is a big problem. Requiring users to verify their identity in two or more ways would make it much harder for attackers to get in, even if they steal a password.

### 2. Password policies

Since employees are sharing passwords and the database admin password is still set to the default, the organization needs a strong password policy. This would include:

- Salting and hashing passwords
- Stopping password sharing
- Making sure default passwords are changed immediately

### 3. Firewall maintenance

The firewalls currently have no rules to filter traffic coming in and out of the network, which leaves the door wide open for attackers. Regularly checking and updating firewall rules, and blocking unused ports, would control what traffic is allowed in and out and help keep malicious actors out of the network.

## Conclusion

These three methods work well together because they address the exact vulnerabilities found:

- Shared passwords
- A default admin password
- No firewall rules
- No MFA

If implemented consistently, they would greatly reduce the risk of another data breach.

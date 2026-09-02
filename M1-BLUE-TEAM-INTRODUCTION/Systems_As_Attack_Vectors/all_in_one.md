# Systems as Attack Vectors — Overall Notes

## 1. Main Concept

Systems can be an entry point for attackers, just like humans.

A system can be a PC, laptop, server, database, cloud platform, website, etc. Attackers try to gain access to systems and then may steal data, deploy malware/ransomware, disrupt services, or use that access for further attacks.

The basic defense is:

- **Mitigation** → Reduce/prevent attacks
- **Detection** → Detect and investigate attacks that bypass protection

## 2. Important Things to Remember

### What Is a System and Why Is It Valuable?

Systems store data or provide access to important resources.

The value of a system depends on:

What data, access, control, or impact an attacker can gain from compromising it.

Examples:

- **Personal laptop:** Steal accounts or add the device to a botnet.
- **Bank IT administrator's laptop:** Gain access to important internal systems.
- **Mail server:** Access many users' emails and sensitive information.
- **Critical industrial server:** Potentially disrupt or encrypt systems with ransomware.
- **Website management panel:** Modify or damage website content (defacement).

Important idea:

Compromising one user/device may have limited impact, while compromising an important central system can affect many users and systems.

### How Attackers Gain Access to Systems

Most serious attacks first aim for:

**Initial Access → Then steal data, deploy ransomware, disrupt systems, or continue attacking**

**1. Human-led attacks**

Users can unintentionally help attackers compromise systems through:

- Weak or reused passwords.
- Using passwords exposed in data breaches.
- Downloading malware from unsafe/pirated sources.
- Connecting malicious or unknown USB devices.

**2. Vulnerabilities**

A vulnerability is a security flaw in software that attackers may exploit.

Important terms:

- **Vulnerability:** The weakness/flaw.
- **Exploit:** A method or code used to abuse the weakness.
- **CVE:** A public identifier used to identify a known vulnerability.
- **Patch:** A vendor update that fixes the vulnerability.
- **Zero-day:** A vulnerability for which a patch may not yet be available when attackers are exploiting it.

Basic flow:

**Vulnerability discovered → CVE becomes known → Attackers may exploit it → Defenders patch and monitor**

When there is no patch, organizations can:

- Restrict access to trusted IPs/users.
- Apply vendor-provided temporary mitigations.
- Block known attack patterns using tools such as IPS/WAF.
- Monitor for signs of exploitation.

**3. Misconfigurations**

A misconfiguration is an insecure system setup, not a software bug.

Examples:

- Weak or default passwords.
- Database or system unnecessarily exposed to the Internet.
- Too much/unrestricted access.
- Incorrect cloud/security configuration.
- Poorly configured IoT devices being used in botnets.

Example attack chain:

**Weak password → System exposed to the Internet → Attacker finds it → System is compromised**

Important difference:

- **Vulnerability** = flaw in software → usually fixed with a patch
- **Misconfiguration** = insecure setup → fixed by correcting the configuration

Misconfigurations can be proactively found through:

- Penetration testing
- Vulnerability scanning
- Configuration audits using security best practices such as CIS Benchmarks

**4. Supply Chain Attacks**

A supply chain attack happens when attackers compromise a trusted software, application, library, dependency, or update.

Basic idea:

**Compromise one trusted supplier/software → Malicious component/update reaches many users → Many organizations may be affected**

Examples include SolarWinds and 3CX.

These attacks can be difficult to prevent because organizations depend on many third-party applications and software components.

### Defending Systems

Common mitigation measures:

- **Patch Management:** Track vulnerabilities and patch affected systems.
- **IT Security Training:** Help IT staff avoid insecure configurations.
- **Network Protection:** Restrict access to trusted users, networks, or IP addresses.
- **Antivirus/EDR:** Help prevent or detect malware and malicious activity.

The overall defense idea:

**Patch vulnerabilities + Configure systems securely + Restrict unnecessary access + Use security tools + Detect what still gets through**

### SOC L1 Perspective

When investigating a system-related incident, think:

- What system is affected?
- How did the attacker gain access?
- Was it a human action, vulnerability, misconfiguration, or supply chain issue?
- What access or impact could the attacker gain?
- What remediation is needed?

The general process is:

**Detect → Investigate → Identify the weakness/entry point → Escalate when needed → Remediate → Improve defenses**

## 3. What I Should Understand After This Room

I should understand that:

Attackers look for the easiest way into an organization. That can be through a human or through a vulnerable or misconfigured system.

As a SOC L1, I should be able to understand the basic difference between vulnerabilities, misconfigurations, human-led attacks, and supply chain attacks, recognize how they can lead to initial access, and understand the importance of mitigation, detection, investigation, escalation, and remediation.

### Final Takeaway

Protect both humans and systems. Prevent what you can, but assume some attacks will bypass defenses—then detect, investigate, and respond.
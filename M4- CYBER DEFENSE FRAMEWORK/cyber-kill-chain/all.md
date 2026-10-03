# 🔗 Cyber Kill Chain

The Cyber Kill Chain is a framework that describes the different stages an attacker goes through to achieve their objective.

## 7 Stages

| Stage | Meaning | Example |
|---|---|---|
| 🔎 **1. Reconnaissance** | Gather information about the target | Find domains, employees, emails |
| 🔨 **2. Weaponization** | Prepare the attack/payload | Create malware or malicious document |
| 📤 **3. Delivery** | Get the payload to the victim | Phishing email, USB, watering hole |
| 💥 **4. Exploitation** | Exploit a vulnerability and execute code | Exploit a CVE |
| 🦠 **5. Installation** | Establish/maintain access | Backdoor, web shell, Run Keys |
| 📡 **6. Command & Control (C2)** | Communicate with and control the compromised system | HTTP/HTTPS, DNS |
| 🎯 **7. Actions on Objectives** | Perform the attacker's actual goal | Steal data, credentials, lateral movement |

---

## 1. 🔎 Reconnaissance — Find information

Gather information about the target before attacking.

**Examples / tools:**

- **theHarvester** → emails, names, subdomains, IPs, URLs
- **Hunter.io** → finds email addresses
- **OSINT Framework** → collection of OSINT tools
- **WHOIS** → domain/registration information

**Types:**

- **Passive:** No direct interaction → Google/searching social media
- **Active:** Direct interaction → port scanning/banner grabbing

---

## 2. 🔨 Weaponization — Prepare the attack

Create/obtain the malicious components.

**Examples:**

- Malicious Office document + VBA/macros
- Malware/worm
- Backdoor
- Phishing template
- C2 infrastructure

**Terms:**

- **Malware** = malicious software
- **Exploit** = code that abuses a vulnerability
- **Payload** = malicious code executed on the victim

---

## 3. 📤 Delivery — Get it to the victim

**Examples:**

- **Phishing/spearphishing** → malicious link/attachment
- **USB drop** → malicious USB
- **Watering hole** → compromise a website the target visits

---

## 4. 💥 Exploitation — Make the attack execute

Exploit a vulnerability/weakness so the attacker's code executes.

**Examples:**

- Malicious macro execution
- **Zero-day exploit** → unknown/unpatched vulnerability
- **Known CVE** → known but unpatched vulnerability

**Signs:**

- Unexpected processes
- Registry changes
- New services
- Suspicious command-line arguments

---

## 5. 🦠 Installation — Stay in the system

Establish persistence so the attacker can return.

**Examples:**

- **Web shell** → PHP/ASP/JSP malicious script
- **Meterpreter** → Metasploit payload providing an interactive shell
- **Windows Services** → persistence
- **Run Keys / Startup Folder** → execute malware at login
- **Timestomping** → modify file timestamps to hide activity

---

## 6. 📡 Command & Control (C2) — Communicate/control

The compromised machine communicates with the attacker's C2 infrastructure.

**Examples:**

- **HTTP** → port 80
- **HTTPS** → port 443
- **DNS tunneling**
- **IRC** → historically used for C2

> **C2 Beaconing** = infected machine repeatedly "checks in" with the C2 server.

---

## 7. 🎯 Actions on Objectives — Achieve the goal

**Examples:**

- Credential theft
- Privilege escalation
- Internal reconnaissance
- Lateral movement
- Data collection
- **Exfiltration** → steal data out
- Delete backups/shadow copies
- Corrupt/overwrite data

---

## ⚠️ Limitations

The Kill Chain was created by Lockheed Martin in 2011. It was designed around **malware and attacks that break in through the network perimeter**, so it has gaps:

| Gap | Why it's a problem |
|---|---|
| Modern complex attacks | Many don't follow 7 neat steps (e.g. cloud attacks, stolen credentials with no malware) |
| Changing attacker TTPs | **TTPs** = Tactics, Techniques, Procedures (the *how* of an attack). Attackers keep changing them, and the model is too high-level to track this |
| Insider threats | An insider already has access, so Delivery and Exploitation don't really apply |

### Frameworks to learn next

- **MITRE ATT&CK** → detailed catalog of attacker tactics & techniques
- **Unified Kill Chain** → broader attack lifecycle, covers more of what happens after initial access

---

## 🧠 One-line memory

**Find → Prepare → Deliver → Exploit → Stay → Control → Goal**
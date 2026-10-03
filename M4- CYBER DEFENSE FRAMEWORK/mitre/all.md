# MITRE — Easy Notes

## What is MITRE?

A group that writes down how hackers attack, so everyone uses the same words for it.

---

## 1. What is MITRE ATT&CK?

MITRE ATT&CK is a knowledge base of real-world adversary behaviour.

It helps analysts understand:

- What attackers do
- Why they do it
- How they do it
- How to detect/investigate it

### Three parts, always in this order

| Level | Meaning | Example |
|---|---|---|
| **Tactic** | The goal | "Get inside the network" |
| **Technique** | How they do it | "Send a fake email" |
| **Sub-technique** | The exact way | "Fake email with a bad attachment" |

**Simple way to remember:** Goal → Method → Exact method.

Each technique has an ID starting with `T`. Example: `T1595`.
A sub-technique adds a dot. Example: `T1595.002`.

**The Matrix** is just a big table. Goals (tactics) are the column titles at the top. Methods (techniques) sit under each one.

---

## 2. Example: APT28

> "APT28 uses Registry Run Keys."

The full thinking is:

```text
Tactic:         Persistence
   ↓
Technique:      Boot or Logon Autostart Execution
   ↓
Sub-technique:  Registry Run Keys / Startup Folder
   ↓
Procedure:      APT28's documented real-world use of that mechanism
```

---

## 3. Common SOC Examples

| Observed behaviour | ATT&CK idea |
|---|---|
| Phishing link | Initial Access → Phishing |
| PowerShell executing commands | Execution → PowerShell |
| CMD executing commands | Execution → Windows Command Shell |
| Run key modified for automatic startup | Persistence → Registry Run Keys |
| `rundll32.exe` loading suspicious DLL | Defense Evasion → System Binary Proxy Execution |
| `whoami`, `net user` | Discovery |
| `netstat` | System Network Connections Discovery |
| SMB/admin shares used to access another machine | Lateral Movement |
| Repeated periodic C2 connections | Command & Control → possible beaconing |
| Data sent outside the network | Exfiltration |

> **Important:** Don't classify something just because it *could* be malicious.
>
> **Observed behaviour → understand context → map to ATT&CK.**

---

## 4. Important Distinction: `rundll32.exe`

`rundll32.exe` is a **legitimate Windows binary**.

An attacker can abuse it to execute a malicious DLL:

```text
rundll32.exe
      ↓
malicious DLL
      ↓
code executes
```

This is: **Defense Evasion → System Binary Proxy Execution: Rundll32**

Don't automatically assume `rundll32.exe = malware`.

Investigate:

- The DLL
- The path
- The command line
- The parent process
- The resulting activity

---

## 5. CAR (Cyber Analytics Repository)

**Purpose:** Ready-made detection logic for ATT&CK techniques.

Each CAR entry includes:

- Description of the behavior it detects
- Linked Tactic(s), Technique, Sub-technique
- Implementation in 3 forms: **Pseudocode**, **Splunk query**, **LogPoint query**
- Level of Coverage (how complete the detection is)

**Example logic:** Alert when a scheduled-task file is created by anything other than the normal Windows process (`svchost.exe`), since that process creating one is expected and not suspicious.

**CAR's own matrix:** Shows which techniques already have a detection recipe (colored) and which don't (a gap).

---

## 6. D3FEND

Tells you **how to stop or block** a hacker technique.

It has 7 simple steps:

1. **Model** — understand your system
2. **Harden** — make it harder to break
3. **Detect** — notice the attack
4. **Isolate** — cut them off
5. **Deceive** — trick them
6. **Evict** — kick them out
7. **Restore** — fix the damage

IDs start with `D3-` instead of `T`. Example: `D3-CRO`.

---

## 7. Other Tools

- **Emulation Library** = a script that copies a real hacker group's attack, step by step.
- **Caldera** = a tool that runs that script for you automatically.
- **AADAPT** = same idea as ATT&CK, but for crypto/blockchain attacks.
- **ATLAS** = same idea as ATT&CK, but for AI attacks.

---

## 8. Who Uses This Stuff?

| Role | What they do |
|---|---|
| **CTI team** | Studies hacker groups |
| **SOC analyst** | Checks alerts |
| **Detection engineer** | Builds alarms |
| **Incident responder** | Figures out what happened |
| **Red team** | Tests defenses by attacking |

---

## 9. Summit — What It Taught Me

**Summit = detecting attacker behaviour.**

### Progression

```text
Hash
 ↓
IP
 ↓
Domain
 ↓
Host behaviour
 ↓
Network behaviour
 ↓
TTP / attacker behaviour
```

### Examples

- **Hash** → block exact malware file
- **IP** → block C2 IP
- **Domain** → block malicious C2 domain
- **Registry modification** → detect disabling Defender
- **Repeated same-size connections** → possible C2 beaconing
- **CMD + system commands + output file** → detect attacker activity

### Main lesson

> Don't only look for the IOC. Ask what the attacker is actually doing.

---

## 10. Eviction — What It Taught Me

**Eviction** = using MITRE ATT&CK Navigator to understand a known threat group's TTPs.

You were given APT28's highlighted techniques and matched questions to them.

### Main lesson

> Navigator shows the attacker's documented techniques; the SOC analyst uses those techniques to understand and investigate possible activity.
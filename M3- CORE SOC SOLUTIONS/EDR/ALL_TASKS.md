# 🛡️ EDR — Complete Core Notes (Tasks 2–6)

## 1. What is EDR?

**EDR = Endpoint Detection and Response.**

It is a security solution that protects and monitors **endpoints**.

### Endpoint means:

```
💻 Laptop
🖥️ Desktop
🖥️ Server
```

EDR continuously monitors what happens on these devices, detects suspicious activity, and helps security analysts investigate and respond.

### The three main pillars of EDR:

```
👀 Visibility → 🚨 Detection → 🛑 Response
```

| Pillar | Meaning |
|---|---|
| **Visibility** | See what is happening on an endpoint |
| **Detection** | Identify suspicious/malicious activity |
| **Response** | Take action against the threat |

---

## 2. Why do we need EDR if we already have Antivirus?

### Traditional AV mainly asks:

> **"Do I recognize this file/threat as malicious?"**

EDR asks a broader question:

> **"What is happening on this endpoint, and does the behavior look suspicious?"**

Example:

```
WINWORD.EXE
     ↓
PowerShell.exe
     ↓
Downloads a file
     ↓
Connects externally
```

Even if:

-  Word is legitimate
-  PowerShell is legitimate
-  The downloaded file is unknown

…the **complete behavior may still be suspicious**.

### Main difference:

```
AV
↓
Recognizes and blocks known threats


EDR
↓
Monitors endpoint activity
↓
Collects evidence
↓
Connects events
↓
Detects suspicious behavior/patterns
↓
Helps investigate and respond
```

> **Important:** Modern AV can also have advanced capabilities. The key idea is that EDR provides deeper endpoint visibility, investigation context, and response capabilities.

---

## 3. How does an EDR work?

An EDR usually has two important parts:

## 👀 EDR Agent / Sensor

Installed on the endpoint.

Its job:

```
Watch endpoint activity
        ↓
Collect data
        ↓
Send data to EDR console
```

The agent is basically the **eyes and ears** of the EDR.

---

## 🧠 EDR Console

The central platform where data from multiple endpoints is collected and analyzed.

```
💻 Endpoint 1 ──┐
💻 Endpoint 2 ──┤
🖥️ Server ──────┤
                ↓
           🧠 EDR Console
                ↓
          Alerts + Investigation
                ↓
           👨‍💻 SOC Analyst
```

The console gives the SOC analyst a central place to:

-  View alerts
-  Investigate activity
-  See endpoint details
-  Take response actions

---

## 4. What is Telemetry?

**Telemetry = detailed activity data collected from an endpoint by the EDR agent.**

Think of it as:

> **The evidence or activity record of what happened on the endpoint.**

Main telemetry you should know:

| Telemetry | Main question it answers |
|---|---|
| **Process Activity** | What executed? What started it? |
| **Network Connections** | Where did the endpoint/process connect? |
| **Command Line** | What command/arguments were executed? |
| **File Activity** | What files were created, changed, or deleted? |
| **Registry Activity** | What system configuration was changed? |

---

## 5. Process Tree — Very Important

A process tree shows the relationship between processes.

```
Parent Process
       ↓
Child Process
```

Example:

```
explorer.exe
      ↓
chrome.exe
```

Could be normal.

But:

```
WINWORD.EXE
      ↓
PowerShell.exe
      ↓
payload.exe
```

🚨 This may require investigation.

### Why?

Because EDR lets us see **how events are connected**.

This is one of the most important ideas from the entire room:

> **An individual event may look legitimate, but the complete chain of events can reveal an attack.**

---

## 6. How does EDR detect threats?

EDR analyzes telemetry in several important ways.

## 🧩 Behavioral Detection

**Question: Is this behavior suspicious?**

Example:

```
WINWORD.EXE
      ↓
PowerShell.exe
```

Both are legitimate programs, but this relationship may be suspicious.

---

## 📈 Anomaly Detection

**Question: Is this unusual for this endpoint?**

The EDR understands the normal/baseline behavior of an endpoint.

```
Normal behavior
       ↓
Baseline
       ↓
New/unusual behavior
       ↓
🚨 Possible anomaly
```

Important:

> **Unusual does not automatically mean malicious.**

It may result in a **false positive**, so the analyst investigates.

---

## 🎯 IOC Matching

**IOC = Indicator of Compromise**

Common examples:

```
Malicious IP
Malicious Domain
Malicious File Hash
```

EDR compares observed activity against known threat intelligence.

```
File Hash
    ↓
Threat Intelligence
    ↓
Match?
    ↓
🚨 Alert
```

---

## 🧠 Pattern / Machine Learning Detection

Sometimes individual events look harmless:

```
PowerShell       → Possibly normal
File download    → Possibly normal
Network activity → Possibly normal
```

But together:

```
PowerShell
    ↓
Download
    ↓
File execution
    ↓
External connection
```

🚨 The complete pattern may indicate an attack.

You **do not need to understand the ML algorithms**. Just understand that EDR can analyze complex patterns.

---

## 7. What is MITRE ATT&CK Mapping?

EDR may map suspicious activity to known attacker behavior.

Example:

```
Scheduled Task Created
        ↓
MITRE ATT&CK
        ↓
Tactic: Persistence
Technique: Scheduled Task/Job
```

### Easy understanding:

> **MITRE ATT&CK gives a common way to describe what attackers are trying to do and how they are doing it.**

For now, don't memorize the framework. You will learn it later.

---

## 8. What happens when EDR generates an alert?

This is the basic SOC workflow:

```
🚨 Alert
   ↓
Acknowledge / Prioritize
   ↓
Investigate the evidence
   ↓
Understand the attack chain
   ↓
False Positive OR True Positive?
```

### False Positive

Something was flagged but is actually legitimate.

```
🚨 Alert
   ↓
Investigation
   ↓
Legitimate activity
   ↓
False Positive
```

### True Positive

The activity is actually malicious.

```
🚨 Alert
   ↓
Investigation
   ↓
Malicious activity confirmed
   ↓
True Positive
   ↓
Respond / Escalate
```

---

## 9. How does a SOC analyst investigate in EDR?

Suppose you receive:

```
🚨 Suspicious PowerShell Alert
```

You investigate the telemetry:

```
Who started PowerShell?
        ↓
What command was executed?
        ↓
What files were created/downloaded?
        ↓
What network connections occurred?
        ↓
What happened afterward?
```

This lets you reconstruct:

```
Attack Start
     ↓
Execution
     ↓
Download
     ↓
Network Activity
     ↓
Further Actions
```

This is called understanding the **attack chain / timeline**.

---

## 10. EDR Response Capabilities

If the threat is confirmed, EDR can help respond.

## 🔒 Isolate Host

Disconnect/restrict the compromised endpoint from the network.

Used to contain threats and prevent:

-  Lateral movement
-  Further attacker communication
-  Spread to other systems

---

## 🛑 Terminate Process

Stop a specific malicious process.

```
Malicious Process
       ↓
Terminate
       ↓
Process stops
```

Useful when isolating the entire machine would cause unnecessary business disruption.

---

## 📦 Quarantine

Move a suspicious/malicious file into an isolated location where it cannot execute normally.

```
Malicious File
      ↓
Quarantine
      ↓
Cannot execute normally
```

---

## 💻 Remote Access / Response

EDR may allow authorized analysts to remotely interact with the endpoint.

Used for:

-  Deeper investigation
-  Collecting information
-  Running approved response actions/scripts

---

## 📁 Artifact Collection

**Artifact = evidence collected from an endpoint.**

Examples:

```
Event Logs
Memory Dump
Folder Contents
Registry Data
```

Used for deeper investigation and forensic analysis.

---

## 11. EDR vs SIEM

EDR focuses primarily on **endpoint activity**.

But an organization has multiple security tools:

```
EDR
Firewall
Email Security
IAM
DLP
Other Security Tools
```

These can send logs to a central system:

```
Multiple Security Tools
         ↓
        SIEM
         ↓
   Central Investigation
         ↓
    SOC Analysts
```

### Simple difference:

```
EDR = Deep visibility into endpoints

SIEM = Centralizes/analyzes logs from many sources
```

You will study SIEM properly later, so this is enough for now.

---

## 🎯 THE ENTIRE ROOM IN ONE FLOW

If you understand this, you understand what the room wanted to teach:

```
💻 Endpoint
     │
     ▼
👀 EDR Agent
     │
Collects TELEMETRY:
Processes
Commands
Files
Network
Registry
     │
     ▼
🧠 EDR Console
     │
Analyzes activity using:
• Behavior
• Anomalies
• Known IOCs
• Attack patterns
     │
     ▼
🚨 Alert
     │
     ▼
👨‍💻 SOC Analyst
     │
Investigates:
Process Tree
Commands
Files
Network Activity
Timeline
     │
     ▼
False Positive? ──→ Close
     │
True Positive
     ▼
🛑 Respond:
Isolate
Terminate
Quarantine
Remote Response
Collect Evidence
```

---

## 🧠 Important Terms From This Room

These are the terms I would actually keep in your notes:

| Term | Simple Meaning |
|---|---|
| **Endpoint** | A device such as a laptop, desktop, or server |
| **EDR** | Endpoint Detection and Response security solution |
| **Agent/Sensor** | Software on the endpoint that collects activity |
| **EDR Console** | Central platform for monitoring and investigation |
| **Telemetry** | Activity/evidence collected from the endpoint |
| **Process Tree** | Parent-child relationship between processes |
| **Alert/Detection** | Suspicious activity identified by EDR |
| **IOC** | Known indicator associated with compromise |
| **Threat Intelligence** | Information about known threats/indicators |
| **False Positive** | Alert triggered by legitimate activity |
| **True Positive** | Alert caused by real malicious activity |
| **MITRE ATT&CK** | Framework for describing attacker behavior |
| **Quarantine** | Isolating a file to prevent normal execution |
| **Host Isolation** | Restricting a compromised device's network access |
| **Artifact** | Evidence collected for investigation/forensics |

---

## Final: What This Room Wanted You to Learn

**Not how CrowdStrike buttons work. Not how machine learning works. Not every EDR product.**

The actual lesson is:

> **An EDR gives the SOC analyst visibility into what is happening on endpoints. It collects telemetry, detects suspicious behavior, provides context such as process trees and timelines for investigation, and allows actions to contain or respond to confirmed threats.**

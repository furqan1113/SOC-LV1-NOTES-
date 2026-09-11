# 🛡️ SIEM — Tasks 1–5: Complete Guide

> **Goal:** Understand how events become logs, how logs reach a SIEM, how SIEM processes them, how detection rules create alerts, and what a SOC analyst does with those alerts.

---

## 🧠 The Big Picture

Imagine you're a **SOC analyst monitoring a company's network**.

A company may have:

* 💻 Windows computers
* 🐧 Linux servers
* 🔥 Firewalls
* 🌐 Web servers
* 🔐 VPNs
* 🗄️ Databases
* 🚨 IDS/IPS

Something happens somewhere.

The SOC analyst eventually needs to answer:

> **What happened? Is it suspicious? Is it an attack? What should we do?**

That's where a **SIEM** comes in.

---

# 1. 📜 Everything Creates Logs

Whenever something happens on a system, it can generate a **log**.

### Examples

```text
Employee logs into Windows
        ↓
Windows creates a log

Employee opens a file
        ↓
Windows creates a log

Someone runs PowerShell
        ↓
Windows creates a log

Someone connects through VPN
        ↓
VPN creates a log

Someone accesses a website
        ↓
Web server creates a log

Firewall blocks traffic
        ↓
Firewall creates a log
```

### Key Definitions

| Term           | Meaning                              |
| -------------- | ------------------------------------ |
| **Log**        | A recorded event/activity            |
| **Log Source** | The system/device producing the logs |

### Common Log Sources

* Windows
* Linux
* Web server
* Firewall
* VPN
* Database
* IDS/IPS

> 💡 **Remember:**
> **Something happens → System records it → Log is created**

---

# 2. 🌍 The Problem: Logs Are Everywhere

Imagine a company has:

```text
500 Windows PCs
50 Linux servers
20 Firewalls / network devices
10 Web servers
```

All of these systems are producing logs.

Without a SIEM, an analyst might have to investigate them individually:

```text
PC 1       → Check logs
PC 2       → Check logs
PC 3       → Check logs
...
Firewall   → Check logs
Web Server → Check logs
VPN        → Check logs
```

That's terrible for a SOC.

## The 3 Major Problems

### 1. Too Many Logs

Hundreds or thousands of events can happen.

### 2. Logs Are Scattered

Different systems store their own logs.

### 3. Logs Have Different Formats

Windows logs may look different from Linux logs, which may look different from firewall logs.

---

## ⚠️ The Biggest Problem: Lost Context

One event by itself might look completely normal.

But several events together can tell a completely different story.

For example:

```text
Successful VPN Login
        +
Sensitive File Access
        +
PowerShell Execution
        +
Large Outbound Connection
```

Individually, these events might not prove anything.

Together, they could tell a story of:

> **Compromised account → attacker activity → possible data theft**

---

# 3. 🧠 SIEM Solves This

## SIEM = Security Information and Event Management

Think of SIEM as the **central security brain for logs**.

```text
Windows ───────┐
Linux ─────────┤
Web Server ────┤
Firewall ──────┤
VPN ───────────┤
Database ──────┤
               ↓
              SIEM
               ↓
         SOC Analyst
```

Instead of the analyst going everywhere:

> **Bring the logs to one place.**

### Core Purpose

```text
Many Log Sources
       ↓
      SIEM
       ↓
Centralized Analysis
       ↓
   SOC Analyst
```

---

# 4. 📥 How Do Logs Get Into the SIEM?

> **Ingestion = getting logs into the SIEM.**

There are several ways logs can arrive.

---

## 4.1 🤖 Agent / Forwarder

A small program runs on an endpoint and sends logs to the SIEM.

```text
Windows PC
    ↓
Agent / Forwarder
    ↓
   SIEM
```

### Splunk terminology

Splunk commonly uses the term **Forwarder**.

---

## 4.2 📡 Syslog

**Syslog** is a common protocol used to send logs to a centralized destination.

```text
Firewall ──┐
Server ────┤
Database ──┤
           ↓
         Syslog
           ↓
          SIEM
```

---

## 4.3 📁 Manual Upload

An existing log file can be uploaded into the SIEM for analysis.

```text
Log File
   ↓
Manual Upload
   ↓
  SIEM
```

---

## 4.4 🔌 Port Forwarding

The SIEM listens on a particular port and systems send their logs there.

```text
Endpoint
   ↓
 Logs
   ↓
SIEM listening on port
```

---

### 🧠 Easy Way to Remember

Don't overthink the ingestion methods.

Just remember:

> **Ingestion = How do logs arrive at the SIEM?**

| Method                | Basic Idea                                |
| --------------------- | ----------------------------------------- |
| **Agent / Forwarder** | Software sends logs                       |
| **Syslog**            | Logs sent using a common logging protocol |
| **Manual Upload**     | Existing log file is uploaded             |
| **Port Forwarding**   | Logs are sent to a listening SIEM port    |

---

# 5. 🧩 SIEM Processes and Organizes Logs

Raw logs can look very different.

The SIEM processes them so they become useful for analysis.

The important concepts are:

```text
Parsing
   ↓
Normalization
   ↓
Correlation
```

---

# 5.1 🔍 Parsing

### What is Parsing?

> **Parsing = extracting useful fields from a raw log.**

Example:

```text
Raw Log
   ↓
Parsing
   ↓
IP = 10.0.0.5
User = John
EventID = 4688
Process = powershell.exe
```

The raw log is broken into useful pieces of information called **fields**.

### Remember

```text
Raw Log
   ↓
Parsing
   ↓
Useful Fields
```

---

# 5.2 🧱 Normalization

Different log sources may represent information differently.

**Normalization** converts information into a more consistent structure.

> **Normalization = making logs consistent/standardized so they can be analyzed together.**

### Why does this matter?

Detection rules need to work with information consistently.

```text
Windows Logs ──┐
Linux Logs ────┤
Firewall Logs ─┤
VPN Logs ──────┤
               ↓
        Normalization
               ↓
      Consistent Structure
```

---

# 5.3 🔗 Correlation

One of the most important SIEM concepts.

> **Correlation = connecting related events together.**

Imagine the SIEM sees:

```text
VPN
 ↓
Successful login from unfamiliar IP

        +

File Server
 ↓
User accesses sensitive documents

        +

Windows
 ↓
PowerShell executed

        +

Network
 ↓
Large outbound connection
```

Individually:

```text
Login                 → Could be normal
File access            → Could be normal
PowerShell             → Could be normal
Outbound traffic       → Could be normal
```

Together:

```text
Login
  ↓
Sensitive File Access
  ↓
PowerShell
  ↓
Large Outbound Traffic
```

This could indicate:

> **Compromised account → attacker activity → possible data theft**

That's the power of **correlation**.

---

# 6. 🚨 Detection Rules

Now the SIEM has:

* Logs
* Parsed fields
* Normalized data
* Correlated events

But how does it know when something deserves an alert?

## Detection Rules

A detection rule is essentially:

```text
IF these conditions happen
        ↓
THEN create an alert
```

### Important

> **Detection Rule = IF conditions match → ALERT**

---

# 7. 🆔 Event ID ≠ Alert

This is one of the most important concepts.

❌ Don't think:

> **Event ID = Alert**

Instead:

> **Event ID = Information about what event happened**

The **detection rule** decides whether the event should generate an alert.

---

# 8. 🧹 Example: Event Log Cleared

Windows records an event.

```text
Event ID = 104
```

For this task:

> **Event ID 104 indicates an attempt to clear/remove event logs.**

A SIEM detection rule could be:

```text
IF
    Log Source = WinEventLog
AND
    Event ID = 104

THEN
    🚨 ALERT: Event Log Cleared
```

### Complete Flow

```text
Windows generates event
        ↓
Event ID = 104
        ↓
SIEM receives it
        ↓
Detection rule checks it
        ↓
Does it match?
        ↓
       YES
        ↓
🚨 ALERT
```

### Critical Point

> **The event did not automatically become an alert.**

The **rule** checked the event and generated the alert because its conditions matched.

---

# 9. 👤 Example: WHOAMI

Windows records process execution.

For this task:

> **EventCode 4688 = process execution**

Suppose the log contains:

```text
EventCode = 4688
NewProcessName = whoami
```

A detection rule could be:

```text
IF
    Log Source = WinEventLog

AND
    EventCode = 4688

AND
    NewProcessName contains "whoami"

THEN
    🚨 WHOAMI Command Execution DETECTED
```

The rule checks the **field values**.

---

## If Conditions Match

```text
4688 + whoami
       ↓
Conditions satisfied
       ↓
🚨 Alert
```

## If Conditions Don't Match

```text
4688 + something else
       ↓
Rule doesn't match
       ↓
No alert from this rule
```

---

# 10. 🧩 Why Are Fields Important?

Because detection rules look at them.

Think of every parsed log as:

```text
FIELD → VALUE
```

Example:

```text
EventCode      → 4688
NewProcessName → whoami
Log Source     → WinEventLog
```

A detection rule essentially asks:

> **"Do these fields contain the values I'm looking for?"**

That's why **parsing and normalization** are so important.

---

# 🔄 The Processing Pipeline

```text
Raw Log
   ↓
Parsing
   ↓
Fields Extracted
   ↓
Normalization
   ↓
Consistent Fields
   ↓
Detection Rule
   ↓
🚨 Alert
```

---

# 11. 📋 Common Detection Rule Examples

## 🔐 Brute-Force-Like Activity

```text
5 Failed Logins
within 10 seconds
        ↓
🚨 Alert
```

---

## 🔑 Suspicious Login Sequence

```text
Multiple Failed Logins
        ↓
Successful Login
        ↓
🚨 Alert
```

---

## 🔌 USB Device

```text
USB Connected
        ↓
🚨 Alert
```

Useful when USB usage is restricted.

---

## 📤 Large Outbound Traffic

```text
Outbound Traffic > 25 MB
        ↓
🚨 Potential Data Exfiltration
```

> ⚠️ The threshold depends on company policy.

---

# 12. ⚠️ Alert ≠ Attack

This is **extremely important for SOC work**.

Suppose:

```text
Employee forgets password
        ↓
5 Failed Login Attempts
        ↓
SIEM Rule Triggers
        ↓
🚨 Alert
```

Did an attacker definitely attack?

> **No.**

The employee may simply have entered the wrong password several times.

This is a:

## False Positive (FP)

> **An alert happened, but the activity was legitimate.**

---

## ✅ True Positive (TP)

Now imagine:

```text
5 Failed Logins
        ↓
Successful Login
        ↓
Suspicious Activity
        ↓
Investigation
        ↓
Actually an Attacker
```

This is a:

## True Positive (TP)

> **The alert represented genuine suspicious/malicious activity.**

---

# 13. 👨‍💻 What Does a SOC Analyst Do?

The basic workflow is:

```text
🚨 ALERT
   ↓
Analyst Investigates
   ↓
┌─────────────────────┐
│                     │
↓                     ↓
False Positive     True Positive
│                     │
↓                     ↓
Tune Rule          Further Investigation
                      ↓
                 Confirm Suspicious Activity
                      ↓
                    Respond
```

---

## 🔎 During Investigation

The analyst may examine:

* Events associated with the alert
* Network flows/activity
* Conditions that triggered the rule
* Other relevant logs
* Additional context

Then the analyst decides:

> **What actually happened?**

---

# 14. 🛡️ Response

If the activity is confirmed as suspicious, possible actions include:

### 👤 Contact Asset Owner

Ask:

> **"Did you actually perform this activity?"**

---

### 🖥️ Isolate Infected Host

Stop the compromised machine from communicating with the network.

---

### 🚫 Block Suspicious IP

Prevent further communication from/to the suspicious IP as appropriate.

> ⚠️ The exact response depends on the organization's procedures and your authorization.

---

# 15. 📊 SIEM Dashboards

A **dashboard** is basically the SOC analyst's **overview screen**.

It can summarize things such as:

```text
🚨 Alerts
🔐 Failed Logins
🌐 Network Events
📊 Events Ingested
⚙️ Rules Triggered
```

The analyst can then investigate interesting alerts/events in more detail.

---

# 🔥 The Entire SIEM Flow

If you remember this flow, you've connected **Tasks 1–5**:

```text
                 EVERYTHING HAPPENS
                        ↓
                 SYSTEMS CREATE LOGS
                        ↓
          ┌─────────────┴─────────────┐
          ↓                           ↓
     Host-Centric                Network-Centric
          ↓                           ↓
   Windows / Linux             Firewall / VPN / IDS
          └─────────────┬─────────────┘
                        ↓
                   LOG SOURCES
                        ↓
                  LOG INGESTION
                        ↓
       ┌──────────────┬──────────────┐
       ↓              ↓              ↓
     Agent          Syslog      Manual Upload
   / Forwarder                       / Port
                                    Forwarding
       └──────────────┬──────────────┘
                        ↓
                       SIEM
                        ↓
                    PARSING
                 "Extract fields"
                        ↓
                  NORMALIZATION
                 "Make consistent"
                        ↓
                   CORRELATION
                  "Connect events"
                        ↓
                 DETECTION RULE
              "Do conditions match?"
                        ↓
                     🚨 ALERT
                        ↓
                  SOC ANALYST
                        ↓
                   INVESTIGATE
                        ↓
              ┌─────────┴─────────┐
              ↓                   ↓
        FALSE POSITIVE       TRUE POSITIVE
              ↓                   ↓
          Tune Rule          Investigate
                                  ↓
                                RESPOND
                          ┌───────┼───────┐
                          ↓       ↓       ↓
                       Contact  Isolate  Block IP
                        Owner     Host
```

---

# 🧠 The 5 Things You MUST Remember

If you forget everything else, remember these five.

---

## 1️⃣ Logs

> **Something happens → system records it as a log.**

---

## 2️⃣ SIEM

> **SIEM brings logs from many sources into one place.**

---

## 3️⃣ Processing

> **Parse → Normalize → Correlate**

| Concept          | Meaning                     |
| ---------------- | --------------------------- |
| 🔍 **Parse**     | Extract fields              |
| 🧱 **Normalize** | Make information consistent |
| 🔗 **Correlate** | Connect related events      |

---

## 4️⃣ Detection

> **Detection Rule = IF conditions match → ALERT**

### Remember:

> **Event ID is an event identifier, NOT automatically an alert.**

Example:

```text
Event ID 104
      ↓
Event occurred
      ↓
Detection Rule checks it
      ↓
Rule matches?
      ↓
🚨 Alert
```

---

## 5️⃣ SOC

> **Alert → Investigate → FP/TP → Respond**

```text
🚨 Alert
   ↓
Investigate
   ↓
┌───────────────┐
↓               ↓
False Positive  True Positive
↓               ↓
Tune Rule       Respond
```

---

# 🎯 Quick Revision Cheat Sheet

| Concept                | One-Line Meaning                                        |
| ---------------------- | ------------------------------------------------------- |
| 📜 **Log**             | Recorded event/activity                                 |
| 📍 **Log Source**      | System producing logs                                   |
| 🧠 **SIEM**            | Central place for security logs                         |
| 📥 **Ingestion**       | Getting logs into SIEM                                  |
| 🤖 **Agent/Forwarder** | Software that sends logs                                |
| 📡 **Syslog**          | Common protocol for sending logs                        |
| 📁 **Manual Upload**   | Upload an existing log file                             |
| 🔌 **Port Forwarding** | Send logs to a listening port                           |
| 🔍 **Parsing**         | Extract useful fields                                   |
| 🧱 **Normalization**   | Make data consistent                                    |
| 🔗 **Correlation**     | Connect related events                                  |
| 🆔 **Event ID**        | Identifies an event                                     |
| 🚨 **Detection Rule**  | Conditions that can generate an alert                   |
| ⚠️ **Alert**           | Something matched a detection condition                 |
| ❌ **False Positive**   | Alert but activity was legitimate                       |
| ✅ **True Positive**    | Alert represented genuine suspicious/malicious activity |
| 👨‍💻 **SOC Analyst**  | Investigates alerts and decides what happened           |
| 🛡️ **Response**       | Actions taken after confirmed suspicious activity       |
| 📊 **Dashboard**       | SOC overview screen                                     |

---

# 🧩 The One Mental Model

When revising, think about SIEM as a pipeline:

```text
              SOMETHING HAPPENS
                      ↓
                    LOG
                      ↓
                 LOG SOURCE
                      ↓
                 INGESTION
                      ↓
                    SIEM
                      ↓
                  PARSING
                      ↓
               NORMALIZATION
                      ↓
                CORRELATION
                      ↓
              DETECTION RULE
                      ↓
               🚨 ALERT
                      ↓
              SOC INVESTIGATION
                      ↓
               ┌──────┴──────┐
               ↓             ↓
              FP             TP
               ↓             ↓
          Tune Rule       Respond
```

> 💡 **If you understand this pipeline, you understand the core idea behind Tasks 1–5.**

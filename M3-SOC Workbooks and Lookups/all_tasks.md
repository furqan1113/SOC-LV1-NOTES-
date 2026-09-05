# 📘 SOC Workbooks & Lookups — My Notes

## 1️⃣ Why do SOC analysts need lookups?

When an alert happens, the alert alone often doesn't give enough context.

For example:

> G.Baker accessed a financial server and shared a financial report with R.Lund.

Before calling this malicious, I need more information:

- Who is G.Baker?
- What is their job?
- Is accessing financial data part of their role?
- What is the server?
- Who normally has access to it?
- Who is R.Lund and why would they receive the file?

👉 **Lookups give context to the alert.**

---

## 2️⃣ Identity Inventory 👤

An Identity Inventory contains information about users and accounts.

It can include:

- Name
- Username
- Email
- Job role
- Location
- Department
- Privileges
- Allowed access

**Example**

```
G.Baker
Role: CFO
Location: UK
Access: VPN, HQ, FINANCE
```

If G.Baker accesses a financial server, that may be normal because their role is related to finance.

**Sources of Identity Information**

- Active Directory / Entra ID
- SSO providers
- HR systems
- Internal CSV or Excel sheets

👉 **Main purpose:** Understand WHO the user/account is and whether their activity makes sense.

---

## 3️⃣ Asset Inventory 🖥️

An Asset Inventory contains information about company devices and servers.

It can include:

- Hostname
- Location
- IP address
- Operating System
- Owner
- Purpose

**Example**

```
HQ-FINFS-02
Location: UK Datacenter
OS: Windows Server
Purpose: Financial file server
Owner: Central IT
```

If an alert involves this server, I now understand that it contains financial data and should investigate accordingly.

👉 **Main purpose:** Understand WHAT the device is and WHY it exists.

---

## 4️⃣ Network Diagrams 🌐

A network diagram shows:

- Networks and subnets
- Servers
- VPNs
- Firewalls
- Internet-facing services
- Connections between networks

It helps turn random IP addresses into meaningful information.

**Example from the room**

```
Threat Actor
     ↓
VPN Service (TCP/10443)
     ↓
VPN Subnet (10.10.0.0/16)
     ↓
Attempts to scan Database subnet
     ↓
Attempts to scan Office subnet
```

The investigation showed:

- External IP `103.61.240.174` connected to VPN port `10443`
- After VPN access, it received internal IP `10.10.0.53`
- It scanned the Database subnet
- Then it scanned the Office subnet

👉 Instead of seeing random IPs, the network diagram helps reconstruct the attack path.

**My simple understanding:**

> Network diagram = Where did the activity come from, where did it go, and what network was involved?

---

## 5️⃣ SOC Workbook / Playbook / Runbook 📋

These terms are similar in this context.

A **SOC Workbook** is a structured set of steps that tells an analyst how to investigate a particular type of alert.

For example:

> Unusual Login Location Workbook

Instead of randomly investigating, the analyst follows a logical process.

### Basic structure

#### Stage 1 — Enrichment 🔍

Get more context.

Ask:

- Who is the user?
- What is their location?
- Is the IP malicious?
- Is the IP related to VPN?
- What is normal behaviour for this user?

Tools/resources might include:

- Identity Inventory
- Asset Inventory
- Threat Intelligence
- Network diagrams

#### Stage 2 — Investigation 🕵️

Look at the actual evidence.

Ask:

- What happened?
- When did it happen?
- Is it unusual?
- What happened before and after?
- Are there related suspicious events?
- Is there evidence that this is malicious?

Use:

- SIEM logs
- EDR logs
- Email analysis
- Historical activity

#### Stage 3 — Decision / Escalation 🚨

Based on the evidence:

**If expected and legitimate:**

```
False Positive
     ↓
Close alert
```

**If suspicious or malicious:**

```
True Positive
     ↓
Write report
     ↓
Escalate to L2 if needed
```

---

## 🧠 The Most Important Part: Don't Memorise Every Box

This is the thing you were confused about, and honestly, you do **NOT** need to remember the exact 6 boxes from the drag-and-drop task.

For example, you don't need to memorise:

> "First click this, then use EML analyser, then investigate recipients..."

Instead, remember the **logic**.

### 🔥 Universal SOC Investigation Formula

I would remember this:

```
CONTEXT → INVESTIGATE → DECIDE → ACT
```

**1. CONTEXT**

Who/what is involved?

Use:
- Identity inventory
- Asset inventory
- Network diagrams
- Threat intelligence

**2. INVESTIGATE**

What actually happened?

Check:
- SIEM logs
- Email details
- Processes
- Commands
- IP activity
- Previous and following events

**3. DECIDE**

Is it malicious or legitimate?

Ask:
- Is this expected?
- Does it match the user's role?
- Is there suspicious behaviour?
- Is there evidence of an attack?

Then: **TP or FP**

**4. ACT**

What should happen next?

- Write comment/report
- Close if FP
- Escalate if TP and deeper investigation/remediation is needed

---

## 📧 Example: Suspicious Email Workbook

You completed the practical, and its logic is basically:

```
START
  ↓
Take ownership of alert
  ↓
Get context about recipient
  ↓
Analyse email
  ↓
Check links/files and threat indicators
  ↓
Check related activity
  ↓
Is email malicious?
 ↙                ↘
YES                NO
 ↓                  ↓
Report             Close as FP
 ↓
Escalate to L2
```

You don't need to remember the exact TryHackMe wording.

If you understand why each step comes before the next, you understand the workbook.

---

## 🎯 One-line definitions to remember

| Term | Definition |
|---|---|
| **Identity Inventory** | Information about users and accounts. |
| **Asset Inventory** | Information about devices and servers. |
| **Network Diagram** | Shows how networks, systems, and subnets connect. |
| **SOC Workbook** | A structured guide that tells analysts what steps to follow during an investigation. |
| **Enrichment** | Gathering additional context. |
| **Investigation** | Analysing evidence to determine what happened. |
| **Escalation** | Passing an alert to L2 when deeper investigation or action is needed. |
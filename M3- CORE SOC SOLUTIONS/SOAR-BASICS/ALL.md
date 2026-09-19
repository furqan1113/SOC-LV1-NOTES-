# 🧠 SOAR — Everything So Far

## 1. Start with the SOC

A SOC's job is basically:

**Monitor → Detect → Investigate → Respond → Communicate**

It uses several security tools to do this.

```
                 SOC
                  │
      ┌───────────┼───────────┐
      ↓           ↓           ↓
     SIEM        EDR      Threat Intel
      │           │           │
      └───────────┼───────────┘
                  ↓
          Firewall / IAM
                  ↓
             IT / Ticketing
```

### What each one does

- **SIEM** → collects/correlates logs and helps detect suspicious activity.
- **EDR** → watches endpoints and can detect/respond to endpoint threats.
- **Threat Intelligence** → provides information about known/suspected malicious IPs, domains, hashes, etc.
- **Firewall** → controls network traffic.
- **IAM** → manages identities/accounts/access.
- **Ticketing** → documents and tracks incidents.

---

## 2. The problem with the traditional SOC

Having all these tools is useful, but it creates problems:

### Alert fatigue

```
Many alerts
   ↓
Too many to investigate manually
```

### Disconnected tools

```
SIEM → separate
EDR → separate
Firewall → separate
TI → separate
IAM → separate
```

Analysts may have to jump between them.

### Manual processes

The analyst repeatedly does:

```
Alert
 ↓
Check SIEM
 ↓
Check TI
 ↓
Check EDR
 ↓
Check IAM
 ↓
Block/disable something
 ↓
Create ticket
```

### Talent shortage

There may not be enough analysts to handle everything manually.

---

## 3. Enter SOAR

SOAR is the software/platform that helps coordinate these tools and automate workflows.

Think:

```
SIEM ─┐
EDR ──┤
TI ───┤
IAM ──┼──→ SOAR
FW ───┤
IT ───┘
```

Instead of the analyst manually moving between all of them, SOAR can coordinate actions through one platform.

---

## 4. The three words in SOAR

This is probably the most important thing to remember.

### 🔗 Orchestration = CONNECT

Connect different security tools.

```
SIEM + EDR + TI + Firewall + IAM
                 ↓
                SOAR
```

### ⚙️ Automation = DO IT AUTOMATICALLY

Execute predefined steps without requiring the analyst to manually perform every step.

### 🛡️ Response = TAKE ACTION

For example:

- Block IP
- Disable account
- Create ticket
- Isolate endpoint

So:

| Word | Meaning |
|------|---------|
| **Orchestration** | Connect |
| **Automation** | Do automatically |
| **Response** | Take action |

---

## 5. Where do Playbooks fit?

This is the other major concept.

A **playbook** is a predefined workflow inside SOAR. Think of it as a recipe.

For example, suppose the SIEM detects:

> **VPN brute-force alert**

The playbook could say:

```
VPN brute-force alert
        ↓
Check user's historical IP
        ↓
Check IP reputation
        ↓
Check successful logins
        ↓
Is IP malicious?
      /       \
    YES        NO
     ↓          ↓
Disable       Continue /
user          investigate
     ↓
Block IP
     ↓
Create ticket
```

SOAR follows the workflow and communicates with the different tools.

---

## 6. Phishing playbook

Same idea, different alert.

```
Suspicious email
       ↓
Create ticket
       ↓
URL or attachment?
    /          \
  URL        Attachment
   ↓             ↓
Analyze       Analyze
   ↓             ↓
Threat Intelligence
       ↓
Determine next action
```

You don't need to memorize the exact flowchart. Remember:

> **Playbook = predefined workflow for a particular recurring situation.**

---

## 7. CVE playbook

Same concept again:

```
New CVE
  ↓
Analyze details
  ↓
Assess risk
  ↓
Create patching ticket
  ↓
Test patch
  ↓
Deploy appropriately
```

The point isn't CVEs specifically. The point is:

> **A repeated SOC process can be turned into a playbook.**

---

## 8. Does SOAR replace the analyst?

**No.** This is important.

SOAR is particularly useful for repetitive and well-defined work, but analysts still handle:

- Important decisions
- Complex investigations
- Verification
- Business context
- Creating/improving playbooks

Think:

```
             SOC Analyst
                  │
             creates/
             manages
             playbooks
                  ↓
                SOAR
                  ↓
       Automates repetitive work
                  ↓
       Analyst handles judgment
       and complex investigation
```

---

## 🔥 The whole thing in one example

Imagine this happens: **an attacker tries to brute-force a VPN account.**

### Without SOAR

```
SIEM
 ↓
Alert
 ↓
Analyst notices it
 ↓
Open SIEM
 ↓
Check IP
 ↓
Open Threat Intelligence
 ↓
Check reputation
 ↓
Open IAM
 ↓
Check account
 ↓
Open Firewall
 ↓
Block IP
 ↓
Open ticketing system
 ↓
Create incident
```

Lots of manual work.

### With SOAR

```
             SIEM
              ↓
       VPN brute-force alert
              ↓
             SOAR
              ↓
        Playbook starts
              ↓
     ┌────────┼─────────┐
     ↓        ↓         ↓
    SIEM      TI       IAM
     │        │         │
     └────────┼─────────┘
              ↓
       Decision/action
              ↓
      Firewall / Ticket
```

- The SOAR platform **orchestrates** the tools.
- The **playbook** defines the workflow.
- The workflow can be **automated**.
- The resulting actions are the **response**.
- And the SOC analyst remains involved where judgment is needed.

---

## 🧠 What you actually need to remember

If you can explain these 6 lines from memory, you're done with the core concepts:

1. **SOC** → monitors, detects, investigates and responds to threats.
2. **Traditional SOC problems** → alert fatigue, disconnected tools, manual processes, talent shortage.
3. **SOAR** → software/platform that connects security tools and helps automate response workflows.
4. **Orchestration** → connects/coordinates tools.
5. **Automation** → performs predefined tasks automatically.
6. **Playbook** → predefined workflow telling SOAR what steps to perform for a particular type of alert.
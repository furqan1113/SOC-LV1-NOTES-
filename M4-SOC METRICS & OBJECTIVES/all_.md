# 📝 SOC Metrics and Objectives — Quick Notes

This last module is mainly awareness and understanding. You don't need to spend too much time memorising every formula right now. As an L1 analyst, the important thing is understanding **what** SOC performance metrics measure and **why** they matter.

---

## 1. Core Metrics

**Alerts Count (AC)**
Total number of alerts received.
Too many alerts = analyst overload and noise. Too few can also indicate visibility or SIEM problems.

**False Positive Rate (FPR)**
```
False Positives / Total Alerts
```
Measures how much alert noise the SOC receives. A very high rate means detection rules may need tuning. ( highest acceptable False Positive Rate for SOC team is 80% )

**Alert Escalation Rate (AER)**
```
Escalated Alerts / Total Alerts
```
Shows how often L1 analysts escalate alerts to L2. L1 should filter normal noise but should not hesitate to escalate something they don't understand.

**Threat Detection Rate (TDR)**
```
Detected Threats / Total Threats
```
Measures how reliably the SOC detects real threats. The goal should be as close to 100% as possible.

---

## 2. Important SOC Time Metrics

Think of the attack timeline like this:

```
Attack happens → SOC detects it → L1 starts triage → SOC stops/remediates it
```

**MTTD — Mean Time to Detect**
⏱️ Time between the attack happening and SOC tools detecting it.

**MTTA — Mean Time to Acknowledge**
⏱️ Time taken for L1 to acknowledge/start investigating the alert.

**MTTR — Mean Time to Respond**
⏱️ Time taken to stop/remediate the actual threat.

**Easy way to remember:**

```
Detect → Acknowledge → Respond
```
or:
```
See it → Start working → Stop it
```

### The question you did

- Alert detected after 12 minutes → **MTTD = 12**
- L1 moved it to In Progress 10 minutes later → **MTTA = 10**
- After that, 6 minutes before escalation + L2 spent 35 minutes cleaning malware

So:
```
MTTR = 6 + 35 = 41
```

Therefore:
```
12, 10, 41
```

> The important idea here is that **MTTR includes the time from the response process beginning until the threat is actually remediated**, so the 6-minute escalation period is included with the 35-minute cleanup.

---

## 3. How SOC Can Improve Metrics

**High False Positive Rate** — Too much alert noise.
Possible improvements:
- Tune SIEM/EDR detection rules
- Exclude trusted/expected activities
- Automate common alert triage using SOAR or scripts

**High MTTD** — Threats are detected too slowly.
Possible improvements:
- Improve detection rules
- Run detection rules more frequently
- Ensure logs reach the SIEM without delays

**High MTTA** — L1 takes too long to start investigating.
Possible improvements:
- Real-time analyst notifications
- Better alert distribution between analysts

**High MTTR** — The SOC takes too long to stop the threat.
Possible improvements:
- Escalate real threats quickly
- Have clear incident-response procedures and workbooks
- Ensure L1 knows when and how to escalate

---

## The Main Thing to Remember From This Module

Metrics are basically used to answer:

> How much noise does our SOC receive, how quickly do we detect threats, how quickly do analysts start working, and how quickly do we stop the attack?

For your SOC L1 learning, I would not spend much more time on this module. Just remember the major terms:

| Metric | Meaning |
|---|---|
| **FPR** | Noise |
| **TDR** | Are we detecting threats? |
| **MTTD** | Detect |
| **MTTA** | Start investigating |
| **MTTR** | Stop/respond |

That's enough for now. Later, when you work with a real SOC or SIEM, these metrics will make much more practical sense.
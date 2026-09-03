# SOC / SIEM Basics

## 1. Main Concept

Something happens → system records it → security tool checks it → if suspicious, you get an alert.

**Example:**
Furqan logs into a computer → Windows records the login → log is sent to SIEM → SIEM sees something unusual → Alert created

---

## 2. Important Things to Remember

### Event = Something happened

Examples:
- User logged in
- A program started
- A file was downloaded

### Log = Record of what happened

The system writes down details of the event.

**Example:** `User X logged in at 10:00 from IP address X`

### Alert = "Hey, check this!"

A SIEM/EDR creates an alert when an event or multiple events look suspicious. Not every event becomes an alert.

```
Millions of Events → Millions of Logs → Only suspicious ones → Alerts
```

### SOC L1's Job

When an alert appears:

**Check it → Understand what happened → Decide if it is dangerous → Escalate if needed**

---

## 3. What to Keep in Mind

The easiest way to remember this task:

| Term  | Meaning |
|-------|---------|
| Event | Action happened |
| Log   | Record of that action |
| Alert | Security tool thinks the action may be suspicious |

As a SOC L1, you mostly work with **alerts**, not manually with millions of events.

**Your question for every alert:**
> What happened, and is it actually a threat?

---

## 4. Where Alerts Can Be Managed

- **SIEM:** Common central place for monitoring and managing alerts.
- **EDR/NDR:** Can also generate and show alerts.
- **SOAR:** Can collect and centralise alerts from multiple security tools, especially in larger SOCs.
- **ITSM/Ticket system:** Can be used to track and manage alerts/incidents as tickets.

---

## 5. SOC Roles in Alert Triage

- **L1:** Reviews alerts, investigates basic evidence, decides whether activity is bad or normal, and escalates real threats.
- **L2:** Performs deeper investigation and remediation.
- **SOC Engineer:** Makes sure detections and alerts contain useful information for analysts.
- **SOC Manager:** Monitors the speed and quality of alert handling.
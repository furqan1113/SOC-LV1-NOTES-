# Task 5 — Alert Triage

## 1. Main Concept

**Alert Triage** = The complete process of handling an alert from the moment you pick it until you finish it.

**Simple flow:**
Prioritise → Assign to yourself → In Progress → Understand alert → Investigate → Decide TP/FP → Comment → Escalate if needed → Close

Think of it as:
**Pick the alert → Take ownership → Investigate it → Make a decision → Document it → Close or escalate it**

## 2. Important Things to Remember

### The Complete Alert Triage Flow

| Step | What You Do | Why |
| ---- | ------------- | ---- |
| 1. Prioritise | Choose the right alert first | Handle important threats quickly |
| 2. Assign to yourself | Take ownership of the alert | Prevent multiple analysts working on the same alert |
| 3. Move to In Progress | Show that you are investigating | Let the team know it is being handled |
| 4. Read the alert | Check name, description and important fields | Understand what the alert is about |
| 5. Note key indicators | Check hostname, user, IP, command, etc. | Know what/who you need to investigate |
| 6. Check for a workbook | Follow the alert's investigation instructions if available | Investigate in a standard and correct way |
| 7. Investigate in SIEM/EDR | Analyse the actual activity and logs | Find out what really happened |
| 8. Check surrounding events | Look before and after the alert | See the bigger picture and related suspicious activity |
| 9. Use Threat Intelligence if needed | Check IPs, domains, hashes, etc. | Verify whether something is known to be malicious |
| 10. Make a verdict | Decide True Positive or False Positive | Determine whether it was a real threat |
| 11. Add a comment | Write what you checked and why you made the verdict | Document your investigation for others |
| 12. Escalate if needed | Send serious/real threats to L2 | Allow deeper investigation and response |
| 13. Close the alert | Mark the investigation as finished | Complete the triage process |



## 3. What to Keep in Mind

The easiest way to remember the entire task is:

**TAKE → UNDERSTAND → INVESTIGATE → DECIDE → DOCUMENT → ACT**

In a real SOC L1 situation:

```
Alert appears
      ↓
Take ownership
      ↓
Understand what triggered it
      ↓
Investigate the user/host/IP and surrounding activity
      ↓
Decide: Real threat or not?
      ↓
Explain what you found in comments ant take notes 
      ↓
Escalate if necessary
      ↓
Close the alert
```

### The Main SOC L1 Mindset

Don't just look at the alert and decide based on its name or severity. Investigate the actual evidence, understand what happened, and then make your verdict.

This task is essentially the core workflow of a SOC L1 analyst.

---


# SOC L1 Alert Reporting — All-in-One Notes with Examples

## 1. Main Concept

After investigating an alert, an SOC L1 needs to:

**Report what was found → Make a verdict → Escalate if needed → Communicate with the right people**

**Simple workflow:**

```
Investigate → Report → Verdict → Close OR Escalate → Communicate
```

---

## 1️⃣ Alert Reporting

**Reporting** = Writing what you found and why you made your decision.

The report helps L2 or another analyst understand the case without starting from zero.

### Use the 5 Ws

| Question | Meaning | Example |
|----------|---------|---------|
| **Who** | Who was involved/affected? | Eddie Huffman, IT Manager |
| **What** | What happened? | Received a phishing email pretending to be Microsoft |
| **When** | When did it happen? | Mar 27, 2025, 19:25 |
| **Where** | Which system/account? | e.huffman@tryhackme.thm |
| **Why** | Why TP or FP? | SPF/DKIM failed and email used phishing techniques |

### Simple report example

> Eddie Huffman, IT Manager, received an email pretending to be from Microsoft Support. The email used urgent language and asked the user to download a report. SPF and DKIM checks failed, showing that the sender was not properly verified as Microsoft. Because of these phishing signs, I classified this alert as a **True Positive**.

### Remember

Only write what you can see or verify from the evidence. Don't add assumptions.

---

## 2️⃣ Escalation

**Escalation** = Passing an alert to L2 because it needs deeper investigation, action, or help.

### Escalate when:

- Major cyberattack is suspected.
- Deeper investigation or DFIR is needed.
- Remediation is required.
- Other teams need to be involved.
- You don't fully understand the alert.

### Practical Example — Domain Discovery

You investigated an alert and found:

- Host: `DMZ-MSEXCHANGE-2013`
- Commands checking Domain Admins and Domain Controllers.
- Commands running as `NT AUTHORITY\SYSTEM`.
- Parent process: `revshell.exe`.

**Your reasoning:**

> The commands are performing Active Directory/domain discovery. The parent process `revshell.exe` is highly suspicious and may indicate that the server is compromised.

**Verdict:** True Positive

### What next?

Because the server may be compromised and may require:

- Host isolation
- Deeper investigation
- Incident response

**You should:**

```
Write report → Set TP → Reassign alert to L2 → Escalate
```

---

## 3️⃣ Communication

**Communication** = Informing the right person/team when something important, urgent, unclear, or broken happens.

### Examples

| Situation | What to Do |
|-----------|------------|
| Critical alert, L2 not responding | Contact L2 → L3 → Manager/emergency contact |
| Teams/Slack account may be compromised | Don't message the user through the compromised account |
| Example | Call the user or use another trusted method |
| Too many alerts at once | Prioritise alerts and inform L2 about the high alert volume |
| You later realise you made a wrong verdict | Immediately inform L2 |
| SIEM logs are broken | Investigate what you can and report the issue; don't skip the alert |

### Important example

**User's Teams account may be hacked.**

❌ **Don't** send a Teams message asking:
> "Was this login from you?"

The attacker may control or read the account.

✅ **Use a trusted alternative:**
Call the user or contact them through another verified communication method.

---

## 🔥 What I Should Remember for SOC L1

### Full workflow

```
Alert → Prioritise → Investigate → Gather Evidence → Report → Verdict → Close OR Escalate → Communicate
```

### Easy example of the whole process

1. Suspicious phishing email appears
2. → L1 investigates it
3. → Finds SPF/DKIM failures and impersonation
4. → Writes what was found
5. → Sets True Positive
6. → If further action is required, such as checking other recipients or resetting credentials
7. → Escalates to L2

### Main Point

**Reporting** tells others what I found. **Escalation** gets the right level of help/action. **Communication** ensures the right people know what is happening.

### SOC L1 Mindset

> Don't blindly close alerts. Investigate using evidence, explain your reasoning clearly, and escalate or ask for help when the threat is serious or you are unsure.

---

## 🔥 Practical Alert Workflow — Important

When you start working on an alert:

```
Alert appears → Assign to yourself → Move to In Progress → Investigate
```

### Why assign it to yourself?

It shows the team you are responsible for investigating this alert and prevents multiple analysts from working on the same alert.

### After investigation:

**If you can finish it yourself**

```
Investigate → Write report/comment → Set TP/FP verdict → Close alert
```

**If it needs escalation**

```
Assign to yourself → Investigate → Write report → Set verdict → Reassign from yourself to L2 → L2 continues investigation
```

### The important difference

| Stage | Assignee |
|-------|----------|
| Alert is waiting | Unassigned / awaiting action |
| You start investigation | Assign to yourself (L1) |
| You finish it yourself | You close it |
| Alert needs deeper investigation/action | Reassign to L2 |

### One practical flow to remember

```
Take ownership → Investigate → Report → Verdict → Close OR assign to L2 → Communicate
```

### Simple example

**Suspicious `revshell.exe` alert:**

```
Alert → Assign to yourself → In Progress → Investigate → Find suspicious domain discovery + revshell.exe → Write report → True Positive → Reassign to L2 → Escalated.
```
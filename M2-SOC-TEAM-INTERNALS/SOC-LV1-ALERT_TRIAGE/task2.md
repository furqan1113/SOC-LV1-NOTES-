# Anatomy of an Alert

## 1. Main Concept

When an alert appears, it contains important information that helps you understand:

**What happened → When it happened → How serious it may be → Who is handling it → What evidence/details are available → What was the final result**

Think of an alert like a case file containing information you need to investigate.

| Alert Property   | Simple Meaning                                             | What You Should Think                  |
| ---------------- | ----------------------------------------------------------- | ---------------------------------------- |
| **Event Time**   | When the actual activity happened                          | **When did it happen?**                |
| **Alert Time**   | When the security tool created the alert                   | **When was I notified?**               |
| **Alert Name**   | Short title explaining what was detected                   | **What happened?**                     |
| **Severity**     | How urgent/serious the alert appears                        | **How serious could this be?**         |
| **Status**       | Current stage of the alert investigation                   | **Is anyone working on it?**           |
| **Verdict**      | Final decision about whether it was a real threat or not   | **Was it actually malicious?**         |
| **Assignee**     | Analyst responsible for the alert                           | **Who is handling it?**                |
| **Description**  | Explains why/how the alert was triggered                   | **Why did this alert appear?**         |
| **Alert Fields** | Actual evidence and details, such as hostname or command   | **What information do I investigate?** |

## 2. What to Keep in Mind

When you open an alert as a SOC L1, don't just randomly read everything. First understand these questions:

- What happened? → **Alert Name**
- When did it happen? → **Event Time**
- How urgent does it look? → **Severity**
- Is someone already working on it? → **Status/Assignee**
- Why was it triggered? → **Description**
- What evidence/details do I have? → **Alert Fields**
- What was the final decision? → **Verdict**
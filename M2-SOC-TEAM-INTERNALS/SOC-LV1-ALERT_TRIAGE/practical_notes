## 4. Triage in Practice

**Alert Triage** = Investigate the alert using evidence and context, then decide whether it is a real threat or not.

**Flow:**
Alert → Investigate → Check evidence/context → TP or FP → Comment → Close/Escalate

Triage here means: checking an alert properly and deciding what it actually is and what to do with it.

| Alert                               | Evidence / Context                                                                 | Verdict            | Why?                                                                                                                        |
| ------------------------------------ | ------------------------------------------------------------------------------------ | -------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **Potential Data Exfiltration**     | `5.8 GB` sent to `*.zoom.us` from `UK04/MEETINGROOM`, with `5.2 GB` also received     | **False Positive**  | Zoom video meetings can generate large two-way traffic. The destination and meeting-room context make it likely legitimate.  |
| **Double-Extension File Creation**  | File: `cats2025.mp4.exe` downloaded from a suspicious domain                        | **True Positive**   | The file is disguised as an MP4 video but is actually an `.exe` executable, a common malicious/phishing technique.           |
| **Download from GitHub Repository** | Accessed `github.com/facebook/react` from a developer user/network                  | **False Positive**  | The React repository is legitimate, and accessing/downloading it fits the developer context.                                |

**SOC L1 job = Don't guess.** Use the alert evidence and surrounding context to justify your verdict.

So, in one sentence:
> Triage = Taking an alert and checking its details and context to decide whether it is a real threat or normal activity, then taking the correct action.

The key part is that the alert itself is only the starting point.

**Alert says something might be wrong → Triage checks the evidence → Verdict says whether it actually was wrong.**
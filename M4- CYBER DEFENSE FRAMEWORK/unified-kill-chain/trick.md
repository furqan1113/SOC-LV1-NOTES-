# 🏦 UKC Walkthrough — ABC Bank Example

## 🟢 GET IN — Initial Foothold

### 1. Reconnaissance
An attacker researches ABC Bank and learns that employees use LinkedIn and that the company has a public email format such as `name@abcbank.com`.

### 2. Resource Development / Weaponization
The attacker prepares a fake website and an email that looks like it came from a legitimate company service.

### 3. Delivery
The attacker sends an employee a convincing email containing a link to the fake website.

### 4. Social Engineering
The email claims that the employee needs to verify their account, convincing the employee to interact with it.

### 5. Exploitation
The attacker takes advantage of a weakness in the employee's system or application to gain unauthorized access.

### 6. Persistence
The attacker establishes a way to maintain access even if the employee restarts their computer.

### 7. Defense Evasion
The attacker attempts to avoid security monitoring and make their activity look less suspicious.

### 8. Command & Control
The compromised computer communicates with infrastructure controlled by the attacker, allowing the attacker to interact with it.

---

## 🟠 GET THROUGH — Moving Inside the Network

### 9. Pivoting
The attacker uses the compromised employee's computer as a starting point to reach other parts of ABC Bank's internal environment.

### 10. Discovery
The attacker examines the environment to determine what computers, servers, accounts, and resources are available.

### 11. Privilege Escalation
The attacker obtains access with greater permissions than the original compromised account had.

### 12. Execution
The attacker runs commands or other actions on a system they have accessed.

### 13. Credential Access
The attacker obtains additional credentials that could provide access to other systems.

### 14. Lateral Movement
Using the additional access, the attacker moves from the employee's computer to another internal system, such as a server containing sensitive business information.

---

## 🔴 GET THE OBJECTIVE

### 15. Collection
The attacker gathers the information they were interested in, such as selected company documents.

### 16. Exfiltration
The attacker transfers the collected information outside ABC Bank's environment.

### 17. Impact
If disruption is part of the objective, the attacker may interfere with business systems or data.

### 18. Objectives
The attacker has now achieved the purpose of the operation — for example, stealing confidential information for financial gain.

---

## 🧠 Imagine the Whole Story As:

> Research ABC Bank → Trick an employee → Get inside → Stay inside → Avoid detection → Move through the network → Find valuable information → Take it → Achieve the goal.

# 🔗 UKC vs Threat Modelling — The Two Stories

## 🗡️ The Attacker's Story (UKC)

**Get In:**
> Find → Prepare → Deliver → Trick → Exploit → Stay → Hide → Control 

**Spread Through:**
> Pivot -> Discover → Escalate → Execute → Steal → Move

**Get Out:**
> Collect → Exfiltrate → Impact → Objective

---

## 🛡️ The Defender's Story (Threat Modelling)

Done *before* it happens — the mirror of the attacker's story:

> Identify assets → Find weaknesses → Protect → Prevent recurrence

---

## 🧠 The One Sentence That Ties It Together

> **"Know what an attacker would do (UKC), then ask what you'd need to protect against it (Threat Modelling)."**

Every UKC phase is basically a question a threat model should already have an answer for.
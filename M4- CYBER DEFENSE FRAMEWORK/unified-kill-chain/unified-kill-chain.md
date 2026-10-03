# 🔗 Unified Kill Chain — From the Root

Imagine an attacker wants to steal important company data.

The entire UKC can be understood as:

> **GET IN → MOVE THROUGH → GET OUT / ACHIEVE GOAL**

---

## 🟢 1. IN — Get a Foothold

The attacker is outside the organization and wants to get inside.

### 🔎 Reconnaissance — "What is there?"

They investigate:

- What servers exist?
- What software do they use?
- Who works there?
- What emails can I find?
- What might be vulnerable?

**Example:**

```
Find company.com
   ↓
Find VPN
   ↓
Find employees
   ↓
Find vulnerable web server
```

### 🔨 Weaponization — "Prepare my attack"

Now they prepare the things needed for the attack. Could be:

- Malware
- Payload
- C2 server
- Reverse-shell infrastructure

> "I know what I'm attacking. Now I'll prepare my equipment."

### 📤 Delivery — "Get it there"

Get the attack to the victim.

**Example:** Send malicious attachment by email.

### 🎭 Social Engineering — "Trick the human"

Instead of technically breaking in, manipulate someone.

**Example:** "Hey, I'm from IT. Please log in here." → Victim enters credentials.

### 💥 Exploitation — "Use the weakness"

The attacker takes advantage of a vulnerability.

**Example:** Vulnerable web application → execute attacker's code.

This is where they actually get code/access running.

### 🦠 Persistence — "Make sure I can come back"

The attacker doesn't want to lose access.

**Example:** Create a malicious service/backdoor.

So:
- **Exploitation** = Get in
- **Persistence** = Stay in

### 🥷 Defense Evasion — "Don't get caught"

The attacker tries to bypass security. Examples:

- Avoid antivirus
- Avoid IDS
- Hide malicious activity
- Bypass firewall/WAF

### 📡 Command & Control (C2) — "Talk to my machine"

The attacker establishes communication with the compromised computer.

```
Attacker
   ↕
C2 server
   ↕
Victim machine
```

Now they can send commands and receive information.

### ↪️ Pivoting — "Use this machine to reach another"

This is where the attacker starts using the compromised machine as a stepping stone.

```
Internet
   ↓
💻 Web Server ← compromised
   ↓
🔒 Internal Server
   ↓
🗄️ Database
```

The internal server wasn't directly reachable from the Internet. The attacker uses the web server to reach it.

---

## 🟡 2. THROUGH — Spread Through the Network

Now the attacker is inside. Their goal becomes:

> "What else can I reach, and how can I get more control?"

### 🔎 Discovery — "What's around me?"

They investigate:

- Users
- Computers
- Servers
- Files
- Shares
- Software
- Network
- Permissions

Basically: *"What's inside this organization?"*

### ⬆️ Privilege Escalation — "Can I become more powerful?"

Maybe they currently have: **Normal User**

They want: **Administrator / SYSTEM / ROOT**

They exploit vulnerabilities or misconfigurations.

### ⚙️ Execution — "Run my stuff"

Now they execute attacker-controlled code on systems. Examples:

- Malicious scripts
- Scheduled tasks
- Remote tools
- C2 commands

### 🔑 Credential Access — "Get passwords"

They steal credentials. Examples:

- Credential dumping
- Keylogging

**Why?** Because legitimate credentials can help them access other systems while looking more like a normal user.

### ↔️ Lateral Movement — "Move to other computers"

```
Computer A
   ↓
Computer B
   ↓
Server
   ↓
Domain environment
```

They use stolen credentials and privileges to move around.

---

## 🔴 3. OUT — Achieve the Actual Objective

Now they've reached the valuable stuff. They ask:

> "What did I actually come here for?"

### 📂 Collection — "Gather it"

Find valuable data:

- Documents
- Emails
- Browser data
- Files
- Audio/video
- Other sensitive information

### 📤 Exfiltration — "Take it OUT"

Move stolen data outside the organization.

```
Company
   ↓
Sensitive data
   ↓
📤 Attacker's server
```

- **Collection** = gather it
- **Exfiltration** = take it out

### 💥 Impact — "Damage it"

If the attacker's goal is disruption/destruction:

- Ransomware
- Data destruction
- Disk wiping
- Website defacement
- DoS
- Removing access

This attacks **Integrity** or **Availability**.

### 🎯 Objectives — "Why did they do all this?"

The final strategic goal, for example:

- 💰 **Money** → ransomware
- 🕵️ **Espionage** → steal confidential information
- 💥 **Destruction** → damage systems
- 📰 **Reputation damage** → leak private information

---

## 🧠 Now Look at the Whole Thing

Don't memorize 18 random words. See the story:

```
                 UNIFIED KILL CHAIN

                    🟢 IN
             "How do I get inside?"
                       ↓
        Recon → Weaponize → Deliver
                       ↓
             Social Engineering
                       ↓
                  Exploit
                       ↓
                Persistence
                       ↓
              Defense Evasion
                       ↓
                 C2 / Control
                       ↓
                  Pivot
                       ↓
                  🟡 THROUGH
          "How do I spread/get control?"
                       ↓
                Discovery
                       ↓
            Privilege Escalation
                       ↓
                 Execution
                       ↓
             Credential Access
                       ↓
             Lateral Movement
                       ↓
                    🔴 OUT
           "How do I achieve my goal?"
                       ↓
                 Collection
                       ↓
                Exfiltration
                       ↓
                   Impact
                       ↓
                  Objective
```

---

## 🔥 Connection with the Cyber Kill Chain

This is the big realization:

**Traditional Cyber Kill Chain:**

```
Find → Prepare → Deliver → Exploit → Stay → C2 → Goal
```

**Unified Kill Chain** takes that same idea and opens it up into much more detail:

```
Get in → Establish control → Explore → Escalate → Steal credentials
   → Move around → Collect → Exfiltrate/Destroy → Achieve objective
```

So you weren't supposed to learn UKC as 18 unrelated definitions. You were supposed to understand:

> An attacker starts outside → gets a foothold → establishes control → explores the environment → gains more privileges → moves through the network → reaches valuable assets → steals/damages something → achieves their objective.

### 🔄 One very important UKC idea: it isn't always a straight line

**Example:**

```
Get into PC A
   ↓
Discover PC B
   ↓
Pivot to B
   ↓
Discover more
   ↓
Find vulnerability
   ↓
Exploit B
   ↓
Discover PC C
   ↓
Pivot to C
```

The attacker can repeat phases and move backward/forward.


# 🔗 UKC vs Threat Modelling — The Two Stories

## 🗡️ The Attacker's Story (UKC)

**Get In:**
> Find → Prepare → Deliver → Trick → Exploit → Stay → Hide → Control → Pivot

**Spread Through:**
> Discover → Escalate → Execute → Steal → Move

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
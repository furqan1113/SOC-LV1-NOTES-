# Human Vectors — Overall Notes

## 1. Main Concept

Humans can be an entry point into an organization. Instead of directly breaking technical security, attackers may manipulate people to gain access, steal information, or get malware into a system. This is commonly done through social engineering.

Defending against these attacks involves both:

- **Mitigation** → Reduce/prevent attacks
- **Detection** → Find and investigate attacks that bypass protection

## 2. Important Things to Remember

### Why Attackers Target Humans

- Humans have access to email accounts, systems, databases, VPNs, sensitive information, etc.
- Attackers may target a specific person because of their access or privileges.
- Compromising one person can become the starting point for a larger attack.

### Social Engineering

- Social engineering means manipulating a person into helping the attacker, knowingly or unknowingly.
- Attackers often try to appear legitimate and trustworthy.
- They use emotions such as:
  - Urgency
  - Fear
  - Curiosity

### Common Attacks Against Humans

- **Phishing:** Tricks users into clicking malicious links, entering credentials, or opening malicious files.
- **Malicious downloads/websites:** Tricks users into downloading or running malware.
- **Deepfakes:** Fake AI-generated voice/video used to impersonate trusted people.
- **Impersonation:** Pretending to be someone trusted, such as IT support or management.
- Other threats can include USB drops, physical attacks, insider threats, and fake job offers.

These attacks can lead to:

**Stolen credentials → Malware infection → Unauthorized access → Further attacks**

### Defending Humans

There are two main parts:

**1. Mitigation**

Try to prevent attacks or reduce their chance/impact.

Examples:
- Anti-phishing tools → Block phishing emails.
- Antivirus / EDR → Protect and detect malware on devices.
- Trust but verify → Verify suspicious requests, even when they appear to come from trusted people.
- Security awareness training → Teach employees how to recognize threats.
- Phishing simulations → Practice recognizing phishing attacks.

**2. Detection**

No protection is perfect. Some attacks will bypass security controls.

When this happens:

**Attack bypasses protection → SOC detects it → SOC investigates it → Appropriate action is taken**

### Role of a SOC Analyst

Depending on the organization, a SOC analyst may:

- Monitor and investigate alerts.
- Detect attacks targeting employees.
- Work with teams such as IT and HR.
- Help employees who report suspicious activity.
- Suggest security improvements.
- Help improve security policies and employee awareness.
- Help reduce repeated attacks by identifying weaknesses and recommending mitigation.

## 3. What I Should Understand After This Room

I should understand that:

Attackers often target people because people have access to valuable systems and information. They use social engineering to manipulate victims. Security controls and training try to prevent these attacks, but when prevention fails, the SOC must detect and investigate them.

### Simple SOC L1 Takeaway

Humans can be the entry point. Prevent what you can, but assume some attacks will get through—then detect, investigate, and respond. Following cybersecurity news and threat reports helps improve awareness of what is happening in the real world.

### Useful Sites to Follow

- Krebs on Security
- The Hacker News
- BleepingComputer
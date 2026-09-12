## 1. What is Splunk?

**Splunk = a SIEM platform.**

More specifically, **Splunk is one example of a SIEM** (Security Information and Event Management) platform.

Other examples of SIEM platforms include:

* **Splunk**
* **Microsoft Sentinel**
* **IBM QRadar**
* **Elastic Security**
* **LogRhythm**

They all serve the general purpose of **collecting, searching, analyzing, and investigating security logs/events**, although their features and implementations differ.

> **SIEM = the category**
>
> **Splunk = one SIEM product/platform**

It takes logs from different sources and lets analysts **search, analyze and investigate** them.

```text
Windows ──┐
Linux ────┤
VPN ──────┤
Firewall ─┤ → SPLUNK → SOC Analyst
Web Server┘
```


## 2. The 3 Splunk Components

Remember these as **Collect → Process → Search**.

### Forwarder

> **Collect + Send**

Collects logs/data from monitored systems and sends them to the Indexer.

### Indexer

> **Process + Store**

Receives data, parses/normalizes it, creates useful field-value information and stores events.

### Search Head

> **Search + Analyze**

Where the analyst searches the indexed data using **SPL**.

```text
Log Source
    ↓
Forwarder
    ↓
Indexer
    ↓
Search Head
    ↓
Analyst
```

---

## 3. Navigating Splunk

You don't need to memorize every button.

Just know:

* **Search & Reporting** → where you search/investigate logs
* **Dashboard** → visual overview
* **Splunk Bar** → navigation/settings/apps/etc.
* **Add Data** → bring data into Splunk

---

## 4. Adding Data

You practiced uploading **VPN_logs**.

The basic process:

```text
VPN_logs
   ↓
Add Data → Upload
   ↓
Select Source
   ↓
Select Source Type
   ↓
Input Settings
   ↓
Index = VPN_Logs
   ↓
Review
   ↓
Done
```

The VPN file was **newline-delimited JSON**, meaning each line represents an event.

---

## 5. Index

An **index** is where Splunk stores the data so you can search it.

You created:

```text
VPN_Logs
```

So:

```spl
index=VPN_Logs
```

basically means:

> **"Search my VPN_Logs data."**

---

## 6. SPL

### SPL = Search Processing Language

It's simply the language you use to **ask Splunk questions about your logs.**

Think of the `|` as:

> **THEN**

Example:

```spl
index=VPN_Logs
| spath
| search UserName="Maleena"
| stats count
```

Read it:

> Go to VPN_Logs → **THEN** extract fields → **THEN** find Maleena → **THEN** count.

---

## 7. The SPL Commands You Learned

These are the ones worth remembering right now:

### `index=`

**Where to look**

```spl
index=VPN_Logs
```

---

### `spath`

**Extract fields from JSON**

```spl
| spath
```

Your VPN data is JSON, so `spath` makes fields such as:

```text
UserName
Source_ip
Source_Country
```

available for searching.

---

### `search`

**Filter/find what you want**

```spl
| search UserName="Maleena"
```

Means:

> Only show events where UserName is Maleena.

---

### `stats count`

**How many matching events?**

```spl
| stats count
```

---

### `values(UserName)`

**Which unique usernames appeared?**

```spl
| stats values(UserName)
```

---

### `as`

**Rename the output**

```spl
count as Events
```

means:

> Count the events and call the result `Events`.

And:

```spl
values(UserName) as Username
```

means:

> Get the usernames and call that output `Username`.

---

## 8. Your Useful Combined Query

You figured this one out yourself:

```spl
index="Vpn_logs"
| spath
| search Source_ip="107.14.182.38"
| stats values(UserName) as Username count as Events
```

Read it as normal English:

> **Search VPN logs → extract JSON fields → find this IP → tell me which username(s) used it and how many events there were.**

For your data, you found:

```text
Username → Smith
Events   → 26
```

That's actually a nice example of basic SOC-style log investigation.

---

## 9. The Most Important Mental Model

When you're working in Splunk, think:

```text
          I HAVE LOGS
               ↓
       WHERE ARE THEY?
          index=...
               ↓
      ARE THEY JSON?
          spath
               ↓
     WHAT AM I LOOKING FOR?
            search
               ↓
       WHAT DO I WANT TO KNOW?
        ┌──────┴──────┐
        ↓             ↓
      count       values(...)
      HOW MANY?       WHO?
```

That's **much more useful than memorizing SPL syntax**.

---

# 🧠 FINAL CHEAT SHEET

| Thing           | Remember it as                |
| --------------- | ----------------------------- |
| **Splunk**      | SIEM platform                 |
| **Forwarder**   | Collect + Send                |
| **Indexer**     | Process + Store               |
| **Search Head** | Search + Analyze              |
| **Index**       | Where data is stored/searched |
| **SPL**         | Language for searching Splunk |
| `\|`            | THEN                          |
| `index=`        | Where to look                 |
| `spath`         | Extract JSON fields           |
| `search`        | Filter                        |
| `stats count`   | How many?                     |
| `values(field)` | Which unique values?          |
| `as`            | Rename output                 |
| **Dashboard**   | Visual overview               |

### And the biggest thing:

> **You don't need to memorize exact queries. Learn to read them from left to right and understand what question each part is asking.**

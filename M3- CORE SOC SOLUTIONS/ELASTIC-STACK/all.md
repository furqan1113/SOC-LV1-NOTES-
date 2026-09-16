# 🔎 Elastic Stack (ELK) — Complete SOC L1 Notes

## 1. What is Elastic Stack?

Elastic Stack (ELK) is a collection of components used to **collect, process, store, search, analyze, and visualize** large amounts of data/logs.

It was originally developed for general data searching and visualization, but many SOC teams use it for security log analysis and investigations — almost like a SIEM.

> **For SOC L1:** You mainly need to know how to use **Kibana** to search and investigate logs. You don't need to become an expert in how ELK works internally.

---

## 2. ELK Components

The basic pipeline:

```
Logs / Data
     ↓
   Beats          "Collect & Ship"
     ↓
  Logstash        "Process / Normalize"
     ↓
Elasticsearch     "Store & Search"
     ↓
   Kibana         "View & Analyze"
     ↓
SOC Analyst
```

### 🟢 Beats
Host-based data-shipping agents. They collect specific data from endpoints and send it onward.

- `Winlogbeat` → Windows Event Logs
- `Packetbeat` → Network traffic flows

> **Remember:** Beats = Collect & Ship

### 🟡 Logstash
Processes data coming from different sources. Can filter and normalize the data before sending it to its destination.

Basic structure:
```
INPUT → FILTER → OUTPUT
```
- **Input** → where data comes from
- **Filter** → process/normalize the data
- **Output** → where processed data goes

> **Remember:** Logstash = Process

### 🔵 Elasticsearch
A search and analytics engine that stores data/documents. Think of it as a large searchable data store.

> **Remember:** Elasticsearch = Store + Search + Analyze

### 🟣 Kibana
Web-based interface that works with Elasticsearch. This is where the analyst can:

- Search logs
- Investigate events
- Apply filters
- Create visualizations
- Create dashboards

> **Remember:** Kibana = View + Analyze

---

## 3. Kibana Discover

Discover is the main workspace for exploring and investigating logs.

```
Kibana
  ↓
Discover
  ↓
Search / Filter
  ↓
Investigate logs
```

For this room, you worked with the `vpn_connections` data.

### Important Discover Elements

**Logs**
Each row represents a log/event containing fields and values. Example:
```
UserName        = James
Source_ip       = 238.x.x.x
Source_Country  = United States
```

**Fields Pane**
Shows the available fields extracted from the logs (e.g. `UserName`, `Source_ip`, `Source_Country`, `State`, `Action`). You can use these fields to apply filters.

**Index Pattern / Data View**
Tells Kibana which Elasticsearch data you want to explore. For the lab: `vpn_connections`.
> Think: *"Which dataset am I investigating?"*

**Search Bar**
Where you enter searches using KQL.

**Time Filter**
Limits your investigation to a specific period — very important in SOC investigations. For the THM lab, you needed to make sure **January 2022** was included.

**Timeline**
Shows the number of events over time.

```
Normal activity:  ████ ███ ████ ███
Sudden spike:     ████████████████████
```

A spike can indicate unusual activity worth investigating.
> **Important:** A spike is an *anomaly*, not automatically an attack.

**Add Filter**
Allows you to filter specific fields through the UI instead of manually writing a query.

Example: `Source_ip → is → 238.163.231.224`

You can also exclude values.

---

## 4. KQL — Kibana Query Language

KQL is the language used in Kibana's search bar to search/filter Elasticsearch data.

| Platform | Query Language |
|---|---|
| Splunk | SPL |
| Elastic | KQL |

### Free-text Search
```
United States
```
Searches for the term in the available log data rather than specifying one particular field.

### Wildcard `*`
```
United*
```
Means the term can continue after "United." Useful when you don't know the complete term.

---

## 5. KQL Logical Operators

### AND — both conditions must match
```
"United States" AND "Virginia"
```
Meaning: United States **AND** Virginia.

### OR — either condition can match
```
"United States" OR "England"
```
Meaning: United States **OR** England.

### NOT — exclude something
```
"United States" AND NOT ("Florida")
```
Meaning: United States, **but not** Florida.

---

## 6. Field-Based KQL ⭐

This is especially important for SOC investigations.

**Syntax:**
```
Field : Value
```

Example:
```
Source_ip : 238.163.231.224
```
Meaning: Find events where `Source_ip` is `238.163.231.224`.

**Combining fields:**
```
Source_ip : 238.163.231.224 AND UserName : Suleman
```
Meaning: Find events from this IP **AND** belonging to Suleman.

**Grouped conditions:**
```
Source_Country : "United States"
AND
(UserName : "James" OR UserName : "Albert")
```
Meaning: US events where the user is either James or Albert.

---

## 7. SOC Investigation With KQL

This is where everything comes together. Suppose you are investigating:
```
Source_ip : 238.163.231.224
```

You can progressively narrow your investigation:

```
IP → User → Country → State → Time → Action
```

Example:
```
Source_ip : 238.163.231.224
AND NOT State : "New York"
```
You're asking: *"Show me activity from this IP, excluding New York."*

This is exactly the kind of filtering you practiced in the room.

---

## 8. Visualizations

Once you've found useful information, you don't always want to look at raw logs. Kibana can turn the data into:

- Tables
- Pie charts
- Bar charts
- Other visualizations

Example — *VPN Connections by Country*:
```
USA       █████████████
France    ███████
India     ████
```

**Why?** Because visualizations make patterns and relationships easier to see.

---

## 9. Correlation

Correlation here means looking at the relationship between different fields, for example:
```
Source_IP ↔ Source_Country
```

You could create a table:

| Source IP | Country | Count |
|---|---|---|
| X.X.X.X | USA | 500 |
| Y.Y.Y.Y | France | 300 |

This helps you understand which IPs are associated with which countries and how much activity they generated.

---

## 10. Failed VPN Investigation

You also practiced investigating failed VPN connections. The important filter was:
```
action : failed
```

Then you could analyze:
```
UserName
Source_ip
```

Questions you answered included:
- Which user had the greatest number of failed attempts?
- How many failed VPN connections occurred in January?

This is basic but realistic SOC analysis.

---

## 11. Dashboards

A dashboard is a collection of saved searches and visualizations in one place.

```
Visualization 1 ─┐
Visualization 2 ─┤
Saved Search ────┼──→ Dashboard
Visualization 3 ─┘
```

Example SOC dashboard:

```
┌──────────────────────────────────────┐
│        VPN SECURITY DASHBOARD        │
├──────────────────┬───────────────────┤
│ Failed Attempts  │ Countries         │
│                  │                   │
│ James      45    │ USA     ███████   │
│ Smith      31    │ France  ████      │
│ John       12    │ India   ██        │
├──────────────────┴───────────────────┤
│ VPN Activity Over Time               │
│       📈                             │
└──────────────────────────────────────┘
```

It gives analysts a single view of important information.

---

## 🔥 Complete Elastic SOC Workflow

This is probably the best thing to remember from the entire room:

```
                    LOGS
                     ↓
                   BEATS
              Collect / Ship
                     ↓
                 LOGSTASH
             Process / Normalize
                     ↓
              ELASTICSEARCH
                Store / Search
                     ↓
                  KIBANA
                     ↓
                DISCOVER
                     ↓
             Search with KQL
                     ↓
               Filter / Analyze
                     ↓
             Find anomalies
                     ↓
             Visualization
                     ↓
                Dashboard
```

And as the SOC analyst:

```
I have thousands of logs.
       ↓
Which ones matter?
       ↓
Search/filter them.
       ↓
What happened?
       ↓
Is anything unusual?
       ↓
Investigate further.
```

---

## 🧠 MUST REMEMBER

If you forget almost everything else, remember these:

**ELK**
- Beats → Collect
- Logstash → Process
- Elasticsearch → Store/Search
- Kibana → Analyze/Visualize

**Kibana**
- Discover = investigate logs

**KQL**
- `Field : Value`
- `AND` = both
- `OR` = either
- `NOT` = exclude
- `*` = wildcard

**Visualization**
Turn data into charts/tables to see patterns more easily.

**Dashboard**
Combine saved searches + visualizations into one overview.
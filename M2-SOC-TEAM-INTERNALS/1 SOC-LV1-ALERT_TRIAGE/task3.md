# Task 4 — Alert Prioritisation

## 1. Main Concept

When there are many alerts, you cannot investigate all of them randomly.

**Alert Prioritisation = Deciding which alert to investigate first.**

The goal is to investigate the most important threats quickly.

## 2. Important Things to Remember

| Step               | What to Do                     | Simple Meaning                                                                                          |
| ------------------ | ------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **1. Filter alerts**  | Check status/assignee           | Don't take alerts already reviewed or being investigated by someone else. Take new and unresolved alerts. |
| **2. Sort by Severity** | Critical → High → Medium → Low  | Investigate alerts that could cause the biggest impact first.                                            |
| **3. Sort by Time**   | Oldest → Newest                 | If alerts have the same priority, investigate the older one first because the threat may have been active longer. |

### Why Severity Comes First?

A Critical alert is generally more likely to represent a serious threat and potentially have a greater impact than a Low or Medium alert.

But remember:
> Severity is used to decide priority. It does not prove that the alert is a real attack.

### Why Check the Oldest Alert?

Imagine two alerts have similar severity:
- Alert A → Created 1 hour ago
- Alert B → Created 5 minutes ago

Usually investigate Alert A first because if it is a real attack, the attacker may have already had more time to cause damage.

## 3. What to Keep in Mind

When you see many alerts:

1. Is it new and unassigned?
2. How severe is it?
3. If severity is similar, which one is older?

### SOC L1 Priority Flow

**Ignore alerts already handled → Critical first → Then High → Then Medium → Then Low → Oldest first within the same priority**

The point: Don't randomly pick alerts. Use a systematic order so serious threats are less likely to be missed or delayed.
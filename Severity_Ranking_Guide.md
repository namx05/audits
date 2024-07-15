# Severity Ranking Guide

> This guide is just a note of Owen's YouTube video: [Is This A Critical? How To Rank Vulnerability Severity
> ](https://www.youtube.com/watch?v=f4UdAnHUpSE)

<br>

Table of contents:

- [Pashov's Guide](#pashov)
- [Critical](#critical)
- [High](#high)
  - [Difference b/w High and Mediums](#difference-between-high--medium)
- [Medium](#medium)
  - [Difference b/w Medium and Low](#difference-between-medium--low)
- [Low](#low)

<br>

# Pashov's Severity Ranking System

| Severity           | Impact: High | Impact: Medium | Impact: Low |
| ------------------ | ------------ | -------------- | ----------- |
| Likelihood: High   | Critical     | High           | Medium      |
| Likelihood: Medium | HIgh         | Medium         | Low         |
| Likelihood: Low    | Medium       | Low            | Low         |

<br>

# Critical

- You know a critical when you see one 😀
- Anything that a malicious actors can pull off to successfully take a nontrivial amount of value (20%+) out of the protocol
- Or “griefing” attacks that have wide bearing implications, e.g. a malicious actor can brick withdrawals and cause all users to lose their deposited funds.

### Difference Between High & Medium

- How guaranteed is it? How impactful is it?
  - Does it rely on frontrunning on a network with no mempool? → High (or even medium)
  - is it 100% certain the user will profit? or is it more like 70%? → High
- How impactful is it?
  - Does it effect all users in a significant way? → probably a critical
  - Does it cause one user to lose all their funds?
    - can it be repeated to effect every user? → Critical
    - can it literally only apply to one special user? → High
  - Does it take time to play out?
    - Months+? → Probably High
    - Days? → Critical

<br>

# High

- Attacks that are not straightforward, might be somewhat unlikely but have large consequences.
- more impact and more likelihood than medium findings, however not a guaranteed protocol ending hack
- attacks that require significant amount of capital (that cannot be flash loaned)
  - TWAP manipulation that would have significant effect on the protocol
  - reference exchange manipulation
  - abusing the protocol’s logic with large amounts of value
- often griefing attacks are High
  - Griefing attacks are simple attacks that harms other users or the protocol itself, but do not pose any obvious benefit to the malicious actor
  - significant gas griegfing “can I cause the protocol to expend $500 in extra gas a day??”
  - DoS is often a form of griefing, but can also be critical if the DoS has wide implications on the functionality of the protocol.

### Difference Between High & Medium

- How guaranteed is it? How impactful is it?
  - Rare, but huge consequences → Likely still high
  - rare, with decent consequences → probably medium
  - probable with huge consequences → High or even Critical
  - Probable with decent consequences → High

<br>

# Medium

- No significant impact, however not trivial impact.
  - A few $ effect on a user or the protocol
- Can also be things that have significant impact but are extremely rare.
- things that pose a potential risk that can be leveraged by an attacker, e.g. rounding in the wrong direction.
- centralization Risks

### Difference between Medium & Low

- If user’s behave correctly, will it impact them in any noticeable way (besides gas)?
  - yes → Medium+
  - No → Low
- Does it pose a risk of nontrivial exploit or mishap in the future?
  - yes → Medium
  - No → Low

<br>

# Low

- Owen Thrum always thought that It’s best to combine gas optimization, QA, and best practices into low findings.
  - If you want to systemize auditing to the greatest extent possible, having less buckets and less complexity will help.
- Bugs that have very noticeable impact or litreally no impacts.

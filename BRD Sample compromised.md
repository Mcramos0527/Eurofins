# Damaged Sample Intake Alert — Business Requirements Document (v2, Final Discovery)

**Ticket:** #1 · **Prepared by:** Max Ramos · **Team:** Eurofins IT Business Analysis
**Status:** :white_check_mark: Cleared to proceed to Epic/Feature/Story breakdown

---

## Table of Contents
- [1. Purpose](#1-purpose)
- [2. Background](#2-background)
- [3. Current State by Site](#3-current-state-by-site)
- [4. Key Findings](#4-key-findings)
- [5. Scope](#5-scope)
- [6. Stakeholders](#6-stakeholders)
- [7. Interim Mitigation](#7-interim-mitigation-in-effect-now)
- [8. Success Criteria](#8-success-criteria)
- [9. Resolved Questions](#9-resolved-questions)
- [10. Approval](#10-approval)

---

## 1. Purpose

Replace the manual, paper-based methods currently used at all three lab sites (Dublin, Madrid, Lisbon) to identify and handle damaged samples with a system-enforced flag, block, and audit trail. This closes a data integrity gap in which a damaged sample can be tested and reported without any independent system control catching it.

## 2. Background

Ticket #1 was raised by the Madrid QC Lead reporting that damaged samples were not being flagged consistently. Discovery was conducted across three rounds:
1. Independent site-by-site mapping with all three QC Leads
2. A technical review with the Solution Architect
3. A joint working session with all three QC Leads, the Architect, and a Dublin night-shift technician, to validate operational fallbacks before finalizing scope

## 3. Current State by Site

### Madrid
Damaged sample flagged with a physical sticky note attached to the sample. Sample remains in the normal testing queue with no physical separation. No system status differentiates a damaged sample from a normal one.

> :warning: **Confirmed failure:** sticky note missed, sample tested, out-of-range result surfaced approximately two days later and was traced back.

### Dublin
Damaged sample physically moved to a dedicated rejection bin, separate from the normal queue. Sample ID recorded on a shared whiteboard. QC review required before the sample can leave the bin. No system status differentiates a damaged sample from a normal one.

> :warning: **Confirmed failure:** whiteboard wiped at end of week before review occurred; sample was mistakenly returned to the queue.

### Lisbon
Damaged sample is not registered into LIMS until a shift supervisor makes an accept/reject decision on the spot. Rejected samples are logged in a paper reject book. No system record exists during the decision window.

> :warning: **Confirmed gap:** if the supervisor check is skipped, the sample can be registered and tested normally with no hard stop preventing it.
>
> :white_check_mark: **Follow-up:** this registration sequencing is legacy practice, not a documented operational requirement — final sign-off from Lisbon's manager pending.

## 4. Key Findings

### Finding 1 — Shared root cause
All three sites rely entirely on a subsequent out-of-range test result as the only detection mechanism. No site has any independent system control. A damaged sample producing a plausible, in-range result would go undetected at any of the three sites today.

### Finding 2 — Upstream judgment gap
No standardized definition of "damaged" exists across sites. Borderline cases are judged inconsistently, with no review or record of the decision — including cases where a flag is raised and then cleared without documentation.

### Finding 3 — Frequency is unmeasured
No site formally tracks how often this occurs. The only figure available (approximately 50–60 incidents over six months) is Madrid's estimate, not a logged number.

### Finding 4 — Informal second-opinion channel already in use `NEW`
A Dublin night-shift technician confirmed that borderline cases are already informally escalated today — typically by texting a photo of the sample to whoever is reachable (often, but not always, the day-shift lead). There is no defined on-call list; reachability is based on personal knowledge of who tends to answer, not a documented rotation. This channel currently carries real accept/reject decisions with no audit trail.

### Finding 5 — No system, anywhere, is shift-aware `NEW`
Confirmed with the Architect and both Madrid and Dublin QC Leads: neither LIMS nor any other system at Eurofins currently tracks who is on shift in real time. Shift scheduling exists only as informal shared spreadsheets at each site. Automatic system-based routing to "whoever is currently on duty" is not feasible without separate, currently non-existent, workforce infrastructure.

## 5. Scope

**In scope:**
- [x] System-enforced flag for a damaged sample at intake, across all three sites
- [x] Automatic block from the testing queue once flagged
- [x] Audit trail entry for every flag, and for every override/clearance, including who cleared it and when
- [x] Notification to the relevant site's QC Lead; **failed notification attempts must themselves raise an alert** (not fail silently) — independent of the block, which does not depend on notification success
- [x] Second-reviewer ("four-eyes") requirement on clearing a flag, with a defined fallback for single-staffed shifts: a manually maintained, site-owned shared list of reachable second reviewers, plus a maximum wait time before escalation
- [x] Lisbon: align registration sequencing with Madrid/Dublin (register immediately, flag as a subsequent status update) — pending final confirmation from Lisbon's manager

**Out of scope (for this phase):**
- [ ] A standardized cross-site definition of damage severity (parked for future discussion)
- [ ] Automated frequency/trend reporting dashboards
- [ ] Retroactive review of historical samples
- [ ] **System-aware, automatic shift-based routing** of second-reviewer requests — parked as a future recommendation. Depends on workforce-scheduling infrastructure that does not currently exist, and the usage data to justify that investment doesn't exist yet either. Revisit only once real data is available under the in-scope fix.

## 6. Stakeholders

| Stakeholder | Role |
|---|---|
| Madrid QC Lead | Originating requester |
| Dublin QC Lead | Site stakeholder |
| Lisbon QC Lead | Site stakeholder |
| Dublin night-shift technician | Operational input |
| Accessioning technicians (3 sites) | End users |
| Phyllis Coyle | Product Manager |
| Solution Architect | Technical scoping |

## 7. Interim Mitigation (in effect now)

Madrid and Dublin have agreed, as their own operational decision, to combine their existing workarounds (sticky note **and** rejection bin together, rather than either alone) while the permanent fix is built. Lisbon's workflow has no equivalent physical workaround to combine and continues as-is pending the system fix.

## 8. Success Criteria

Zero damaged samples reach testing without a system-recorded exception, for 30 consecutive days post-hypercare, across all three sites.

## 9. Resolved Questions

| Question | Resolution |
|---|---|
| Is Lisbon's registration sequencing a hard constraint? | No — legacy practice, not a requirement (final sign-off pending) |
| Does override require four-eyes? | Yes, with a defined fallback for single-staffed shifts (shared reviewer list + escalation timeout) |
| Must notification failure be visible? | Yes — must alert independently of the block itself |
| Should the system auto-route to on-shift staff? | **Parked** — not pursued in this phase |

## 10. Approval

Reviewed with Product Manager (Phyllis Coyle) and Solution Architect. Cleared to proceed to Epic/Feature/Story breakdown and sprint scoping.

---
*Related: Ticket #1 · Meeting minutes — Cross-Site Discovery · Architect Review · Joint Working Session*

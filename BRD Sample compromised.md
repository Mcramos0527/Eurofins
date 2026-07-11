# Damaged Sample Intake Alert — Business Requirements Document

**Ticket:** #1 · **Prepared by:** Max Ramos · **Team:** Eurofins IT Business Analysis
**Status:** :white_check_mark: Cleared to proceed to solution scoping (PM sign-off: Phyllis Coyle)

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
- [9. Open Questions for Engineering](#9-open-questions-for-engineering)
- [10. Approval](#10-approval)

---

## 1. Purpose

Replace the manual, paper-based methods currently used at all three lab sites (Dublin, Madrid, Lisbon) to identify and handle damaged samples with a system-enforced flag, block, and audit trail. This closes a data integrity gap in which a damaged sample can be tested and reported without any independent system control catching it.

## 2. Background

Ticket #1 was raised by the Madrid QC Lead reporting that damaged samples were not being flagged consistently. Discovery sessions were conducted independently with QC Leads at all three sites to compare current-state handling before any solution was proposed.

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

## 4. Key Findings

### Finding 1 — Shared root cause
All three sites rely entirely on a subsequent out-of-range test result as the only detection mechanism. No site has any independent system control. A damaged sample producing a plausible, in-range result would go undetected at any of the three sites today.

### Finding 2 — Upstream judgment gap
No standardized definition of "damaged" exists across sites. Borderline cases are judged inconsistently by individual technicians (or, in Lisbon, a shift supervisor), with no review or record of the decision — including cases where a flag is raised and then cleared without documentation.

### Finding 3 — Frequency is unmeasured
No site formally tracks how often this occurs. The only figure available (approximately 50–60 incidents over six months) is Madrid's estimate, not a logged number.

## 5. Scope

**In scope:**
- [x] System-enforced flag for a damaged sample at intake, across all three sites
- [x] Automatic block from the testing queue once flagged
- [x] Audit trail entry for every flag, and for every override/clearance
- [x] Notification to the relevant site's QC Lead

**Out of scope (for this phase):**
- [ ] A standardized cross-site definition of damage severity (parked for future discussion)
- [ ] Automated frequency/trend reporting dashboards
- [ ] Retroactive review of historical samples

## 6. Stakeholders

| Stakeholder | Role |
|---|---|
| Madrid QC Lead | Originating requester |
| Dublin QC Lead | Site stakeholder |
| Lisbon QC Lead | Site stakeholder |
| Accessioning technicians (3 sites) | End users |
| Phyllis Coyle | Product Manager |
| IT / Architecture | Solution scoping |

## 7. Interim Mitigation (in effect now)

Madrid and Dublin have agreed, as their own operational decision, to combine their existing workarounds (sticky note **and** rejection bin together, rather than either alone) while a permanent fix is scoped. This does **not** address Finding 2 (the upstream judgment gap) and does **not** apply to Lisbon, whose current workflow has no equivalent physical workaround to combine.

## 8. Success Criteria

Zero damaged samples reach testing without a system-recorded exception, for 30 consecutive days post-hypercare, across all three sites.

## 9. Open Questions for Engineering

- Does LIMS currently have any data model concept that a damaged-sample status could build on, or does this require new data model work?
- Lisbon's workflow delays LIMS registration until after a human decision — does the solution need a different technical trigger point for Lisbon versus Madrid/Dublin?
- What is the right mechanism to guarantee segregation of duties between who can flag a sample and who can clear/override that flag?

## 10. Approval

Reviewed and cleared to proceed to solution scoping with architecture/engineering, per Product Manager sign-off (Phyllis Coyle).

---

*Related: Ticket #1 · Meeting minutes — Cross-Site Discovery Discussion*

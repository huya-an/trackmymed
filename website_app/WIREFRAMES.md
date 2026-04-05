# TrackMyMed — Web App Wireframes

> Low-fidelity wireframes and navigation decisions for the consumer-facing web application.
> Agency/supervisor views are deferred — this document covers the family/personal user tier only.

---

## Navigation Structure

```
Dashboard                   ← Today across ALL patients (cross-patient daily view)

── Dorothy Johnson ──        ← Patient section (one per person being managed)
   Medications               ← Med list, schedule, pill count, OCR scan
   Care Circle               ← Members, roles, invites, alert settings (per patient)
   Reminders                 ← Escalation ladder config (channels, order, timing)
   Activity Log              ← Full audit trail: every dose, who, how, verification quality
   Reports                   ← Weekly report card, patterns, escalation trends, PDF export

── Robert Johnson ──         ← Second patient (e.g. managing both parents)
   Medications
   Care Circle
   Reminders
   Activity Log
   Reports

── Add Patient ──

Settings                     ← Account, billing, profile
```

### Navigation decisions

- **Care Circle is per patient** — the people caring for Dorothy are different from those caring for Robert.
- **Reports is per patient** — every report type in the plan (weekly card, audit log, escalation history, pattern intelligence, doctor export) is patient-scoped.
- **Dashboard is cross-patient** — the only cross-patient view needed for family tier. Covers "how are all my people doing today."
- **Agency/supervisor views deferred** — cross-patient organizational reporting is an agency-tier feature, not needed for family MVP.

### Role-based access (same screens, different permissions)

| Role | Sees | Can Do |
|---|---|---|
| **Primary Contact** | Everything | Full control, invite/remove members, configure reminders |
| **Helper** | Schedule + current meds + activity log | Log doses, view history |
| **Observer** | Weekly report email only | Read-only in app |

---

## Shell

Applies to all screens. Sidebar is 220px fixed. Main content area fills remaining width.

```
╔══════════════════════════════════════════════════════════════════════════════════════╗
║  WEB APP — SHELL                                                                    ║
╠═══════════════╦════════════════════════════════════════════════════════════════════╣
║  SIDEBAR      ║  TOP BAR                                                           ║
║  220px        ║  [Page Title]                          [Action Btn] [Primary CTA]  ║
║               ╠════════════════════════════════════════════════════════════════════╣
║  TrackMyMed   ║                                                                    ║
║  ───────────  ║  MAIN CONTENT AREA                                                 ║
║  Dashboard    ║                                                                    ║
║               ║                                                                    ║
║  Dorothy J.   ║                                                                    ║
║   Medications ║                                                                    ║
║   Care Circle ║                                                                    ║
║   Reminders   ║                                                                    ║
║   Activity Log║                                                                    ║
║   Reports     ║                                                                    ║
║               ║                                                                    ║
║  + Add Patient║                                                                    ║
║               ║                                                                    ║
║  Settings     ║                                                                    ║
║  ───────────  ║                                                                    ║
║  [●] Sarah J. ║                                                                    ║
║  Primary      ║                                                                    ║
╚═══════════════╩════════════════════════════════════════════════════════════════════╝
```

---

## Screen 1 — Dashboard

Cross-patient. Shows today's status for everyone being managed.

```
╔══════════════════════════════════════════════════════════════════════════════════════╗
║  SCREEN 1 — DASHBOARD                                                               ║
╠═══════════════╦════════════════════════════════════════════════════════════════════╣
║  TrackMyMed   ║  Dashboard                              [🔔]  [+ Add Medication]   ║
║  ───────────  ╠════════════════════════════════════════════════════════════════════╣
║▶ Dashboard    ║                                                                    ║
║               ║  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌────────────┐  ║
║  Dorothy J.   ║  │ Today's     │ │ 7-Day       │ │ Care Circle │ │ Next       │  ║
║   Medications ║  │ Doses       │ │ Adherence   │ │             │ │ Reminder   │  ║
║   Care Circle ║  │ 4 / 5 taken │ │ 91%         │ │ 3 members   │ │ 8:00 PM    │  ║
║   Reminders   ║  └─────────────┘ └─────────────┘ └─────────────┘ └────────────┘  ║
║   Activity Log║                                                                    ║
║   Reports     ║  ┌───────────────────────────────────────┐ ┌──────────────────┐   ║
║               ║  │ Today's Schedule          View all →  │ │ Care Circle      │   ║
║  + Add Patient║  │                                       │ │ Activity         │   ║
║               ║  │ ● Lisinopril 10mg   8:00 AM  [Taken]  │ │                  │   ║
║  Settings     ║  │ ○ Metformin 500mg  12:00 PM [Pending] │ │ Maria confirmed  │   ║
║  ───────────  ║  │ ● Atorvastatin 20mg  8:00 PM [Taken]  │ │ 8 AM dose        │   ║
║  [●] Sarah J. ║  │                                       │ │ Today, 8:07 AM   │   ║
║  Primary      ║  │                                       │ │ ──────────────── │   ║
╚═══════════════║  │                                       │ │ SMS sent to      │   ║
                ║  │                                       │ │ Dorothy          │   ║
                ║  │                                       │ │ Today, 7:55 AM   │   ║
                ║  └───────────────────────────────────────┘ └──────────────────┘   ║
                ╚════════════════════════════════════════════════════════════════════╝
```

---

## Screen 2 — Medications

Per patient. Med list grouped by time of day. Pill count, Med Lock status, refill alerts.

```
╔══════════════════════════════════════════════════════════════════════════════════════╗
║  SCREEN 2 — MEDICATIONS                                                             ║
╠═══════════════╦════════════════════════════════════════════════════════════════════╣
║  TrackMyMed   ║  Medications                    [⊙ Scan Label]  [+ Add Medication] ║
║  ───────────  ╠════════════════════════════════════════════════════════════════════╣
║  Dashboard    ║                                                                    ║
║               ║  Morning                                                           ║
║  Dorothy J.   ║  ┌──────────────────────────────────────────────────────────────┐  ║
║▶  Medications ║  │ ● Lisinopril      10mg · 8:00 AM · 28 pills   [Med Lock ✓] … │  ║
║   Care Circle ║  ├──────────────────────────────────────────────────────────────┤  ║
║   Reminders   ║  │ ● Metformin       500mg · 8:00 AM with food · 14 pills      … │  ║
║   Activity Log║  └──────────────────────────────────────────────────────────────┘  ║
║   Reports     ║                                                                    ║
║               ║  Evening                                                           ║
║  + Add Patient║  ┌──────────────────────────────────────────────────────────────┐  ║
║               ║  │ ○ Atorvastatin    20mg · 8:00 PM · 30 pills   [Med Lock ✓] … │  ║
║  Settings     ║  └──────────────────────────────────────────────────────────────┘  ║
║  ───────────  ║                                                                    ║
║  [●] Sarah J. ║  ⚠ Metformin running low — 14 pills remaining. Request refill.     ║
║  Primary      ║                                                                    ║
╚═══════════════╩════════════════════════════════════════════════════════════════════╝
```

---

## Screen 3 — Care Circle

Per patient. Members, roles, invites, per-member alert settings.

```
╔══════════════════════════════════════════════════════════════════════════════════════╗
║  SCREEN 3 — CARE CIRCLE                                                             ║
╠═══════════════╦════════════════════════════════════════════════════════════════════╣
║  TrackMyMed   ║  Care Circle — Dorothy Johnson                  [+ Invite Member]  ║
║  ───────────  ╠════════════════════════════════════════════════════════════════════╣
║  Dashboard    ║                                                                    ║
║               ║  ┌───────────────────────────────────────┐ ┌──────────────────┐   ║
║  Dorothy J.   ║  │ Circle Members              3 members │ │ Alert Settings   │   ║
║   Medications ║  ├───────────────────────────────────────┤ │                  │   ║
║▶  Care Circle ║  │ [●] Sarah Johnson (You)               │ │ Missed dose      │   ║
║   Reminders   ║  │     sarah@email.com                   │ │ alerts      [ON] │   ║
║   Activity Log║  │     Gets all alerts & weekly report   │ │                  │   ║
║   Reports     ║  │                    [Primary Contact]  │ │ Weekly report    │   ║
║               ║  ├───────────────────────────────────────┤ │ email       [ON] │   ║
║  + Add Patient║  │ [●] Michael Johnson                   │ │                  │   ║
║               ║  │     michael@email.com                 │ │ Circle           │   ║
║  Settings     ║  │     Can log doses & view schedule     │ │ activity   [OFF] │   ║
║  ───────────  ║  │                          [Helper] …  │ └──────────────────┘   ║
║  [●] Sarah J. ║  ├───────────────────────────────────────┤                        ║
║  Primary      ║  │ [●] Linda Park                        │                        ║
╚═══════════════║  │     Receives weekly report only       │                        ║
                ║  │                        [Observer] …  │                        ║
                ║  ├───────────────────────────────────────┤                        ║
                ║  │ PENDING INVITE                        │                        ║
                ║  │ [○] james@email.com · Observer        │                        ║
                ║  │     Invited 2 days ago    [Resend]   │                        ║
                ║  └───────────────────────────────────────┘                        ║
                ╚════════════════════════════════════════════════════════════════════╝
```

---

## Screen 4 — Reminders

Per patient. Configure the escalation ladder: which channels fire, in what order, how long to wait between steps.

```
╔══════════════════════════════════════════════════════════════════════════════════════╗
║  SCREEN 4 — REMINDERS                                                               ║
╠═══════════════╦════════════════════════════════════════════════════════════════════╣
║  TrackMyMed   ║  Reminders — Dorothy Johnson                                       ║
║  ───────────  ╠════════════════════════════════════════════════════════════════════╣
║  Dashboard    ║                                                                    ║
║               ║  Patient contact                                                   ║
║  Dorothy J.   ║  ┌──────────────────────────────────────────────────────────────┐  ║
║   Medications ║  │ Dorothy's phone:  +1 (555) 000-0000                          │  ║
║   Care Circle ║  │ Preferred channel: SMS                          [Edit]        │  ║
║▶  Reminders   ║  └──────────────────────────────────────────────────────────────┘  ║
║   Activity Log║                                                                    ║
║   Reports     ║  Escalation ladder                                                 ║
║               ║  ┌──────────────────────────────────────────────────────────────┐  ║
║  + Add Patient║  │ Step 1 │ Push notification        [ON]   Wait: 15 min  [Edit] │  ║
║               ║  │ Step 2 │ SMS text message          [ON]   Wait: 20 min  [Edit] │  ║
║  Settings     ║  │ Step 3 │ AI voice call (Amy)       [ON]   Wait: 30 min  [Edit] │  ║
║  ───────────  ║  │ Step 4 │ Alert care circle         [ON]   Always              │  ║
║  [●] Sarah J. ║  └──────────────────────────────────────────────────────────────┘  ║
║  Primary      ║                                                                    ║
╚═══════════════║  ⓘ AI voice calls require Premium plan.                            ║
                ╚════════════════════════════════════════════════════════════════════╝
```

---

## Screen 5 — Activity Log

Per patient. Full chronological audit trail of every dose event with verification quality signal.

```
╔══════════════════════════════════════════════════════════════════════════════════════╗
║  SCREEN 5 — ACTIVITY LOG                                                            ║
╠═══════════════╦════════════════════════════════════════════════════════════════════╣
║  TrackMyMed   ║  Activity Log — Dorothy Johnson          [Filter ▾]  [Export CSV]  ║
║  ───────────  ╠════════════════════════════════════════════════════════════════════╣
║  Dashboard    ║                                                                    ║
║               ║  Today — Apr 6, 2026                                               ║
║  Dorothy J.   ║  ┌──────────────────────────────────────────────────────────────┐  ║
║   Medications ║  │ 8:07 AM  Lisinopril 10mg     Confirmed by Maria  [Geotag ✓]  │  ║
║   Care Circle ║  │                              ████████████ Strongest           │  ║
║   Reminders   ║  ├──────────────────────────────────────────────────────────────┤  ║
║▶  Activity Log║  │ 7:55 AM  SMS reminder sent → Dorothy                          │  ║
║   Reports     ║  ├──────────────────────────────────────────────────────────────┤  ║
║               ║  │ 8:00 AM  Metformin 500mg     Confirmed via SMS reply         │  ║
║  + Add Patient║  │                              ████████░░░░ Moderate            │  ║
║               ║  └──────────────────────────────────────────────────────────────┘  ║
║  Settings     ║                                                                    ║
║  ───────────  ║  Yesterday — Apr 5, 2026                                           ║
║  [●] Sarah J. ║  ┌──────────────────────────────────────────────────────────────┐  ║
║  Primary      ║  │ 8:15 PM  Atorvastatin 20mg   Confirmed via AI call (Amy)     │  ║
╚═══════════════║  │                              █████████░░░ Strong              │  ║
                ║  ├──────────────────────────────────────────────────────────────┤  ║
                ║  │ 8:00 PM  AI call placed → Dorothy (SMS had no response)       │  ║
                ║  ├──────────────────────────────────────────────────────────────┤  ║
                ║  │ 8:10 AM  Lisinopril 10mg     Confirmed by Dorothy (push)      │  ║
                ║  │                              ██████░░░░░░ Lighter              │  ║
                ║  └──────────────────────────────────────────────────────────────┘  ║
                ╚════════════════════════════════════════════════════════════════════╝
```

**Verification quality signal (shown as bar):**
| Method | Signal |
|---|---|
| Caregiver in-person + geotag | Strongest |
| Patient confirmed via AI voice call | Strong |
| Patient confirmed via SMS reply | Moderate |
| Patient confirmed via push / button click | Lighter |

---

## Screen 6 — Reports

Per patient. Weekly report card, pattern intelligence, escalation trends, doctor visit export.

```
╔══════════════════════════════════════════════════════════════════════════════════════╗
║  SCREEN 6 — REPORTS                                                                 ║
╠═══════════════╦════════════════════════════════════════════════════════════════════╣
║  TrackMyMed   ║  Reports — Dorothy Johnson       [📅 This week ▾]  [↓ Export PDF]  ║
║  ───────────  ╠════════════════════════════════════════════════════════════════════╣
║  Dashboard    ║                                                                    ║
║               ║  ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────────────┐  ║
║  Dorothy J.   ║  │ Weekly    │ │ Doses     │ │ Missed    │ │ Escalations       │  ║
║   Medications ║  │ Adherence │ │ On Time   │ │ Doses     │ │ Needed            │  ║
║   Care Circle ║  │   91%     │ │  19 / 21  │ │     2     │ │   1 phone call    │  ║
║   Reminders   ║  └───────────┘ └───────────┘ └───────────┘ └───────────────────┘  ║
║   Activity Log║                                                                    ║
║▶  Reports     ║  ┌──────────────────────────────────────┐ ┌───────────────────┐   ║
║               ║  │ Daily Adherence  ● Taken  ● Missed   │ │ Pattern Insights  │   ║
║  + Add Patient║  │                                      │ │                   │   ║
║               ║  │  █  █     █  █  █     █              │ │ Weekend dip       │   ║
║  Settings     ║  │  █  █  ▄  █  █  █  ▄  █              │ │ 2 of 3 misses     │   ║
║  ───────────  ║  │  █  █  █  █  █  █  █  █              │ │ were Sat–Sun      │   ║
║  [●] Sarah J. ║  │ Mon Tue Wed Thu Fri Sat Sun           │ │ ─────────────     │   ║
║  Primary      ║  │                                      │ │ SMS preferred     │   ║
╚═══════════════║  └──────────────────────────────────────┘ │ 90% first contact │   ║
                ║                                            │ ─────────────     │   ║
                ║                                            │ ↑ vs last month   │   ║
                ║                                            │ 91% vs 84%        │   ║
                ║                                            └───────────────────┘   ║
                ╚════════════════════════════════════════════════════════════════════╝
```

**Report contents (from product plan):**
- Doses given on time, late, or missed
- Who administered each dose
- Escalation history — first contact vs required escalation, trends over time
- Pattern intelligence — time-of-day, day-of-week, escalation trends, pill count discrepancies
- Exportable PDF for doctor visits

---

## Feature Coverage Checklist

| Plan Feature | Screen |
|---|---|
| Escalation Ladder (SMS → AI call → alert) | Reminders |
| Proof of Care / audit trail | Activity Log |
| Verification quality signal (geotag > AI call > SMS > push) | Activity Log |
| Med Lock (double-dose prevention) | Medications |
| Pill count reconciliation + refill alerts | Medications |
| OCR label scanning | Medications |
| Care circle + role-based access | Care Circle |
| Per-patient alert settings | Care Circle |
| Weekly Care Report Card | Reports |
| Pattern intelligence | Reports |
| Escalation history trends | Reports |
| Doctor visit PDF export | Reports |
| Cross-patient daily overview | Dashboard |
| Account, billing, profile | Settings |
| Easy Button hardware | Phase 2 — deferred |
| Alexa integration | Phase 2 — deferred |
| Agency/supervisor dashboards | Agency tier — deferred |

---

*Last updated: April 2026*
*Pencil design file: C:\trackmymeds\design\1st template test*

# MedTrack — Product Plan

## Vision
A medication tracking platform with accountability partners, serving both individuals and small businesses. Goal: help people never forget their medication.

## Discovery Answers
*(Recording answers as we discuss)*

### 1. Target Business Scenario
> **Three core user groups:**
>
> **A. Home Health Agencies (B2B)**
> Multiple employees coordinating care for one individual. The home office needs visibility that medications are being administered properly. This is their operational accountability tool.
>
> **B. Long-Distance Family Caregivers (B2C)**
> Families who don't live close to aging parents/grandparents. Not yet at the point of needing a home agency, but need peace of mind that mom/dad/grandma/grandpa are taking their meds.
>
> **C. Families Overseeing Home Agencies (B2C monitoring B2B)**
> Adult children who ARE paying for a home health agency and want to verify they're getting what they pay for. Medication adherence = proof of care quality. This is a trust & accountability layer on top of the agency.

### 2. Accountability Partner Definition
> **Varies by group, all support multiple people:**
>
> **A. Home Health Agency**
> - Home office monitors all caregivers across all patients
> - Caregivers hand off shifts — critical safety feature: prevent double-dosing when shifts change
> - System must track WHO administered WHAT and WHEN to prevent overlap
>
> **B. Long-Distance Family**
> - Group sharing among siblings/family members (not just one person carrying the load)
> - Primary contact with backup contacts
> - No artificial limit on number of people in the group
>
> **C. Family Oversight of Agency**
> - One or multiple siblings watching over agency care
> - No restrictions on group size
>
> **The Medication Taker Themselves**
> - YES, the patient should interact with the system too
> - Must be EASY — this is likely an elderly person
> - Innovation opportunity — explore multiple confirmation methods:
>   - Physical hardware button (click to confirm)
>   - SMS/text message reply ("Did you take your 5pm meds?" → reply YES)
>   - Phone call (automated voice prompt, press 1 to confirm)
>   - App notification (if they're app-capable)
>   - Smart speaker integration?
> - Cost considerations matter — needs to scale to millions of users
> - This is a key differentiator — no competitor does multi-channel patient confirmation

### 3. Primary User Age Range
> **All demographics. Not niching down.**
> - Elderly (grandparents/parents being monitored by family or agencies)
> - Adults managing their own chronic conditions
> - Parents tracking children's medications — **DEFERRED (see note below)**
> - The core product must work for everyone — "help people take their medication"
>
> **COPPA Note:** Children under 13 create compliance complexity (parental consent requirements, data collection restrictions, FTC enforcement). Defer this demographic to a future extension. Focus MVP on adults 18+.
>
> **Design implication:** UI needs to be simple enough for an 80-year-old but not feel patronizing to a 35-year-old. The multi-channel confirmation approach (SMS, call, hardware, app) naturally solves this — each user picks the channel that fits them.

### 4. Key Differentiators

#### FEATURE 1: The Escalation Ladder
> **What it is:** An intelligent, multi-channel, adaptive reminder and escalation system. First software-only platform to offer what previously required $50/month hardware subscriptions.
>
> **Channels (MVP — US only):**
> 1. Push notification (app) — Free
> 2. SMS/Text message — reply to confirm (~$0.01/msg)
> 3. Automated AI phone call — conversational voice bot (~$0.10-0.15/min)
> 4. Email — for summary digests to accountability partners, not real-time patient reminders
> 5. Alexa/smart speaker integration — proactive reminder, voice confirmation
>
> **Deferred to Phase 2:**
> - Easy Button hardware device
> - Video call
> - Smartwatch
> - WhatsApp / international messaging
>
> **Escalation Logic:**
> Patient gets reminder via preferred channel → No response in X minutes → Next channel fires → Still nothing → Primary accountability partner alerted → Backup partners alerted → Agency home office alerted (if applicable). System learns which channels each patient responds to best and adapts over time.
>
> **AI Voice Call Spec:**
> - Friendly, warm, soothing voice with a persona name (e.g., "Hi, this is Amy from MedTrack, an automated assistant here to help you")
> - Clearly identified as a bot/automated assistant — not pretending to be human
> - **HARD GUARDRAILS — THE AI WILL NEVER:**
>   - Give medical advice of any kind
>   - Say what a medication is or what it's for
>   - Say how much to take or dosage information
>   - Make wellness assessments or diagnoses
> - **THE AI WILL:**
>   - Ask if the patient has taken their medication and confirm
>   - If patient is confused or has questions, provide comfort: "I'm going to contact your caregiver right now, just hold on"
>   - Escalate to the care circle immediately when the patient expresses confusion, distress, or asks medical questions
>   - Pass along ALL learnings/context from the conversation to the care circle (e.g., "Margaret reported stomach pain and couldn't find her pills")
>   - This is NOT a wellness call — but any information volunteered by the patient is captured and shared with caregivers
>
> **Business Model for AI Calls:**
> - Some amount of AI calls included free
> - AI calling is a premium/paid feature beyond the free tier
> - Exact pricing TBD in business plan phase
>
> **Competitive Advantage:**
> No pure software competitor offers more than push notifications to the patient. SMS and phone calls currently exist only on expensive hardware platforms (MedMinder, Hero Health). MedTrack would be the first to deliver multi-channel + escalation + AI voice in software alone. Alexa integration does not exist in any competitor.

#### FEATURE 2: Proof of Care
> **What it is:** An auditable, verifiable log of every medication event with timestamp and location data. Creates trust and transparency across all user segments.
>
> **Core capabilities:**
> - Every medication event is **timestamped** (when was the dose confirmed/administered)
> - Every caregiver-administered dose is **geotagged** (confirms caregiver was at the patient's location) — especially important for paid caregivers
> - All events logged with **who** administered/confirmed the dose
> - **Weekly Care Report Card** — automated summary sent to the care circle
>   - Doses given on time, late, or missed
>   - Who administered each dose
>   - Patterns and trends
>   - Especially valuable for families paying for home health agencies (proof you're getting what you pay for)
>   - Also useful for family accountability groups and personal use
>
> **What we're NOT doing:**
> - No photo verification — impractical and invasive
>
> **Applies to all user segments:**
> - Agencies: home office verifies caregiver performance
> - Families overseeing agencies: proof of care quality
> - Long-distance families: peace of mind that meds are being taken
> - Personal use: self-accountability and shareable reports for doctor visits

#### FEATURE 3: Medication Verification & Safety System (Med Lock)
> **What it is:** A comprehensive medication safety system that prevents errors, tracks pill inventory, and creates a rich audit trail with verification quality signals.
>
> **A. Smart Bottle Setup via OCR**
> - Patient or caregiver snaps a photo of the prescription label
> - OCR auto-extracts: medication name, dosage, frequency (day/night), pill count
> - Extracted data is sent to the care circle for human verification before going live
> - Goal: make medication setup as frictionless as possible while maintaining accuracy
>
> **B. Pill Count Reconciliation**
> - Starting count recorded from the bottle (e.g., 30 pills)
> - Each logged dose decrements the count
> - At any time, a caregiver can reconcile: "We've logged 10 doses, there should be 20 left"
> - Mismatch triggers an alert — catches overdosing, missed logging, or diversion
> - Low pill count triggers refill reminders
>
> **C. Rich Logging — Every Entry Records:**
> - **What** medication was taken
> - **When** it was taken (timestamp)
> - **Who** confirmed it (patient self, caregiver name, AI bot)
> - **How** it was verified — verification method carries weight:
>   - Caregiver in-person + geotag = strongest anchor
>   - Patient confirmed via AI voice call = strong
>   - Patient confirmed via SMS reply = moderate
>   - Patient confirmed via push notification / button click = lighter
> - This weighting gives care circles and agencies a quality-of-verification signal, not just a yes/no
>
> **D. Escalation History in the Log**
> - Track whether patient confirmed on first contact or required escalation
> - Surface trends over time: "Patient confirmed on first text 90% in January, but required phone call escalation 60% in February"
> - Changes in escalation patterns are meaningful care signals (cognitive decline, routine changes, medication side effects)
> - Feeds into the Weekly Care Report Card (Feature 2)
>
> **E. Med Lock (Double-Dose Prevention)**
> - When a dose is logged, that medication is locked for the dosing window
> - Next shift caregiver sees: "Lisinopril — given by Maria at 2:15 PM. Next dose: 8:15 PM."
> - Cannot log the same medication again until the window opens
> - Critical safety feature for blood thinners, insulin, heart medications
> - Prevents errors during shift handoffs at home health agencies

#### FEATURE 4: The Easy Button (Phase 2 — Hardware)
> **What it is:** A small, cheap physical button that sits next to the pill box. Removes all technology barriers for non-tech-savvy patients.
>
> **How it works:**
> - Button lights up and beeps when it's med time
> - Patient presses it to confirm they took their meds
> - Confirmation feeds directly into the same dashboard/log as all other channels
> - That's it. No phone, no app, no screen.
>
> **Design:**
> - Single button (dead simple)
> - Color-changing LED indicates context: e.g., blue for morning, orange for evening
> - WiFi connected (no cellular — avoids data plan costs)
> - Requires patient to have home WiFi
>
> **Manufacturing:**
> - Design in-house, outsource manufacturing
> - Target cost: ~$15-20 per unit at scale
> - FCC certification required for WiFi device
>
> **Phase 2 — not in MVP**

#### FEATURE 5: Pattern Intelligence
> **What it is:** AI-driven pattern detection across all adherence data. Surfaces insights that humans would never catch manually. This is the heart of the Care Report Card.
>
> **Pattern types to detect:**
> - Time-of-day patterns: "Evening meds missed 4 of last 7 days, mornings never missed"
> - Day-of-week patterns: "Adherence drops every weekend"
> - Shift correlation: "3 PM shift changes correlate with 40% higher miss rate for 3:30 PM dose"
> - Escalation trends: "Patient used to confirm on first text, now requires phone call 60% of the time"
> - Caregiver performance patterns: "Caregiver A logs on time 95%, Caregiver B is late 40%"
> - Pill count discrepancies and trends
>
> **Output:**
> - Powers the Weekly Care Report Card (Feature 2)
> - Real-time alerts for significant pattern changes
> - Historical trend views in the dashboard
> - Exportable/shareable reports for doctor visits
> - Especially critical for home health agencies — shows operational performance clearly
>
> **HARD GUARDRAIL:**
> - Surfaces PATTERNS AND DATA ONLY — never medical advice
> - Never recommends dosage changes, medication changes, or clinical actions
> - Presents facts: "here's what's happening" — the humans decide what to do about it
>
> **MVP vs Phase 2:**
> - Core to MVP — this is a key differentiator and the backbone of the reporting system

### 5. Accountability Direction & Role-Based Access
> **Personal use:** Can be one-way or two-way. No restrictions. Two friends or a couple can mutually track each other.
>
> **Small business (agency):** One-way, but with multiple layers/circles:
> - **Hands-on caregivers** — limited view. They see what they need for their shift: current medications, schedule, recent doses, Med Lock status. They come and go; many people rotate through.
> - **Supervisors / case managers** — holistic view. Full medication history, all caregiver logs, pattern intelligence reports, pill count reconciliation, performance data across all caregivers on a case.
> - **Business owner / home office** — organizational view. All cases, all supervisors, all caregivers. Operational dashboards.
>
> **Personal / family circles also have layers:**
> - **Primary contact** (e.g., adult child managing parent's care from afar) — full access, gets all reports, manages the circle
> - **Helpers** (e.g., Aunt Susie who stops by, a neighbor) — limited view, can log doses and see the current schedule but not full history or reports
> - **Observers** (e.g., a sibling who wants visibility but isn't actively caregiving) — read-only, gets the weekly report
>
> **Key architectural note:** Role-based data access must be designed into the data model from day one. Not all users in a circle see the same data. This affects API design, UI views, and notification routing.
>
> **Important UX distinction:** Some users are far away and are "extra eyes" — they just need to know things are happening. Others are hands-on and need operational tools. The interface should reflect which role you're in.

### 6. Business Model
> **Philosophy: Low paywall, high traction.** Attract users with generosity. Don't nickel-and-dime on things that are cheap to provide. Monetize on things that genuinely cost us money to deliver.
>
> **Free Tier (generous — this is our acquisition engine):**
> - Unlimited medications (this alone beats Medisafe's 2-med paywall)
> - Full log history (storage is cheap, don't gate it)
> - Push notification reminders
> - SMS text reminders to patient (critical — patients can participate without downloading the app; may add SMS cap later if costs require it)
> - Full escalation ladder (multi-channel + adaptive learning)
> - Care circle with role-based access
> - Weekly reports
> - Med Lock / shift safety
> - OCR bottle scanning for medication setup
> - Pattern intelligence (basic trends)
> - Alexa integration
> - Email digests
>
> **Premium (personal) — genuinely expensive-to-deliver features:**
> - AI voice calls
> - Advanced pattern intelligence (deeper analysis, predictive insights)
> - Priority support
>
> **Business Tier (agencies) — operational tools at scale:**
> - Everything in Premium
> - Multi-caregiver management across cases
> - Geotag verification on caregiver doses
> - Supervisor vs caregiver role-based dashboards
> - Organizational reporting across all patients/cases
> - Caregiver performance analytics
> - Bulk onboarding tools
>
> **Hardware (Phase 2):**
> - Easy Button — sold as a one-time purchase
>
> **Pricing TBD** — but the principle is clear: free tier should be so good that people switch from Medisafe immediately. Premium earns its price through channels that cost real money to operate.

### 7. Privacy Positioning
> **Lead with it. This is a core brand pillar.**
>
> - We will NEVER sell user data. Period.
> - This is a front-and-center marketing message, not fine print
> - 79% of competitors share data with third parties — we are the antidote
> - Build to HIPAA-equivalent standards from day one (positions us for B2B agency sales AND gets ahead of incoming HIPRA legislation)
> - Clear, human-readable privacy policy — not legalese
> - Brand messaging: "Your health data is yours."
>
> **Ethical AI:**
> - Our AI features (voice calls, pattern intelligence) are built on ethical AI principles
> - AI never gives medical advice, never oversteps its role
> - AI is transparent — always identifies itself as an automated assistant
> - AI exists to serve the patient and care circle, not to monetize their data
> - "Ethical AI" is a brand pillar alongside privacy — especially important as we market the premium AI features
> - This is a trust differentiator: our AI helps, it doesn't exploit
>
> **Competitive advantage:** Trust is everything in health. Being the privacy-first, ethical-AI medication platform in a market full of data sellers is a powerful differentiator, especially for the agency/B2B segment where HIPAA compliance is expected.

### 8. Platform Strategy
> **Full platform approach — web + mobile:**
>
> **Mobile App: React Native (iOS + Android)**
> - Single codebase, native performance on both platforms
> - For patients, caregivers, and family members on the go
> - Reliable push notifications, background tasks, geolocation for Proof of Care
>
> **Web Application:**
> - Full-featured web app — not a dumbed-down companion
> - Essential for care circles, especially business tier supervisors and home offices
> - Dashboards, reporting, pattern intelligence, caregiver management
> - Family members who prefer desktop also use this
> - Must feel like the same platform as the mobile app — consistent experience
>
> **This is a platform, not just an app.**

### 9. Web Application Purpose
> **The web app is a full-featured platform, not a companion — it does everything the mobile app does.**
>
> Key use cases:
> - **Dashboard** — manage medications, view schedules, see care circle status
> - **Onboarding/intake** — set up a new patient, add medications (including OCR upload)
> - **Caregiver logging** — log that meds were given during a visit
> - **Reports & pattern intelligence** — view weekly reports, trends, escalation history
> - **Circle management** — invite members, set roles, manage permissions
> - **Agency administration** — supervisor dashboards, caregiver management, multi-case views
>
> Many users (especially supervisors, family members, business admins) prefer managing on a desktop/web browser rather than a phone app. The web app is a first-class citizen.

### 10. MVP Timeline
> **Target launch: Early May 2026 (~2 months)**
>
> **Launch plan:**
> - Product launch into the App Store (iOS) and Google Play (Android) + web app
> - Paid advertising to follow launch
> - Pitch to caregiving agencies for B2B adoption
>
> **Implication:** Must scope MVP ruthlessly. Core experience must be rock solid. Phase 2 features (Easy Button, etc.) are clearly post-launch.

### 11. Team & Roles
> **Two-person team + AI (Claude as product owner & development partner)**
> - Lean team — speed is an advantage, not a limitation
> - Claude provides: product strategy, architecture, code, design guidance
> - Implication: tech stack choices must maximize productivity for a small team (React Native + shared web codebase is the right call)

---

---

## Brand & Marketing Direction

### Ad Testing Results (7 concepts designed in Pencil)
> **What resonated:**
> - Organic/emotional ads are the headliners — "Know Mom Took Her Meds Today", "She Just Answers the Phone", "Every Dose. Every Day. Every Person."
> - B2B "Proof of Care" ad works well for agency-targeted campaigns
> - Warm, family-focused tone is the brand voice
>
> **What didn't work:**
> - Dark/luxury premium aesthetic (Ad 4) — too dark, wrong tone for this product
> - Competitive ads (vs Medisafe, data selling) are NOT headliners
> - Competitive differentiators like "unlimited meds" and "never sell your data" should appear as **supporting side elements** in organic ads, not as the main message
> - Direct competitor attack ads are deferred — may use later with very focused targeting
>
> **Brand voice emerging:** Warm, reassuring, family-centered, confident but not aggressive. We lead with care, not competition.

### Design Direction
> - Warm cream/off-white backgrounds
> - Natural green (#3D8A5A) as primary accent
> - Terracotta/coral (#D89575) as secondary accent
> - Outfit font family (geometric sans-serif, friendly)
> - Soft shadows, generous corner radii, approachable
> - Stock photography: real people, warm lighting, kitchen/living room settings

---

## Next Steps (Roadmap)

### Phase 1: Brand Foundation
1. **Logo design** — explore options in Pencil
2. **Brand color scheme** — finalize palette based on ad testing direction
3. **Brand voice guide** — tone, do's and don'ts
4. **Style system** — typography, spacing, components

### Phase 2: Web Platform
5. **MedTrack Dashboard (web app)** — full-featured web application
   - Landing/marketing page
   - User dashboard
   - Care circle management
   - Reporting & pattern intelligence
   - Agency admin views

### Phase 3: Mobile App
6. **MedTrack App (React Native — iOS + Android)**
   - Patient-facing reminders & confirmation
   - Caregiver logging with geotag
   - Care circle views
   - Push notifications + SMS integration

### Phase 4: Integrations & Hardware
7. Alexa integration
8. AI voice calling (premium)
9. Easy Button hardware (Phase 2 product)

---

## Competitive Landscape Summary
- **Medisafe**: Market leader, just alienated users with paywall (2 free meds only)
- **MyTherapy**: Best free alternative, caregiver alerts
- **Pillo**: Free unlimited, Android-only
- **CareZone**: Walmart-backed, pharmacy delivery focus
- **Caring Village**: Group caregiver coordination, only one with web app
- **Key gaps**: No peer accountability, no workplace tools, terrible privacy, no web-first

---

## Addendum: Business Viability Assessment

### Why This Can Win

**Timing is exceptional.** Medisafe alienated millions of users with their January 2026 paywall (2-medication free limit). There's a wave of people actively searching for alternatives right now. MedTrack enters at the exact moment the market leader stumbled.

**The moat is real.** Multi-channel escalation (SMS, AI voice, Alexa) in a software-only platform — nobody does this. Hardware companies charge $50/month for what we'll offer free or cheap. That's not a small feature gap, that's a category difference.

**The B2B angle changes the economics.** Consumer medication apps struggle to monetize because users resist paying for health tools. But home health agencies will pay gladly — this solves compliance, liability, and client retention problems. One agency contract could be worth hundreds of individual subscriptions.

**Privacy-first is defensible.** With HIPRA legislation incoming, every competitor will eventually be forced to clean up their data practices. We'll already be there. That's a trust advantage that compounds over time.

### Keys to Success

1. **Nail the free tier.** The generous free tier is the acquisition engine. If it's genuinely better than Medisafe's paid tier, word of mouth does the work.
2. **SMS-first for patients.** The fact that grandma doesn't need an app is the single most powerful pitch. Lead with it everywhere.
3. **Land 3-5 agency contracts early.** One home health agency validating the product is worth more than 10,000 free users for credibility and revenue.
4. **Ship fast, iterate faster.** Two months is tight but right. Launch with core reminders + SMS + care circles + basic reporting. Add AI voice and pattern intelligence in fast follow-ups.
5. **The weekly Care Report Card.** This is the retention hook. Families will stay because the report gives them something no other app does — proof and peace of mind.

### Challenges

1. **Notification reliability on Android.** The #1 complaint across ALL medication apps. Android's aggressive battery optimization kills background processes. SMS as a fallback mitigates it, but it's still a pain point.
2. **AI voice call costs at scale.** At $0.10-0.15/minute, if 100K users each get 2 calls/day, that's $600K-900K/month in API costs. The premium pricing must be carefully modeled.
3. **HIPAA/HIPRA compliance is expensive.** Doing it right means encrypted infrastructure, audit logs, BAAs with every vendor, annual risk assessments. Budget $20-50K upfront for compliance infrastructure and legal review.
4. **Two-person team, full-platform ambition.** Web app + React Native app + SMS integration + Alexa + AI voice is a lot of surface area. Ruthless prioritization is survival.
5. **User trust with health data.** Even with great privacy practices, earning trust takes time and consistency. One breach or misstep could be devastating.
6. **Agency sales cycles.** B2B healthcare sales are slow. Compliance reviews, pilot programs, procurement — could take 3-6 months per agency. Don't count on B2B revenue in the first 6 months.

### Likelihood of Success

**High for gaining traction, moderate for building a sustainable business.**

The product-market fit signals are strong — real pain point, clear gap in the market, terrible incumbents, good timing. MedTrack will get users. The question is whether traction converts to revenue before the runway runs out.

**Most likely path to success:** Launch free, grow fast on the Medisafe migration wave, land 3-5 agency pilots through direct outreach, use those pilots to prove the B2B model, then raise a seed round or bootstrap off agency revenue. The consumer premium (AI calls) is gravy on top.

**Biggest risk:** Trying to build everything at once and shipping nothing great. The team needs to be laser-focused on the core loop — add meds, get reminders, confirm doses, notify the circle — and make that *flawless* before adding AI voice, pattern intelligence, or Alexa.

**Bottom line:** This is a genuinely viable business in a large, growing market ($770M in 2025, projected $2.5B by 2034) with weak competition and perfect timing. The idea is strong. Execution will be everything.

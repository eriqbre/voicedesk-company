# VoiceDesk — Company Strategy Brief

**Status:** LOCKED for execution · **Date:** 2026-08-24  
**Owner:** Eriq Breland (`eriqbre`) · **Working product name:** VoiceDesk  
**This file is the constitution.** CoS executes it. Do not wait for more strategy.

Hand this repo to CoS as standing orders. The rest of the team reads only the sections that apply to them.

---

## 0. How CoS uses this document

1. Read this file once. Keep it loaded. Do not re-research the vision.
2. Run the company. Spawn other agents only per §9. Do not keep a standing army.
3. Elon builds in `eriqbre/voicedesk-v1`. Nobody rewrites that foundation.
4. Escalate to Owner only the list in §14. Everything else is a CoS decision.
5. Token budget is tight (Owner is on Cursor Ultra). Waste is a firing offense.

**Success for CoS:** Owner can paste this brief, walk away, and later open a TestFlight build that he actually uses for mail, calendar, and tasks by voice — then Bridget can too.

---

## 1. Company thesis

VoiceDesk is a **native smartphone voice assistant** for Florida real estate agents. The agent talks to one trusted partner who already knows their world — Gmail, calendar, tasks, listings, people, Florida statutes, and the broker’s compliance pack — and who can run a transaction file from first call to closing.

The product is not a CRM with a microphone. It is not a web desk wrapped in Capacitor. It is **one continuous Grok Voice conversation**. Cards appear when there is desk evidence. Voice narrates; cards prove.

**The company around the app is also the product.** Support, marketing, QA, and most operations are AI agents. The fewest possible humans stay in the loop.

### Humans

| Person | Role | When they touch the product |
|---|---|---|
| **Eriq** | Owner, first tester, ship/kill, capital | Daily once Phase 1 is walkable |
| **Bridget** | Design partner (Coastal Properties listing agent, Tampa Bay) | Only after Eriq says it is ready for her. Her feedback drives many rebuilds. She is not a public launch, not staff, not a spokesperson. |

No other humans until Owner says otherwise.

---

## 2. Why Voxa is retired (do not reopen)

Voxa was the first attempt: a large web / Capacitor desk (`voxa-spec`, `voxa-agents`, `voxa-admin-spec`) with tabbed chrome, locked design system, billing, closing desk, marketing, teams.

**It did not achieve the goal.** Voice was an overlay on a traditional desk. The desk won. The voice-first product lost.

VoiceDesk is the next iteration: **started from scratch, voice-first**, so remaining functionality can be layered onto a foundation that actually works.

### Rules for Voxa repos

- **Do not build Voxa.** Do not port the tabbed desk chrome. Do not keep the Next.js app alive as the product.
- **Do not delete the repos** (history + end-state feature catalog). Mark them archived in their READMEs.
- **Read them only to harvest a specific future capability** (closing file, compliance pack inheritance, Review-queue behavior, fair-housing flags). Open the relevant contract or mock, not the 180k-line spec.
- Locked VoiceDesk interaction model **beats** any Voxa UX lock.

End-state harvest list (concepts, not screens) lives in §6 Phase 3–5.

---

## 3. Product north star

### One-line

A Florida realtor opens the app, talks, and runs the day and the deal file without opening Gmail, Calendar, Tasks, or a transaction manager.

### Interaction model (LOCKED) — Style C

- **Conversation thread is the chrome.** No home dashboard of widgets as the product.
- **Content cards** are evidence and actions: email, listing, person, calendar, task, draft/confirm, statute/confidence, activity/audit, later: transaction file / checklist / document.
- Grok Voice (speech-to-speech, `grok-voice-latest`, default voice Eve) is how you work. Typing is a fallback, not the design center.
- Assistant answers **anything** (desk or general). Desk questions spawn cards. General questions stay in conversation.
- Never sound like IVR, a command menu, or a form.

### Agency (LOCKED)

| User intent | What the app does |
|---|---|
| Question / “what’s in my inbox” | Speak the answer + show cards. No write. |
| “Draft a reply…” | Draft card. **Never send.** |
| “Send it” / “send that” / “yes send” | Score the action (§7). Show confirm card with exact payload. On confirm, send. Log Activity as delivered only after the provider succeeds. |
| “Schedule…” / “remind me…” | Draft the event/task → confirm → write. |
| Money, contracts, mass email, anything Red-gated | Confirm is mandatory. No shortcuts. |

**Silent send is a bug.** Reporting “sent” without provider success is a bug.

### v1 integrations (LOCKED)

- Google only: Gmail, Calendar, Tasks.
- Other mail (Outlook / Microsoft 365 / IMAP) is backlog, not now.
- No MLS / Stellar in early phases.
- No Follow Up Boss / kvCORE as a dependency. We are not a CRM clone.
- Public listing data only via a **licensed** source when we get there. No scrape-as-architecture.

### Platforms

- **Now:** native iPhone (`app.voicedesk.ios`) in `eriqbre/voicedesk-v1`.
- **Android:** required before Coastal office rollout. Not before Bridget dogfood on iPhone is real.
- Linux CI tests the **logic** package. It cannot run the iOS Simulator. Do not pretend it can.

---

## 4. Closed dogfood (LOCKED)

Keep the app to **Eriq, then Bridget**, until the **full feature set** in §6 is ready for other humans.

| Stage | Who | Gate |
|---|---|---|
| 0 | Elon + CI | Linux `swift test` green |
| 1 | Eriq only | He can run a real morning by voice without Gmail |
| 2 | Bridget | Eriq says it is useful enough that her time is not wasted |
| 3–4 | Still just them | Transaction file works for a live Coastal listing |
| 5 | Coastal agents, then Florida | Owner explicit “open the gate” |

**Forbidden until Stage 5:** public TestFlight marketing, ads, “sign up”, broker sales outreach, App Store listing as a business, landing pages that take payment.

Marketing **does** research and drafts GTM now. Marketing **does not** spend attention or tokens on live campaigns.

---

## 5. What Elon already shipped (do not rebuild)

Repo: [`eriqbre/voicedesk-v1`](https://github.com/eriqbre/voicedesk-v1)

Read `PRODUCT_REQUIREMENTS.md`, `README.md`, `TESTING_AND_BRANCHING.md` before any code.

**Shipped**

- Live Grok speech-to-speech (AVAudioEngine + WebSocket)
- Conversation + inline cards (Style C)
- Google Sign-In (GIDSignIn 9.2.0) when `GOOGLE_CLIENT_ID` is set
- Gmail / Calendar / Tasks **read** + disk offline cache
- Confirm-before-act + Activity log
- Writes **queued, not delivered** (no write scopes yet)
- Sample listing + Fla. Stat. § 475.278 card
- VoiceDeskLogic Linux-testable domain + regression fixtures
- CI: Linux unit tests on every push; macOS Simulator is **manual dispatch only** (expensive)

**Stubbed / next**

- Gmail / Calendar / Tasks **write** (this is the next real leverage)
- Email ↔ listing ↔ people graph + claim UX (`slice/3-graph-listings` in README)
- Statute RAG corpus
- Wake word (phrase is an open Owner decision)
- Ephemeral xAI tokens (long-lived key on device is dogfood-only)
- Listing market data
- Android

Elon’s job is to **take this to the next level**, not start over.

---

## 6. Build order — layer features, don’t boil the ocean

One slice in flight. A slice is walkable on device, tested on Linux, and does not expand mid-flight.

### Phase 1 — Eriq’s daily driver (NOW)

Goal: Owner stops opening Gmail / Calendar / Tasks for ordinary morning work.

| ID | Slice | Done when |
|---|---|---|
| 1.1 | **Graph** email ↔ listing ↔ people (infer + claim) | “What’s going on with Beach Drive?” shows mail + people + next event |
| 1.2 | **Gmail write scopes** + send on explicit confirm | Confirm → actually delivered; failure stays a failed draft |
| 1.3 | **Calendar + Tasks write** on confirm | Spoken “move showing to 4” persists to Google |
| 1.4 | **Morning briefing** from live cache | Open app → talk → inbox + calendar + tasks in one turn |
| 1.5 | **Compliance score v0** on drafts | Every draft shows a score chip; heuristic + cited snippet; no silent send |

Phase 1 explicitly does **not** include MLS, Outlook, Android, marketing posts, SMS, e-sign, or a full closing desk.

### Phase 2 — Bridget-ready

Goal: Eriq hands Bridget a build she can use in a real workday, then we rebuild from her notes.

| ID | Slice | Done when |
|---|---|---|
| 2.1 | Florida statute corpus + RAG (see §7) | Law questions cite section + confidence |
| 2.2 | Coastal compliance pack ingest (versioned docs she/Eriq provide) | Answers attribute “Coastal pack, doc X, p. Y” |
| 2.3 | Scoring **gates** (Green / Yellow / Red / Unknown) | Red blocks send; Yellow forces confirm with reason |
| 2.4 | Listing claim from mail/calendar + add-by-address | Her listings are “mine” without MLS |
| 2.5 | Car / glance behavior (wake-word decision or tap-to-talk polish) | Usable between showings |

**Bridget dogfood pass** (from VoiceDesk PRD, still the bar):

- Morning by voice: inbox + calendar
- Open an email, see related listing + people
- Claim a listing
- Send one confirmed email
- Schedule one calendar item
- Ask a law question, see confidence + citation
- She does not bail to Gmail to finish those flows

Expect **many rebuilds** after her first week. That is the process, not a failure.

### Phase 3 — Transaction file (the important layer)

This is the feature that makes VoiceDesk a company, not a voice mail client.

**Job:** From the first call with a prospective seller (or buyer) through closing day, the file — documents, due dates, and people — is in the app and one question away.

Harvest **behavior** from Voxa’s Closing desk / listing setup / roles / key dates. Do **not** harvest Voxa chrome.

Minimum viable file:

1. **Deal object** tied to a listing + side (list / buy) + stage.
2. **Parties:** seller, buyer, listing agent, buyer’s agent, TC, title, lender, inspector, appraiser, insurance, HOA/condo, surveyor. Voice: “add the title company.”
3. **Florida residential timeline** (FR/BAR-shaped, adjustable): listing agreement → live → showing → offer → executed contract → inspection → appraisal → financing → HOA/condo → insurance (wind/flood) → walkthrough → closing → post-close.
4. **Documents:** expected vs received vs outstanding, with due dates. Voice: “what’s still out on 414 Beach?”
5. **Chase:** draft (not send) follow-ups to the right party; confirm to send.
6. **Key dates radar:** inspection end, loan commitment, HOA docs, closing.
7. **Audit:** every change logged.

**Not in Phase 3:** replacing SkySlope/Dotloop e-sign for the whole brokerage; MLS forms libraries; TC marketplace.

### Phase 4 — Coastal office

- Android
- Invite-gated Coastal agents
- Broker-level compliance pack + activity audit a broker can live with
- Ephemeral xAI tokens (key leaves the device)

### Phase 5 — Open Florida

- Self-serve signup
- Billing live (prices from §8, locked by Owner after Marketing memo)
- Broker Partner program
- Support agent live
- Marketing campaigns allowed

### Later backlog (do not pull forward)

Outlook / Microsoft 365 · Stellar MLS · CRM replace · SMS / text line · social posting · IAP · team seats · transfer-of-book.

---

## 7. Legal line and scoring gates (LOCKED)

The app **explains** Florida statutes and broker rules. It is **not a lawyer** and **not the broker-of-record**. Every law/compliance answer says so once per session, not every turn.

### What must be scored

Every **draft** and every **proposed send/schedule** is scored against:

1. Florida statutes and related rules relevant to the act (license law Ch. 475, brokerage relationship 475.278, fair housing, HOA/condo, landlord-tenant if rental, advertising rules, etc.)
2. The **versioned broker compliance pack** for that desk (Coastal first)

### Gates

| Gate | Meaning | Behavior |
|---|---|---|
| **Green** | High confidence the act is allowed | Draft normally. Explicit “send it” → confirm card → send. |
| **Yellow** | Possible issue or missing fact | Card shows the risk and the citation. User must confirm with the warning visible. |
| **Red** | High confidence this violates a rule/statute (fair housing language, undisclosed dual agency, missing brokerage relationship disclosure, etc.) | **Block send.** Explain which rule. User may override only with an explicit spoken or tapped acknowledgment that is audited. |
| **Unknown** | We do not have the doc or the statute match is weak | Do not bluff. Say what’s unknown. Treat like Yellow or refuse to send if the act is high-stakes. |

Confidence on the **law** is separate from confidence on the **facts** of the deal. Show both when they differ.

Statute corpus is Owner-ratified before Bridget relies on it. Compliance agent drafts; Owner (later: Florida-licensed reviewer if Owner hires one) signs off.

---

## 8. Pricing and GTM — working model, not locked

**Buyer:** the agent is the user and the default payer. Brokers may subsidize.

**Do not bill anyone until Phase 5.** Research now so the model is ready.

### Market comps (2026, for the research to beat)

| Product | Who pays | Ballpark |
|---|---|---|
| Follow Up Boss | Agent / team | ~$69 / user / mo |
| Dotloop Premium | Agent, sometimes brokerage | ~$35 / mo |
| SkySlope | Usually **brokerage** | ~$25/agent or ~$340+ / brokerage |
| BoldTrail / kvCORE | Team / brokerage | ~$499+ / mo |
| B.Claw-class AI layer | Agent | ~$99–$599 / mo |
| ChatGPT Plus | Agent | $20 / mo — **this is the fake competitor**. We are not this. |
| Human TC / VA | Agent | ~$500–$2,500 / mo |

Florida has the most Realtors in the US (~216k). Most close little. **ICP is producing agents and small independents like Coastal**, not the bottom 70%.

### Working commercial hypothesis (Marketing must validate or replace)

**A. Agent Direct**

| Plan | Price | Includes |
|---|---|---|
| Founding (Eriq / Bridget) | $0 | Everything, dogfood |
| **VoiceDesk** | **$79/mo** or $790/yr | Voice OS + Gmail/Calendar/Tasks + graph + statute answers + included voice minutes |
| **VoiceDesk File** | **$129/mo** or $1,290/yr | + transaction file, chase, document radar, broker pack |

Voice has real COGS (Grok speech-to-speech). Plans must include a minute pool (research target: **500–800 min/mo**) and a clear overage. Do not hide usage in a way that bankrupts us at scale.

**B. Broker Partner (the subsidy path)**

This is the strategy to test. SkySlope already trained brokers to pay for compliance. FUB trained agents to pay for the daily tool. We want both.

- Broker pays a **platform fee** (research band: **$199–$499/mo** per office) to be “in” VoiceDesk: hosted compliance pack, audit export, branding, agent discount.
- Partnered agents pay **$49/mo** (or the broker buys N seats).
- Broker value prop: fewer E&O landmines, one pack for every agent, visibility without reading their mail.
- Agent value prop: cheaper than Direct, pack already loaded, still *their* assistant.

**C. What we will not do**

- kvCORE-priced all-in-one ($499) as the only door — kills Bridget-class independents.
- $19/mo “AI add-on” — signals a toy and cannot cover voice COGS.
- Broker-only billing with no agent love — the assistant has to feel personal or they will not talk to it.

### ROI frame for Marketing copy (later)

A producing Florida agent’s time is the asset. If VoiceDesk returns **2 hours/week**, it is cheap at $129. Price to **hours returned**, not to Dotloop.

### Marketing’s Phase-now job (research only)

Deliver one memo to Owner + CoS (see `prompts/MARKETING.md`):

1. Validated or replacement prices
2. Minute-pool / COGS model vs xAI Voice
3. Broker Partner term sheet (what the broker actually buys)
4. Name research (VoiceDesk is working; Voxa is taken)
5. Positioning vs FUB + Dotloop + ChatGPT + a VA
6. Coastal-first then Florida Realtors GTM **sequence** (not campaigns)

Do not build a marketing site that takes signups.

---

## 9. The AI company — roster, behavior, spawn rules

### Standing team (already created)

Only these four exist by default.

### 9.1 CoS — Chief of Staff

**You run the company.** You do not write app code. You do not redesign Style C.

**Every cycle**

1. Check `voicedesk-v1` main: tests, open PRs, Elon’s current slice.
2. Unblock Elon. That is the highest-leverage action.
3. Keep PO’s backlog matched to §6. Kill scope that is not the current phase.
4. Keep Marketing on the research memo until it is done; then park Marketing.
5. Report to Owner in **one short delta** (what shipped, what’s blocked, one ask). No recap of this brief.
6. Spawn extras only from the table below, time-boxed, with a one-page brief. Kill them when the artifact lands.

**Never**

- Parallelize two Elons onto the same files
- Load full Voxa specs “for context”
- Start Android, billing, or ads
- Dispatch macOS CI unless a slice truly needs Simulator (it costs money)
- Ask Owner questions this brief already answers

**Escalate to Owner only:** §14.

### 9.2 Elon — Builder

**Repo:** `voicedesk-v1` only, unless CoS opens `voicedesk-api` later.

**How you act**

- First-principles native iOS. SwiftUI conversation + cards. Grok Voice is the product.
- Read PRD + this brief + the slice ticket. Then ship the slice.
- Preserve Linux-testable VoiceDeskLogic. New behavior = new tests. Fixtures over live Grok.
- Follow `TESTING_AND_BRANCHING.md`. Do not merge red Linux tests.
- One slice. Show → confirm → act. No silent send. No fake Google. No fake Grok.
- When a backend becomes unavoidable (ephemeral tokens, RAG corpus, billing), tell CoS. Do not quietly stand up a Next.js desk.

**Definition of done for a slice**

- Linux `swift test --package-path VoiceDeskLogic` green
- Behavior matches the slice ticket and Style C
- Owner (or Bridget, later) can walk it per `TESTING_AND_BRANCHING.md`
- README / PRD stubs table updated
- No secrets committed

**You do not**

- Rebuild Voxa
- Invent MLS fields
- Add a settings wizard
- Change the product name
- Optimize for App Store marketing

### 9.3 Product Owner / Manager

**How you act**

- Translate §6 into **slice tickets** of 1–2 pages. Elon should not have to interpret the constitution mid-code.
- Protect Style C. Push back on tab bars, dashboards-as-home, and “just one more settings screen.”
- Harvest Voxa **capabilities** into VoiceDesk-shaped tickets **when that phase starts**, not before.
- After Bridget feedback: turn notes into slices. Do not turn notes into a new product.
- Own the scoring-gate UX with Compliance when Phase 2 starts.
- You do not write production Swift unless Elon is blocked on a 10-line fix and CoS says so.

### 9.4 Marketing

**How you act now:** research and strategy artifacts only.  
**How you act at Phase 5:** GTM execution, still AI-first.

- Write as if talking to Bridget: producing listing agent, Coastal-class independent, car-between-showings.
- No hype that the app is for sale.
- Pricing memo is your first and only current deliverable.
- Name/brand options are a **proposal**. Owner picks.

---

### Spawned agents (CoS creates these only when the work exists)

| Agent | Spawn when | Deliverable | Kill when |
|---|---|---|---|
| **Compliance** | Phase 2.1–2.3 starts, or a Red-gate design is needed | Statute inventory + gate table + Coastal pack schema | Artifact merged to company repo and Elon ticketed |
| **Knowledge** | Corpus must be built | RAG pipeline design + chunked FL statutes + pack versioning | First corpus in place; Elon owns runtime |
| **QA** | Elon opens a PR that is more than logic tests | Walk script + extra fixtures + “would Bridget hit this” | PR merged |
| **Pricing analyst** | Optional, **one shot**, if Marketing wants a second brain | Combined with Marketing memo — do not produce two memos | Memo delivered |
| **Android** | Phase 4 only | Kotlin/Swift-equivalent plan that **shares VoiceDeskLogic ideas**, not a rewrite of product rules | After Bridget iPhone dogfood is real **and** Owner opens Phase 4 |
| **Support** | First time Bridget (or later a Coastal agent) needs help | AI runbook: reproduce → fixture → ticket → Elon. No human inbox theater | Idle after runbook exists; wake on tickets |
| **Ops / Admin** | Phase 4 broker audit | Thin operator console spec (do not revive full voxa-admin) | Spec accepted |

**Hard cap:** besides Elon, at most **two** spawned or standing non-CoS workers doing real work at once. Marketing parks after the memo. PO is cheap if they only write tickets.

---

## 10. Token efficiency protocol (non-negotiable)

Owner is on **Cursor Ultra**. Treat tokens like runway.

1. **CoS is the only always-on agent.** Everyone else is a function call with a stop condition.
2. **Elon works one slice.** No speculative refactors, no “while I’m here” design-system rewrites.
3. **Read less.** `PRODUCT_REQUIREMENTS.md` + the slice ticket + the files you will touch. Not the whole Voxa tree.
4. **Tests are cheaper than live Grok.** Voice regression JSONL fixtures. Mock Google in UI tests. Never burn `XAI_API_KEY` in CI.
5. **macOS CI is expensive.** Linux unit tests are the merge gate. Simulator workflow is `workflow_dispatch` only.
6. **Artifacts over chat.** Memos and tickets live in `voicedesk-company`. Do not re-prompt a 20-page recap.
7. **No duplicate brains.** One pricing memo. One statute inventory. One graph spec.
8. **Kill finished agents.** A parked Marketing expert still costs context if you keep them in the loop.
9. **Do not generate HTML mockups** that fight Style C. If Elon needs a card, describe it in 10 lines.
10. **Do not npm-install a second product** in this Grok Build web sandbox. VoiceDesk is native iOS. This Linux preview is the wrong runtime.

---

## 11. Repositories

| Repo | Role | Rule |
|---|---|---|
| [`voicedesk-v1`](https://github.com/eriqbre/voicedesk-v1) | **The product** | Elon owns. All app code. |
| [`voicedesk-company`](https://github.com/eriqbre/voicedesk-company) | **The company OS** | This brief, memos, tickets, CoS log. |
| `voxa-spec` | Archived feature catalog | Read-only harvest |
| `voxa-agents` | Archived | Read-only |
| `voxa-admin-spec` | Archived | Read-only |
| `voicedesk-api` | **Do not create until** ephemeral tokens, RAG host, or billing need a server | CoS proposes; Owner does not have to pre-approve if Phase 2 is blocked without it — still notify |

CoS: add a short `ARCHIVED.md` pointer on the three Voxa repos (do not delete).

---

## 12. First two weeks (execute, don’t plan to plan)

**Day 1**

- CoS reads this file + VoiceDesk README/PRD.
- Archive-banner the Voxa repos.
- PO writes tickets **1.1 Graph** and **1.2 Gmail write** from current code, not from fantasy.
- Elon starts **1.1** (README already points at `slice/3-graph-listings`) unless 1.2 is faster to close for Eriq dogfood — CoS picks based on what unblocks Owner using the app tomorrow.
- Marketing starts the pricing memo (time-box 1 working pass, not a dissertation).

**Days 2–7**

- Elon ships 1.1 or 1.2 to main, Linux tests green.
- Owner dogfoods on device. CoS collects his notes into tickets, not into a new vision.
- Marketing memo v1 in this repo.
- No Compliance spawn yet unless Elon hits 1.5 in the same week (unlikely — don’t force it).

**Days 8–14**

- Remaining Phase 1 slices in order that makes the morning briefing real.
- PO drafts Phase 2 statute inventory outline (still not a spawn until 2.1 starts).
- CoS weekly delta to Owner: walkable behaviors, blockers, token spend notes.

---

## 13. Quality bar

- If voice works and the screen doesn’t show the evidence, it is broken.
- If the screen works and voice is secondary, it is broken.
- If it says sent and Gmail doesn’t have it, it is broken.
- If it invents an email, listing, or statute not on a card / citation, it is broken.
- If Bridget needs Gmail to finish a Phase-2 flow, that flow is not done.
- Linux tests green is the floor. Device walk is the ceiling until Simulator CI is justified.

---

## 14. Owner-only decisions

Escalate these. Decide everything else.

1. Product **name** (replace VoiceDesk)
2. Wake-word **phrase**
3. **Bridget is allowed to test**
4. **Coastal office** / public Florida / paid launch
5. **Lock prices** after the Marketing memo
6. Delete (vs archive) Voxa repos
7. Buying a **licensed listing-data** vendor
8. Hiring any additional **human** (lawyer, TC, contractor)
9. Exceptions to **no silent send**
10. Spending past token comfort / enabling expensive macOS CI as default

---

## 15. One paragraph for every new agent CoS spawns

> You work for VoiceDesk, a native iPhone Grok-voice assistant for Florida realtors. Conversation is the chrome; cards are evidence; no silent send; Google-only for now; Eriq then Bridget only. Constitution: `eriqbre/voicedesk-company` `STRATEGY_BRIEF.md`. Product code: `eriqbre/voicedesk-v1`. Voxa is archived — harvest concepts, never chrome. You will produce [ARTIFACT] in [N] passes and stop. Do not spawn further agents. Do not load the entire Voxa spec. Token budget is tight.

---

*Locked 2026-08-24 for CoS execution. Amendments only by Owner.*

# Pricing and GTM — VoiceDesk

**Status:** research memo v1 · **Date:** 2026-08-24  
**For:** Owner + CoS  
**Not for:** ads, site, signups, campaign copy  
**Sources:** `STRATEGY_BRIEF.md` §8, `prompts/MARKETING.md`, [xAI Voice pricing](https://docs.x.ai/developers/pricing) (2026-08-24), rival notes already on file (Nora / Sohala / Magellan).

Owner locks prices (§14). This is the recommendation, not a lock.

---

## 1. Prices — keep the dollars, replace the minute pools

The §8 ladder is right. $19 is a toy. $499 as the only door kills Coastal-class independents. The hole is minutes, not list price.

**Recommendation: keep $79 / $129 / Broker Partner. Do not ship the 500–800 included-minute target on the $79 plan.**

| Plan | Price | Includes | Voice pool | Overage |
|---|---|---|---|---|
| Founding (Eriq / Bridget) | $0 | Everything, dogfood | uncapped, watched | n/a |
| **VoiceDesk** | **$79/mo** or $790/yr | Voice OS + Gmail / Calendar / Tasks + graph + statute answers | **400 min/mo** | **$0.18/min** |
| **VoiceDesk File** | **$129/mo** or $1,290/yr | + transaction file, chase, document radar, broker pack | **700 min/mo** | **$0.15/min** |

Annual = 10× month (two months free). Agent is the user and the default payer.

### Why not replace $79

| Comp | Ballpark | Verdict |
|---|---|---|
| Follow Up Boss | ~$69 / user / mo | We are $10 more and **not a CRM**. Agents already pay this. Do not go to $49 Direct or we look like a FUB add-on. |
| Dotloop Premium | ~$35 / mo | Different job (signature). File at $129 is 3.7× Dotloop because it is chase + radar + voice, not e-sign. Do not price File at $49. |
| SkySlope | broker-paid, ~$25/agent or ~$340+ / office | Train the **broker** check. Our Partner fee rhymes with this, not with BoldTrail. |
| BoldTrail / kvCORE | ~$499+ / mo | Refuse as the only door. |
| B.Claw-class AI layer | ~$99–$599 / mo | File sits at the **floor** of that band on purpose. |
| Sohala (voice, not CRM) | $59–79 / mo | $79 is their ceiling with a real Google desk. Going to $59 cannot cover Grok Voice. |
| Magellan (they *are* the CRM) | $28–50 / agent + 4-seat min | Wrong comparison. We are not the CRM. |
| ChatGPT Plus | $20 / mo | Fake competitor. See §5. |
| Human TC / VA | ~$500–$2,500 / mo | File is a slice of a cheap TC, not a replacement. |

### Hours-returned math (the real price test)

§8: if it returns **2 hours/week**, $129 is cheap. Show the math, do not invent closed volume.

- 2 hr/week × 4.3 weeks = **8.6 hr/month**
- Conservative producing-listing-agent time: **$80/hr** (appointment / follow-up time, not GCI/hour)
- Value = 8.6 × $80 = **$688/month**
- File $129 → **5.3×**
- Direct $79 → **8.7×**

If Bridget’s first month does not return ~2 hours, the price is wrong and the product is not ready. Do not discount. Fix the morning loop.

**Do not bill anyone until Phase 5.**

---

## 2. Voice COGS and the minute pool

Product voice is Grok speech-to-speech (`grok-voice-latest`, Eve). xAI list (docs.x.ai, 2026-08-24):

| Mode | List |
|---|---|
| Speech-to-speech **Think Fast 2.0** | **$0.08 / audio min** ($4.80/hr) + $0.004 / text input |
| Think Fast 1.0 (deprecated) | $0.05 / min |

`grok-voice-latest` moved to 2.0. **Plan at $0.08/min.** Treat text-input as noise (~$0.01/min at a few turns). Do not plan on $0.05.

### Assumed use (producing listing agent, car + desk)

- Morning briefing: ~6 min
- Between-showing loops: ~15–25 min
- Draft / confirm / chase: ~10 min
- **Workday ~30–40 min × 22 days ≈ 660–880 min/mo** if she lives in the mic
- **Realistic first-year mix: ~350–500 min/mo** (she still opens Gmail some hours)

500–800 included on a $79 plan **does not leave margin**.

| Pool | Voice COGS @ $0.08 | Left from $79 | Left from $129 |
|---|---|---|---|
| 400 min | $32 | $47 | $97 |
| 600 min | $48 | $31 | $81 |
| 800 min | $64 | $15 | $65 |

Other COGS later (Google, RAG host, ephemeral tokens, support) will eat the leftover. **Voice must stay under ~45% of list on the median user.**

### Recommendation

- **Direct $79 → 400 included.** Covers a normal Bridget day without inviting all-day babble. Heavy users overage or upgrade to File.
- **File $129 → 700 included.** Matches a live transaction week.
- **Overage:** $0.18 Direct / $0.15 File (2×-ish list COGS). Show a running minute chip in the thread. Soft-warn at 80%.
- **Founding:** uncapped, CoS watches the bill. If Eriq or Bridget blow 2,000 min, that is a product-design bug, not a pricing bug.
- **Hard rule:** do not hide usage. A silent $0.08/min at scale bankrupts Phase 5.

Pin the model version in the app. Do not ride `grok-voice-latest` into a surprise rate hike without a plan change.

---

## 3. What a broker actually buys

Coastal is a small independent, not a 400-agent franchise IT buyer. Price the **office**, not BoldTrail.

**Replace the $199–$499 band with a single Coastal-class number: $249/mo platform** (or $2,490/yr). $199 is too cheap to host a pack + audit. $499 smells like kvCORE and will not get a yes from a 15-desk broker.

| Line | What they get | What they do **not** get |
|---|---|---|
| Hosted compliance pack | Versioned Coastal docs the app scores against. Attribution: “Coastal pack, doc X, p. Y.” | We are not broker-of-record. Pack is theirs; we host it. |
| Audit export | Activity log of scored drafts / sends / overrides (Red-gate acknowledgments). CSV / PDF monthly. | **No mail body access. No calendar voyeurism.** Visibility without reading their agents’ Gmail. |
| Agent discount | Partnered agents at **$49/mo** (Direct features + pack already loaded), or broker buys N seats at $49. | Unlimited free seats. No “whole office free forever.” |
| Seat vs platform | Platform = pack + audit + “in.” Seats = talking assistants. | Platform-only with no agent love. The assistant has to feel personal. |

### Why Coastal would pay

SkySlope already trained them to pay for compliance. One pack on every talking agent is cheaper than a TC lecture and an E&O claim. The check is for **fewer landmines and one audit trail**, not for “AI.”

### Contract shape (Phase 5, not now)

- **Annual platform** $2,490 (or month-to-month $249).
- **Seats monthly** at $49, billed to broker or to the agent (broker chooses).
- 90-day out. Pack leaves with them.
- Written: we do not read agent mail; audit is action log only.
- Floor: 5 partnered seats or the platform fee still stands (stops a 1-seat “partner”).
- Android is required before **office** rollout (Phase 4). Do not sell Coastal office on iPhone-only.

Agent value: cheaper than $79, pack already loaded, still *their* Eve.

---

## 4. Name — five options (hygiene notes, not a legal opinion)

VoiceDesk is the working name. Voxa is taken and retired. Owner picks (§14). Bundle ID today: `app.voicedesk.ios`.

| # | Name | Why it fits | Hygiene notes |
|---|---|---|---|
| 1 | **VoiceDesk** | Honest: voice is the chrome, desk is the job. Already in the constitution. | **Crowded.** `voicedesk.com` registered. `voicedesk.app` is a **Miami inbound-call AI** that already demos estate-agent / property-manager lines. `voicedeskai.co` is another voice-agent shop with real-estate templates. AU “VOICEDESK” (BT) is dead. Fine as a **working** name. Risky as a Phase 5 public mark without a US knock-out search and a different public domain (`.ai` / compound). |
| 2 | **EveDesk** | Default voice is Eve. Short. | Do **not** make the company the voice — voices get swapped. “Eve” is a crowded word mark. No knock-out run here. |
| 3 | **FileTalk** | Phase 3 is the company: the file, by voice. | Descriptive. Likely registerable as a composite. Domain likely a compound (`filetalk.app`). Check USPTO 9/42. |
| 4 | **ShoreDesk** | Florida / coastal without saying Coastal Properties. | Weaker product story (sounds like a beach CRM). Cleaner than VoiceDesk on first glance; still needs a search. |
| 5 | **DealThread** | Conversation thread *is* the chrome; the deal is the file. | Close to “thread” / “deal desk” clutter. Not a Dotloop collision. Search USPTO + App Store before lock. |

**Proposal:** keep **VoiceDesk** through Bridget dogfood. Do not buy a brand campaign on it. Owner runs a real knock-out (USPTO 9/42, FL fictitious name, App Store) before Phase 5. If `voicedesk.app` is still in the call-center lane, pick FileTalk or DealThread rather than fighting Miami in Google.

---

## 5. Positioning (one line each)

Talk to Bridget. Not SaaS.

- **vs another CRM:** Not another CRM. Keep Follow Up Boss. This is the partner who already has your Gmail, your day, and (later) the file — you talk, cards prove it.
- **vs another Dotloop:** Dotloop is the signature. This is the voice that knows what’s still out on 414 Beach and drafts the chase. We do not replace e-sign in Phase 3.
- **vs just use ChatGPT:** ChatGPT is $20 and does not have your inbox, your showings, or Coastal’s pack. It also will not sit on a confirm card. Silent send is a bug here; there it is a feature.

We are not Nora (MetroList, not Stellar). We are not Sohala (no Florida file). We are not Magellan (they *are* the CRM).

---

## 6. GTM sequence (Phase 5 only — channels, not a media buy)

**Forbidden until Owner opens Stage 5:** public TestFlight marketing, ads, “sign up,” broker sales outreach, App Store as a business, landing pages that take payment.

Android before Coastal **office**. Bridget iPhone dogfood before Android.

| Step | Who | Channel | Done when |
|---|---|---|---|
| **0. Closed** | Eriq, then Bridget | TestFlight private. Her notes, not a case study. She is not a spokesperson. | She runs the Phase-2 bar without bailing to Gmail. |
| **1. Coastal office** | Invite-gated producing agents at Coastal (5–15 people they already know) + broker on Partner | Hallway, listing-huddle, one broker lunch. Pack loaded. **No ads.** | 8+ weekly-active talkers, broker uses the audit export once, E&O story is a sentence not a deck. |
| **2. Tampa Bay producing listing agents** | Independents and small shops, Bridget-class, not first-year licensees, not franchise IT | Coastal alumni, local board / showing-desk word, one FAR local meeting if someone invites. Still no media buy. | Agents pay Direct or File on their own card. |
| **3. Florida Realtors** | Producing agents + Coastal-class brokers statewide | Self-serve signup + Broker Partner cloned from Coastal. FAR education / broker councils. Support agent live. | Billing live at locked prices. Then — and only then — campaigns are allowed. |

ICP stays the producing agent and the small independent. Not the bottom 70% of the 216k Florida Realtors. Not a 400-agent franchise until Owner says so.

---

## Stop

This is the memo. Park Marketing until CoS wakes it for a price lock, a name pick, or Phase 5.

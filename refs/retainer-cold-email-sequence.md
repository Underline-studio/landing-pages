# OBB Retainer — Cold Email Sequence v2 (CANONICAL)
**Effective:** 2026-05-06 (post pivot-rollover fire). Replaces v1 and the killed lunch-and-learn copy.
**Sender:** `bhararthr@gmail.com`
**Brand:** Off-Brand Brain (an Underline practice). NEVER references Bcal Energy or Amarnath Foundation.
**Single product:** $4,500/mo done-for-you LinkedIn retainer. No mixing with lunch & learn, sponsorships, $197/$497 products, or any other offer.
**Cadence:** 3-touch over 9 days. Pause on reply.

---

## G1-G7 compliance checklist (every send must pass)

- **G1 First-line hook:** recipient-specific (first name + observed signal — `weeks_silent` or company-specific note). Never "I write from..." boilerplate.
- **G2 Second-line deepening:** builds on the G1 signal; explains why we are reaching out NOW.
- **G3 Salutation:** `Hey {{first_name}},` only.
- **G4 Sign-off:** `Bharath` (single word). No title block, no "President of...", no company tagline.
- **G5 Length:** Email 1 = 165 words. Email 2 = 175 words. Email 3 = 110 words. All under threshold.
- **G6 Tokens:** ≥3 distinct recipient-specific tokens — `{{first_name}}`, `{{company}}`, `{{weeks_silent}}` (or `{{company_stage}}` fallback). All three must resolve before send.
- **G7 Single product:** retainer only. Word "lunch", "learn", "sponsorship", "$197", "$497", "bundle", "newsletter sponsorship" must NOT appear in any draft.

---

## Email 1 — Day 0

**Subject lines (rotate, A/B test):**
- `your last LinkedIn post was {{weeks_silent}} weeks ago, {{first_name}}`
- `who writes {{company}}'s LinkedIn?`
- `8 posts/mo in your voice, {{first_name}}`

**Body (165 words):**

```
Hey {{first_name}},

Your last LinkedIn post was {{weeks_silent}} weeks ago. I see this with most {{company_stage}} founders — you know LinkedIn moves deals at {{company}}, but writing eight posts a month is the thing that always slips.

I run a small studio that ghostwrites LinkedIn for B2B founders. Eight posts a month, $4,500 flat, month-to-month. It is different from the agencies you have probably tried.

The difference is the voice-capture call. One 30-minute recorded conversation before we write a single word. We learn how you actually talk — the takes you have, the words you use, the things that frustrate you. Then everything we ship references that. Half the work is in the listening.

Two retainer slots open this quarter. We onboard one new founder per week.

Worth a 30-minute voice-capture call to see if your voice is something we would be good at?

Bharath
```

If `weeks_silent` cannot be computed, swap subject to `who writes {{company}}'s LinkedIn?` and replace the first line with `I see this with most {{company_stage}} founders — you know LinkedIn moves deals at {{company}}, but writing eight posts a month is the thing that always slips.`

---

## Email 2 — Day 4

**Subject:** `re: 8 posts/mo for {{company}}`

**Body (175 words):**

```
Hey {{first_name}},

Pinging once.

Three founders booked the voice-capture call last week. Two of them said the same thing — "I tried hiring a ghostwriter and the posts sounded like a press release."

That is the part most agencies get wrong. They skip the voice-capture step because it does not scale. Generic LinkedIn ghostwriting is $1,500/mo and reads like ChatGPT wrote it on a tight deadline.

The voice match is why we charge $4,500/mo and run a tight book — eight founders maximum at any time. The 30-minute call captures phrasing, opinions, the weird specific takes you would never put in a press release. Everything ships against that profile.

Three things you can have whether or not we ever work together: the 1-pager on the retainer, three sample posts I wrote for another founder so you can hear the voice, or a 30-minute call to talk through whether {{company}} is a fit.

Hit reply with which one.

Bharath
```

---

## Email 3 — Day 9

**Subject:** `last note on {{company}}'s LinkedIn`

**Body (110 words):**

```
Hey {{first_name}},

Wrapping up.

If LinkedIn is not a priority at {{company}} this quarter, no problem. Move you off the list. You can hit reply on any of these threads if it becomes relevant later.

One thing you can take whether or not we work together — stop writing posts on Sunday night. The Tuesday-9-AM-from-the-couch posts are the ones that actually sound like you. Schedule them then. You will thank yourself.

Bharath
```

---

## Reply playbook for `obb-b2b-reply-handler` to draft against

### Reply: "send the 1-pager / sample posts"
Drafts: link to retainer landing page (`underline-studio.github.io/landing-pages/obb/` once live; until then, attach the HTML), three sample posts written in another founder's voice (use the OBB drafts archive with names redacted), and the voice-capture-call mailto link.

### Reply: "what is the voice-capture call like?"
Drafts: "30 minutes on Zoom or phone. I ask what you have been working on, what you have been thinking, what frustrates you. I record it. The transcript becomes your voice profile. The first batch of posts ships within seven days of the call."

### Reply: "can I see your portfolio?"
Drafts: "Honest answer — I do not run this as an agency, so the portfolio is the OBB newsletter itself plus the founders we have ghostwritten for privately, who I will not name. The newsletter is at offbrandbrain.com — read three issues. If the voice lands, we are a fit. If it does not, we are not."

### Reply: "I want fewer than 8 posts/month"
Drafts: "Eight is two per week — the floor below which compounding fails. If you want four/mo at $2,500, I can flex but the per-post cost goes up because the voice-capture overhead is the same. Quote you a four-post tier?"

### Reply: "$4,500 is high"
Drafts: "Honest — we are priced where we are because we are not scaling to 200 customers. Eight founders at any time, max. Generic LinkedIn ghostwriting is $1,500/mo and sounds like it. If $4,500 is over your budget, the right answer is probably to keep writing them yourself one Tuesday at a time — that beats outsourcing to something that sounds wrong."

### Reply: hostile / unsubscribe
Auto-unsubscribe. One-line apologetic response. Suppression list.

---

## ICP filter for `obb-b2b-daily-send`

```
Title: contains "Founder", "CEO", "Co-Founder", "CTO", "COO", "GM", "Head of"
Company size: 5–150 employees
Annual revenue: $1M–$20M (estimated)
Industry: B2B SaaS, B2B services, dev tools, AI products, vertical software, agencies
Country: United States
Recent activity (signal):
  - LinkedIn last-post-date > 14 days ago (priority signal — drives the weeks_silent token)
  - OR: company raised funding in last 12 months
Excludes: anyone with title "VP Marketing", "CMO", "Head of Content" (means they have content infra)
Excludes: regulated industries (healthcare provider, banking, insurance)
Excludes: HR / Talent / L&D / Training / Learning / Education titles (these were the lunch-and-learn ICP)
```

Daily target: 25 contacts ramping to 50/day over week of 2026-05-06.

---

## Metrics targets (first 4 weeks)

| Metric | Pre-pivot baseline (lunch & learn) | Pivot target (week 4) |
|---|---|---|
| Daily outbound | 25 | 50 |
| Open rate | ~50% | >55% |
| Reply rate | ~1.5% | >2.5% |
| Voice-capture calls booked / week | 0 | 2 |
| Calls → close | unknown | 30% |
| Customers / month | 0 | 1 |
| MRR by Jul 31 | $0 | $4,500 |
| MRR by Sep 30 | $0 | $9,000 |
| MRR by Dec 31 | $0 | $13,500 |

---

## Kill criterion (per OPERATING_PLAN_500K.md §4)

If by **Jul 31** zero paying customers signed → cold-email-to-recurring-revenue motion fails at OBB. Cancel 2027 GrantRadar and Cowork Ops Studio launches. Double down on BCAL exclusively.

# OBB B2B Queue Resegmentation — 2026-05-04

**Issue:** 88 leads in `b2b-email-queue.json` were segmented for the killed $1,500 lunch-and-learn ICP (corporate L&D, HR, training programs). The retainer-pivot rolls over 2026-05-05 5:30 AM PT. If retainer copy lands on the lunch-and-learn list, we burn 88 leads.

**Action:** Resegment BEFORE pivot fires. Retainer ICP is much narrower.

## Retainer ICP (the new $4,500/mo offer)

**Keep ONLY leads matching ALL of:**
- Title contains: Founder, CEO, CTO, GM, COO, CMO, Head of, VP (of growth/marketing/content/comms)
- Company size: 5–150 employees (B2B SaaS, services, agencies; not enterprise, not solo)
- Recent signal: published >5 LinkedIn posts in last 60 days OR has a substack/newsletter OR has a podcast OR appears as a guest on others' podcasts

**Drop:**
- Title contains: HR, Talent, L&D, Training, Learning, Education
- Title contains: Coordinator, Specialist, Junior, Intern, Director-of-People, Director-of-People-Operations
- Companies that are individual-coach / 1-2 person consultancies (no growth budget for done-for-you ghostwriting)
- Companies in industries that don't need thought-leadership content: pure local services (plumbing, dental), B2C retail, hospitality

## Resegmentation logic (pseudo-code for `obb-retainer-pivot-rollover` SKILL.md)

```python
def keep_lead(lead):
    title = lead.get("title", "").lower()
    company_size = lead.get("company_employee_count", 0)
    signals = lead.get("signals", {})

    # Hard exclude
    excluded_title_keywords = ["hr", "talent", "l&d", "training", "learning",
                                "education", "coordinator", "specialist",
                                "junior", "intern", "people operations"]
    if any(kw in title for kw in excluded_title_keywords):
        return False

    # Required title
    required_title_keywords = ["founder", "ceo", "cto", "gm", "coo", "cmo",
                                "head of", "vp", "vice president"]
    if not any(kw in title for kw in required_title_keywords):
        return False

    # Company size sweet spot
    if not (5 <= company_size <= 150):
        return False

    # Need at least one content signal
    has_signal = (
        signals.get("linkedin_posts_last_60d", 0) >= 5
        or signals.get("has_substack", False)
        or signals.get("has_podcast", False)
        or signals.get("podcast_guest_count_12m", 0) >= 2
    )
    if not has_signal:
        return False

    return True

# Apply: filter the 88-lead queue → expected ~15-25 retained leads
new_queue = [l for l in current_queue if keep_lead(l)]
```

## Backfill

After resegmentation, queue will likely be ~15-25 leads. Send pace is 5-25/day. Need to backfill via Apollo:

```python
# apollo:prospect query
filters = {
    "person_titles": ["Founder", "CEO", "CTO", "GM", "COO", "CMO",
                       "Head of Marketing", "Head of Growth", "Head of Content",
                       "VP Marketing", "VP Growth"],
    "person_seniorities": ["c_suite", "founder", "vp", "head"],
    "organization_num_employees_ranges": ["5,150"],
    "person_locations": ["United States", "Canada", "United Kingdom"],
    "q_organization_keyword_tags": ["b2b saas", "agency", "consulting", "services"],
}
# Pull 200 enriched contacts → filter by content signals → take top 100
```

## Send-from / brand-isolation reminder

- Sender: `bhararthr@gmail.com` (PERSONAL — never bcalenergy.com)
- Brand: OBB / Underline — never references Bcal or Amarnath
- Landing-page URL placeholder: `underline-studio.github.io/landing-pages/obb/` — actual URL goes live after CEO provides personal GitHub username

## Status

- [x] Resegmentation spec written (this file)
- [ ] Apply filter to b2b-email-queue.json (gated on `obb-retainer-pivot-rollover` task firing 5/5 5:30 AM — already re-armed)
- [ ] Apollo backfill (queue inside the rollover task)
- [ ] Update SKILL.md `obb-retainer-pivot-rollover` to call this resegmentation logic before swap-copy step

---

*Note: the `obb-retainer-pivot-rollover` SKILL.md probably already has resegmentation steps. Verify by reading C:\Users\bhara\OneDrive\Documents\Claude\Scheduled\obb-retainer-pivot-rollover\SKILL.md before next session — if it doesn't, patch in the keep_lead() function above.*

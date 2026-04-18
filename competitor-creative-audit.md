# Competitor Creative Audit: Master Prompt

> Paste this entire file into Claude Code from a folder containing a `.env` (your API keys). If a `CLAUDE.md` business brief is already present and filled in, Claude loads it and proceeds. Otherwise Claude interviews you conversationally for the business specifics and writes the `CLAUDE.md` for you. Either way, Claude runs the audit end-to-end, produces a single consolidated report in markdown and Word formats, and saves supporting screenshots alongside.
>
> Built by Nishant Kapoor at EntireCommerce AI. Version 1, April 2026.

---

You are executing the Competitor Creative Audit playbook for the brand in the current working directory. Follow these steps in order. Do not skip steps. Do not invent data. Honour the voice conventions in Step 13.

---

## Step 1. Load or populate the business brief

Look for `CLAUDE.md` in the current working directory.

**If `CLAUDE.md` exists and is fully filled in** (no `{placeholder}` text remaining, competitor list populated with Facebook page names), read it and proceed to Step 2.

**If `CLAUDE.md` does not exist, contains placeholder text, or is missing required fields, run the business-brief interview before proceeding.** Do not skip. Do not guess the inputs.

### The business-brief interview

Ask the user the following questions conversationally, one batch at a time. After each batch, write the answers into `CLAUDE.md` in the current working directory (create the file if missing) and confirm with the user before moving to the next batch.

**Batch 1: Brand overview.** Brand name. Primary URL. Ecommerce platform (Shopify, WooCommerce, custom, something else). Geographic focus. Stage (pre-launch, first year, established with trading history, mature).

**Batch 2: Product.** What you sell in one sentence. Price range or AOV. Catalog size (number of active SKUs).

**Batch 3: Paid-ads context (specific to this playbook).** Primary ad platforms the brand uses. Ad spend band (under $5K/mo, $5K to $25K, $25K+, pre-launch). Current creative pain in one sentence.

**Batch 4: Target audience.** Core buyer in one sentence, in your own words. Secondary buyer if relevant. Where they hang out online (Reddit subs, niche forums, YouTube channels, podcasts, Instagram accounts they follow).

**Batch 5: Positioning.** Why you win in one sentence. Pricing tier vs category median.

**Batch 6: Competitor list (load-bearing for this playbook).** Three to five competitors the buyer also considers. For each, the brand name, the URL, and the Facebook page name (the exact string on `facebook.com/{page-name}`). Also the category head term in one line.

**Batch 7: Tool stack.** Website and CMS. Analytics (GA4 or other). Ad platforms (Meta, Google, TikTok, LinkedIn). Social-content tools (Buffer, Later). CRO tools (Clarity, Hotjar, FullStory). AI assistants already in use.

### Minimum required to proceed to Step 2

If after the interview you still do not have these eight fields captured, ask again before proceeding:

1. Brand name
2. Primary URL
3. Primary ad platforms
4. What the brand sells (one sentence)
5. Core buyer (one sentence)
6. Three to five competitor URLs with Facebook page names
7. Category head term (one line)
8. Differentiators the client thinks they have (one line)

Do not invent any value. Ask the user.

---

## Step 2. Inventory tool access

Read the `.env` file in the current working directory. Print a credential inventory to the user in this format:

```
External tools (public data)
- Serper: configured / not configured
- DataForSEO: configured / not configured
- Ahrefs: configured / not configured
- Keywords Everywhere: configured / not configured
- Apify (Instagram + TikTok scraping): configured / not configured
- Google PageSpeed Insights (GOOGLE_AI_KEY): configured / not configured

Internal tools (your brand's own data, optional)
- Meta Ads API: configured / not configured
- Google Ads API: configured / not configured
- Meta Business Manager: configured / not configured

Meta Ad Library: no API key required (public web). Fallback chain configured (Playwright → third-party indexes → Apify → manual screenshots).
```

For each tool flagged "not configured", the corresponding section will either fall back (External) or stub honestly (Internal).

### Offer setup instructions for missing tools

After printing the inventory, go through each tool flagged "not configured". For each one, ask the user:

> "`{Tool}` is not configured. Want me to look up the current sign-up steps and API-key retrieval flow, so you can wire it in? Answer `yes`, `no`, or `skip all`."

If the user answers `yes`, use WebSearch and WebFetch to pull the current sign-up flow for that specific tool (pricing tiers, free-tier availability, where the API key lives in the account settings, the exact `.env` variable name this playbook expects). Include a one-line estimate of credit cost for a typical audit run where known.

If `no`, skip that tool. If `skip all`, stop offering and proceed to Step 3.

After the user adds any new credentials to `.env`, reprint the updated credential inventory before continuing.

Never hardcode sign-up URLs or pricing numbers from memory. Pull fresh from the web every time.

---

## Step 3. Path and mode selection

Based on the `.env` inventory and the brand's ad-spend state (inferred from `CLAUDE.md` or the Meta Ad Library page for the brand's own Facebook name), auto-detect the path and offer a mode:

**Path A (paid-ads-active).** The brand has active Meta or Google ads. The audit produces a swipe file, whitespace map, 10 to 15 ranked starter briefs, and a 30-60-90 test plan.

**Path B (pre-launch / new brand).** No ads running yet. The audit maps the competitive landscape and surfaces the day-one angle the brand can own.

| Mode | Trigger |
|---|---|
| Full | 3 to 5 competitors, all 10 sections. Standard engagement. |
| Quick | 1 competitor named, Meta + hooks only. Sprint-sized. |
| Pre-launch | Path B, 5+ competitors, heavy whitespace mapping. |
| Focused | Path A, 1 competitor named, deep teardown. |

State the detected path and proposed mode, ask the user to confirm or override. Record the mode in the report header.

---

## Step 4. Section 1. Competitor profiles

For each of the 3 to 5 competitors, produce a profile card (300 to 500 words).

Fields:

- Brand name, URL, Facebook page name (from user input)
- One-sentence positioning (WebFetch the competitor's homepage + About page)
- Assumed target audience (synthesise from homepage copy, ad audience cues, review corpus if public)
- Top 10 selling products (Shopify best-seller collection if available. Otherwise the homepage "featured" grid plus any Reviews.io / Yotpo / Loox sort-by-popular view.)
- Price range (PDP scan across the top 10)
- Social presence (followers by platform via WebFetch on LinkedIn company page, Instagram profile, TikTok profile, X profile)
- Creative volume (active ads count from Meta Ad Library on date of audit)
- Visible partnerships, PR, influencer tie-ins (homepage press bar, About page logos, recent social mentions)

Save per-competitor supporting data to `data/competitor-creative-audit/{date}/raw/{competitor-slug}/`.

---

## Step 5. Section 2. Meta Ad Library 30-day scan

For each competitor, execute the full teardown. Meta Ad Library via raw WebFetch returns empty. Use the fallback chain:

1. Playwright or headless-browser script (if the environment supports it).
2. Third-party Meta Ad Library indexes (adscan.ai, foreplay.co).
3. Apify Meta Ad Library scraper (if `APIFY_TOKEN` is in `.env`).
4. Manual browser screenshots of the first 10 to 15 ads per competitor. Paste into `data/competitor-creative-audit/{date}/screenshots/{competitor-slug}-meta-ad-01.png`, `-02.png`, etc.

If none of the above is available, ship this section with "Meta Ad Library: unable to verify via WebFetch; manual screenshot pass required" and add it to the Access-grant checklist.

### 2A. Active ad inventory

- Active ad count on the date of audit.
- Breakdown by ad type: static image, carousel, video, UGC, collection.
- First-run date distribution: how many ads are under 7 days old, 7 to 30 days, 30+ days. A 30+ day ad is a probable evergreen winner.
- Platform mix: Meta, Instagram, Messenger, Audience Network.

### 2B. Hook taxonomy per competitor

Categorise each ad's opening 3 seconds (first line of copy for static, first 3 seconds of video) into one of 8 hook types:

| Hook type | Example pattern |
|---|---|
| Social proof | "Over 10,000 golfers are..." |
| Urgency / scarcity | "Last 48 hours before..." |
| Identity / aspiration | "If you're the kind of golfer who..." |
| Authority | "Built by PGA coaches..." |
| Contrarian | "Everything you've been told about wedge distance is wrong..." |
| Transformation | "I went from 12 handicap to 6 in 90 days..." |
| Comparison | "[Brand] vs [Competitor]: here's what we found" |
| Education / curiosity | "The one thing about launch monitors nobody mentions..." |

Count frequency of each hook type per competitor. Flag the dominant hook.

### 2C. Creative copy patterns

- Average headline length (characters).
- Average primary text length (characters).
- Use of bullets, emojis, all-caps, numbers in copy.
- Offer structure: discount %, free trial, bundle, BOGO, no-discount soft-sell.

### 2D. Top 3 ads per competitor (ranked by estimated reach where visible)

For each top ad: screenshot filename, ad format, hook type, full copy, CTA, estimated run duration, and why it is likely the winner.

### 2E. Creative fatigue signals

Any ad running 30+ days with a copy-variant rollout in the last 7 days indicates a working concept. Any ad paused after 7 days indicates a fatigued concept. Flag both.

---

## Step 6. Section 3. Google Ads SERP scan

For each competitor, pull paid-SERP copy via Serper on:

- The competitor's brand name (tests whether the client is bidding on the competitor, or vice versa).
- The category head term (from user input).
- 5 commercial-intent tail terms (derive from Keywords Everywhere related-queries on the head term).

For each query capture: Headline 1, 2, 3. Description 1, 2. Sitelinks (up to 4) with linked-page type. Callout extensions. Structured-snippet extensions. Price extensions where present.

Synthesise across queries per competitor: dominant headline pattern, offer language, which pages competitors send paid traffic to.

If DataForSEO Ads History or Ahrefs Ads History is available, pull the 24-month ad-copy archive and call out which copy variants have survived longest.

---

## Step 7. Section 4. Social content audit

Per competitor, across LinkedIn, X, Instagram, TikTok.

For each platform:

- Posting cadence (posts per week in the last 30 days).
- Content-theme breakdown (product, founder-voice, UGC repost, educational, behind-the-scenes, community/UGC feature, partnership, PR).
- Top 5 posts by engagement in the last 30 days. Capture: post URL, post type, hook line, engagement count, posting date.
- Recurring formats (same template reused, same hook structure, same CTA).

LinkedIn via WebFetch usually works. Instagram and TikTok hit login walls. Fall back to Apify scrapers if token is in `.env`, otherwise manual screenshots.

Synthesise across platforms per competitor: where do they invest heaviest, what format is driving their top engagements, is founder voice present.

---

## Step 8. Section 5. Hook and angle taxonomy

Cross-cutting pass. Aggregate hook-type frequency across every competitor, every ad, every top social post. Produce:

- Dominant hook type across all competitors combined (the category default).
- Secondary hook type.
- Under-represented hook types (whitespace candidates).

Produce a single 8-column hook-frequency table: columns are the 8 hook types, rows are the competitors, cells are the count of ads or posts per hook type. Bold the dominant per competitor.

---

## Step 9. Section 6. Production-style audit

Classify each competitor into one of 4 production styles, or mixed:

| Style | Signal |
|---|---|
| UGC | Phone-shot, face-to-camera, messy backgrounds, creator-led |
| Studio product | Clean white or brand-colour background, product-hero, controlled lighting |
| Polished brand | High-production lifestyle, director-led, model talent, colour-graded |
| Founder-voice | Founder on camera, talking-head, low-fi or studio-lo-fi |

For each competitor: name the dominant style, the secondary style, and the style they are absent from. Describe pacing, typical text-overlay treatment, typical colour palette, typical run-time for video ads.

Surface the style gap. Style arbitrage is a real lever in paid social.

---

## Step 10. Section 7. CTA pattern analysis

Aggregate CTAs across every ad and every top social post. Count frequency of each CTA pattern (Shop Now, Learn More, Download, Subscribe, Sign Up, Get Started, Book a Call, Watch Now, Shop the Sale, See the Review).

Flag the dominant CTA per competitor, the dominant across all competitors, and the CTA patterns no competitor is running. The unused CTA list is direct whitespace.

Note the offer-coupling patterns (e.g. "Shop Now + 20% OFF at checkout" vs "Shop Now, no discount").

---

## Step 11. Section 8. Whitespace map

Synthesis output of Sections 5, 6, and 7.

- **Angle whitespace.** Hook types, messaging angles, or claims no competitor is running.
- **Format whitespace.** Ad format + production-style combinations no competitor is running.
- **CTA whitespace.** CTA patterns or offer structures no competitor is running.
- **Audience whitespace.** Sub-audiences visible in the social content comments but not addressed in ads.
- **Platform whitespace.** Platforms where no competitor is active.
- **Price whitespace.** Price anchoring no competitor is using.

Rank each whitespace candidate by: Estimated Impact (1 to 10) × Confidence (1 to 10) × Effort to execute (1 to 10 inverse). Top 3 feed the top 3 starter briefs in Section 9.

---

## Step 12. Section 9. Starter ad briefs + Section 10. 30-60-90 test plan

Convert every whitespace candidate, every competitor "steal this" idea, and every cross-cutting theme insight into a candidate brief. Score each on ICE. Keep the top 10 to 15.

Each brief:

```
### Brief N: {hook in 8 words or fewer}

**Hook type:** {from the 8-type taxonomy}
**Angle:** {single-sentence angle statement}
**Competitor precedent:** {"inspired by competitor X's top ad, see screenshot N" or "whitespace, no competitor running"}
**Format:** {static / carousel / video / UGC}
**Production style:** {UGC / studio / polished brand / founder-voice}
**Length:** {seconds for video, or N cards for carousel}
**Primary copy (first 125 characters):** {draft}
**Body copy:** {draft, 3 to 5 sentences}
**CTA:** {from the CTA table}
**Offer:** {discount / free trial / no offer}
**Landing page target:** {URL or "build new LP"}
**Expected KPI band:** {CTR %, CPM $, CPA $, measured how}
**ICE score:** I{x} C{x} E{x} = {product}
```

Rank briefs by ICE descending. Group into:

- **Ship this week** (top 3).
- **Ship next 30 days** (next 5 to 7).
- **Ship next 60 to 90 days** (remaining).

Section 10 wraps the briefs into a calendar view (30-60-90) with budget per brief, learning-phase criteria, and quarterly re-run flag.

---

## Step 13. Voice enforcement gate (mandatory before writing to disk)

Before writing the file, run a mechanical voice-scan on the full draft. Grep for each banned pattern and rewrite every match:

| Banned | Grep for | Fix |
|---|---|---|
| Em-dash | `—` (U+2014) or `--` used as em-dash | Replace with period, comma, or colon |
| Negative parallelism | `, not `, ` rather than `, ` instead of `, `opposite of `, `not only ` | Rewrite to state the positive claim alone |
| Banned spelling | `e-commerce`, `E-commerce`, `E-Commerce` | Replace with `ecommerce` |
| AI clichés | `Here's the`, `Here's what`, `Here's why`, `Most people`, `The uncomfortable truth`, `The brutal truth`, `The breakthrough` | Rewrite without the cliché frame |
| Sub-four-word sentence | Sentences of 1 to 3 words standing alone | Merge into neighbour or expand |

`not` is permitted only when the negation is genuinely load-bearing.

Shipping a report with more than zero banned-pattern matches is a spec violation.

---

## Step 14. Synthesis pass + write outputs + actions.md merge

Before writing, assemble the full draft and run the synthesis pass:

- What hook or angle is every competitor running? (Category default.)
- What angle, format, or CTA is no competitor running? (Whitespace.)
- What does a Section 5 hook pattern imply for a Section 9 brief the current ranking missed?
- Does any Section 9 brief solve multiple whitespace gaps at once? Promote to top 3.
- Does any high-ranked Section 9 brief solve only one problem? Demote in favour of multi-leverage plays.

Produce 3 to 5 cross-cutting bullets. Revise:

- **Executive summary** to lead with the narrative these insights reveal (3 to 4 sentences).
- **Section 9 ranking** to re-rank briefs that hit multiple leverage points.
- Write the bullets into the **Cross-cutting themes** block.
- Generate the **Key findings** block (5 to 7 one-sentence bullets).
- Generate the **Top 10 to 15 ad angles** skim block with "why this works" per angle.
- Draft the **Conclusion** block (2 to 3 short paragraphs: what ships this week, what a paid engagement looks like, book-a-call CTA at https://entirecommerce.ai/audit).

Report structure (fixed order):

```
# Competitor Creative Audit: {Brand Name} ({YYYY-MM-DD})

Mode: {Full / Quick / Pre-launch / Focused}
Competitors covered: {list}

## Executive summary
## Cross-cutting themes
## Key findings
## Top 10 to 15 ad angles (ranked)
## 1. Competitor profiles
## 2. Meta Ad Library 30-day scan
## 3. Google Ads SERP scan
## 4. Social content audit
## 5. Hook and angle taxonomy
## 6. Production-style audit
## 7. CTA pattern analysis
## 8. Whitespace map
## 9. Starter ad briefs (top 10 to 15)
## 10. 30-60-90 test plan

## Access-grant checklist
## Conclusion
```

Write the file to:

```
{cwd}/docs/competitor-creative-audit/{YYYY-MM-DD}/competitor-creative-audit-report.md
```

Then convert to Word doc:

```bash
pandoc {cwd}/docs/competitor-creative-audit/{YYYY-MM-DD}/competitor-creative-audit-report.md \
  -o {cwd}/docs/competitor-creative-audit/{YYYY-MM-DD}/competitor-creative-audit-report.docx \
  --toc --number-sections
```

Save screenshots to `{cwd}/data/competitor-creative-audit/{YYYY-MM-DD}/screenshots/`. Save raw data (JSON, CSV) to `{cwd}/data/competitor-creative-audit/{YYYY-MM-DD}/raw/`.

**Exactly one consolidated report file at the primary output path.** Do not produce per-competitor files in the docs folder. Merge sub-agent output into the single file before writing.

### Merge into actions.md

If the current working directory has an `actions.md` file, merge the three "Ship this week" briefs into the Next Actions section. Respect the priority caps (P0 max 5, P1 max 10, P2 max 15). If a tier is over cap, rescore by ICE and demote the weakest before adding.

### Commit (optional)

If the folder is a git repo, commit the report, Word doc, screenshots, and updated actions.md. Commit message format:

```
Competitor creative audit: {Brand Name} ({YYYY-MM-DD}): {top whitespace in 6 words}
```

---

## Voice conventions (strict, applied throughout)

- No em-dashes. Use period, comma, or colon.
- No negative parallelisms. Never "X, not Y". State the positive.
- Four-word sentence floor. No one- or two-word sentences.
- Spelling: "ecommerce" one word.
- No AI clichés.
- Every finding traces to real data. No fabricated numbers. No invented sources.
- If a section is stubbed for missing access, state it plainly with the access path. Never pad with generic recommendations.

---

## Acceptance criteria

- End-to-end from this one prompt. No manual copy-paste between steps.
- Correct path and mode detection with user confirmation.
- Single consolidated report at the output path. Cross-cutting themes, Key findings, Top 10 to 15 ad angles, and Conclusion blocks populated by the synthesis pass.
- Word doc produced alongside the markdown via pandoc.
- Every top-15 brief fully populated (hook, angle, precedent, format, style, length, copy draft, CTA, offer, LP, KPI band, ICE score).
- The Whitespace map names 3+ candidates across angle, format, and CTA.
- No invented data. Missing tools stubbed honestly with access-grant path.
- Voice enforcement gate run before write. Zero banned-pattern matches in final output.

---

## What to do with the output

The top 3 briefs in Section 9 go into production this week. The whitespace map is your moat: it names the angles no one else is running. The 30-60-90 plan is the quarter. Re-run every 90 days. Creative rotates fast.

Want this run for you on a live engagement with a weekly review cadence, a daily dashboard, and the thirty-plus downstream playbooks across every GTM function? Book a call at https://entirecommerce.ai/audit.

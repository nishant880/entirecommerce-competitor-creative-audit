<div align="center">

---

### 🎯 **[Want us to run this for you? Book a call →](https://entirecommerce.ai/audit)**

---

</div>

# Competitor Creative Audit Playbook

## A deep teardown of 3 to 5 DTC competitors' active ads, SERP copy, and top-performing social posts, classified into hooks, angles, production styles, and CTA patterns, with a ranked shortlist of 10 to 15 ad angles your brand can steal, beat, or own. Run on your own brand in 45 to 90 minutes inside Claude Code. Delivered as a Word doc, the markdown source, and a supporting screenshots folder in your GitHub repo. Built by Nishant Kapoor at EntireCommerce AI.

---

<div align="center">

### ⚡ Fastest way to use this playbook

**Paste this document's URL into Claude Code and say:**

> *"Read this and take me through it step by step."*

**Claude will interview you for the business context, walk you through any missing API setup, and run the full competitor audit end-to-end. You don't need to read the rest of this document.**

</div>

---

## Who This Playbook Is For

This playbook is for three people.

**The founder-led DTC brand owner whose Meta ads just fatigued.** Your CTR has been sliding for four weeks. Your creative team keeps shipping testimonial carousels because that worked six months ago. You want to know exactly what every competitor is running, what is working for them, and the five angles you could ship next week that no one else is running. You want the swipe file and the briefs, in one doc, today.

**The paid-ads operator (fractional CMO or in-house growth lead) onboarding a new client.** You are two weeks into a new engagement. You need to walk into the first strategy call with a clear view of the competitive creative landscape, the dominant angles, the whitespace, and a ranked shortlist of 10 to 15 briefs the client can ship in the next 90 days. You want the same depth every time, delivered by the same process.

**The pre-launch DTC brand mapping the category.** You have not spent a dollar on ads yet. You do not know what the category default looks like. You want a snapshot of how the top 3 to 5 incumbents are positioning, what formats they are running, what CTAs they are using, and the angle you can own on day one.

If you have been scrolling Meta Ad Library by hand, screenshotting ads into Notion, writing hook-taxonomy decks for your creative team, piecing together Instagram reels into a swipe file, this playbook collapses all of that into one consolidated output in a single Claude Code session.

---

## What The Competitor Creative Audit Actually Is

**The short version.** Ten sections in one consolidated report. Claude Code runs the teardown end-to-end: profiles the 3 to 5 competitors you name, pulls their active Meta ads, captures their Google Ads SERP copy, audits their top-performing posts on LinkedIn, X, Instagram, and TikTok, classifies every hook into an 8-type taxonomy, maps production style, counts CTA frequency, identifies whitespace across angle, format, and CTA, and hands back a ranked shortlist of 10 to 15 starter ad briefs, each one fully populated with hook, angle, format, copy draft, CTA, offer, and KPI band. Plus a dedicated synthesis pass that reads the whole draft end-to-end and surfaces three to five cross-cutting themes, the creative-strategy narrative the data reveals when every competitor is in view at once.

**Best for.** Premium DTC brands. AOV $500+ or 2x category median. Founder-led. Paid-ads-active on Meta or Google (or planning to go active). US, UK, or English-speaking European markets.

**How it's different.** Three things most competitor audits skip.

First, the **whitespace map**. Competitor audits usually tell you what competitors are doing. The whitespace map tells you what they are all missing. Angle whitespace, format whitespace, CTA whitespace, audience whitespace, platform whitespace, price whitespace. Each one is a candidate for the angle your brand can own.

Second, the **synthesis pass**. Section-by-section teardown gives you a directory of findings. The synthesis pass gives you the story. A hook pattern in Section 5 might imply a format play in Section 6 that no competitor is using, which turns into the top brief in Section 9. None of those connections surface from a competitor-at-a-time read. Claude does the cross-read explicitly.

Third, the **starter briefs**. Most audits stop at "here's what they're running". This playbook ends with 10 to 15 ready-to-ship briefs. Each brief is a one-page creative doc: hook, angle, competitor precedent, format, production style, length, copy draft, CTA, offer, landing page target, expected KPI band, and ICE score. Your creative team takes them straight into production.

**Skip this playbook if** you're a service business, a B2B SaaS, or a brand selling at the mass-market tier. The audit is tuned for premium DTC and the recommendations will be directionally off for other contexts.

---

## Setup (15 Minutes)

### Prerequisites

Before you start, make sure you have:

- **Claude Code** installed. Download from [claude.com/claude-code](https://claude.com/claude-code). Verify with `claude --version`.
- **pandoc** installed for the Word-doc export. On macOS: `brew install pandoc`. On Windows: [pandoc.org/installing.html](https://pandoc.org/installing.html). Verify with `pandoc --version`.
- **A project folder** on your machine. One per brand you audit. Name it after the brand.
- **A Meta account** logged into a browser on the same machine. Meta Ad Library will sometimes gate you for login even on public pages.

### Cost overview

The playbook itself is free. You pay for API credits consumed by tools the audit uses. Most are free or near-free.

| Tool | Subscription model | Typical per-run cost | Role |
|---|---|---|---|
| Meta Ad Library | Free, public web | $0 | The primary ad-teardown data source. No API key. |
| Serper | Free tier gives 2,500 credits | Under $0.50 | Recommended. Powers the Google Ads SERP scan. |
| DataForSEO | Pay-as-you-go, no monthly fee | $0.50 to $3 | Optional. Ads History endpoint covers 24-month ad-copy archive. |
| Ahrefs | $129+ per month | Optional | Skip unless you already have an account. DataForSEO covers most of the same ground. |
| Keywords Everywhere | ~$10 one-time for 100K credits | Under $0.50 | Used for tail-term discovery on the head term. |
| Apify | Free tier ~5K actor credits/month | $0 to $5 | Optional. Unlocks Instagram and TikTok top-post scraping when WebFetch hits a login-wall. |
| Google PageSpeed Insights | Free | $0 | Uses a free Google Cloud API key (`GOOGLE_AI_KEY`). |
| Meta Ads API | Free, your own account | $0 | Internal tool. Partner invite to score your own creative fatigue. |
| Google Ads | Free to read | $0 | Internal tool. Read-only. |

**Typical total cost per full audit run: $0 to $10** across the paid external tools.

Numbers above are approximate as of April 2026. Pricing changes. When you run the master prompt, Claude will print the credential inventory and offer to look up current sign-up steps and pricing for any tool you're missing, straight from the web.

### Step 1: Create the project folder

```bash
mkdir my-brand-competitor-audit && cd my-brand-competitor-audit
```

Drop the three files from this bundle (CLAUDE.md, competitor-creative-audit.md, README.md) into the folder.

**Gotcha I hit:** if you already ran another EntireCommerce playbook (GTM Audit, SEO Audit) in the same folder, the CLAUDE.md business brief is likely already populated. Reuse it. Skip Step 3.

### Step 2: Set up your .env (optional: let Claude walk you through)

Create a `.env` file in the project folder. Add the API keys you have. Missing keys are fine: Claude will print the credential inventory and offer to walk you through sign-up for each missing tool when you run the master prompt.

Minimum recommended `.env`:

```
SERPER_API_KEY=your_key
DATAFORSEO_LOGIN=your_login
DATAFORSEO_PASSWORD=your_password
KEYWORDS_EVERYWHERE_API_KEY=your_key
GOOGLE_AI_KEY=your_google_cloud_api_key_for_pagespeed
APIFY_TOKEN=your_apify_token_if_you_have_one
AHREFS_API_KEY=your_key_if_you_have_one
```

**Gotcha I hit:** Meta Ad Library via raw WebFetch returns empty every time. The page is JS-rendered. The playbook's fallback chain runs Playwright, third-party indexes, the Apify Meta Ad Library scraper, and manual screenshots in that order. Expect to paste 10 to 15 manual screenshots per competitor into `data/competitor-creative-audit/{date}/screenshots/` if nothing else works.

**Gotcha #2:** Never commit your `.env` to a public repo. Add `.env` to your `.gitignore` before your first commit.

### Step 3: Populate CLAUDE.md (or let Claude interview you)

You have two options:

**Option A (recommended, fastest):** Leave `CLAUDE.md` as-is. When you run the master prompt in Step 5, Claude will interview you conversationally: brand overview, product, audience, positioning, tool stack, competitor list, creative pain. Claude writes the file for you progressively. Takes about 10 minutes.

**Option B (DIY):** Open `CLAUDE.md` and replace every `{placeholder}` with your brand's specifics yourself before running the audit. Founder voice, one or two sentences per field.

**Gotcha #3:** Three to five competitor brand names + URLs + Facebook page names are load-bearing. Facebook page name is the exact string on `facebook.com/{page-name}` that Meta Ad Library uses to pull a brand's ad history. Without it, Claude has to auto-discover the Ad Library ID for each competitor, which sometimes fails. Your hand-picked list with Facebook page names is always sharper.

### Step 4: Open Claude Code in the folder

```bash
claude
```

Claude Code loads `CLAUDE.md` automatically on session start. Confirm you see "Loaded CLAUDE.md" in the session log.

---

## The Three Files in This Bundle

### File 1: CLAUDE.md (business-briefing template)

**Path:** `{your-project-folder}/CLAUDE.md`
**What it does:** Claude Code loads this on every session start. It's where your brand's specifics live: product, audience, positioning, competitor list, creative pain, tool stack. Every playbook you run from this folder reads from here first.
**How to use it:** Replace every `{placeholder}` with your specifics. Keep it tight, one to two sentences per field beats a paragraph. Founder voice beats marketing copy.

### File 2: competitor-creative-audit.md (the master prompt Claude runs)

**Path:** `{your-project-folder}/competitor-creative-audit.md`
**What it does:** The prompt Claude executes end-to-end to produce the audit. Covers all ten sections plus the synthesis pass plus the voice-enforcement gate plus the pandoc Word-doc export.
**How to use it:** Paste its entire contents into Claude Code and hit enter. Don't edit it unless you know what you're doing, the structure is load-bearing.

### File 3: README.md

**Path:** `{your-project-folder}/README.md`
**What it does:** You're reading it. Setup, run, and troubleshooting reference. Safe to ignore once you've run the audit once.

---

## Your First Run

Five steps. Forty-five to ninety minutes.

1. **Open Claude Code in your project folder.** `cd my-brand-competitor-audit && claude`
2. **Paste the full contents of `competitor-creative-audit.md` into the terminal.** Hit enter.
3. **Claude prints a credential inventory.** You'll see which External tools are wired and which Internal tools are missing. Claude offers to walk you through sign-up for each missing one.
4. **Claude confirms the mode** (Full, Quick, Pre-launch, or Focused) based on your inputs.
5. **Claude runs the audit.** Pulls competitor Meta ads, captures Google Ads SERP copy, audits top social posts, classifies every hook, maps production styles, counts CTAs, writes the whitespace map, drafts the top 10 to 15 starter briefs, runs the synthesis pass, runs the voice gate, writes the report.

Output lands at:

```
{your-project-folder}/docs/competitor-creative-audit/YYYY-MM-DD/competitor-creative-audit-report.md
{your-project-folder}/docs/competitor-creative-audit/YYYY-MM-DD/competitor-creative-audit-report.docx
{your-project-folder}/data/competitor-creative-audit/YYYY-MM-DD/screenshots/
{your-project-folder}/data/competitor-creative-audit/YYYY-MM-DD/raw/
```

---

## What You'll Get

Ten high-value deliverables in one consolidated report plus a supporting screenshots folder.

1. **Executive summary with cross-cutting themes.** A 3-4 sentence narrative plus 3-5 strategic insights spanning multiple competitors or sections. Produced by a dedicated synthesis pass that reads the whole draft end-to-end. This is where the creative-strategy story of the category emerges.
2. **Competitor profile cards.** One 300 to 500-word card per competitor: positioning, audience, top 10 selling products, price range, social presence, active ad volume, partnerships and PR.
3. **Meta Ad Library 30-day scan per competitor.** Active ad count, format mix, hook taxonomy, copy patterns, top 3 ads ranked by estimated reach, creative fatigue signals, evergreen winners flagged.
4. **Google Ads SERP scan.** Paid-SERP copy on brand queries, head term, and five tail terms per competitor. Headlines, descriptions, sitelinks, callouts, offer language. Plus 24-month ad-copy archive where Ads History data is available.
5. **Social content audit.** Top 5 posts per platform per competitor on LinkedIn, X, Instagram, TikTok. Posting cadence, content themes, recurring formats.
6. **Hook and angle taxonomy.** Every ad and top post classified into an 8-type hook framework. Dominant hook per competitor, dominant across all competitors, under-represented hook types (the whitespace candidates).
7. **Production-style chart.** UGC vs studio vs polished brand vs founder-voice, per competitor. Pacing, text-overlay treatment, palette, typical video run-time.
8. **CTA pattern analysis.** CTA frequency per competitor and across the category. Offer-coupling patterns (discount vs no-discount, Shop Now vs Learn More).
9. **Whitespace map.** Angle, format, CTA, audience, platform, and price whitespace. Each whitespace candidate ranked by ICE.
10. **Top 10 to 15 starter ad briefs with 30-60-90 test plan.** Every brief fully populated with hook, angle, competitor precedent, format, production style, length, copy draft, CTA, offer, landing page target, expected KPI band, and ICE score. Plus a 30-60-90 test plan sequencing the briefs into a quarter of production.

**Format.** One consolidated Word doc (shareable with your team) plus the markdown source and the supporting competitor-screenshots folder in your GitHub repo. Typically 5,000 to 9,000 words. Reading time around 30 minutes cover to cover, 90 seconds to skim via the Top 10 to 15 ad angles block at the top.

---

## Modes

The audit auto-detects which mode applies to your brand and adapts section depth accordingly.

| Mode | When it applies | What changes |
|---|---|---|
| Full | 3 to 5 competitors, paid-ads-active brand | Standard engagement. All 10 sections. Full synthesis pass. 10 to 15 starter briefs. |
| Quick | 1 competitor named, Meta + hooks only | Sprint-sized. Used when one competitor dominates or the founder flagged one brand. Skips social-content audit and production-style audit. |
| Pre-launch | New brand, 5+ competitors, no ads running yet | Category-level landscape scan. Heavy whitespace mapping. Light on fatigue scoring. |
| Focused | 1 competitor, deep teardown | The brand is gaining share fast. The founder needs to understand exactly how before countering. |

---

## Honest Caveats

**Meta Ad Library WebFetch fails more often than it succeeds.** The Meta Ad Library page is JS-rendered and WebFetch returns empty on most runs. The spec includes a fallback chain (Playwright, third-party ad-library indexes, Apify scraper, manual screenshots) but the manual-screenshot path requires your time. Plan on spending 20 to 40 minutes capturing 10 to 15 screenshots per competitor if the automated chain fails.

**Instagram and TikTok hit login walls.** WebFetch against a public profile page sometimes works, sometimes returns a login-wall HTML blob. If Apify is wired, the Instagram and TikTok scrapers cover it. If not, plan on manual screenshots for those two platforms.

**The synthesis pass depends on Claude holding the whole draft in context simultaneously.** On very large reports (above 9,000 words, typical when auditing five competitors with full social-content depth), the cross-cutting read can lose depth. If the Cross-cutting Themes block feels thin, rerun with three competitors.

**Starter briefs are starters.** The copy drafts in Section 9 are creative-direction drafts. Your copywriter or creative team still has work to do before the ad ships. The brief tells them exactly what to write toward.

**Voice rules are strictly enforced.** Claude runs a mechanical grep-pass for em-dashes, negative parallelisms ("X, not Y"), banned spelling ("e-commerce"), and AI clichés ("Here's the...") before writing the report to disk. If you spot a banned pattern in the output, flag it and rerun the voice gate.

**Competitor ad rotation is fast.** Re-run quarterly. A 6-month-old swipe file is worse than useless.

**The playbook is tuned for premium DTC and will miss on edge cases.** If you sell B2B SaaS, run a service business, or target the mass market, the audit's recommendations will be directionally off.

---

## Quick-Start Checklist

Work top-to-bottom. Items you'd run first are ordered first.

- [ ] Claude Code installed (`claude --version` works)
- [ ] pandoc installed (`pandoc --version` works)
- [ ] Meta account logged into your browser on the same machine (for manual Meta Ad Library fallback)
- [ ] Project folder created for the first brand you want to audit
- [ ] CLAUDE.md from this bundle copied into the project folder
- [ ] competitor-creative-audit.md from this bundle copied into the project folder
- [ ] Serper API key added to `.env`
- [ ] DataForSEO credentials added to `.env` (optional but recommended)
- [ ] Apify token added to `.env` if you have one (unlocks Instagram and TikTok)
- [ ] CLAUDE.md filled in, competitor list populated with Facebook page names
- [ ] First run executed and Word doc produced at `docs/competitor-creative-audit/{date}/`
- [ ] Report reviewed, top 3 "Ship this week" briefs identified
- [ ] Top 3 briefs merged into your team's actions.md
- [ ] Screenshots folder committed to your GitHub repo alongside the report
- [ ] Re-run quarterly to track competitor creative movement
- [ ] Book a call if you'd rather we run this for you on a live engagement: [entirecommerce.ai/audit](https://entirecommerce.ai/audit)

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| "pandoc not found" at Word-doc export | pandoc not installed | `brew install pandoc` (macOS) or [pandoc.org/installing.html](https://pandoc.org/installing.html) |
| Meta Ad Library scan returns empty | WebFetch against JS-rendered page | Use the fallback chain in the spec: Playwright → third-party index (adscan.ai) → Apify Ad Library scraper → manual screenshots |
| Instagram or TikTok profile audit fails | Login wall on WebFetch | Add an Apify token to `.env` and rerun. Otherwise fall back to manual screenshots. |
| Report splits into per-competitor files instead of one consolidated file | Sub-agent split issue | Rerun. The spec explicitly bans per-section files; a clean run should consolidate. |
| Voice gate flags em-dashes or "X, not Y" patterns in output | Style drift in sub-agent output | Paste the banned-patterns list back into Claude and ask it to scan-and-fix the full file |
| Fewer than 10 briefs produced in Section 9 | Too few competitors or too thin ad inventory | Rerun with one extra competitor, or lower the ICE threshold in Section 9 to keep more candidates |
| Whitespace map returns empty | All competitors running the same angles, or audit scope too narrow | Add one adjacent-category competitor to widen the scope |

---

## Credit

Built by Nishant Kapoor at EntireCommerce AI.

- **LinkedIn**: [linkedin.com/in/nishantkapoor1](https://www.linkedin.com/in/nishantkapoor1)
- **Email**: nishant@entirecommerce.co
- **Book a call**: [entirecommerce.ai/audit](https://entirecommerce.ai/audit)
- **Full playbook library** (GTM audit, weekly review, SEO audit, CRO review, competitor creative audit, and thirty-plus more): [entirecommerce.ai/playbooks](https://entirecommerce.ai/playbooks)

Use this playbook freely. Share it with other DTC founders. If you ship a case study running it on your brand, tag us. We'll link to it from the site.

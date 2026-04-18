# Business brief: {Your brand}

> This file is the business brief Claude Code loads automatically on every session start. It grounds every playbook you run from this folder in your brand's specifics.
>
> **Two ways to populate it:**
>
> **Option A (fastest, recommended).** Leave the file as-is (or delete it entirely). Run the Competitor Creative Audit master prompt and Claude will interview you conversationally, ask every question below, and fill in the file for you as you go. Takes about 10 minutes. You answer questions in plain language; Claude writes the structured brief.
>
> **Option B (DIY).** Fill in every `{placeholder}` yourself before running the audit. Keep it tight: one to two sentences per field. Use founder voice over marketing copy.
>
> Either way the end state is the same: a populated `CLAUDE.md` that every future playbook (GTM audit, SEO audit, weekly review, etc.) reads from.

---

## Brand overview

- **Brand name**: {Your brand name}
- **Primary URL**: {https://yourbrand.com}
- **Ecommerce platform**: {Shopify / WooCommerce / Custom / etc.}
- **Geographic focus**: {US, UK, EU, global, etc.}
- **Stage**: {Pre-launch / first year / established with trading history / mature}

## Product

- **What you sell (one sentence)**: {e.g. "Launch-monitor-backed short-game training systems for club golfers improving wedge consistency."}
- **Price range**: {e.g. "$500 to $1,200. AOV $650."}
- **Catalog size**: {Number of active SKUs or product lines}

## Paid-ads context (specific to this playbook)

- **Primary ad platforms**: {Meta, Google, TikTok, LinkedIn, X, Pinterest, etc. List every platform the brand is running paid on today, or planning to run on soon.}
- **Ad spend band**: {e.g. "Under $5K/mo" / "$5K to $25K" / "$25K+" / "Pre-launch, no spend yet"}
- **Current creative pain (one sentence)**: {e.g. "All our ads are testimonial carousels; CTR dropped 30% this month" or "We're pre-launch and have no creative yet."}

## Target audience

- **Core buyer (one sentence)**: {e.g. "Club golfers in the US aged 35 to 55 frustrated by inconsistent wedge distances inside 100 yards."}
- **Secondary buyer (if any)**: {Second audience segment if material}
- **Where they hang out online**: {Reddit subs, niche forums, YouTube channels, Instagram accounts, podcasts}

## Positioning

- **Why you win (one sentence, in your words)**: {What you do that nobody else does, or do better. Feeds the Whitespace map in Section 8.}
- **Pricing tier vs category median**: {e.g. "priced 3x category median" / "premium of the category" / "value tier"}

## Competitor list (load-bearing for this playbook)

List 3 to 5 competitors the buyer also considers. For each, provide the brand name, the URL, and the Facebook page name (the exact string on `facebook.com/{page-name}` that Meta Ad Library uses). Without the Facebook page name, Claude has to auto-discover the Ad Library ID, which sometimes fails.

- {Competitor 1}: {URL}, Facebook page name: {page-name}
- {Competitor 2}: {URL}, Facebook page name: {page-name}
- {Competitor 3}: {URL}, Facebook page name: {page-name}
- {Competitor 4}: {URL}, Facebook page name: {page-name} (optional)
- {Competitor 5}: {URL}, Facebook page name: {page-name} (optional)

**Category head term (one line)**: {e.g. "launch monitor" or "lab-grown diamond pendant" or "luxury watch resale". Drives the paid-SERP scan in Section 3.}

## Tool stack

List every tool you use for marketing. Claude will detect which have API credentials wired in `.env`.

- **Website / CMS**: {Shopify, WordPress, Next.js, etc.}
- **Analytics**: {GA4, Mixpanel, etc.}
- **Ad platforms**: {Google Ads, Meta Ads, TikTok, etc.}
- **Social-content tools**: {Buffer, Later, native scheduling}
- **CRO / session behaviour**: {Microsoft Clarity, Hotjar, FullStory}
- **AI assistants / prompts**: {Claude, ChatGPT, internal tools}

## Voice and brand guidelines (optional)

- **Spelling conventions**: {e.g. "ecommerce one word, never e-commerce"}
- **Phrases to avoid**: {Any banned clichés, industry jargon you reject}
- **Phrases the brand owns**: {Your recurring taglines, headlines, or catchphrases}
- **Tone**: {Direct / warm / technical / luxury / conversational}

## Session history (updated by Claude across sessions)

> Claude will append notes below as it learns patterns specific to your business. Leave this section blank to start; it grows over time.

---

## How Claude should use this file

On every session start, load this brief and treat it as the ground truth for your brand's specifics. When you run any EntireCommerce playbook (like `competitor-creative-audit.md`) in this folder, cross-reference the inputs here before asking the user for them. Do not invent values. If a field is blank, ask the user to fill it in before proceeding with work that depends on it.

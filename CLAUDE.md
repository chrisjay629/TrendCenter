# NOIZE — Project Intelligence File

This file is the source of truth for planned features, tech decisions, and context. Reference it at the start of every session.

---

## New Tools We're Integrating

| Tool | Purpose | Status |
|---|---|---|
| **Exa.ai** | Semantic web search built for AI agents — replaces/supplements Google News RSS; indexes X/Twitter content without needing X's API | Planned |
| **Jina Reader** | Free API — prefix any URL with `r.jina.ai/` to get clean markdown of any page; fixes article extraction and og:image failures | Planned |
| **Firecrawl** | Scrapes JS-heavy pages and some paywalls; best shot at TikTok page content | Planned |

---

## New Features to Implement

### HIGH PRIORITY

#### 1. "First Signal" Alert (X / Twitter Early Warning)
- Use Exa to detect topics trending on X that have NOT yet appeared on YouTube, Google News, or Reddit
- Flag these as "X-Only" with a timestamp — this is the creator's 24–72 hour head-start window
- This changes NOIZE's pitch from "trend dashboard" to "get there before anyone else"

#### 2. Deep Dossier (Real Sources, No Hallucinations)
- Currently the Investigate dossier is GPT generating from memory/training data
- New flow: Exa finds 10 real articles on the topic → Jina Reader extracts full text → GPT synthesizes from actual content
- Result: real quotes, real data, zero hallucinated facts, linked sources

#### 3. TikTok Data via Firecrawl
- Use Firecrawl to attempt scraping TikTok's trending hashtag pages and Creative Center
- Not guaranteed but far better than raw requests
- Test on: TikTok trending page, hashtag pages, TikTok Ad Library

---

### MEDIUM PRIORITY

#### 4. "Pre-Peak Alert" — Catch Trends 3 Days Early
- Use Exa's time-filtered semantic search to find topics gaining web mentions but not yet exploding
- Show a "signal strength" velocity meter
- Most creators react after peak — this closes that gap

#### 5. "Who's Talking" Intelligence
- For any trending topic, show WHO is pushing it on X: journalists, big creators, brands
- Estimate: "10 journalists, 3 brands, 2 major creators discussing this → estimated mainstream crossover: 24–48 hrs"

#### 6. Hook & Angle Bank (from X)
- Pull most-engaged X posts about a trend
- Use as raw hook material for Blueprint generation
- Real audience language, already proven to resonate

#### 7. "X vs Everywhere Else" Gap Map
- Side-by-side comparison: trending on X only (opportunity), trending on YouTube only (past peak), trending on both (mainstream)
- Helps creators instantly see where a trend is in its lifecycle

#### 8. Niche Intelligence Mode
- Creator declares their niche (fitness, finance, gaming, etc.)
- Exa does semantic search scoped to that niche only
- Fitness creator never sees political news — just what's moving in their world

#### 9. Sentiment Arc
- Track whether X conversation about a topic is trending positive, negative, or controversial over time
- Helps creators decide: ride the trend, take a counter angle, or avoid it if it's turning toxic

---

### LOWER PRIORITY / FUTURE

#### 10. Thread Intelligence
- Exa finds the best long X threads on any topic
- Summarize and feed into the Dossier as free deep research

#### 11. "Creator DNA Scanner"
- Paste a YouTube channel URL
- Exa + Jina scrape their top content
- GPT analyzes what hooks, formats, and topics perform best for that creator's audience specifically
- Personalized strategy, not generic advice

#### 12. Paywall Intel
- Use Jina Reader to extract content from light paywalls (Bloomberg, Axios, WSJ)
- Feed premium publication signals into trend intelligence

#### 13. Real Reddit Sentiment
- Use Firecrawl to pull actual Reddit comment threads (not just post titles)
- Extract real audience reactions to feed into Blueprint generation

#### 14. AI Video/Image Generation (via Higgsfield API)
- After a trend is detected, offer "Generate a TikTok-style video for this trend"
- Call Higgsfield's REST API (`cloud.higgsfield.ai`) from Streamlit
- Requires Higgsfield Plus plan ($39/month) for API key
- Adds actual content production to NOIZE's intelligence output

---

## NOIZE as a Media Property — "The Daily Signal"

### The Big Idea
NOIZE already gathers faster, deeper trend data than any journalist can manually. The writing step is just one GPT call away. NOIZE becomes its own news column — written for content creators, not the general public.

### Core Concept
**"The Daily Signal" — by NOIZE**
- Auto-generated every morning from all sources (Exa, Jina, Google News, Reddit, X, YouTube)
- Written in NOIZE's noir/Chief Detective Pugson voice — sharp and punchy, not dry news copy
- Each story compressed to 3–4 sentences max
- Every story includes a **Creator Angle** — why this matters for your content, what to do with it
- Trend velocity embedded in each item: *"Moving 4x faster than normal. Window: 18 hrs."*
- Published before mainstream media catches up

### What Makes It Different From Regular News
- Written FOR content creators, not the general public
- Tells you what to DO with the story, not just what happened
- Published before it goes mainstream (First Signal advantage)
- One compressed narrative — the whole day in one read, not 30 separate articles
- Velocity data tells you how much time you have

### Growth Path
- **Phase 1:** Column tab inside the NOIZE app (auto-generated daily)
- **Phase 2:** Email newsletter — subscribers get it every morning
- **Phase 3:** Own URL (e.g. noize.news) — fresh daily content = Google SEO
- **Phase 4:** Auto-post column headline to X every morning (distribution flywheel)
- **Phase 5:** Standalone media property — not just an app feature, a brand

### Visual Design — Old-School Broadsheet Newspaper
The column looks like a 1940s newspaper. The contrast is the brand: cutting-edge AI trend intelligence dressed like a classic broadsheet.

- **Masthead:** "THE DAILY SIGNAL" in large bold serif across the top. Subtitle: *"All the trends fit to shoot."* Edition number, date, price ("Two cents")
- **Paper texture:** Aged cream/yellowed background — not white. Feels like holding a real newspaper
- **Multi-column layout:** Stories flow in actual newspaper columns (2–3 col grid), not modern cards
- **Typography:** Playfair Display or similar classic serif. Headlines in ALL CAPS condensed. Body copy tight and dense like newsprint
- **Datelines:** *"NEW YORK, THURSDAY — Sources confirm the fitness accountability trend is moving at 4x velocity..."*
- **Byline:** Every piece credited to *"Chief Detective Pugson, NOIZE Intelligence Bureau"*
- **Pull quotes** styled as classic newspaper breakouts with ruled lines
- **"BREAKING" stamp** in red — the only color on the page
- **Trend velocity as a barometer** — old mechanical gauge graphic, not a modern chart
- **Above/below the fold** hierarchy — biggest story gets top placement just like a real paper
- **Section dividers** with old-school ruled lines between stories

### Technical Approach
- Morning cron job pulls from all data sources
- Exa semantic search for X + web signals
- Jina Reader extracts full article text for context
- GPT synthesizes into NOIZE voice column
- Cached and served to all users (like existing Strange Signals pattern)
- Optional: user selects their niche → personalized version of the column
- Rendered as a styled HTML page inside Streamlit (custom CSS for newspaper look)
- Shareable as a standalone link with full newspaper styling intact

---

## Architecture Upgrades from Seeker Blueprint

Seeker is a persistent AI investigation engine with architectural patterns that translate directly into NOIZE. These are not features — they are how the engine works under the hood.

### Three-Tier Cost Discipline
NOIZE currently fires expensive GPT calls for everything. The correct architecture:
- **Tier 1 (free, always runs):** Platform scrapers, SQLite velocity math, gap scores, signal tier classification. No LLM, no API cost.
- **Tier 2 (cheap, runs on qualifying signals):** Pre-filter triage, authenticity verification. Single gpt-4o-mini call.
- **Tier 3 (expensive, rationed):** Deep Dossier, Blueprint generation, Daily Signal. Full GPT call, only fires after Tier 1 + 2 pass.
- Rule: **prime the expensive call with cheap intelligence before firing it.**

### Signal Tier System (replaces raw velocity tracking)
Every trend gets classified. Lives in `database.py` as a `signal_tier` column:
- **Confirmed** — appearing on 3+ independent platforms simultaneously
- **Emerging** — on 2 platforms, gaining velocity
- **Weak Signal** — one platform only, early detection
- **Noise** — single mention, no cross-platform confirmation
- A trend crossing tiers is more important than its absolute rank. Weak Signal → Emerging in 6 hours = Pre-Peak Alert trigger.

### Cross-Platform Gap Detection (the First Signal engine)
Platform disagreement IS the intelligence. Fire all scrapers in parallel (ThreadPoolExecutor). Compare results. A topic on X/Reddit with zero YouTube/Google News results gets a high gap score and triggers the First Signal flag. The current code discards this friction. This IS the feature.

### Source Credibility Ledger
SQLite table: `source_credibility` — tracks which subreddits, channels, and outlets consistently surface trends first. Auto-updates every 72 hours based on which signals materialized. Compounds over time. NOIZE gets smarter with no manual work.

### Saturation / Window Calculator
Rolling velocity window on `hashtag_snapshots`. Acceleration decreasing = approaching peak. Rate negative = past peak. Output: *"Window open — 18 hrs estimated"* on every trend card. Computable from existing data.

### Miss Log (Trust Engine)
SQLite table: `miss_log` — when a flagged trend doesn't materialize, log it. Show it publicly. *"NOIZE flagged this as Emerging on Tuesday. It didn't cross over. Reason: single platform signal."* Showing misses builds more trust than hiding them. Miss Log auto-feeds the Source Credibility Ledger.

### Pre-Filter Triage Gate
Before any expensive Dossier or Blueprint call, run cheap checks:
1. Has this topic been investigated in the last 7 days? (SQLite, free)
2. How many platforms show signal? (existing scraper data, free)
3. What is the source credibility score? (ledger lookup, free)
4. Is velocity accelerating or decelerating? (SQLite query, free)
Only topics passing triage trigger the expensive GPT synthesis.

### Multi-Lens Blueprint (Observer Council)
Replace the single monolithic Blueprint GPT call with 5 targeted cheap calls:
- **Early Adopter Lens** — is this actually early or has it been done?
- **Saturation Lens** — how many creators already covered this?
- **Counter-Trend Lens** — is a controversy forming that makes this risky?
- **Hook Lens** — what language is the actual audience using?
- **Monetization Lens** — does this topic type historically perform for revenue?
Five cheap calls feed one final synthesis. Better output, lower cost per call.

### Trend Forecast / Impact Map (added to Dossier)
Three-column forecast section:
- **Likely Peaks** — velocity-based peak timing estimate with historical comparisons
- **Adjacent Opportunities** — related topics likely to emerge next
- **Unknown Territory** — faint signals with no confirmation yet, first-mover advantage if they materialize

### Detection Lead Time — The Headline Metric
Track average hours between NOIZE first flagging a trend and it appearing in mainstream Google News/YouTube Trending. Publish it. *"NOIZE detected this 31 hours before mainstream."* This is the metric that justifies the product — not claimed, demonstrated.

### Overnight Consolidation Pass (add to scheduler.py)
3 AM job, no LLM calls — pure math:
- Compute cross-platform gap scores for all topics in last 24 hours
- Update velocity trajectories
- Update Source Credibility Ledger
- Pre-classify Signal Tiers
- Flag top 5 topics that crossed a tier boundary overnight
Daily Signal generates from pre-computed overnight intelligence, not expensive real-time calls at peak hours.

---

## Tech Notes

### Higgsfield Supercomputer
- NOT a solution for TikTok trend data — they face the same wall (use TikTok Ad Library + web crawl)
- Their REST API covers image/video generation only — not trend research
- Could be used for feature #14 above
- API available at Plus tier ($39/month), Python SDK available

### TikTok Reality Check
- No public API for live trending data
- TikTok Ad Library IS publicly accessible — worth mining
- Firecrawl is the best scraping attempt; Exa indexes some TikTok content
- Exa is the strongest current option for TikTok signal without an official API

### X (Twitter) Data
- X's official API costs $100/month minimum — not worth it
- Exa has indexed X content and can search it semantically for free
- Exa is the solution for X trend data

---

## Current Stack (as of June 2026)
- Python 3.9+ / Streamlit / Plotly
- OpenAI GPT-4o-mini (dossiers, blueprints, Strange Signals)
- Google News RSS + Google Trends
- YouTube Data API v3
- Reddit (post titles)
- SQLite (velocity tracking)
- Railway (deployment)

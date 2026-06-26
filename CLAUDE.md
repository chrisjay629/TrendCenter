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

### Technical Approach
- Morning cron job pulls from all data sources
- Exa semantic search for X + web signals
- Jina Reader extracts full article text for context
- GPT synthesizes into NOIZE voice column
- Cached and served to all users (like existing Strange Signals pattern)
- Optional: user selects their niche → personalized version of the column

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

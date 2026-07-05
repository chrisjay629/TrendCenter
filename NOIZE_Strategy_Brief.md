# NOIZE — Strategy Brief
### Prepared for Management Review | June 2026

---

## What NOIZE Is Today

NOIZE is a real-time trend intelligence dashboard for content creators. It monitors the internet across multiple platforms — Google News, YouTube, Reddit, Google Trends — and turns what's trending into ready-to-use content strategies. Creators type a topic and get a full dossier, a script, a posting strategy, and AI prompts to execute it, all in one place.

The app is live, deployed, and working. This document is about where it goes next.

---

## What We Discovered This Session

### The TikTok Problem (and the Solution)
Getting live TikTok trend data has been one of the hardest problems to solve. TikTok has no public API for trending data. We researched Higgsfield Supercomputer — a heavily marketed AI tool claiming to "watch TikTok in real time" — and found that even they face the same wall. Their TikTok intelligence comes from the TikTok Ad Library (publicly accessible) plus web crawling. No one has a magic solution here.

However, we identified three tools that collectively solve or significantly reduce this problem:

---

## Three New Tools to Integrate

### 1. Exa.ai
**What it is:** A web search engine built specifically for AI agents. It searches by meaning, not keywords.

**Why it matters for NOIZE:**
- Has indexed X (Twitter) content — meaning NOIZE can search what people are saying on X without paying X's $100/month API fee
- Can find topics gaining web mentions before they explode into mainstream news
- Semantic search means a fitness creator can search for "fitness accountability trends" and get truly relevant results, not keyword matches
- Has also indexed some TikTok content, giving us a window into TikTok signals without direct access

**This is the biggest single unlock.** X is where trends break first — before YouTube, before news outlets, before Reddit picks them up. Exa gives us X data for free.

---

### 2. Jina Reader
**What it is:** A free API that converts any webpage into clean, readable text for AI processing. You prefix any URL with `r.jina.ai/` and get the full article content back.

**Why it matters for NOIZE:**
- Fixes article extraction failures (currently some news sources block NOIZE's scraper)
- Enables NOIZE to actually read full articles before summarizing them — instead of generating from headlines only
- Works on some light paywalls (Bloomberg, WSJ, Axios)
- Zero cost, no API key required for basic use
- Immediate quality improvement to the Dossier feature with minimal development work

---

### 3. Firecrawl
**What it is:** A scraping service that handles JavaScript-heavy sites and some anti-bot protections that standard scrapers can't get through.

**Why it matters for NOIZE:**
- Best current option for attempting to access TikTok pages
- Can pull actual Reddit comment threads (not just post titles) for deeper audience sentiment
- Handles news sites that currently block NOIZE's article extraction
- Has a free tier (500 pages/month) to test before committing

---

## New Features Pipeline

### HIGH PRIORITY — These change what NOIZE fundamentally is

**1. "First Signal" Alert**
Detect topics trending on X that have NOT yet appeared on YouTube or Google News. Flag them separately with a timestamp. This is a creator's 24–72 hour head-start window. No other trend tool surfaces this gap specifically. This single feature shifts NOIZE's pitch from "trend dashboard" to "get there before everyone else."

**2. Deep Dossier — Real Sources, No Hallucinations**
Currently the Investigate dossier is generated from GPT's training data — which means it can hallucinate details, invent quotes, or get facts wrong. The new flow: Exa finds 10 real articles on the topic → Jina Reader extracts the full text → GPT synthesizes from actual sourced content. Result: real quotes, real data, zero invented facts, linked sources at the bottom.

**3. TikTok Data Attempt via Firecrawl**
Attempt to scrape TikTok's trending hashtag pages and Creative Center. Not guaranteed to work given TikTok's restrictions, but Firecrawl is the best tool available for this. Even partial data is a meaningful improvement over nothing.

---

### MEDIUM PRIORITY — Competitive differentiation features

**4. "Pre-Peak Alert" — Catch Trends 3 Days Early**
Most creators find a trend after it peaks. Using Exa's time-filtered search, NOIZE can find topics gaining momentum but not yet exploding. Show a "signal strength" velocity meter. The creator who acts on day 1 instead of day 4 gets all the algorithm benefit.

**5. "Who's Talking" Intelligence**
For any trending topic, show WHO is driving it on X: journalists, major creators, brands. If 10 journalists and 3 major brands are all discussing the same thing, it's 24–48 hours from going mainstream. NOIZE could estimate crossover timing based on the profile of who's talking.

**6. Hook & Angle Bank**
Pull the most-engaged X posts about any trend. Use them as raw material for the Blueprint's hook suggestions. Instead of AI-invented hooks, creators get hooks written in language the actual audience is already using and responding to.

**7. "X vs Everywhere Else" Gap Map**
Side-by-side comparison showing where a trend sits in its lifecycle across platforms. Trending on X only = early opportunity. Trending on YouTube and Google News = likely past peak. Trending on both X and YouTube = mainstream window closing. Creators can read the lifecycle at a glance.

**8. Niche Intelligence Mode**
Creator selects their niche (fitness, finance, gaming, beauty, etc.). Exa's search is then scoped to that niche specifically. A fitness creator never sees political news — only what's moving in their world. Content becomes more targeted and more useful.

**9. Sentiment Arc**
Track whether the X conversation around a topic is trending positive, negative, or turning controversial over time. Helps creators avoid jumping on trends that are about to become PR nightmares.

---

### FUTURE / GROWTH PHASE

**10. Thread Intelligence**
Long X threads are free, high-quality research that someone has already compiled. Exa finds the best threads on any topic; NOIZE summarizes them and feeds them into the Dossier.

**11. Creator DNA Scanner**
Paste any YouTube channel URL. NOIZE scrapes their top content, analyzes what hooks, formats, and topics perform best for that specific creator's audience, and generates personalized strategy — not generic advice.

**12. Paywall Intel**
Use Jina Reader to extract signals from premium publications (Bloomberg, WSJ, Axios). Premium publication coverage is a leading indicator of mainstream crossover.

**13. Real Reddit Sentiment**
Use Firecrawl to pull actual Reddit comment threads instead of just post titles. Real audience reactions fed directly into Blueprint generation.

**14. AI Video/Image Generation**
After a trend is detected, offer "Generate a TikTok-style video for this trend" using the Higgsfield API. Turns NOIZE from an intelligence tool into a production tool. Requires Higgsfield Plus ($39/month) for API access.

---

## The Biggest New Idea: NOIZE as a Media Property

### "The Daily Signal" — A NOIZE Column

NOIZE is already gathering trend data faster than any journalist can do manually. Adding one GPT call to synthesize that data into a written column makes NOIZE its own news publication.

**The concept:**
- Auto-generated every morning from all data sources
- Written in NOIZE's existing noir voice ("Chief Detective Pugson, NOIZE Intelligence Bureau")
- Each story compressed to 3–4 sentences
- Every story includes a Creator Angle — what to DO with this story, not just what happened
- Trend velocity embedded: "Moving 4x faster than normal. Window: 18 hours."
- Published before mainstream media catches up

**Why it's different from regular news:**
No news publication writes for content creators specifically. They report what happened. NOIZE tells creators what to do with it, how fast they need to move, and what angle to take. That's an entirely different product from the same information.

**The Design:**
Old-school 1940s broadsheet newspaper aesthetic. Aged cream paper texture, multi-column layout, Playfair Display serif typography, dense newsprint-style body copy. Trend velocity shown as a mechanical barometer gauge. "BREAKING" stamp in red — the only color on the page. Bylined by "Chief Detective Pugson, NOIZE Intelligence Bureau."

The contrast between cutting-edge AI trend intelligence and a 1940s newspaper design IS the brand moment. It's instantly recognizable, highly shareable, and nothing else looks like it.

**The growth path:**
- Phase 1: Column tab inside the NOIZE app (daily, auto-generated)
- Phase 2: Email newsletter — subscribers get it every morning
- Phase 3: Own URL (noize.news) — fresh daily content builds Google SEO
- Phase 4: Auto-post column headline to X every morning (distribution flywheel)
- Phase 5: Standalone media property — not just an app feature, a brand

---

## How the Engine Gets Smarter (Architecture Upgrades)

*These are under-the-hood changes that make every feature above dramatically better. Based on patterns from a separate, validated AI investigation engine called Seeker.*

### The Three-Tier Cost Rule
Right now NOIZE fires expensive AI calls for everything. The smarter approach:
- **Tier 1 — Free, always runs:** Data scrapers, database math, trend scoring. No AI cost.
- **Tier 2 — Cheap, selective:** A quick, inexpensive AI verification call before going deeper. Filters out noise.
- **Tier 3 — Expensive, rationed:** Full Dossier, Blueprint, Daily Signal generation. Only fires after Tiers 1 and 2 pass.

**The rule: prime the expensive call with cheap intelligence first.** The Dossier that has read 10 real articles before it generates will always be better than one that fires cold. And it costs less per call because it's better targeted.

### Signal Tiers — Every Trend Gets a Confidence Level
Instead of just showing trending topics, every trend gets classified:
- **Confirmed** — on 3+ independent platforms simultaneously
- **Emerging** — on 2 platforms, gaining velocity
- **Weak Signal** — one platform, early detection
- **Noise** — single mention, no movement

A trend crossing from Weak Signal to Emerging in 6 hours is more valuable than something already Confirmed everywhere. The crossing IS the alert.

### Source Credibility Ledger
Track which sources consistently surface trends first. If a specific subreddit, YouTube channel, or news outlet keeps appearing 48 hours before a trend explodes, its signals automatically carry more weight. NOIZE gets smarter every day with no manual intervention.

### The Window Calculator
Every trend card shows a timer: "Window open — estimated 18 hours." Computed from velocity math on existing data. No new infrastructure. When the window closes, the card says "Approaching saturation — act now or skip."

### The Miss Log — Show the Misses, Build Real Trust
When NOIZE flags a trend that doesn't materialize, log it publicly: "NOIZE flagged this as Emerging on Tuesday. It didn't cross over. Here's why." A tool that shows its misses earns more trust than one that hides them. The Miss Log also automatically feeds back into the Source Credibility Ledger, making the system self-correcting.

### Detection Lead Time — The Proof Metric
Track the average hours between NOIZE first flagging a trend and it appearing in mainstream Google News or YouTube Trending. Publish that number in the app. *"NOIZE detected this 31 hours before mainstream coverage."* This is the metric that proves the product's value — not claimed, demonstrated, with receipts.

---

## Competitive Context

**Higgsfield Supercomputer** — heavily marketed as an AI that "watches TikTok in real time." Research showed they face the same TikTok data restrictions as everyone else. Their TikTok capability comes from the public Ad Library + web crawling. Their platform ($39–$99/month) is designed for ad creative production, not trend intelligence. Their video generation API is worth using for feature #14 above, but they are not a threat to NOIZE's core intelligence layer.

**Traditional trend tools** (SparkToro, TrendTok, Exploding Topics) — show what's already trending. None of them have the creator-specific angle, the content blueprint output, or the "get there first" early detection that NOIZE is building toward.

**The gap NOIZE is filling:** No tool currently gives content creators both the early signal AND the ready-to-execute strategy AND the timing intelligence. That combination is NOIZE's moat.

---

## Summary: What Changes, What Stays

| What Stays | What Gets Upgraded |
|---|---|
| The noir detective brand and Pugson voice | Dossier becomes real-sourced, not hallucinated |
| Streamlit / Python stack | Exa replaces/supplements Google News RSS |
| SQLite for velocity tracking | X data added via Exa (no API cost) |
| Railway deployment | TikTok attempted via Firecrawl |
| Strange Signals feature | Blueprint becomes multi-lens, smarter |
| The core Investigate flow | Trend cards get Signal Tiers and Window timers |
| | The Daily Signal column added |
| | Detection Lead Time published as proof metric |

---

*Document compiled from research session — June 2026*
*All features and architecture patterns documented in CLAUDE.md for development reference*

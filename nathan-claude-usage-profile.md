# Nathan Veer — Comprehensive Claude Usage Profile

> **Purpose:** Reference document for future Claude sessions. Describes how Nathan uses Claude across professional and personal domains, what's been built, what's integrated, and how it all fits together.
>
> **Last compiled:** 2026-05-06
> **Source:** `~/Library/Mobile Documents/com~apple~CloudDocs/Claude/` — full workspace scan

---

## A. Identity & Setup

| Field | Value |
|-------|-------|
| **Name** | Nathan Veer |
| **Role** | Sales Engineer, Americas SE Team, Brightcove (acquired by Bending Spoons, Feb 2025) |
| **Work email** | nveer@brightcove.com |
| **Personal email** | veer.nathan@gmail.com |
| **Timezone** | America/Chicago (Central Time) — all outputs display CT |
| **Gong User ID** | `7899388448181301224` |
| **Devices** | Mac Studio (home/personal MAX account), Laptop (work/enterprise account) |
| **Core skill** | Making complex things simple |
| **Weekly cadence** | 16+ customer calls/week across enterprise, mid-market, and SMB tiers |
| **Church** | Gathering House |
| **Spouse** | Lisa (Lisa Michelle Veer) |

### Voice & Style Rules (VOICE.md)

Nathan has codified his communication style into five rules that apply to every output Claude produces:

1. **Lead with the answer** — no preamble, no "Great question!", no "Just wanted to circle back." Result first, context second.
2. **Bullets over paragraphs** — structure by default. Prose only when format *is* the message.
3. **Direct, warm, never hedged** — disagreement is fine; say it plainly. No "I think maybe we could perhaps."
4. **Compress ruthlessly** — every sentence earns its place. Cut hollow closings, restated context, undefined acronyms.
5. **No emoji** — Nathan strips emoji from drafts. Never decorate.

**Channel-specific shapes:**
- **Email:** Two-line opener naming the ask → bulleted body → one-line close with next action
- **Slack:** One-sentence lead-in → bulleted body → closing CTA on its own line (not a bullet)
- **Customer-facing writing:** Plain English first, technical depth second
- **Internal product feedback:** Customer name + behavior + business impact + what should change
- **Church (Gathering House):** Warmth dial up, brevity stays. Encouraging, community-focused, plain English. Name the person and the moment.

### Working Preferences

- **Always use multiple agents in parallel** — non-negotiable default (3–6 per batch)
- **Do, don't tell** — try to do something before describing it
- **Draft reviews** — always save email/Slack drafts to reviewable `.md` or `.docx` files; never describe-only
- **Multi-draft sessions** — when 2+ drafts ready, create `draft-review-YYYY-MM-DD.md` with all side by side
- **Auto-research open questions** — never leave a researchable question unanswered; check support.brightcove.com first
- **Save everything to files** — chat doesn't persist between tasks

---

## B. Workspace Architecture

Nathan's Claude workspace lives in iCloud at `~/Library/Mobile Documents/com~apple~CloudDocs/Claude/` and is organized as a hierarchical system with routing logic:

```
Claude/                          ← root (iCloud-synced)
├── CLAUDE.md                    ← global rules (206 lines, 29 rules in SE workspace)
├── MEMORY.md                    ← workspace facts, read on entry
├── VOICE.md                     ← Nathan's tone (5 rules + channel shapes)
├── PROFESSIONAL/
│   ├── SE_Workspace/            ← primary SE work area (own CLAUDE.md + MEMORY.md)
│   │   ├── context/             ← accounts, SE team IDs, BigQuery reference, Slack channels
│   │   ├── commands/            ← slash command definitions
│   │   ├── reference/           ← competitive intel, battlecards (11+ files)
│   │   ├── skills/              ← publish-report
│   │   ├── scripts/             ← API integration scripts, Slack mark-read MCP
│   │   ├── outputs/             ← generated reports by type
│   │   ├── plans/               ← scaling plan, implementation plans
│   │   ├── Gong/                ← Gong feature-request tooling + Gong Skill
│   │   ├── brightcove-drive-migration/ ← Drive migration plugin
│   │   └── .claude/skills/      ← morning-call-schedule, call-companion, session-log
│   ├── Brightcove_Research/     ← ad-hoc research artifacts
│   └── plugin-build/            ← GOOSE plugin source (distribution template)
│       └── se-command-center/   ← git-tracked, versioned plugin
├── PERSONAL/
│   ├── home-assistant/          ← HA automation (own CLAUDE.md + MEMORY.md)
│   ├── gathering-house/         ← Church/worship/Sunday Keys (own CLAUDE.md + MEMORY.md)
│   ├── YNAB/                    ← Budget automation (Python toolkit)
│   ├── Limitless/               ← OMI wearable + lifelog export + plugin
│   ├── Investments/             ← Ratior (precious metals) + Coinbase (crypto)
│   └── Unifi/                   ← Network discovery + automation
└── _archive/                    ← stale/legacy (home-assistant-stale, SE_Workspace-stale, etc.)
```

**Routing logic:** Each subfolder has its own `CLAUDE.md` that wins on conflict within its domain. Root `CLAUDE.md` provides global rules. On task start, Claude reads the relevant subfolder `CLAUDE.md` + `MEMORY.md` based on what the task is about.

---

## C. Professional Workflows — SE Command Center

The SE Command Center is Nathan's operational hub. It has 12+ slash commands, 29 codified rules, and integrates with 10+ data sources.

### C.1 Commands (Slash Workflows)

| Command | Purpose | Key Details |
|---------|---------|-------------|
| `/prime` | Session startup | Reads all context files, confirms understanding, runs disk cleanup, checks first-run state |
| `/daily_prep` | Morning call prep | Dark-theme HTML timeline with enriched meeting cards; color-coded by type (blue=customer, gray=internal, yellow=hold, red=escalation, purple=work block, green=new-opp, violet=demo) |
| `/morning_schedule` | Daily 7am briefing | Loads Google Calendar, classifies customer vs internal, preps call companion state file |
| `/call_prep [customer]` | Pre-call briefing | Parallel agents hit Gmail, Gong/BigQuery, Salesforce/BigQuery, Notion, Calendar; generates HTML with email intel, Gong summary, Salesforce snapshot, action items |
| `/call_companion` | Live call resource assistant | Monitors Granola during calls; detects resource requests (docs, follow-ups, examples, competitor questions); researches Brightcove docs in parallel; creates Notion follow-up page with copy-paste email snippets |
| `/call_debrief [customer]` | Post-call outcomes | Action items, account context updates, follow-up page creation |
| `/email_triage` | Inbox triage & drafting | Categorizes emails, drafts responses, creates review file; conservative archive rules with 3-criteria safety check |
| `/slack_triage` | Slack inbox triage | 4 parallel scanner agents (DMs, @mentions, Tier 1 channels, thread replies); urgency scoring; priority contacts flagging; draft responses in summary file |
| `/account_summary [customer]` | Full account overview | History, health, recommendations from BigQuery + Notion + Gong |
| `/competitor_analysis [competitor]` | Competitive research | Web search, Gong mentions, doc comparison; battlecards for JW Player, Vimeo OTT, Disney Brand Life, Kaltura |
| `/task_triage` | Todoist work tasks | Pull tasks, auto-close done items, run autonomous research, queue drafts for approval |
| `/create_plan` / `/implement` | Workspace changes | Plan and execute workspace modifications |
| `/migrate-history` | One-time migration | Legacy Call Follow-Ups → Active Customers DB |

### C.2 The 29 Rules (SE Workspace CLAUDE.md)

Nathan has codified 29 hard rules from real mistakes and edge cases. Key highlights:

- **Rule 0a:** Never create Notion hub pages or duplicate DBs (ghost databases discovered 2026-03-05)
- **Rule 2:** Filter Gong transcripts by SE emails on joined task table, NOT by owner_id
- **Rule 4:** support.brightcove.com = source of truth for all product questions
- **Rule 10:** Auto-research open questions — embed `✅ Researched Answer` inline
- **Rule 11:** Real-time schedule check before any call — search Gmail last 24h first (caught a Farm Journal reschedule)
- **Rule 12a:** Account owner notification callout block on every follow-up page
- **Rule 15a:** Reply-to-all mandatory — BLOCK send if threadId or inReplyTo is missing
- **Rule 15d:** Check entitlements (BigQuery) before drafting emails implying feature availability
- **Rule 18:** All call prep = HTML files, never .md or .docx — dark theme, card-based layout
- **Rule 22:** Multi-source verification mandatory — every claim traceable to a verified tool call (exists after hallucinated FamilyLife churn alert, 2026-03-02)
- **Rule 23:** Brightcove Gateway disconnection protocol — stop and notify, never silently skip
- **Rule 24:** Salesforce domain = `brightcove2.lightning.force.com` (not `brightcove`)
- **Rule 29:** Never create Google Drive files — all outputs to workspace as .md or .html

### C.3 Context Files

| File | Contents |
|------|----------|
| `context/about_me.md` | Nathan's role, strengths, weekly workflow (16+ calls/week), technical background |
| `context/se_team.md` | 5 current SEs + 4 former SEs with Gong User IDs for filtering |
| `context/current_accounts.md` | 10+ active accounts with tier, cadence, AE, competitors, status, Notion links |
| `context/slack_channels.md` | Tiered Slack channels (Tier 1: always scan, Tier 2: @mentions only, Tier 3: watch list), priority DM contacts with 🔴/🟡 flags |
| `context/bigquery_reference.md` | Full SQL guide for Brightcove Gateway — verified schemas, join patterns, templates |

### C.4 Active Accounts (as of Feb 2026)

- **Enterprise:** MLS (~$370K), YesTV/Applicaster (weekly NGL migration), Wonder Project (HDR10 escalation)
- **Mid-Market:** Lifeway (monthly, Beacon→Applicaster migration), Jukin/TMB (JW Player consolidation), Harvest (biweekly, Live 2.0), Littelfuse (re-engagement after 2+ yr gap)
- **SMB:** What's Next Media/PYMNTS (cloud playout), Major League Fishing (AI Suite, international expansion), Watchguard (new prospect)
- **Key situations:** Wonder Project escalated to exec level; YesTV renewal end of March; MLS Bending Spoons concerns; FamilyLife NOT renewing (handled graciously)

### C.5 Reference / Competitive Intelligence

11+ battlecard and analysis files in `reference/`:
- JW Player (Connatix) battlecard
- Vimeo OTT battlecard + APAC analysis
- Disney Brand Life battlecard
- Kaltura replacement notes
- Vimeo/Qumu deep dive
- Brightcove vs JW vs Ooyala
- Competitors Notion overview
- Gmail MCP setup guide
- Why Choose Brightcove
- Gong competitive analysis

**Live competitive intel:** https://bcov-competitive-intel-hub.lovable.app/# (Salesforce win/loss data, Jan 2022–present, 14 competitors)
**Live roadmap:** https://brightcove-briefing.lovable.app/initiatives

---

## D. Plugins & Skills Built

### D.1 GOOSE — AI Sales Co-Pilot (The Big One)

**What it is:** A Claude Desktop plugin that transforms Claude into a full-stack sales assistant for Brightcove reps. Originally built as "SE Command Center" for Nathan's personal use, now being scaled as "Brightcove Sales Co-Pilot" for 50–100 reps.

**Distribution status:**
- v1.0: Personal SE workspace (Nathan only)
- v2.0: BigQuery replaces direct Salesforce API; local with beta testers
- v3.0: Multi-user Sales Co-Pilot — restructured for non-technical reps
- Published to GitHub: `nveer/brightcove-se-command-center` (renaming to `brightcove-sales-co-pilot`)
- #goose-beta-test Slack channel for beta support
- Scaling plan: 5-phase rollout over 6–8 weeks (Pilot → Team → Full)

**Plugin contents:**
- 7+ command files (call_prep, call_companion, call_debrief, daily_prep, email_triage, account_summary, competitor_analysis, onboarding, prime, migrate_history)
- Skills: Gong API, Salesforce (deprecated → BigQuery), SE-necessity scoring
- Context templates for multi-user personalization
- BigQuery reference for Brightcove Gateway
- Notion output configuration
- SessionStart hook triggers automatic onboarding

**Onboarding flow (5 steps):**
1. Collect user info (name, role, team, focus)
2. Verify Google connections (Gmail, Calendar, Drive)
3. Auto-setup Gmail write access
4. Connect to shared Active Customers Notion database
5. Verify setup completion

**Scaling plan highlights:**
- Ship v3.0 without Gong (blocked on Gateway team adding Gong to BigQuery)
- Default to post-call mode (works out of box); real-time via Granola is optional upgrade
- Templates instead of code generation for non-technical reps
- Pilot (5–10 reps) → Team (20–30) → Full (50–100)
- Success metric: 70%+ adoption with at least one command per week

### D.2 Brightcove Brand Skill

Installed Cowork plugin for auditing content against Brightcove brand guidelines. Used for writing copy, creating emails, drafting presentations, checking brand voice/colors/tone.

### D.3 OTT Partner Recommender

Custom skill that recommends the best OTT app partner (Vimeo OTT, Applicaster, Accedo/Leyra, AppsFactory, Enveu) for a Brightcove sales opportunity. Matches customer technical/commercial requirements to the right partner.

### D.4 Todoist Integration

Skill for Todoist task management — add tasks from calls, pull tasks, close tasks, extract action items from meetings.

### D.5 Gong Feature Request Extractor

A 5-stage pipeline that:
1. Pulls Gong calls via API (batched by month)
2. Smart-filters transcripts for customer asks + SE gap confirmations (regex detection)
3. AI classifies each finding (parallel subagents, ~60% → 95%+ precision)
4. Deduplicates and consolidates by problem group (target: 5–15 groups per quarter)
5. Pushes consolidated results to Notion database

Uses Notion DB `ff528d35-49d5-4882-85d6-5b55537687ba` for output.

### D.6 Brightcove Drive Migration Plugin

Helps sales reps migrate customer files from personal Google Drive folders to centralized sales bucket. Automatically matches accounts, previews plan, executes moves. Designed for org-wide deployment.

### D.7 Publish Report Skill

End-to-end HTML report publishing pipeline: Claude writes file → iCloud SE_Workspace → git push → Cloudflare Pages deploys. Live URL: `https://reports-aoy.pages.dev/[filename].html`. Repo: `nveer/Reports` on GitHub.

### D.8 SE Necessity Scoring

Evaluates each customer call on today's calendar and rates SE necessity:
- 🔴 Skip — no SE needed
- 🟡 Review — check before committing
- 🟢 Attend — SE presence warranted

Uses 4-criteria engagement model with configurable AE-specific weighting.

---

## E. Integrations Map

| Integration | Type | Purpose | Key Details |
|-------------|------|---------|-------------|
| **Brightcove Gateway (BigQuery)** | MCP | Account data, contracts, usage, Gong transcripts | Project: `brightcove-lumenx-42`, Dataset: `external_shared_views`. 6 table categories. |
| **Gmail** | MCP | Customer communication, inbox triage, draft/send | Primary tool. Threading rules, reply-to-all mandatory, auto-archive. |
| **Google Calendar** | MCP | Schedule parsing, call prep, morning briefing | Read-only. Customer vs internal classification by attendee domains. |
| **Notion** | MCP | Account management, call follow-ups, feature request DB | Active Customers DB (primary), Customer Call Prep DB, deprecated Call Follow-Ups DB. |
| **Gong API** | Bash scripts | Pull call transcripts, search calls, feature request extraction | Direct API via `gong_api.py`; also via BigQuery (v_raw_salesforce_transcript). Filter by SE user IDs. |
| **Granola** | MCP | Live call transcription | Powers call-companion real-time mode during active customer calls. |
| **Slack** | MCP | Team communication, triage, product feedback | Tiered channel scanning, priority DM contacts, #goose-beta-test support. |
| **Jira / Atlassian** | MCP | Issue tracking, Confluence | Connected connector. |
| **Google Drive** | MCP | Read contracts, decks, reference docs | Read-only. Rule 29: never CREATE files in Drive. |
| **Home Assistant** | REST API (curl) | Home automation control | Nabu Casa remote URL, long-lived token (expires 2036), Bash + curl pattern. |
| **Coinbase** | Custom MCP | Crypto portfolio monitoring | Custom `coinbase_mcp.py` server via Advanced Trade API. Read-only (View permissions). |
| **YNAB** | Python scripts | Budget analysis, transaction management | Custom toolkit: analysis, transactions, trends, reports. Standard library only. |
| **Todoist** | MCP/Skill | Task management | Cowork plugin for task CRUD, call action item extraction. |
| **Cloudflare Pages** | Git pipeline | Report hosting | `nveer/Reports` repo → auto-deploy on push to main → `reports-aoy.pages.dev`. |

---

## F. Automations & Scheduled Tasks

### F.1 Professional Automations (Configured via Cowork Scheduled Tasks)

| Automation | Schedule | What It Does |
|------------|----------|-------------|
| **Daily Email Triage** | 7:30 AM CT | Scans inbox, categorizes emails, drafts responses, creates review file |
| **Daily Call Prep** | 6:00 AM CT | Generates dark-theme HTML timeline with enriched meeting cards for all customer calls |
| **Morning Schedule** | ~7:00 AM CT | Loads calendar, classifies events, preps call companion state |
| **Midday Monitor** | Hourly | Checks for schedule changes, new urgent items, call companion triggers |
| **Post-Call Debrief** | Every 15 min (safety net) | Detects completed customer calls, triggers debrief if not already done |
| **Call Companion** | During active customer calls | Monitors Granola transcript, researches resources in real-time, builds Notion follow-up |

### F.2 Home Assistant Automations (45 total, Raspberry Pi)

Nathan runs 45 unique automations on a Raspberry Pi (HA Core 2026.2.1, HA OS 17.0) managing 2,842 entities including 39 lights, 8 cameras, 1 garage door, 1 front door lock, and 2 persons.

**Key automations include:**
- Occupancy-based lighting (living room, kitchen, master bedroom, office, laundry, garage, entry)
- Master Bathroom Lights with humidity condition (< 65 threshold, learned from Zigbee sensor lag)
- Master Bedroom dual-sensor cross-check (both sensors must be OFF before lights off)
- Driveway lights at sunset/sunrise
- Plant watering notifications
- Goodnight scene (Apple TV integration)
- CO2-triggered fan control
- Garage deep freeze / fridge temperature monitoring (YoLink sensors)
- Shark robot vacuum scheduling

**Hard-won fixes (do NOT revert):**
- Daily restart uses `homeassistant.restart`, NOT `hassio.host_reboot`
- Humidity automation no longer calls `automation.turn_off` on bathroom lights (race condition)
- Master Bathroom Lights has built-in `humidity < 65` condition
- Master Bedroom: both motion sensors must be OFF before lights turn off

**Known disabled automations (intentional):**
- Garage door auto-open (safety concern)
- Nathan's Night Off routine
- Modem Power Cycle
- Master Bedroom Ceiling Fan auto-off

**6 Lovelace Dashboards:**
1. Home Overview — scenes, living room lights, security, who's home
2. Living Room — deep control, TV/media, air purifier
3. Security — cameras, entry, presence
4. Office — desk lights, CO2, scenes
5. Systems — plant sensors, energy, automation health, restart tools
6. Lisa's Lights — Lisa-specific light controls

---

## G. Personal Projects

### G.1 Home Assistant (Deep)

- **Hardware:** Raspberry Pi, HA OS 17.0, Core 2026.2.1
- **Network:** Local IP 192.168.110.31, Remote via Nabu Casa
- **Access pattern:** Bash + curl (REST API), NOT an MCP server
- **Token:** Long-lived JWT, expires 2036, stored in `CONNECTION.md`
- **Session workflow:** Type "prime" → Claude reads README + CONNECTION + last 3 session notes → hits live API → reports status
- **SOPs documented:** troubleshoot-automation, add-new-automation, dashboard-update
- **Diagnostic history:** Multiple diagnosis reports (duplicate automation IDs, rogue `automation.turn_off` calls, state persistence bugs)
- **Config backups:** Pre/post fix snapshots of automations.yaml
- **Session notes:** Detailed per-session logs (presence sensor fix, automation troubleshoot, master bedroom sensors, stand light + CO2 fan, goodnight scene, office lights stuck on, etc.)
- **Zigbee mesh:** Humidity sensors, occupancy sensors, light bulbs (Hue LCA017 full color in hallway)
- **Key entities:** Stand light (most-toggled), Big Light (office overhead switch), Shark vacuum, weather forecast, garage freeze/fridge sensors

### G.2 YNAB Budget Toolkit

Full Python toolkit for budget analysis via YNAB API:
- **Analysis:** Budget overview, category deep dive, overspent check
- **Transactions:** Recent transactions, search (payee/memo/amount/date), add transaction
- **Trends:** Monthly income vs spending + savings rate, top payees, category trends
- **Reports:** HTML spending report with category breakdown, CSV export
- **Stack:** Python standard library only, no external packages. API rate limit: 200 req/hr.

### G.3 Investments

**Ratior (Precious Metals):**
- Joint account with Lisa (M-0257873)
- Gold/Silver Ratio strategy: >40:1 = buy silver, <40:1 = buy gold
- Purchase price: €2.3854/g silver (Feb 2026), current: €2.5515/g
- Tax-free date: Feb 3, 2027 (12-month holding period)
- Interactive `dashboard.html` with portfolio value + ratio history charts
- Portal: https://my.ratior.ag

**Coinbase (Crypto):**
- Custom MCP server (`coinbase_mcp.py`) for Claude Desktop integration
- Advanced Trade API, read-only (View permissions)
- Tools: get accounts, portfolio summary, spot prices, order history, list products

### G.4 Gathering House (Church)

- Sunday Keys / worship planning
- Service order, song lists, key sheets
- Team communication drafts (volunteers, leads)
- Node.js project in `Worship Planning/` folder
- Tone rule: warmth dial up, brevity stays same
- Separate voice from SE work — encouraging, community-focused, no corporate jargon

### G.5 Limitless (OMI Wearable)

- OMI wearable device + lifelog export
- Obsidian vault integration (daily template, conversation template)
- Custom Claude system prompt for OMI
- Custom MCP server (`limitless_mcp/`)
- Plugin with `/lifelogs` command and limitless skill

### G.6 Unifi

- Network discovery and automation (referenced in workspace map, details sparse)

### G.7 3D Prints

- Lives OUTSIDE Claude workspace at `~/Documents/3D-Prints/`
- Includes AV/stage builds for church, monitor arm parts, hardware projects

---

## H. Infrastructure & Meta-Engineering

### H.1 CLAUDE.md Optimization

Nathan has built a sophisticated multi-level CLAUDE.md system:
- **Root CLAUDE.md** (206 lines): Global rules, routing map, integration list, parallel agents strategy, MCP preferences, file retention policy
- **SE_Workspace CLAUDE.md** (233 lines): 29 codified rules, BigQuery reference, Notion databases, command registry, working conventions
- **Home Assistant CLAUDE.md**: Priming sequence, REST API patterns, entity reference, process rules, common tasks
- **Gathering House CLAUDE.md**: Voice adjustment, scope boundaries
- **MEMORY.md files** at each level: Durable facts, hard-won fixes, working agreements
- **VOICE.md**: Codified tone rules applied to all outputs

### H.2 Token & Context Management

- File retention policy: auto-cleanup at `/prime` (keep last 3 days of call prep HTML, email triage, draft reviews)
- Cowork VM disk limit: ~1–2GB
- Output size cap: ~500KB per file; summarize transcripts, don't dump
- No zip backups in iCloud-synced directory
- Schema cache (`bigquery_schema_cache.md`) eliminates round-trips
- Gong transcript files saved to /tmp to avoid shell argument-length limits

### H.3 Publishing Pipeline

- **GitHub Pages/Cloudflare:** `nveer/Reports` repo → Cloudflare Pages auto-deploy → `reports-aoy.pages.dev`
- One terminal command to publish: cp + git add + commit + push (Claude provides the exact command)
- Verification via WebFetch after deploy

### H.4 Plugin Build System

- Git-tracked plugin at `plugin-build/se-command-center/`
- `.plugin` archive format for Claude Desktop distribution
- CHANGELOG.md for tracking pending changes
- Distribution template treated as read-only — modifications happen in working copy

### H.5 Competitive Intelligence Platforms

- **Competitive Intel Hub:** https://bcov-competitive-intel-hub.lovable.app/# — live Salesforce win/loss (Jan 2022–present, 14 competitors)
- **Product Briefing / Roadmap:** https://brightcove-briefing.lovable.app/initiatives — real-time roadmap

---

## I. Key Accounts & Team

### SE Team (Current)

| Name | Gong ID | Email |
|------|---------|-------|
| Nathan Veer (PRIMARY) | 7899388448181301224 | nveer@brightcove.com |
| Carl Rutman | 8899814756055145201 | crutman@brightcove.com |
| Mike Smith | 6045889534289259170 | mksmith@brightcove.com |
| Josef Nguyen | 2588855042808875732 | jnguyen@brightcove.com |
| Tasha Harwood | 3920090429787644145 | tharwood@brightcove.com |

### Key Internal Stakeholders (Slack Priority)

| Name | Role | Priority |
|------|------|----------|
| Phil Green | VP Sales, Media (Nathan's boss) | 🔴 Always flag |
| Erin Cullen | SVP Sales, Enterprise | 🔴 Always flag |
| Filippo Maria De Salazar | Bending Spoons (Goose collaborator) | 🟡 Action needed |
| Morgan Drake | Customer Success Director | 🟡 Action needed |
| David Fernandez Tejedor | Sales @ Brightcove/BS | 🟡 Action needed |
| Ann-Margaret Belke | Sr. Account Management Director | 🟡 Action needed |

---

## J. Lessons Learned & Hard-Won Rules

These rules exist because something went wrong:

| Rule | Incident | Date |
|------|----------|------|
| Rule 22 (multi-source verification) | Hallucinated FamilyLife churn alert | 2026-03-02 |
| Rule 0a (no duplicate Notion DBs) | Ghost databases + orphaned pages | 2026-03-05 |
| Rule 11 (real-time schedule check) | Farm Journal reschedule not caught | Pre-March 2026 |
| Rule 24 (Salesforce domain) | Old `brightcove` domain redirects/fails | Pre-March 2026 |
| HA: no `automation.turn_off` in automations | Race condition in bathroom humidity | Feb 2026 |
| HA: `homeassistant.restart` not `hassio.host_reboot` | Pi killed instead of graceful restart | Feb 2026 |
| HA: duplicate automation IDs | State machine unpredictability during restarts | Feb 2026 |
| Rule 29 (no Google Drive files) | Outputs lost/misplaced | April 2026 |
| Gong join pattern | `t.task_id_c = tk.id` NOT `t.id = tk.id` | Verified 2026-03-03 |

---

## K. The Big Picture — What Claude Means to Nathan

Nathan is arguably one of the most sophisticated Claude power users in a sales engineering context. His setup represents:

1. **A full-stack sales automation platform** — from morning email triage through live call companion to post-call debrief and account intelligence, Claude handles the entire SE workflow.

2. **A home automation brain** — 45 automations, 2,842 entities, REST API control, diagnostic scripts, and session-noted troubleshooting history all managed through Claude.

3. **A financial monitoring system** — YNAB budget analysis, Ratior precious metals strategy, Coinbase portfolio monitoring.

4. **A community service tool** — church worship planning, volunteer communications, separate voice and tone for community context.

5. **A product he built and ships** — the GOOSE plugin (SE Command Center → Sales Co-Pilot) is distributed to 50+ reps with a formal scaling plan, onboarding flow, and beta testing channel.

6. **A living documentation system** — every mistake becomes a rule, every rule has a source, every workspace has its own CLAUDE.md, and the whole system is version-controlled and iCloud-synced.

**Pre/post Bending Spoons acquisition context:** Brightcove was acquired by Bending Spoons in February 2025. Nathan's Claude infrastructure became even more critical as the organization navigated transition — providing continuity, productivity, and institutional knowledge during a period of change. The GOOSE plugin in particular represents Nathan's contribution to making the sales team more effective at scale during this transition.

---

## L. File Index

### Root
- `CLAUDE.md` — Global rules (206 lines)
- `MEMORY.md` — Workspace facts (31 lines)
- `VOICE.md` — Tone rules (56 lines)

### PROFESSIONAL/SE_Workspace/
- `CLAUDE.md` — SE Command Center rules (233 lines, 29 rules)
- `MEMORY.md` — SE workspace facts (40 lines)
- `CHANGELOG.md` — Pending changes log
- `context/about_me.md` — Nathan's role profile
- `context/se_team.md` — SE team Gong IDs
- `context/current_accounts.md` — Active account details
- `context/slack_channels.md` — Slack triage configuration
- `commands/create_plan.md`, `implement.md`, `slack_triage.md` — Command definitions
- `skills/publish-report/SKILL.md` — Cloudflare publishing
- `.claude/skills/morning-call-schedule/SKILL.md` — Morning briefing
- `.claude/skills/call-companion/SKILL.md` — Live call assistant (298 lines)
- `Gong/Gong Skill/SKILL.md` — Gong API skill
- `Gong/gong-feature-requests-skill/SKILL.md` — Feature request pipeline
- `brightcove-drive-migration/README.md` — Drive migration plugin
- `plans/sales-co-pilot-scaling-plan.md` — v3.0 scaling plan (769 lines)
- `reference/` — 11+ battlecards and competitive analysis files

### PROFESSIONAL/plugin-build/se-command-center/
- `README.md` — GOOSE plugin overview
- `INSTALL.md` — Installation instructions
- `commands/onboarding.md` — 5-step onboarding workflow
- `skills/salesforce/SKILL.md` — Deprecated (→ BigQuery)
- `skills/gong/SKILL.md` — Gong API access
- `context/bigquery_reference.md` — BigQuery SQL guide
- `context/output_config.md` — Notion output configuration

### PERSONAL/home-assistant/
- `CLAUDE.md` — HA workspace rules (comprehensive, with API patterns)
- `MEMORY.md` — HA facts and hard-won fixes
- `README.md` — Quick start guide
- `CONNECTION.md` — API credentials (token valid until 2036)
- `processes/` — troubleshoot-automation, add-new-automation, dashboard-update
- `diagnostics/` — ha_diagnosis_report, ha_diagnosis_report_v2, ha_final_diagnosis
- `session-notes/` — Per-session logs (10+ sessions documented, Feb–Mar 2026)
- `dashboards/` — 6 Lovelace dashboard YAMLs
- `config-backups/` — automations.yaml snapshots
- `scripts/` — ha_diagnose.sh, ha_diagnose_v2.sh

### PERSONAL/gathering-house/
- `CLAUDE.md` — Church workspace rules
- `MEMORY.md` — Church workspace facts
- `Worship Planning/` — Node.js project with dependencies

### PERSONAL/YNAB/
- `README.md` — Full Python toolkit documentation
- `processes/` — monthly-review, add-transaction, search-transactions

### PERSONAL/Investments/
- `Ratior/README.md` — Precious metals strategy, dashboard, portfolio tracking
- `Ratior/knowledge-base.md` — Full account reference
- `Coinbase/README.md` — Custom MCP server setup

### PERSONAL/Limitless/
- `README.md` — (minimal)
- `docs/omi-setup-guide.md` — OMI wearable setup
- `obsidian-vault/` — Daily and conversation templates
- `prompts/claude-system-prompt.md` — Custom system prompt
- `limitless_mcp/README.md` — Custom MCP server
- `plugin/` — Commands (lifelogs) and skills (limitless)
- `processes/` — omi-setup, mcp-server-setup
- `MERGE_REPORT.md` — Merge documentation

### _archive/
- `home-assistant-stale/` — Archived HA configs
- `SE_Workspace-stale/` — Archived SE workspace
- `WORKSPACE_ORGANIZATION_PLAN.md` — Original reorg plan
- `MANUAL_CLEANUP.md` — Cleanup instructions
- `Dashboard.md` — Legacy dashboard
- `Testing Plugin/` — Plugin troubleshooting notes
- `SESSIONS.md` — Stale session log
- `AI-Healthcheck/` — Health reports
- `Projects/` — Legacy projects (NewsDay)
- `sub-claude-backups/` — Backup CLAUDE.md files

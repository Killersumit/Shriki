# ⚡ SHRINKR — Master Company Blueprint
### Premium URL Monetization Platform · v2.0 · 2026

> *"We are not building a link shortener. We are building a revenue engine disguised as infrastructure."*

---

## TABLE OF CONTENTS

1. [Company Vision & Identity](#1-company-vision--identity)
2. [Market Intelligence](#2-market-intelligence)
3. [Competitive Moat](#3-competitive-moat)
4. [Design System — "Ethereal Glass"](#4-design-system--ethereal-glass)
5. [Technical Architecture](#5-technical-architecture)
6. [Database Architecture (Supabase)](#6-database-architecture-supabase)
7. [Security & Fraud Prevention Layer](#7-security--fraud-prevention-layer)
8. [Application Architecture & Routing Matrix](#8-application-architecture--routing-matrix)
9. [Development Phases & Execution Roadmap](#9-development-phases--execution-roadmap)
10. [Business Model & Revenue Streams](#10-business-model--revenue-streams)
11. [Go-To-Market Strategy](#11-go-to-market-strategy)
12. [Infrastructure & DevOps](#12-infrastructure--devops)
13. [Legal, Compliance & Risk Management](#13-legal-compliance--risk-management)
14. [KPIs & Success Metrics](#14-kpis--success-metrics)
15. [Appendix: Naming, Decisions Log & Open Questions](#15-appendix-naming-decisions-log--open-questions)

---

## 1. COMPANY VISION & IDENTITY

### 1.1 The One-Line Pitch
> A self-hosted, white-label URL monetization platform that turns every click into a revenue event — built for the next generation of digital publishers and indie operators.

### 1.2 Mission Statement
Democratize link monetization. Give individual creators, small publishers, and entrepreneurs access to the same revenue infrastructure that was previously only available to funded ad-tech companies.

### 1.3 Brand Values
| Pillar | Meaning |
|---|---|
| **Precision** | Every data point tracked, every payout calculated to the sub-cent. |
| **Transparency** | Members see exactly how earnings are derived. No hidden skimming. |
| **Performance** | Sub-100ms redirect. Sub-second dashboard. Zero compromise. |
| **Trust** | Anti-fraud by design. Clean traffic = premium CPM rates. |

### 1.4 Naming Convention (Working Title: SHRINKR)
- **Domain strategy:** Acquire a short `.io` or `.co` domain. Ideal formats: `shrinkr.io`, `lnkpay.io`, `clickpay.co`
- **Brand tone:** Technical-confident. Never cute. Never corporate. Adjacent to Linear, Resend, Clerk.

---

## 2. MARKET INTELLIGENCE

### 2.1 Problem Space
Legacy PHP platforms (Adlinkfly, GPLinks, ShrinkMe source forks) dominate the self-hosted monetized shortener niche. They suffer from:
- **2000s-era UI/UX** — zero design investment, desktop-only, no mobile consideration
- **Zero fraud protection** — click farms can game payouts trivially
- **No real analytics** — basic click counts, nothing actionable
- **Brittle hosting** — tied to cPanel/shared hosting, can't scale
- **No white-label flexibility** — operators can't brand their platform

### 2.2 Target Operator Segments
| Segment | Profile | Willingness to Pay |
|---|---|---|
| **Indie Publisher** | Runs 1–3 niche blogs, monetizes via shortened content links | Low–Medium |
| **Digital Reseller** | Buys our platform license, operates their own shortener brand | High |
| **Micro-Network Operator** | Runs 100–10,000 publisher accounts, needs admin control | Very High |
| **Affiliate Marketer** | Needs clean tracking + payout to sub-affiliates | Medium |

### 2.3 CPM Rate Reality Check (2026 Benchmarks)
| Traffic Tier | Countries | CPM Range |
|---|---|---|
| **Tier 1** | US, UK, CA, AU | $5 – $15 |
| **Tier 2** | EU, JP, SG | $2 – $5 |
| **Tier 3** | IN, PH, NG | $0.50 – $2 |

*Operator margin: typically 30–50% of ad network CPM is passed to members. The platform retains the remainder.*

---

## 3. COMPETITIVE MOAT

### 3.1 Feature Differentiation Matrix
| Feature | Adlinkfly PHP | Shorte.st | **SHRINKR** |
|---|---|---|---|
| Modern React SPA | ❌ | ❌ | ✅ |
| Mobile-first dashboard | ❌ | Partial | ✅ |
| Real-time fraud detection | ❌ | Basic | ✅ |
| Self-hosted / white-label | ✅ | ❌ | ✅ |
| Serverless / auto-scaling | ❌ | Unknown | ✅ |
| Device fingerprinting | ❌ | ❌ | ✅ |
| Behavioral analytics | ❌ | ❌ | ✅ (Phase 3) |
| Multi-domain support | Partial | ❌ | ✅ |
| Public API | Basic | ✅ | ✅ |
| CPM by country config | ✅ | ❌ | ✅ |

### 3.2 Strategic Moat Summary
1. **Design premium** — operators can charge more because the UX inspires trust in end users
2. **Fraud firewall** — cleaner traffic = better ad rates = higher member CPMs = better retention
3. **Serverless scale** — no $200/month VPS ceiling; scales to 10M clicks/month on Supabase + Cloudflare
4. **White-label depth** — custom domains, custom branding, custom payout rules per installation

---

## 4. DESIGN SYSTEM — "ETHEREAL GLASS"

### 4.1 Philosophy
The UI targets fintech-grade clarity. Inspired by Linear's precision, Stripe's data density, and Resend's no-nonsense developer aesthetics. **Brutalist spatial hierarchy** — every element has one job.

### 4.2 Color Architecture
| Role | Token | Hex |
|---|---|---|
| Canvas (background) | `--color-canvas` | `#FAFAFA` (Crisp Alabaster) |
| Surface (cards/panels) | `--color-surface` | `#FFFFFF` (Pure White) |
| Primary Ink (headings/data) | `--color-ink-primary` | `#09090B` (Near Black) |
| Muted Ink (secondary/labels) | `--color-ink-muted` | `#71717A` (Zinc-500) |
| Accent (CTA) | `--color-accent` | `#4338CA` (Electric Indigo) |
| Accent Hover | `--color-accent-hover` | `#3730A3` |
| Destructive | `--color-destructive` | `#DC2626` |
| Success | `--color-success` | `#16A34A` |
| Warning | `--color-warning` | `#CA8A04` |
| Telemetry lines (charts) | `--color-chart-primary` | `#6366F1` |
| Border (structural only) | `--color-border` | `#E4E4E7` (Zinc-200) |

### 4.3 Geometry & Shadow Rules
- **ZERO colored borders** on metric cards or data containers — surfaces float on shadow alone
- **Ambient Shadow:** `shadow-[0_4px_32px_-12px_rgba(9,9,11,0.06)]` on all white surfaces
- **Focus Ring:** `ring-2 ring-indigo-400/60 ring-offset-2` — keyboard accessibility
- **Border Radius:**
  - Structural panels → `rounded-xl` (12px)
  - Input fields → `rounded-lg` (8px)
  - Primary CTAs → `rounded-full` (999px)
  - Status badges → `rounded-full`
  - Data table rows → no radius (sharp, dense)

### 4.4 Typography Regime
```
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@600;700&family=Plus+Jakarta+Sans:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');
```
| Role | Font | Weights |
|---|---|---|
| Display / Hero headings | `Outfit` | 700 |
| Section headings | `Outfit` | 600 |
| Interface / Body / Labels | `Plus Jakarta Sans` | 400, 500 |
| URLs / Short codes / IPs / Amounts | `JetBrains Mono` | 400, 500 |

**Type Scale (rem):**
- `text-[2.5rem]` — Hero display
- `text-[1.5rem]` — Section heading (H2)
- `text-[1.125rem]` — Card heading (H3)
- `text-[0.875rem]` — Body / Table cells
- `text-[0.75rem]` — Labels / Captions / Timestamps

### 4.5 Component Inventory

**Metric Card (Borderless)**
```
bg-white rounded-xl p-6 shadow-[0_4px_32px_-12px_rgba(9,9,11,0.06)]
├── Label: text-xs uppercase tracking-wider text-zinc-500 font-medium Plus Jakarta Sans
├── Value: text-3xl font-bold text-[#09090B] Outfit
├── Delta: text-sm JetBrains Mono (green if positive, red if negative)
└── Sparkline: recharts ResponsiveContainer h-[40px] — no axes, no grid
```

**Primary CTA Button**
```
bg-[#4338CA] hover:bg-[#3730A3] text-white rounded-full px-6 py-2.5
font-semibold text-sm Plus Jakarta Sans
transition-all duration-200
+ magnetic pull motion effect on hover
```

**Data Table Row**
```
border-b border-zinc-100 hover:bg-zinc-50/60
transition-colors duration-100
staggered motion.tr with staggerChildren: 0.05
```

**Status Badge**
```
rounded-full px-2.5 py-0.5 text-xs font-medium
Active   → bg-green-50  text-green-700
Inactive → bg-zinc-100  text-zinc-500
Pending  → bg-amber-50  text-amber-700
Rejected → bg-red-50    text-red-600
Approved → bg-blue-50   text-blue-700
```

**Bottom Sheet Modal (Mobile)**
```
fixed inset-x-0 bottom-0 z-50 rounded-t-2xl bg-white
shadow-[0_-4px_48px_-8px_rgba(9,9,11,0.12)]
motion.div: y: "100%" → y: 0, type: spring, stiffness: 400, damping: 40
drag="y" dragConstraints={{ top: 0 }} — swipe-to-close gesture
```

### 4.6 Physics & Motion (`motion/react`)
```javascript
// Global spring constant — consistent across all interactive elements
const fluidSpring = { type: "spring", stiffness: 300, damping: 24, mass: 0.5 };

// Page/section entry
const containerVariants = {
  hidden: {},
  visible: { transition: { staggerChildren: 0.05, delayChildren: 0.1 } }
};
const itemVariants = {
  hidden: { opacity: 0, y: 16 },
  visible: { opacity: 1, y: 0, transition: fluidSpring }
};

// Magnetic CTA pull (attach to onMouseMove on button wrapper)
const magneticPull = (e, ref) => {
  const rect = ref.current.getBoundingClientRect();
  const x = (e.clientX - rect.left - rect.width / 2) * 0.2;
  const y = (e.clientY - rect.top - rect.height / 2) * 0.2;
  animate(ref.current, { x, y }, { ...fluidSpring });
};

// Living Canvas background orbs (z-[-1], pointer-events-none)
// Orb 1: w-[600px] h-[600px] bg-indigo-500/5 blur-[140px] rounded-full
//         animate: x [-20,20,-20] y [-30,10,-30] — duration 20s infinite
// Orb 2: w-[500px] h-[500px] bg-pink-500/5 blur-[140px] rounded-full  
//         animate: x [20,-20,20] y [10,-30,10] — duration 25s infinite
```

---

## 5. TECHNICAL ARCHITECTURE

### 5.1 Full Stack at a Glance
```
┌─────────────────────────────────────────────────────────┐
│  CLIENT LAYER                                           │
│  Vite + React 19 (react-router-dom v7)                  │
│  Tailwind CSS (arbitrary values, no Shadcn)             │
│  motion/react · recharts · @phosphor-icons/react        │
│  Deployed: Cloudflare Pages (CDN edge, free tier)       │
└───────────────────┬─────────────────────────────────────┘
                    │ HTTPS / REST / Realtime WS
┌───────────────────▼─────────────────────────────────────┐
│  SUPABASE LAYER                                         │
│  PostgreSQL 15 (Row Level Security everywhere)          │
│  Supabase Auth (email/password + Google OAuth)          │
│  Edge Functions (Deno runtime, globally distributed)    │
│  Supabase Realtime (dashboard live updates)             │
│  Supabase Storage (ad media, user avatars)              │
└───────────────────┬─────────────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────────────┐
│  REDIRECT ENGINE (Critical Path — must be FAST)         │
│  Supabase Edge Function: /r/[alias]                     │
│  → DB lookup (indexed alias column, <5ms)               │
│  → Fraud score calculation (inline, async write)        │
│  → Serve interstitial HTML or 302 redirect              │
│  Target: p95 < 80ms globally                            │
└─────────────────────────────────────────────────────────┘
```

### 5.2 Tech Stack (Pinned Versions — 2026)
| Layer | Technology | Version |
|---|---|---|
| Build tool | Vite | 6.x |
| UI Framework | React | 19.x |
| Routing | react-router-dom | 7.x |
| Styling | Tailwind CSS | 4.x |
| Animation | motion/react (motion.dev) | 11.x |
| Charts | recharts | 2.x |
| Icons | @phosphor-icons/react | 2.x (duotone weight) |
| Backend | Supabase | latest |
| Edge Runtime | Deno (via Supabase Edge) | 2.x |
| Deployment | Cloudflare Pages | — |
| Package manager | pnpm | 9.x |
| Language | TypeScript | 5.x (strict mode) |

### 5.3 Repository Structure
```
shrinkr/
├── apps/
│   └── web/                        # Vite + React SPA
│       ├── src/
│       │   ├── components/         # Shared UI components
│       │   │   ├── ui/             # Primitives (Button, Badge, Input...)
│       │   │   ├── charts/         # recharts wrappers
│       │   │   └── layout/         # AppShell, Sidebar, BottomNav
│       │   ├── pages/              # Route-level components
│       │   │   ├── auth/
│       │   │   ├── install/
│       │   │   ├── member/
│       │   │   ├── admin/
│       │   │   └── interstitial/
│       │   ├── hooks/              # useAuth, useLinks, useAnalytics...
│       │   ├── lib/                # supabase.ts, utils, constants
│       │   ├── stores/             # Zustand global state
│       │   └── types/              # Shared TypeScript interfaces
│       ├── public/
│       └── vite.config.ts
├── supabase/
│   ├── migrations/                 # All SQL migration files
│   ├── functions/
│   │   ├── redirect/               # Core redirect engine
│   │   ├── process-click/          # Async click telemetry + fraud scoring
│   │   ├── payout-calculator/      # Scheduled: nightly balance updates
│   │   └── admin-export/           # GDPR data export handler
│   └── seed.sql
├── docs/
│   ├── BLUEPRINT.md                # This file
│   ├── API.md
│   └── DEPLOYMENT.md
└── package.json                    # pnpm workspace root
```

### 5.4 Critical Performance Requirements
| Operation | Target | Method |
|---|---|---|
| Alias redirect (p95) | < 80ms | Edge Function + indexed DB |
| Dashboard initial load | < 1.2s | Code splitting, lazy routes |
| Link table render (100 rows) | < 16ms | Virtualization (react-window) |
| Real-time click counter update | < 500ms | Supabase Realtime subscription |
| Auth session check | < 50ms | Supabase session from localStorage |

---

## 6. DATABASE ARCHITECTURE (SUPABASE)

### 6.1 Schema Overview
All tables use UUID primary keys. All timestamps are `timestamptz` (UTC). Row Level Security (RLS) is enabled on every table.

### 6.2 Table Definitions

#### `site_settings` — Singleton configuration table
```sql
CREATE TABLE site_settings (
  id               SERIAL PRIMARY KEY,             -- always 1
  site_name        TEXT NOT NULL DEFAULT 'Shrinkr',
  site_logo_url    TEXT,
  default_domain   TEXT NOT NULL,                  -- e.g. 'lnk.io'
  recaptcha_site_key    TEXT,
  recaptcha_secret_key  TEXT,
  ad_code_top      TEXT,                           -- raw HTML/JS injection
  ad_code_middle   TEXT,
  ad_code_bottom   TEXT,
  interstitial_timer_seconds INTEGER DEFAULT 10,
  global_min_payout NUMERIC(10,2) DEFAULT 5.00,
  maintenance_mode  BOOLEAN DEFAULT FALSE,
  allowed_domains   TEXT[],                        -- multi-domain support
  created_at        TIMESTAMPTZ DEFAULT NOW(),
  updated_at        TIMESTAMPTZ DEFAULT NOW()
);
-- RLS: Only admin role can read/write
```

#### `users` — Extended auth profiles
```sql
CREATE TABLE users (
  id               UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  username         TEXT UNIQUE NOT NULL,
  display_name     TEXT,
  avatar_url       TEXT,
  role             TEXT NOT NULL DEFAULT 'member' CHECK (role IN ('admin', 'member')),
  balance_available NUMERIC(12,4) DEFAULT 0.0000,  -- 4 decimal precision
  balance_total_earned NUMERIC(12,4) DEFAULT 0.0000,
  balance_total_withdrawn NUMERIC(12,4) DEFAULT 0.0000,
  is_banned        BOOLEAN DEFAULT FALSE,
  ban_reason       TEXT,
  referrer_id      UUID REFERENCES users(id),
  fraud_score      SMALLINT DEFAULT 0,             -- 0-100, auto-managed
  api_key          TEXT UNIQUE DEFAULT gen_random_uuid()::TEXT,
  timezone         TEXT DEFAULT 'UTC',
  created_at       TIMESTAMPTZ DEFAULT NOW(),
  updated_at       TIMESTAMPTZ DEFAULT NOW()
);
-- RLS: Users can read/update their own row. Admin reads all.
```

#### `links` — Shortened URL records
```sql
CREATE TABLE links (
  id               UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id          UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  original_url     TEXT NOT NULL,
  alias            TEXT NOT NULL,                  -- the short code
  domain           TEXT NOT NULL,                  -- which domain serves this
  title            TEXT,                           -- auto-fetched OG title
  is_active        BOOLEAN DEFAULT TRUE,
  is_hidden        BOOLEAN DEFAULT FALSE,          -- hidden from member's own list
  password_hash    TEXT,                           -- optional password protection
  expiry_at        TIMESTAMPTZ,                    -- optional TTL
  total_clicks     INTEGER DEFAULT 0,              -- denormalized counter
  unique_clicks    INTEGER DEFAULT 0,
  earnings_total   NUMERIC(12,4) DEFAULT 0.0000,
  created_at       TIMESTAMPTZ DEFAULT NOW(),
  updated_at       TIMESTAMPTZ DEFAULT NOW(),
  UNIQUE (alias, domain)
);
CREATE INDEX idx_links_alias_domain ON links(alias, domain);  -- critical for redirect speed
CREATE INDEX idx_links_user_id ON links(user_id);
-- RLS: Members read/write own links. Admin reads all.
```

#### `clicks` — Telemetry engine
```sql
CREATE TABLE clicks (
  id               UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  link_id          UUID NOT NULL REFERENCES links(id) ON DELETE CASCADE,
  user_id          UUID REFERENCES users(id),      -- link owner
  ip_address       INET,
  ip_hash          TEXT NOT NULL,                  -- hashed for dedup
  country_code     CHAR(2),
  country_name     TEXT,
  city             TEXT,
  referrer         TEXT,
  user_agent       TEXT,
  device_type      TEXT CHECK (device_type IN ('desktop','mobile','tablet','bot','unknown')),
  os               TEXT,
  browser          TEXT,
  is_unique        BOOLEAN DEFAULT FALSE,          -- first click from this ip_hash+link
  is_fraud         BOOLEAN DEFAULT FALSE,
  fraud_reason     TEXT,
  earned_amount    NUMERIC(12,6) DEFAULT 0.000000, -- 6 decimal precision
  cpm_rate_applied NUMERIC(8,4),
  created_at       TIMESTAMPTZ DEFAULT NOW()
);
CREATE INDEX idx_clicks_link_id ON clicks(link_id);
CREATE INDEX idx_clicks_user_id ON clicks(user_id);
CREATE INDEX idx_clicks_created_at ON clicks(created_at DESC);
CREATE INDEX idx_clicks_country_code ON clicks(country_code);
-- Partition by month for scale (implemented in Phase 3)
-- RLS: Members read own link clicks. Admin reads all.
```

#### `cpm_rates` — Country-specific payout configuration
```sql
CREATE TABLE cpm_rates (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  country_code CHAR(2) NOT NULL UNIQUE,
  country_name TEXT NOT NULL,
  rate         NUMERIC(8,4) NOT NULL,              -- per 1000 valid clicks
  tier         SMALLINT NOT NULL CHECK (tier BETWEEN 1 AND 3),
  is_active    BOOLEAN DEFAULT TRUE,
  updated_at   TIMESTAMPTZ DEFAULT NOW()
);
-- Pre-populated with ~50 countries on setup
-- RLS: All authenticated users can read. Admin can write.
```

#### `withdrawals` — Payout request queue
```sql
CREATE TABLE withdrawals (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID NOT NULL REFERENCES users(id),
  amount          NUMERIC(12,4) NOT NULL,
  method          TEXT NOT NULL CHECK (method IN ('paypal','crypto_usdt','crypto_btc','bank_transfer','upi')),
  method_details  JSONB NOT NULL,                  -- { "address": "...", "email": "..." }
  status          TEXT DEFAULT 'pending' CHECK (status IN ('pending','approved','rejected','processing','completed')),
  admin_note      TEXT,
  processed_by    UUID REFERENCES users(id),
  requested_at    TIMESTAMPTZ DEFAULT NOW(),
  processed_at    TIMESTAMPTZ
);
CREATE INDEX idx_withdrawals_user_id ON withdrawals(user_id);
CREATE INDEX idx_withdrawals_status ON withdrawals(status);
-- RLS: Members read own withdrawals. Admin reads/writes all.
```

#### `notices` — System announcements
```sql
CREATE TABLE notices (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title       TEXT NOT NULL,
  body        TEXT NOT NULL,
  type        TEXT DEFAULT 'info' CHECK (type IN ('info','warning','success','danger')),
  is_active   BOOLEAN DEFAULT TRUE,
  target_role TEXT DEFAULT 'member' CHECK (target_role IN ('member','admin','all')),
  expires_at  TIMESTAMPTZ,
  created_at  TIMESTAMPTZ DEFAULT NOW()
);
```

#### `domains` — Multi-domain support (Phase 2+)
```sql
CREATE TABLE domains (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  domain      TEXT NOT NULL UNIQUE,
  user_id     UUID REFERENCES users(id),           -- NULL = platform domain
  is_verified BOOLEAN DEFAULT FALSE,
  dns_token   TEXT DEFAULT gen_random_uuid()::TEXT, -- for CNAME verification
  created_at  TIMESTAMPTZ DEFAULT NOW()
);
```

### 6.3 Database Functions (Stored Procedures)
```sql
-- Atomically increment click counter and earnings for a link
CREATE OR REPLACE FUNCTION increment_link_stats(
  p_link_id UUID, p_earned NUMERIC, p_is_unique BOOLEAN
) RETURNS VOID AS $$
BEGIN
  UPDATE links SET
    total_clicks = total_clicks + 1,
    unique_clicks = unique_clicks + (CASE WHEN p_is_unique THEN 1 ELSE 0 END),
    earnings_total = earnings_total + p_earned,
    updated_at = NOW()
  WHERE id = p_link_id;
  
  UPDATE users SET
    balance_available = balance_available + p_earned,
    balance_total_earned = balance_total_earned + p_earned,
    updated_at = NOW()
  WHERE id = (SELECT user_id FROM links WHERE id = p_link_id);
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;
```

### 6.4 Scheduled Jobs (Supabase Cron + Edge Functions)
| Job | Schedule | Purpose |
|---|---|---|
| `process-click-queue` | Every 30s | Flush pending click batches |
| `fraud-audit-daily` | Daily 00:00 UTC | Re-score suspicious click patterns |
| `earnings-reconcile` | Daily 03:00 UTC | Fix balance drift from race conditions |
| `link-expiry-cleanup` | Hourly | Deactivate expired links |
| `analytics-snapshot` | Daily 01:00 UTC | Pre-aggregate 30-day stats |

---

## 7. SECURITY & FRAUD PREVENTION LAYER

*This is the primary moat. Get this wrong and the platform collapses within weeks of launch.*

### 7.1 Threat Model
| Threat | Impact | Mitigation |
|---|---|---|
| Click farms (bot IPs) | Fake earnings drain ad revenue | IP reputation + device fingerprint |
| VPN / proxy rotation | Circumvents IP bans | ASN + datacenter range blocks |
| Same-user self-clicking | Inflated member earnings | IP hash deduplication per link per 24h |
| Residential proxy bots | Hardest to detect | Behavioral signals (scroll, timing) |
| Referral abuse | Fake sub-account clicks | Referral click ratio monitoring |
| SQL injection via alias | DB compromise | Prepared statements, RLS everywhere |
| Admin impersonation | Full platform compromise | 2FA enforcement for admin role |

### 7.2 Fraud Scoring Engine (Edge Function: `process-click`)

**Score bands:**
```
0–20   → Clean click → Full CPM credit
21–50  → Suspect    → 50% CPM credit, flagged for review
51–80  → Likely bot  → 0% credit, click recorded as fraud
81–100 → Confirmed bot → Blocked, no redirect served
```

**Scoring factors (additive):**
```typescript
const fraudSignals = {
  datacenter_asn:       +35,  // IP belongs to AWS/GCP/Azure/Cloudflare ASN
  vpn_proxy_detected:   +30,  // Identified VPN/proxy exit node
  ip_duplicate_24h:     +25,  // Same IP, same link, within 24 hours
  headless_ua:          +20,  // User-agent matches headless Chrome patterns
  missing_ua:           +15,  // No user-agent header
  impossible_geography: +20,  // IP geo ≠ Accept-Language header hint
  rate_burst:           +25,  // >5 clicks from same IP in 60s
  known_bad_ip:         +40,  // In manual blocklist or abuse DB
};
```

### 7.3 IP Intelligence Sources
- **Primary:** [ipapi.co](https://ipapi.co) — free tier for geo + ASN lookup (1000/day)
- **Scale (Phase 2+):** [ipinfo.io](https://ipinfo.io) — paid, ASN + datacenter detection
- **Blocklist:** Maintain a `blocked_ips` table with manual admin overrides + imported block ranges

### 7.4 Deduplication Strategy
```sql
-- Unique click = no row in clicks WHERE ip_hash = $1 AND link_id = $2
-- AND created_at > NOW() - INTERVAL '24 hours'
-- This query MUST use the composite index:
CREATE INDEX idx_clicks_dedup ON clicks(ip_hash, link_id, created_at DESC);
```

### 7.5 Rate Limiting (Edge Function layer)
```typescript
// KV-based rate limiter (Supabase KV or Cloudflare KV)
const RATE_LIMIT = {
  per_ip_per_minute: 10,      // hard stop on redirect serving
  per_ip_per_link_24h: 1,     // only 1 monetized click per IP per link per day
  api_per_key_per_minute: 60, // public API rate limit
};
```

### 7.6 Security Headers (Cloudflare Pages `_headers`)
```
/*
  X-Frame-Options: DENY
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin
  Permissions-Policy: geolocation=(), camera=(), microphone=()
  Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline' https://www.google.com/recaptcha/; ...
```

---

## 8. APPLICATION ARCHITECTURE & ROUTING MATRIX

### 8.1 Route Map
```
/                          → Redirect to /login or /member/dashboard
/install                   → Setup wizard (locked if site_settings exists)

/login                     → Auth: Email/Password + Google OAuth
/register                  → Auth: Registration form + reCAPTCHA
/forgot-password           → Auth: Password reset flow
/terms                     → Public: Terms of Service
/privacy                   → Public: Privacy Policy
/payout-rates              → Public: CPM rate table (SEO page)

/:alias                    → Interstitial monetization engine
/:alias/skip               → Post-countdown redirect trigger (POST only)

/member/dashboard          → Analytics overview + notices
/member/links              → Link management table
/member/links/new          → Create new link form
/member/analytics          → Deep-dive per-link analytics (Phase 2)
/member/withdraw           → Withdrawal request form
/member/tools              → Mass shrinker, API access, full-page script
/member/referrals          → Referral program dashboard (Phase 2)
/member/settings           → Profile, password, notification prefs

/admin/dashboard           → Platform-wide stats
/admin/users               → User management table
/admin/links               → All links across all users
/admin/withdrawals         → Approval queue
/admin/rates               → CPM rate CRUD
/admin/options             → Site settings (tabbed)
/admin/fraud               → Fraud review queue
/admin/notices             → Announcement management
/admin/domains             → Multi-domain management (Phase 2)
```

### 8.2 Phase 1 — The Boot Guard (`/install`)
**Trigger:** `site_settings` table is empty (first run).
**Lock:** `AppRouter` checks on mount → if empty, renders `<InstallWizard />` and blocks all other routes.

**Wizard Steps:**
```
Step 1: Welcome screen + tech stack confirmation
Step 2: Site Identity (name, domain, logo)
Step 3: Database connection test (auto-passed since Supabase handles this)
Step 4: Create Master Admin (email + password, sets role='admin')
Step 5: Initial CPM rates (pre-populated, editable)
Step 6: Ad network setup (can skip) + reCAPTCHA keys
Step 7: Launch confirmation → writes site_settings row → unlocks app
```

### 8.3 Phase 2 — Auth Layer
**Guards:**
```typescript
// Route guard components
<PublicRoute>    // Redirects to /member/dashboard if already authed
<MemberRoute>   // Requires role=member OR role=admin
<AdminRoute>    // Requires role=admin only; redirects banned users
```

**Auth Flow:**
- Supabase email/password + Google OAuth (one-click)
- On register: creates `auth.users` row → Supabase trigger creates `public.users` row
- JWT stored in Supabase session (auto-refresh, 1-hour expiry)
- Password reset via Supabase magic link email

### 8.4 Phase 3 — The Monetization Engine (`/:alias`)

**This is the revenue-critical path. Every millisecond and every UX decision here affects earnings.**

**Redirect Flow:**
```
Browser hits /:alias
    → Edge Function `redirect` receives request
    → Look up alias in links table (< 5ms, indexed)
    → If not found → 404 page
    → If inactive/expired → dead link page
    → If fraud score > 80 from this IP → serve blank 302 to destination
    → Serve interstitial HTML page (inline, no SPA overhead)
    → Async: fire `process-click` edge function (background, non-blocking)
```

**Interstitial Page Spec:**
```
Layout: Single-page, standalone HTML (NOT part of the React SPA)
        Served directly from Edge Function for maximum speed.

┌─────────────────────────────────┐
│  AD ZONE TOP                    │  ← site_settings.ad_code_top injection
│  (728x90 leaderboard desktop /  │
│   320x50 mobile banner)         │
├─────────────────────────────────┤
│  SITE BRANDING (logo + name)    │
├─────────────────────────────────┤
│  "You are being redirected to:" │
│  [destination URL — truncated]  │
├─────────────────────────────────┤
│  AD ZONE MIDDLE                 │  ← site_settings.ad_code_middle injection
│  (300x250 rectangle)            │
├─────────────────────────────────┤
│  COUNTDOWN TIMER                │
│  Large circular progress ring   │
│  "Redirecting in 10..."         │
│                                 │
│  [SKIP AD] ← appears at 0,      │
│  disabled + greyed until timer  │
│  reaches zero                   │
├─────────────────────────────────┤
│  AD ZONE BOTTOM                 │  ← site_settings.ad_code_bottom injection
│  (320x50 or native ad)          │
└─────────────────────────────────┘

Timer behavior:
- JavaScript setInterval decrements display
- At 0: "Skip Ad" button becomes enabled (CSS class swap)
- User must CLICK — no auto-redirect (improves ad viewability scores)
- Click fires POST /:alias/skip → Edge Function validates timer elapsed
  (server-side: click must arrive > 9s after initial request)
- Then issues 302 redirect to original_url
```

### 8.5 Phase 4 — Member Dashboard (`/member/*`)

**Mobile UX Rules:**
- Bottom navigation bar (5 tabs max): Home, Links, Withdraw, Tools, Settings
- Desktop: Left sidebar with same items
- All modals on mobile: bottom sheet with swipe-to-close
- No horizontal scroll anywhere
- Touch targets minimum 44px

**`/member/dashboard` Spec:**
```
┌── Greeting bar: "Good morning, {username}" + current date
├── System Notices: dismissible banner cards from admin
├── Metric Grid (2-col mobile / 4-col desktop):
│   ├── Today's Clicks      (with sparkline)
│   ├── Today's Revenue     (JetBrains Mono, 4 decimals)
│   ├── This Month Clicks
│   └── This Month Revenue
├── Performance Chart:
│   recharts AreaChart
│   X-axis: last 30 days
│   Y-axis: dual (clicks left, revenue right)
│   Gradient fill: indigo-500/20 → transparent
│   Tooltip: custom, shows both metrics
├── Top Links (5 rows):
│   Short URL | Clicks | Revenue | CTR
└── Quick Actions:
    [+ New Link]  [↗ Withdraw]
```

**`/member/links` Spec:**
```
Header: Link count badge + [+ New Link] CTA
Filter bar: Search | Status toggle | Sort (newest/oldest/most clicks)

Table columns:
  Short URL (JetBrains Mono, copyable)
  Destination URL (truncated, tooltip on hover)
  Clicks
  Revenue ($X.XXXX)
  Status badge
  Created date
  Actions: [Copy] [Edit] [QR Code] [Stats] [Deactivate] [Delete]

Row entry: motion.tr staggered slide-up
Copy action: clipboard API + "Copied!" toast notification
Mobile: card layout instead of table (swipe actions)
```

**`/member/tools` Spec:**
```
Tab 1 — Mass Shrinker:
  Textarea: up to 20 URLs (one per line)
  [Shorten All] → processes as array
  Results table: copy all / copy individual
  Export as .txt / .csv

Tab 2 — Full Page Script:
  Code block (JetBrains Mono) showing JS snippet
  User embeds on their site; any outbound link click
  auto-redirects through the shortener
  [Copy Script] button

Tab 3 — API Access:
  Displays user's api_key (blurred by default, click to reveal)
  [Regenerate Key] with confirmation
  Code examples: cURL, JavaScript, Python
  Links to /docs/api
```

**`/member/withdraw` Spec:**
```
Balance display: Available balance (large, JetBrains Mono)
                 Total earned | Total withdrawn (smaller)

Form:
  Amount input (validates: > 0, ≤ balance, ≥ global_min_payout)
  Method select: PayPal | USDT | BTC | Bank Transfer | UPI
  Method details: dynamic fields based on selection
    PayPal → email field
    Crypto → wallet address field  
    Bank   → account number, IFSC, bank name
    UPI    → UPI ID

Submission: creates withdrawal row with status=pending
Success state: "Request submitted. Processing within 48 hours."

Withdrawal history table below form:
  Amount | Method | Status | Requested | Processed
```

### 8.6 Phase 5 — Admin Control Center (`/admin/*`)

**`/admin/options` — Tabbed Settings Hub:**
```
Tab: Site Identity  → Name, Logo, Default Domain, Maintenance Mode
Tab: Ad Codes       → Three rich-text ad code injection zones
Tab: reCAPTCHA      → Site key + secret key fields
Tab: Payouts        → Global minimum payout amount
Tab: Email          → SMTP config for notifications
Tab: Danger Zone    → Reset stats, export data, clear fraud queue
```

**`/admin/users` — User Management:**
```
Search + filter (role, status, join date)
Table: Avatar | Username | Email | Role | Earnings | Balance | Status | Actions
Actions per row: [Edit Balance] [Change Role] [Ban/Unban] [View Links] [Delete]
Ban: requires reason text, recorded in users.ban_reason
```

**`/admin/withdrawals` — Approval Queue:**
```
Tabs: Pending (badge count) | Approved | Rejected | All
Table: User | Amount | Method | Details | Requested | Actions
Actions: [Approve] → status=approved, triggers notification
         [Reject]  → modal with required reason, status=rejected
Bulk actions: Select multiple → Approve All / Reject All
```

**`/admin/rates` — CPM CRUD:**
```
Table: Flag | Country | Tier | Rate ($/1000) | Status | Actions
Inline editing: click rate cell → becomes input → save on blur
Add country: modal form
Import/Export: CSV upload/download for bulk updates
```

**`/admin/fraud` — Fraud Review Queue:**
```
Table: Timestamp | IP | Country | Link | User | Reason | Score | Actions
Actions: [Whitelist IP] [Block IP] [Mark Clean] [Mark Confirmed Fraud]
Stats bar: Total flagged today | Auto-blocked | Manual review needed
```

---

## 9. DEVELOPMENT PHASES & EXECUTION ROADMAP

### 9.1 Execution Philosophy
> Ship working software, not perfect software. Each phase must be independently deployable and immediately valuable.

### 9.2 Phase Breakdown

---

#### **PHASE 0 — Foundation** *(Week 1–2)*
**Goal:** Codebase skeleton, design system, auth.

**Reasoning:** Without a solid design system first, every component needs rework. Establish tokens, primitives, and patterns before building features. This is the investment that pays compound returns across all phases.

**Deliverables:**
- [ ] pnpm workspace initialized, TypeScript strict mode
- [ ] Tailwind 4 configured with design token CSS variables
- [ ] Google Fonts loaded (Outfit, Plus Jakarta Sans, JetBrains Mono)
- [ ] Base UI primitives: Button, Input, Badge, Card, Toast, Modal
- [ ] Living Canvas background (motion orbs)
- [ ] Supabase project created, connection configured
- [ ] Auth tables + RLS policies written
- [ ] `/login` and `/register` pages complete
- [ ] Google OAuth configured in Supabase dashboard
- [ ] Route guards: `PublicRoute`, `MemberRoute`, `AdminRoute`
- [ ] Cloudflare Pages deployment pipeline (GitHub → auto-deploy)

**Success criteria:** A user can register, verify email, log in, and see a placeholder dashboard. Full auth loop working in production.

---

#### **PHASE 1 — Install Wizard + Core Settings** *(Week 3)*
**Goal:** First-run experience and site configuration.

**Reasoning:** The install wizard is what makes this a product, not just code. It's the onboarding experience for operators. It must feel premium.

**Deliverables:**
- [ ] `site_settings` table + migration
- [ ] Boot Guard logic in AppRouter
- [ ] 7-step install wizard with motion transitions
- [ ] Master admin creation flow
- [ ] Initial CPM rates seeded (50 countries)
- [ ] Admin settings page (basic tab structure)

**Success criteria:** Fresh Supabase project + deploy → wizard appears → complete wizard → admin dashboard unlocked.

---

#### **PHASE 2 — Link Management + Redirect Engine** *(Week 4–5)*
**Goal:** The core product. Links can be created, managed, and clicked.

**Reasoning:** The redirect engine is the most performance-critical piece. It must be built as an Edge Function, not as a serverless API route, to guarantee sub-100ms global latency. Get this right before building analytics on top of it.

**Deliverables:**
- [ ] `links` table + `clicks` table + migrations + indexes
- [ ] Edge Function: `redirect` (alias lookup + fraud pre-check + interstitial serve)
- [ ] Edge Function: `process-click` (async, non-blocking: geo lookup + fraud score + DB write)
- [ ] Interstitial HTML template (standalone, fast, three ad zones)
- [ ] 10-second countdown timer with server-side validation of skip
- [ ] `/member/links` table with full CRUD
- [ ] `/member/links/new` create form
- [ ] Copy-to-clipboard on short URLs
- [ ] Link status toggle (active/inactive)

**Success criteria:** Create a link → visit short URL → see interstitial with countdown → skip → land on destination. Click recorded in DB.

---

#### **PHASE 3 — Fraud Engine + Analytics** *(Week 6–7)*
**Goal:** Make the data trustworthy. Build the analytics dashboard.

**Reasoning:** This is what differentiates SHRINKR from every legacy platform. A fraud engine that works means advertisers pay more, which means operators earn more, which means member retention goes up. Analytics gives members a reason to check the dashboard daily.

**Deliverables:**
- [ ] IP intelligence integration (ipapi.co or ipinfo.io)
- [ ] Fraud scoring logic in `process-click`
- [ ] IP hash deduplication (unique click detection)
- [ ] Fraud score written to clicks table
- [ ] `blocked_ips` table + admin management UI
- [ ] `/member/dashboard` — complete metrics + 30-day AreaChart
- [ ] `/admin/fraud` — fraud review queue
- [ ] recharts wrappers: AreaChart, BarChart (for admin)
- [ ] Real-time click counter on dashboard (Supabase Realtime)

**Success criteria:** Bot click gets flagged. Duplicate click within 24h = not counted as unique. Dashboard shows accurate, non-gamed stats.

---

#### **PHASE 4 — Payouts + Tools + Admin** *(Week 8–9)*
**Goal:** Complete the money flow. Operators can manage users and approve withdrawals.

**Deliverables:**
- [ ] `withdrawals` table + migrations
- [ ] `/member/withdraw` complete form with balance validation
- [ ] `/admin/withdrawals` approval queue with bulk actions
- [ ] `/admin/users` full management table
- [ ] `/admin/rates` CPM CRUD with inline edit
- [ ] Mass Shrinker tool (20 URL batch processor)
- [ ] Full Page Script generator
- [ ] API key display + regeneration
- [ ] User balance update via stored procedure

**Success criteria:** Member requests withdrawal → admin approves → member balance updated → withdrawal marked completed.

---

#### **PHASE 5 — Polish, Performance, Production** *(Week 10)*
**Goal:** Production-hardening, performance audit, UI polish pass.

**Deliverables:**
- [ ] Lighthouse score > 90 on all pages
- [ ] Bundle analysis + code splitting audit (target: main bundle < 200kb)
- [ ] Mobile UX full pass — bottom nav, bottom sheets, touch targets
- [ ] Error boundaries on all routes
- [ ] Empty states for all tables (no blank white boxes)
- [ ] Loading skeletons for all data-fetched components
- [ ] Security headers on Cloudflare Pages (`_headers` file)
- [ ] API documentation (`/docs/api`)
- [ ] End-to-end manual test pass on all critical flows
- [ ] Operator deployment guide (`DEPLOYMENT.md`)

---

#### **PHASE 6 — Growth Features** *(Month 3+)*
*Post-launch, based on operator/user feedback*
- [ ] Referral program (sub-affiliate tracking + referral earnings)
- [ ] Custom domain support (DNS verification flow)
- [ ] Per-link analytics deep-dive page
- [ ] A/B redirect testing
- [ ] Link bio / link-in-bio builder
- [ ] Webhook notifications (click events, payout approvals)
- [ ] White-label email templates (custom SMTP per install)
- [ ] AI-powered title auto-fetch from destination OG tags

---

### 9.3 Sprint Planning Template (per week)

Each development sprint follows this reasoning loop:

```
MONDAY   — Planning: Define exact deliverables for the week.
            Ask: "What is the user-facing outcome by Friday?"

TUESDAY–THURSDAY — Build: Feature implementation.
            Rule: Only work on this sprint's deliverables.
            Log all decisions in docs/DECISIONS.md.

FRIDAY   — Review: Does the feature work end-to-end?
            Deploy to Cloudflare Pages staging branch.
            QA the critical path manually.

CONTINUOUS — After every deploy: test the redirect flow.
             It must never break.
```

---

## 10. BUSINESS MODEL & REVENUE STREAMS

### 10.1 Operator Revenue Model (B2B)
SHRINKR is sold as a **white-label SaaS license** to operators who run their own shortener brands on top of our codebase.

| Tier | Price (INR/month) | Target | Included |
|---|---|---|---|
| **Starter** | ₹2,999 | Solo operators, 1 domain | Up to 50k clicks/mo, 100 members |
| **Growth** | ₹7,999 | Small networks | Up to 500k clicks/mo, 1000 members, custom domain |
| **Scale** | ₹19,999 | Large operators | Unlimited, multi-domain, priority support |
| **Agency** | ₹49,999/yr | Resellers | Source code license, 5 installs, white-label rebrand |

*Price to USD equivalent: ~$35 / $95 / $240 / $600 annually — competitive with Adlinkfly's $49 one-time license model but recurring.*

### 10.2 Platform Operator Revenue Model (B2C)
For operators running SHRINKR as their own platform for publishers:

**Revenue pool:** Operator acquires ad network access (Google AdSense, Ezoic, PropellerAds, etc.). Ad codes injected into interstitial pages. CPM revenue flows to operator.

**Payout structure:**
- Operator retains 40–60% of ad CPM revenue
- 40–60% paid out to member publishers via withdrawal system
- Exact split configured in `site_settings`

### 10.3 Margin Analysis (Operator, Scale tier, 1M clicks/month)
```
Tier 1 traffic (US/UK, 20% of clicks):  200,000 × $8 CPM  = $1,600
Tier 2 traffic (EU, 30% of clicks):     300,000 × $3 CPM  = $900
Tier 3 traffic (Asia/Other, 50%):       500,000 × $1 CPM  = $500

Gross ad revenue:                                           $3,000/mo
Member payouts (50% split):                                -$1,500/mo
Platform license cost:                                     -$240/mo
Server/Supabase costs (Scale plan ~$25):                   -$25/mo

OPERATOR NET MARGIN:                                        $1,235/mo (~41%)
```

---

## 11. GO-TO-MARKET STRATEGY

### 11.1 Target Customer Acquisition

**Phase 1 (Months 1–3): Organic seeding**
- Post on developer communities: IndieHackers, HackerNews (Show HN), Reddit r/webdev, r/juststart
- Target Adlinkfly users specifically — post in forums where they discuss its problems
- SEO: Write comparison articles ("Adlinkfly alternative 2026", "self-hosted URL shortener with fraud protection")

**Phase 2 (Months 3–6): Community + Content**
- YouTube demo: "Build your own link shortener business in 2026"
- Gumroad / Lemon Squeezy for license sales (recurring billing)
- Affiliate program: 30% commission to resellers

**Phase 3 (Months 6–12): Platform plays**
- AppSumo lifetime deal (drives 500–2000 first customers fast)
- Partner with web hosting companies (offer SHRINKR as one-click install)
- White-label reseller program

### 11.2 Launch Checklist
- [ ] Landing page (SHRINKR.io) — separate from dashboard, pure marketing
- [ ] Demo instance (demo.shrinkr.io) — pre-loaded with sample data
- [ ] Pricing page
- [ ] Documentation site (docs.shrinkr.io)
- [ ] Support channel (Discord or Crisp)
- [ ] Payment collection (Razorpay for India, Stripe for global)

---

## 12. INFRASTRUCTURE & DEVOPS

### 12.1 Infrastructure Stack
| Service | Purpose | Cost (estimated) |
|---|---|---|
| **Cloudflare Pages** | Frontend CDN + hosting | Free |
| **Supabase Pro** | DB + Auth + Edge Functions | $25/month |
| **Cloudflare R2** | Media storage (ad banners, avatars) | ~$0 (free tier) |
| **Resend** | Transactional email | Free up to 3k/month |
| **Sentry** | Error monitoring | Free tier |
| **GitHub** | Source control + CI/CD | Free |

**Total infrastructure cost: ~$25/month until significant scale.**

### 12.2 Deployment Pipeline
```
Developer pushes to GitHub
    ↓
GitHub Actions:
    - TypeScript type check (tsc --noEmit)
    - ESLint pass
    - Supabase migrations check
    ↓
On merge to main:
    - Cloudflare Pages auto-deploy (frontend)
    - Supabase CLI: supabase db push (migrations)
    - Supabase CLI: supabase functions deploy (Edge Functions)
    ↓
Cloudflare Pages Preview URL for every PR branch
```

### 12.3 Environment Variables
```
# Supabase
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=

# Supabase Edge Functions (server-side secrets)
SUPABASE_SERVICE_ROLE_KEY=
IPINFO_TOKEN=
RECAPTCHA_SECRET_KEY=

# Resend
RESEND_API_KEY=
```

### 12.4 Scaling Thresholds
| Traffic Level | Action |
|---|---|
| < 100k clicks/month | Supabase Free tier sufficient |
| 100k–1M clicks/month | Upgrade to Supabase Pro ($25/mo) |
| 1M–10M clicks/month | Enable Read Replicas + Connection Pooling (PgBouncer) |
| 10M+ clicks/month | Partition `clicks` table by month; add Redis cache layer |

---

## 13. LEGAL, COMPLIANCE & RISK MANAGEMENT

### 13.1 Required Legal Pages
- **Terms of Service** — prohibits adult content, phishing, malware links
- **Privacy Policy** — GDPR-compliant; IP addresses are hashed, not stored raw
- **Cookie Policy** — Interstitial page sets session cookie for dedup
- **DMCA / Abuse Contact** — Required for hosting user-generated content

### 13.2 URL Safety Scanning
**Phase 1:** Manual abuse report form  
**Phase 2:** Integrate [Google Safe Browsing API](https://safebrowsing.google.com) — free, checks destination URLs against phishing/malware DB before shortening. Block link creation if flagged.

```typescript
// Pseudocode: Safe Browsing check on link creation
const isSafe = await checkGoogleSafeBrowsing(originalUrl);
if (!isSafe) {
  throw new Error("DESTINATION_URL_FLAGGED_UNSAFE");
}
```

### 13.3 GDPR Compliance Checklist
- [ ] IP addresses stored as SHA-256 hashes, not raw values (except in admin fraud view — time-limited)
- [ ] User data export endpoint (`/admin/export/:userId` → GDPR ZIP)
- [ ] Account deletion: cascades via FK constraints, removes all PII
- [ ] Cookie consent banner on interstitial page
- [ ] Data retention policy: raw clicks auto-deleted after 2 years

### 13.4 Risk Register
| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| Supabase outage | Low | High | Implement DB connection fallback; monitor uptime |
| Ad network ban (TOS violation) | Medium | High | Strict URL safety policy; abuse reporting system |
| Click farm attack | High | Medium | Fraud engine (Section 7) |
| Domain seizure (malicious links) | Low | Very High | URL safety scanning + DMCA process |
| Supabase cost spike | Low | Medium | Rate limiting + click batching |

---

## 14. KPIs & SUCCESS METRICS

### 14.1 Platform Health KPIs
| Metric | Target (Month 3) | Target (Month 12) |
|---|---|---|
| Redirect p95 latency | < 100ms | < 80ms |
| Uptime | 99.5% | 99.9% |
| Fraud detection rate | > 80% precision | > 95% precision |
| Dashboard load time | < 1.5s | < 1.0s |

### 14.2 Business KPIs
| Metric | Month 1 | Month 6 | Month 12 |
|---|---|---|---|
| Operator licenses sold | 1 (own instance) | 10 | 50 |
| Monthly Recurring Revenue | ₹0 | ₹30,000 | ₹2,00,000 |
| Total links shortened | 500 | 50,000 | 500,000 |
| Platform clicks processed | 5,000 | 500,000 | 5,000,000 |

### 14.3 Member Experience KPIs
| Metric | Target |
|---|---|
| Time to first shortened link | < 2 minutes |
| Withdrawal approval time | < 48 hours |
| Member churn (monthly) | < 10% |
| Support tickets per 100 members | < 5 |

---

## 15. APPENDIX: NAMING, DECISIONS LOG & OPEN QUESTIONS

### 15.1 Architectural Decisions Log

| Decision | Chosen | Rejected | Reason |
|---|---|---|---|
| Frontend framework | Vite + React | Next.js | No SSR needed; edge redirects are separate; simpler ops |
| Backend | Supabase | Firebase, PlanetScale | PostgreSQL required; RLS critical for multi-tenant security |
| CSS methodology | Tailwind arbitrary values | Shadcn/ui, CSS Modules | Max control over design; no generic SaaS look |
| Animation | motion/react | Framer Motion | Same library (rebranded); more tree-shakeable |
| Interstitial rendering | Edge Function HTML | React SPA route | 40% faster render; no JS bundle required for redirect |
| Icons | Phosphor (duotone) | Lucide, Heroicons | Better visual expressiveness for fintech aesthetic |
| CDN | Cloudflare Pages | Vercel, Netlify | Unlimited bandwidth; 300+ edge nodes; free |
| Email | Resend | SendGrid, Postmark | Developer-friendly; excellent free tier |

### 15.2 Open Questions (To Resolve Before Phase 2)
1. **Primary short domain:** What domain will be registered for the live instance?
2. **IP intelligence provider:** ipapi.co free tier (1000/day) enough for MVP, or pay for ipinfo.io from day one?
3. **Ad network strategy:** Which ad networks will the first operator use? (Determines ad code format)
4. **Referral program rate:** What % of referred member earnings goes to referrer?
5. **Multi-language:** Is i18n required for Phase 1, or English-only until market validation?

### 15.3 Future Explorations
- **AI destination title fetching:** Auto-fill link title from OG meta tags using Supabase Edge Function
- **Smart routing:** Route same alias to different destinations by country/device (geo-targeting)
- **Pixel tracking:** Allow members to add Facebook/Google pixels to their interstitial pages
- **SaaS wrapper:** Offer SHRINKR as a fully managed SaaS (no self-hosting) at premium price point
- **Analytics API:** Public API for members to pull their stats into their own tools

---

*SHRINKR Master Blueprint v2.0 — Compiled May 2026*  
*Next review: After Phase 2 completion*

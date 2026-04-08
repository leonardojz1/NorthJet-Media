# NorthJet Media — AI-Powered Lead Generation & SEO Automation

> **3NJ.com | NorthJet Media** — Building AI-powered lead generation networks for local service businesses across Florida.

---

## 🚀 What This Project Does

NorthJet Media is a fully automated lead generation and SEO platform built on a **Raspberry Pi 5**, powered by **n8n**, **xAI Grok API**, **Airtable**, and **Cloudflare**. It targets local service businesses (pet grooming, contractors, cleaning, HVAC, etc.) and delivers two core products:

1. **AI Lead Generation Pipeline** — captures form submissions, scores leads with AI, routes hot leads to CRM and email alerts in real time
2. **AI SEO Keyword Pipeline** — generates secondary/tertiary keyword strategies for local businesses, scores opportunities, and produces ready-to-use HTML meta tags, H1s, FAQ schema, and Local Business schema

---

## 🏗️ Architecture

```
Visitor fills form
      ↓
dog.fullgrooming.com (HTML/CSS site)
      ↓
Cloudflare Tunnel → Raspberry Pi 5
      ↓
n8n Workflow Engine (Docker)
      ↓
xAI Grok API (lead scoring / keyword generation)
      ↓
Airtable CRM + Gmail SMTP alert
```

---

## 🔧 Tech Stack

| Layer | Technology |
|---|---|
| Hardware | Raspberry Pi 5 + AI HAT+ |
| Containers | Docker + Docker Compose |
| Automation | n8n (self-hosted) |
| AI Engine | xAI Grok API (`grok-4.20-0309-reasoning`) |
| Tunnel | Cloudflare Zero Trust Tunnel |
| CRM | Airtable |
| DNS/CDN | Cloudflare |
| Email | Gmail SMTP |
| Frontend | HTML5 + Tailwind CSS |
| Hosting | Namecheap Stellar Business + cPanel |
| Languages | JavaScript (n8n Code nodes), Python (PDF generation) |

---

## 📁 Repository Structure

```
northjet-media/
├── workflows/
│   ├── Pet_Groomer_Lead_Gen_v1.json      # Lead gen pipeline
│   └── seo_free_workflow_WORKING.json    # SEO keyword pipeline
├── sites/
│   ├── dog.fullgrooming.com/
│   │   └── index.html                   # Happy Wags Grooming site
│   └── 3nj.com/
│       └── index.html                   # NorthJet Media agency site
├── docs/
│   ├── NorthJet_Handoff.pdf             # Complete project documentation
│   └── SEO_Arbitrage_QuickRef.pdf       # SEO keyword strategy guide
└── README.md
```

---

## ⚙️ Pipeline 1 — Lead Generation

**Workflow:** `Pet_Groomer_Lead_Gen_v1.json`

**Flow:**
```
Webhook (form POST) 
  → xAI Grok scores lead 1-10
  → IF score > 5 (HOT lead)
    → Create Airtable record
    → Send Gmail HOT LEAD ALERT
```

**Key features:**
- Real-time AI lead scoring using Grok
- Automatic CRM logging to Airtable
- Instant email alerts via Gmail SMTP
- Deployed for Happy Wags Grooming LLC (Bradenton, FL)

**Sample lead scoring prompt:**
```
You are a lead scorer for pet groomers. Score 1-10.
Return ONLY a single number.
Name: {name} Phone: {phone} Message: {message}
```

---

## ⚙️ Pipeline 2 — SEO Keyword Arbitrage

**Workflow:** `seo_free_workflow_WORKING.json`

**14-node pipeline flow:**
```
Webhook → Parse Inputs → Grok Seed Generation
  → Parse Grok Output → Build Autocomplete URLs
  → Scrape Google Autocomplete → Merge Results
  → Opportunity Score Engine → Grok Keyword Placement
  → Parse Placement + Build Schema → Build HTML Injection Map
  → Airtable Log → Send Email → Webhook Response
```

**Key features:**
- Generates 20-60 secondary/tertiary SEO keywords per run
- Scrapes Google Autocomplete for real search data (free)
- Scores keywords using proprietary opportunity formula
- Classifies keywords as 🟢 GREEN / 🟡 YELLOW / 🔴 RED
- Generates H1, meta title, meta description, FAQ Schema, LocalBusiness Schema
- Logs all results to Airtable CRM
- Emails full report on completion

**Opportunity Score Formula:**
```javascript
opp_score = (searches / maxSearches * 40) +    // 40% search volume
            ((100 - competition) / 100 * 30) +  // 30% low competition  
            (cpc / maxCPC * 20) +               // 20% commercial intent
            ((100 - da_avg) / 100 * 10)         // 10% low domain authority
```

**Trigger via curl:**
```bash
curl -X POST http://[PI_IP]:5678/webhook/seo-free \
  -H "Content-Type: application/json" \
  -d '{
    "niche": "pet grooming",
    "city": "Bradenton",
    "state": "FL",
    "client": "Happy Wags Grooming",
    "domain": "dog.fullgrooming.com",
    "nearby": "Sarasota, Palmetto, Parrish, Lakewood Ranch",
    "differentiator": "mobile, comes to you, no cage, one-on-one"
  }'
```

---

## 🎯 SEO Keyword Arbitrage Strategy

The core insight: **primary keywords are owned by national directories** (Yelp, Thumbtack, Petco). Small businesses cannot rank without paid ads. The strategy targets secondary and tertiary terms with the same buying intent but near-zero competition.

| Tier | Example | Competition | Action |
|---|---|---|---|
| Primary (AVOID) | "dog grooming" | 🔴 85-95 | Schema only |
| Secondary (TARGET) | "dog haircut bradenton fl" | 🟢 12-22 | H1, Meta, H2 |
| Tertiary (TARGET) | "goldendoodle trim sarasota" | 🟢 4-15 | Body copy |
| Problem-based | "matted dog hair bradenton" | 🟢 2-12 | FAQ Schema |
| Hyper-local | "dog trim parrish fl" | 🟢 1-6 | Footer links |

---

## 🌐 Live Deployments

| Property | URL | Purpose |
|---|---|---|
| Agency | [3nj.com](https://3nj.com) | NorthJet Media agency site |
| Pilot Client | [dog.fullgrooming.com](https://dog.fullgrooming.com) | Happy Wags Grooming — mobile pet grooming |
| Platform | fullgrooming.com | Pet grooming lead gen network (FL) |
| Contractors | flctr.com | Florida contractor lead gen network (coming soon) |

---

## 🐾 Pilot Client — Happy Wags Grooming LLC

- **Business:** Mobile pet grooming, Bradenton/Sarasota FL
- **Services:** Full groom, haircut, bath, nail trim, de-shed
- **Service area:** Bradenton, Sarasota, Palmetto, Parrish, Lakewood Ranch
- **Booking:** [MoeGo](https://booking.moego.pet/ol/book?name=HappyWagsGroomingLLC)
- **Lead pipeline:** Live — form submissions scored by AI, logged to Airtable, alert sent via email

---

## 📊 Business Model

```
Product                      Price        Margin
─────────────────────────────────────────────────
SEO Keyword Audit            $97–297      ~99%
SEO Audit + Page Optimize    $297–597     ~98%
Monthly SEO Refresh          $97–197/mo   ~98%
Lead Gen Site Bundle         $897+        ~95%
Pro SEO Report (DataForSEO)  $297–597     ~97%
```

**Lead gen network model:**
- Own the SEO traffic on subdomain pages
- Capture leads via AI-scored forms
- Sell leads to local service businesses
- Scale across cities and verticals (fullgrooming.com, flctr.com)

---

## 🗂️ Airtable CRM Schema

**Base:** NorthJet Media CRM

**Table 1 — Lead Gen Leads**
Captures: Name, Phone, Email, Message, Status (hot/cold), AI Score

**Table 2 — SEO Keyword Reports**
Captures: Client, Domain, Niche, City, Tier, Run Date, Top KW per color tier, Recommended KW, Opportunity Score, Green/Yellow/Red counts, H1, Meta Title, FAQ Count, API Cost, Status

---

## 🛣️ Roadmap

- [x] Raspberry Pi 5 Docker infrastructure
- [x] Lead gen pipeline (Happy Wags pilot)
- [x] dog.fullgrooming.com live with SEO optimization
- [x] SEO free pipeline (14 nodes, end-to-end)
- [x] Airtable CRM logging
- [x] Email alerts (SMTP)
- [ ] Google Search Console integration
- [ ] Google Business Profile (Happy Wags)
- [ ] n8n public hostname via Cloudflare tunnel
- [ ] DataForSEO Pro pipeline (real search volume data)
- [ ] FLCTR.com — Florida contractor lead gen network
- [ ] bradenton.fullgrooming.com — generic lead gen landing page
- [ ] 3nj.com rebrand to AI lead gen positioning
- [ ] n8n Cloud backup deployment

---

## 👤 Author

**Jose Z (Leo)**
- Agency: [3NJ.com](https://3nj.com) | NorthJet Media
- Stack: Raspberry Pi 5, n8n, Docker, xAI Grok, Cloudflare, Airtable
- Focus: AI automation, local SEO, lead generation systems

---

*Built with n8n, xAI Grok API, Cloudflare, and a Raspberry Pi 5. Running 24/7 from a single-board computer.*

# Collably

**Where creators and brands meet.**

Collably is a creator-brand marketplace prototype. Creators build profiles with portfolios, skills and rates; brands set up company profiles, draft campaign briefs and search for creators; and both sides can message, negotiate terms and generate deal summaries and receipts.

> **Prototype notice:** Collably is a front-end-only demo. All data is stored in the browser (`localStorage`). There is no backend, no real AI service, no real messaging and no real payments.

---

## Features

### For creators
- Sign up and build a profile: headline, category, location, bio, starting rate, experience, audience size, engagement rate, skills, portfolio links, past work and testimonials
- Profile strength meter and rule-based profile improvement tips
- Discover brands by search and category
- Explore other creators' public profiles
- Connect with brands, negotiate and track deals

### For brands
- Sign up and set up a company profile: category, business type, location, website, about, typical budget, target audience and campaign goals
- Discover creators with search, category, budget and minimum-rating filters
- Ranked creator recommendations with a match score and match notes
- Create and save campaign briefs (name, category, budget, brief, deadline, style, usage requirements)
- Invite creators, message them and negotiate terms

### Shared
- **Messages & negotiation:** per-connection chat, editable proposal (budget, deliverables, deadline, usage/payment terms) and rule-based suggested terms
- **Deals & receipts:** deal summary, simulated payment and a printable receipt
- **Sample workspaces:** one-click demo creator and brand accounts
- Responsive layout for desktop and mobile

---

## Tech Stack

- Plain **HTML, CSS and JavaScript** in a single file (`Index.html`)
- No frameworks, no build step, no dependencies
- Browser `localStorage` for persistence

---

## Getting Started

1. Clone the repository:
   ```bash
   git clone <your-repo-url>
   cd <your-repo-name>
   ```
2. Open `Index.html` in a browser, or serve it locally:
   ```bash
   python -m http.server 8000
   ```
   Then visit `http://localhost:8000/Index.html`.
3. On the landing page, choose **Join as a creator** or **Join as a brand**, or use the **sample workspace** buttons on the sign-up screen to explore instantly.

---

## How It Works

### Matching
Brands see creators ranked by an illustrative, rule-based score (not a machine-learning model):

| Signal | Effect |
|---|---|
| Base score | 40 |
| Same category as the brand | +28 (+20 for a case-insensitive match) |
| Creator rate within brand budget | +20 (partial credit when slightly above) |
| Public rating 4.7+ / 4.0+ | +8 / +5 |
| Has portfolio links | +4 |

Scores are clamped between 35 and 99, and each card shows the reasons behind its score.

### Search & filtering
- **Creators:** free-text search (name, headline, category, location, bio, skills, portfolio), category, maximum budget and minimum rating
- **Brands:** free-text search and category
- When nothing matches, an empty state suggests broadening the search

### Negotiation & deals
1. A brand invites a creator (or a creator connects with a brand), which creates a connection
2. Both sides chat and save a proposal (budget, deliverables, deadline, usage rights)
3. **Suggest negotiation terms** fills in a starting point based on the creator's rate, the brand's budget and the category
4. **Create deal summary** turns the proposal into a draft agreement
5. **Record simulated payment** generates a demo receipt number and receipt

---

## Data Model

Data is stored as JSON in these `localStorage` keys:

| Key | Contents |
|---|---|
| `collably_v3_users` | Accounts (creator and brand profiles) |
| `collably_v3_session` | Current logged-in session |
| `collably_v3_connections` | Brand-creator conversations and proposal terms |
| `collably_v3_deals` | Deal summaries and simulated receipts |
| `collably_v3_campaigns` | Brand campaign briefs |

### Account
```text
Account
├── key, email, password, role (creator | brand)
├── demoAccount (boolean, sample accounts only)
├── createdAt
└── profile -> CreatorProfile | BrandProfile
```

### Creator profile
```text
CreatorProfile
├── name, mobile, headline, category, location, bio
├── budget (starting rate in INR), experience
├── audience, engagement (%)
├── skills            (comma-separated)
├── portfolio         (one per line: title | description | url)
├── work              (past collaborations)
├── reviews           (one testimonial per line)
└── setupComplete, updatedAt
```

### Brand profile
```text
BrandProfile
├── name, mobile, category, branch, location, website
├── description, audience, goals
├── budget (typical campaign budget in INR)
└── setupComplete, updatedAt
```

### Campaign brief
```text
Campaign
├── id, brandKey, name, category, budget
├── brief, deadline, style, usage
└── status (Draft), createdAt
```

### Connection
```text
Connection
├── id, brandKey, creatorKey, brandName, creatorName, category
├── status, lastMessage
├── messages[]  (from, text, at)
└── terms       (budget, deliverables, deadline, usage)
```

### Deal
```text
Deal
├── id, connectionId, creatorKey, brandKey, creatorName, brandName
├── category, budget, deliverables, deadline, usage
├── status, paymentStatus
└── receipt     (number, at, amount, method)
```

Built-in sample data includes 4 demo creators and 4 demo brands across Fashion, Beauty, Travel and Food, and 15 selectable categories.

---

## Project Structure

```text
.
├── Index.html   # The entire app: markup, styles and scripts
└── README.md
```

---

## Limitations

- Accounts and passwords are stored unencrypted in the browser. **Do not use a real or reused password.**
- Data lives only in the current browser, so it is not shared between users or devices.
- Match scores, profile tips and suggested terms are rule-based, not a live AI model.
- Reviews and testimonials are entered manually and are not verified.
- Payments and receipts are simulated. No money moves and no receipt is legally valid.
- Deal summaries are not legal contracts.

---

## Roadmap Ideas

- Real backend with authentication and a database
- AI-specific creator fields: tools/models used, workflow notes, content type and aspect ratio
- Commercial-use and licensing fields on briefs and portfolio items
- Creator verification signals for tools, workflows and past work
- AI-assisted brief builder
- Real messaging, notifications and payment gateway integration

---

## Demo

- Live site: `<add link>`
- Demo video / slides: `<add link>`

## Team

- Smit - `<add role>`
- `<add teammates>`

## License

`<add license>`

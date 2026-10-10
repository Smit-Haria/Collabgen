# AI Content Creator Marketplace

An AI-native marketplace that connects **AI creators** (AI filmmakers, animators, generative artists) with **brands and creative agencies**. Brands can discover creators with proven AI-production skills, publish structured creative briefs, and evaluate AI-specific portfolios, including the tools, models and workflows behind each piece of work.

---

## Overview

Generative AI has created a new class of creative professionals, but traditional freelance marketplaces aren't built for them. Brands struggle to:

- Verify what a creator can actually do with AI tools
- Understand the tools, models and workflows behind generated content
- Manage licensing and commercial-use requirements
- Collaborate through multiple generations and revisions

This platform solves that by putting **tools, workflows, formats and commercial-use terms** at the centre of both creator profiles and brand briefs.

---

## Features

### Core
| Feature | Description |
|---|---|
| **Creator Profiles & AI Portfolios** | Showcase AI-generated videos, animations and graphics along with tools/models used, skills, specialization and workflow notes |
| **Brand / Agency Briefs** | Define campaign requirements, content type, style, format / aspect ratio and commercial-use needs |
| **Creator Search & Filtering** | Filter by skills, specialization, tools, content type and other profile attributes, with a helpful empty-results state |

### Bonus
| Feature | Description |
|---|---|
| **Creator Verification Signals** | Visible trust badges for verified tools, documented workflows and past work |
| **AI-Assisted Brief Builder** | Turns a rough idea into a complete, structured creative brief |

---

## User Flows

**Brand / Agency**
1. Browse or search creators -> apply filters -> open a creator profile
2. View the AI portfolio (work, tools, workflow, verification badges)
3. Create a brief (manually or with the AI Brief Builder)
4. Engage a creator from discovery through delivery

**Creator**
1. Create a profile (skills, specialization, tools)
2. Add portfolio items with tool/model and workflow details
3. Earn verification signals
4. Discover and respond to briefs

---

## Data Model

### Creator Profile
```text
CreatorProfile
├── id
├── name, avatar, bio, location
├── specialization        (e.g. AI Filmmaking, AI Animation, Generative Graphics)
├── skills[]              (e.g. prompt engineering, motion design, video editing)
├── tools[]               (e.g. Runway, Midjourney, Sora, Veo, ComfyUI)
├── content_types[]       (video, animation, image, audio, ...)
├── workflow_summary
├── portfolio[]           -> PortfolioItem
├── verification          -> VerificationSignals
└── availability, rates (optional)
```

### Portfolio Item
```text
PortfolioItem
├── id, title, description
├── media_url, thumbnail_url
├── content_type          (video | animation | graphic | ...)
├── format / aspect_ratio (16:9, 9:16, 1:1, ...)
├── tools_models[]        (tool + model/version used)
├── workflow_steps[]      (e.g. concept -> generation -> upscaling -> edit)
├── prompts / process_notes (optional)
└── commercial_use_status (cleared | restricted | personal-only)
```

### Verification Signals (Bonus)
```text
VerificationSignals
├── verified_tools[]      (tools the creator has proven they use)
├── workflow_documented   (boolean)
└── past_work_verified    (boolean / count)
```

### Creative Brief
```text
Brief
├── id, brand_id
├── title, description
├── campaign_goal
├── content_type          (video | animation | image | ...)
├── style                 (cinematic, minimal, retro, ...)
├── format / aspect_ratio (16:9, 9:16, 1:1, ...)
├── required_skills[]
├── preferred_tools[]
├── commercial_use        -> CommercialUse
├── budget, timeline
└── status                (draft | published | in-progress | delivered)
```

### Commercial Use
```text
CommercialUse
├── usage_type            (organic social | paid ads | broadcast | internal)
├── territory
├── duration
├── exclusivity           (boolean)
└── ai_disclosure_required (boolean)
```

---

## Search & Filtering

Creators can be filtered by any combination of:

- Skills
- Specialization
- Tools / models
- Content type
- Verification status
- Other profile attributes

Filters combine to narrow results. When nothing matches, the UI shows a clear **empty state** with suggestions (remove a filter, broaden search) instead of a blank page.

---

## Getting Started

> Update the commands below to match your stack.

```bash
# clone the repository
git clone <your-repo-url>
cd <your-repo-name>

# install dependencies
npm install

# run the development server
npm run dev
```

Then open `http://localhost:3000` (or the port your app uses).

---

## Project Structure

> Replace with your actual folder layout.

```text
.
├── src/
│   ├── components/     # UI components (profile cards, filters, brief form)
│   ├── pages/          # Creator list, creator profile, brief create/view
│   ├── data/           # Sample creators, portfolios and briefs
│   └── utils/          # Search / filter logic, brief builder
├── public/
└── README.md
```

---

## Evaluation Mapping

| Criterion | Weight | Where it's addressed |
|---|---|---|
| Creator Profiles & AI Portfolios | 30% | Rich profiles, portfolio items with tools/workflows, verification signals |
| Brief Definition | 20% | Structured brief with content type, style, aspect ratio, commercial use, AI Brief Builder |
| Discovery & Filtering | 25% | Multi-attribute search and filters, empty-state handling |
| User Experience | 15% | Simple creator and brand flows, clear portfolio viewing |
| Presentation & Demo | 10% | Working prototype plus short demo / slides |

---

## Demo

- Live site: `<add link>`
- Demo video / slides: `<add link>`

---

## Team

- Smit - `<add role>`
- `<add teammates>`

---

## License

`<add license>`

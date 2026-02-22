# PROJECT_CONTEXT.md — Read This First

> **For any AI assistant continuing work on this project: read this file completely before making any changes or additions.**

---

## Project Overview

**Name:** Global AI Acceptance Index
**Repo:** https://github.com/Die-Hu/Global-AI-Acceptance-Index
**Live Demo:** https://die-hu.github.io/Global-AI-Acceptance-Index/
**Owner:** Die-Hu
**Working Directory:** `/Users/leo/Documents/AIearth/`
**License:** MIT

A single-page interactive data visualization (D3.js + HTML) that maps AI acceptance and high-tech adoption across 121 countries using data from 46 sources. The project also functions as an open research foundation, with a particular focus on the US paradox — why the global AI leader has one of the lowest public acceptance scores.

---

## Strategic Context

This project serves a dual purpose:

1. **Open-source research tool** — a credible, data-driven visualization of global AI attitudes
2. **NIW (National Interest Waiver) foundation** — the project and its research declaration (`DECLARATION.md`) are designed to demonstrate contributions to an area of national importance (US AI competitiveness and public trust). The tone is academic and understated — it should never read as promotional or immigration-motivated.

**Key NIW-relevant data point:** The US scores 36/100 in AI acceptance despite 90/100 in high-tech adoption and $109.1B in private AI investment (2024). This is validated by 5 independent, high-confidence sources (Pew N=3605, Ipsos N=1000, Edelman N=1000, World Risk Poll N=1000).

---

## File Structure

```
/Users/leo/Documents/AIearth/
├── index.html                  # Main visualization (124KB, self-contained)
│                                 - D3.js v7 orthographic globe
│                                 - All 121 country data embedded as JS
│                                 - Responsive: desktop / tablet / mobile
│                                 - Sections: Hero, Globe, Data Panel, Insights,
│                                   Methodology, Source Tiers, Analysis Charts,
│                                   Rankings Table, Footer
│                                 - Features: drag/touch rotation, auto-rotate,
│                                   zoom, region nav, dual mode toggle,
│                                   scatter plot, bar chart, donut chart,
│                                   sortable/searchable table
│
├── preview.png                 # Screenshot for README (4.3MB)
├── README.md                   # Project documentation with badges, features,
│                                 data sources table, methodology, data structure,
│                                 project structure, tech stack, getting started,
│                                 data quality, research context, contributing
├── DECLARATION.md              # Research declaration (NIW-aligned)
│                                 - US paradox analysis with specific data
│                                 - Future research directions (6 areas)
│                                 - Collaboration invitation
├── LICENSE                     # MIT, 2026, Die-Hu
├── CONTRIBUTING.md             # Contribution guidelines
├── DATA_DICTIONARY.md          # Field definitions, confidence levels,
│                                 source credibility tiers, weighted average formula
├── PROJECT_CONTEXT.md          # THIS FILE
│
├── data/
│   ├── ai_acceptance_by_country.json   # FINAL dataset (121 countries, 84KB)
│   │                                     Enhanced format with: data_sources[],
│   │                                     breakdown{positive,negative,neutral},
│   │                                     confidence, is_estimated, year
│   ├── validation_report.json          # Data validation results (43KB)
│   │                                     Cross-validation, anomaly detection,
│   │                                     source credibility assessment
│   └── raw/
│       ├── survey_institutions.json    # Ipsos, Pew, Edelman, WEF, etc. (32KB)
│       ├── readiness_indices.json      # Oxford, Stanford HAI, IMD, etc. (31KB)
│       ├── enterprise_adoption.json    # McKinsey, Microsoft, IBM, etc. (16KB)
│       └── supplementary_countries.json # 70 additional countries (33KB)
```

---

## Data Architecture

### Final Dataset Schema (`data/ai_acceptance_by_country.json`)

```json
{
  "metadata": {
    "total_countries": 121,
    "methodology": "Weighted average (credibility x recency)",
    "lastUpdated": "2026-02-21"
  },
  "data": [{
    "country": "United States",
    "iso_a3": "USA",
    "ai_acceptance_score": 36,      // 0-100, weighted composite
    "high_tech_adoption": 90,       // 0-100, infrastructure/readiness
    "confidence": "high",           // high | medium | low
    "data_sources": [{              // all contributing sources
      "source": "Pew Research Center 2025",
      "value": 38,
      "weight": 0.283,
      "methodology": "Online panel, N=3605, nationally representative",
      "survey_question": "More excited vs more concerned about increased AI use"
    }],
    "breakdown": { "positive": 34, "negative": 64, "neutral": 2 },
    "year": 2025,
    "is_estimated": false
  }]
}
```

### Weighting System
- **Source credibility:** Very High (1.0) = Pew, Stanford HAI, ITU; High (0.85) = Ipsos, Oxford, IMD; Medium-High (0.7) = Edelman, McKinsey
- **Recency:** 2025=1.0, 2024=0.9, 2023=0.7, 2021=0.35
- **Confidence levels:** High = direct survey data; Medium = single source or partial data; Low = estimated from regional patterns

### Data Coverage
- 32 countries: high confidence (direct multi-source survey data)
- 33 countries: medium confidence
- 56 countries: low confidence (estimated)
- 36 countries with measured data, 85 estimated

---

## Tech Stack

- **D3.js v7** via CDN — globe, charts, all visualization
- **TopoJSON v3** via CDN — world-atlas@2/countries-110m.json
- **Google Fonts** — Inter typeface
- **Vanilla HTML/CSS/JS** — no build tools, no framework
- Single self-contained HTML file (all data embedded inline)

---

## Key Design Decisions

1. **Single HTML file** — no server needed, works as static GitHub Pages site
2. **Data embedded in JS** — avoids CORS/fetch issues for local use
3. **ISO alpha-3 codes** — used for country matching against topojson numeric IDs (mapping table included in JS)
4. **Responsive CSS Grid** — desktop sidebar layout collapses to stacked on tablet/mobile
5. **Dark theme** — deep navy with cyan/blue accents, glassmorphism cards
6. **All English** — content switched from Chinese in earlier version

---

## Git History

```
cdece89 Add project preview and research declaration
e2860a7 Fix author attribution and refine content
614a385 Initial release: Global AI Acceptance Index — 121 countries, 46 data sources
```

Author: Die-Hu <2015484859@qq.com>
Git config (local): user.name = "Die-Hu"

---

## What NOT To Do

- Do NOT add "Co-Authored-By: Claude" or any AI attribution to commits
- Do NOT reference "xiaoliddiao" anywhere — that was an old account name, fully removed
- Do NOT make the NIW angle obvious — keep academic/research tone
- Do NOT delete or reduce data coverage — the 121 countries and 46 sources are core value
- Do NOT add unnecessary AI buzzwords or promotional language
- Do NOT change the git user config

---

## Potential Future Work

1. **Deeper US analysis** — media framing, demographic disaggregation, longitudinal tracking
2. **More countries** — currently 121, could expand with new survey data
3. **Time series** — track acceptance changes year over year as new surveys publish
4. **Academic paper** — formalize findings for publication
5. **Additional visualizations** — Sankey diagrams, correlation matrices, regression analysis
6. **Performance** — optimize the 124KB HTML file (lazy-load charts, compress data)
7. **Preview image** — current preview.png is 4.3MB, could compress for faster README loading
8. **i18n** — add Chinese or other language toggle if needed

---

*Last updated: 2026-02-21*

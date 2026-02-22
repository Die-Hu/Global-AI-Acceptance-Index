# :globe_with_meridians: Global AI Acceptance Index

[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen?style=flat-square)](https://die-hu.github.io/Global-AI-Acceptance-Index/)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](#license)
[![Countries](https://img.shields.io/badge/countries-121-orange?style=flat-square)](#)
[![Data Sources](https://img.shields.io/badge/data%20sources-46-purple?style=flat-square)](#data-sources)

An interactive data visualization exploring global attitudes toward artificial intelligence across **121 countries**, compiled from **46 data sources** including surveys, government readiness indices, and enterprise adoption reports.

![Preview](preview.png)

**[View Live Demo](https://die-hu.github.io/Global-AI-Acceptance-Index/)**

---

## Features

- **Interactive 3D Globe** -- drag to rotate, scroll to zoom, touch-enabled for mobile
- **Dual Visualization Modes** -- switch between AI Acceptance scores and High-Tech Adoption rates
- **Region Quick-Navigation** -- jump to Asia, Europe, Americas, Africa, or the Middle East
- **Country Detail Panel** -- per-country breakdown with source citations and methodology notes
- **Analytical Views** -- regional comparison charts, scatter plots, and ranking tables
- **Fully Responsive** -- optimized for desktop, tablet, and mobile
- **Weighted Scoring** -- transparent methodology with source credibility tiers and confidence levels

---

## Data Sources

Data is drawn from 46 sources across four categories:

| Category | Sources |
|---|---|
| **Survey Institutions** | Ipsos AI Monitor 2024, Pew Research Center 2025, Edelman Trust Barometer 2025, Lloyd's Register Foundation World Risk Poll 2021, Standard Insights SE Asia Survey 2024 |
| **Readiness Indices** | Oxford Insights Gov AI Readiness 2024/2025, Stanford HAI Global AI Vibrancy 2025, IMD World Digital Competitiveness 2024, ITU ICT Development Index 2024, Tortoise Media Global AI Index 2024 |
| **Enterprise Reports** | McKinsey, Microsoft, IBM, Salesforce, Deloitte, KPMG |
| **Regional Surveys** | Eurobarometer 554, Afrobarometer, Arab Barometer, ILIA 2024, Asian Barometer |

---

## Methodology

Each country's AI Acceptance Score is computed as a **weighted average** across all available data points. Weights are determined by two factors:

1. **Source Credibility Tier**

   | Tier | Weight | Examples |
   |---|---|---|
   | Very High | 1.0 | Pew Research, Stanford HAI, ITU |
   | High | 0.85 | Ipsos, Oxford Insights, IMD |
   | Medium-High | 0.7 | Edelman, McKinsey |

2. **Recency** -- 2025 data receives full weight (1.0), 2024 data is weighted at 0.9, 2023 at 0.7, and older data is progressively discounted (e.g., 2021 = 0.35).

Countries with direct survey data from Pew, Ipsos, or Edelman are marked **confidence: high**. Countries estimated from readiness indices and regional patterns are marked **confidence: low**.

---

## Data Structure

The primary dataset is `data/ai_acceptance_by_country.json`. Each country entry follows this schema:

```json
{
  "country": "China",
  "iso_a3": "CHN",
  "ai_acceptance_score": 82,
  "high_tech_adoption": 64,
  "confidence": "high",
  "data_sources": [
    {
      "source": "Ipsos AI Monitor 2024",
      "value": 80,
      "weight": 0.343,
      "methodology": "Online survey, N=1000, Global Advisor platform",
      "survey_question": "I am excited about products and services that use AI"
    }
  ],
  "breakdown": { "positive": 76, "negative": 24, "neutral": 0 },
  "year": 2025,
  "is_estimated": false
}
```

---

## Project Structure

```
Global-AI-Acceptance-Index/
├── index.html                              # Single-page application (HTML + CSS + JS)
├── data/
│   ├── ai_acceptance_by_country.json       # Compiled dataset (121 countries)
│   ├── validation_report.json              # Data validation results
│   └── raw/
│       ├── survey_institutions.json        # Ipsos, Pew, Edelman, etc.
│       ├── readiness_indices.json          # Oxford, Stanford, IMD, ITU
│       ├── enterprise_adoption.json        # McKinsey, Microsoft, IBM, etc.
│       └── supplementary_countries.json    # Additional country estimates
├── README.md
└── LICENSE
```

---

## Tech Stack

- **[D3.js](https://d3js.org/) v7** -- globe rendering, choropleth maps, charts
- **[TopoJSON](https://github.com/topojson/topojson)** -- efficient geographic data
- **HTML5 / CSS3** -- glassmorphism UI, CSS Grid, custom properties
- **Vanilla JavaScript** -- no build step, no framework dependencies

---

## Getting Started

No build tools required. Choose one:

**Option A -- View online:**
Visit the **[Live Demo](https://die-hu.github.io/Global-AI-Acceptance-Index/)**

**Option B -- Run locally:**
```bash
git clone https://github.com/die-hu/Global-AI-Acceptance-Index.git
cd Global-AI-Acceptance-Index
# Open index.html in your browser, or start a local server:
python3 -m http.server 8000
```

Then open `http://localhost:8000` in your browser.

---

## Data Quality

Each country is assigned a confidence level:

| Confidence | Criteria | Example Countries |
|---|---|---|
| **High** | Direct survey data from Pew, Ipsos, or Edelman | USA, China, Germany, India |
| **Medium** | Data from readiness indices with partial survey coverage | Chile, Czech Republic, Estonia |
| **Low** | Estimated from regional patterns and readiness indices | Many African and Central Asian nations |

Some data points carry additional flags:
- **Historical baseline** -- data from 2021 or earlier (pre-ChatGPT era), weighted lower
- **Projected** -- forward-looking estimates (e.g., KPMG Q4 2026), flagged accordingly

---

## Contributing

Contributions are welcome. Some ways to help:

1. **Add or update data sources** -- submit new surveys or reports with citations
2. **Improve country coverage** -- fill gaps in underrepresented regions
3. **Fix bugs** -- report issues or submit pull requests
4. **Enhance visualizations** -- propose new chart types or interaction patterns

Please open an issue before starting significant work so we can discuss the approach.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Acknowledgments

This project would not be possible without the following organizations and their publicly available research:

- **Pew Research Center** -- cross-national AI attitudes surveys
- **Ipsos** -- AI Monitor global tracking study
- **Stanford HAI** -- AI Vibrancy Tool and AI Index Report
- **Oxford Insights** -- Government AI Readiness Index
- **IMD** -- World Digital Competitiveness Ranking
- **ITU** -- ICT Development Index
- **Edelman** -- Trust Barometer
- **Tortoise Media** -- Global AI Index
- **Eurobarometer, Afrobarometer, Arab Barometer, ILIA** -- regional survey programs

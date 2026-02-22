# Data Dictionary

This document describes every field in `data/ai_acceptance_by_country.json`.

## Top-Level Structure

| Field | Type | Description |
|-------|------|-------------|
| `metadata` | object | Dataset-level information (sources, methodology, notes) |
| `data` | array | Array of country-level records |

## metadata

| Field | Type | Description |
|-------|------|-------------|
| `description` | string | Brief summary of the dataset |
| `sources` | string[] | List of all survey and index sources used across the dataset |
| `methodology` | string | Explanation of how weighted averages are computed |
| `lastUpdated` | string (date) | ISO 8601 date when the dataset was last refreshed |
| `total_countries` | integer | Number of country records in the `data` array |
| `data_quality_note` | string | Notes on confidence levels, historical baselines, and data cleaning |
| `validation_applied` | string[] | List of validation and cleaning steps applied to the data |

## data (country records)

Each element in the `data` array represents one country.

| Field | Type | Range / Values | Description |
|-------|------|----------------|-------------|
| `country` | string | -- | Common English name of the country |
| `iso_a3` | string | 3-letter code | ISO 3166-1 alpha-3 country code |
| `ai_acceptance_score` | integer | 0 -- 100 | Weighted composite score reflecting public acceptance of AI. Higher means more positive sentiment. |
| `high_tech_adoption` | integer | 0 -- 100 | Composite score for high-tech infrastructure and adoption (internet penetration, cloud usage, digital competitiveness). |
| `confidence` | string | `"high"`, `"medium"`, `"low"` | Confidence in the data point (see Confidence Levels below) |
| `data_sources` | array | -- | Individual survey/index data points that feed into the composite score |
| `breakdown` | object | -- | Sentiment breakdown (see below) |
| `year` | integer | e.g. 2024, 2025 | Primary reference year for the data |
| `is_estimated` | boolean | `true` / `false` | Whether the score was estimated from regional patterns or readiness indices rather than direct survey data |

## data_sources (per country)

Each entry in `data_sources` represents one survey or index contributing to the country's composite score.

| Field | Type | Description |
|-------|------|-------------|
| `source` | string | Name and year of the survey or index |
| `value` | number | The raw score or percentage from this source (0--100) |
| `weight` | number | Weight assigned to this source in the composite calculation (0.0--1.0). Weights within a country sum to 1.0. |
| `methodology` | string | How the data was collected (e.g. survey mode, sample size) |
| `survey_question` | string | The survey question or metric measured |

## breakdown

Sentiment breakdown for each country. Values are percentages that sum to 100.

| Field | Type | Description |
|-------|------|-------------|
| `positive` | integer | Percentage of respondents with positive sentiment toward AI |
| `negative` | integer | Percentage of respondents with negative sentiment toward AI |
| `neutral` | integer | Percentage of respondents with neutral sentiment toward AI |

## Confidence Levels

| Level | Meaning |
|-------|---------|
| `high` | Based on direct survey data from major polling organizations (Pew, Ipsos, Edelman) with nationally representative samples |
| `medium` | Based on a single high-quality source or a combination of readiness indices and partial survey data |
| `low` | Estimated from regional patterns, readiness indices, or older (pre-2023) survey data with no recent direct polling |

## Source Credibility Tiers

Sources are assigned credibility weights used in the composite calculation:

| Tier | Weight | Sources |
|------|--------|---------|
| Very High | 1.0 | Pew Research Center, Stanford HAI, ITU |
| High | 0.85 | Ipsos, Oxford Insights, IMD |
| Medium-High | 0.7 | Edelman, McKinsey |

## Weighted Average Computation

The `ai_acceptance_score` for each country is computed as follows:

1. Each data source's raw `value` is multiplied by a weight that combines **source credibility** and **recency** (2025 = 1.0, 2024 = 0.9, 2023 = 0.7, 2021 = 0.35).
2. The per-source weights are normalized so they sum to 1.0 within each country.
3. The final score is the weighted sum: `score = sum(value_i * weight_i)` across all sources for that country, rounded to the nearest integer.

![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Assessment | Pre-Flight Check — Define Your Weather Prediction Problem

## Overview

This assessment is the launchpad for your mid-course project: **Weather Intelligence Pipeline — Can We Trust This Data?** Starting next week you will spend two weeks building an end-to-end pipeline that ingests weather data, evaluates its quality, and delivers a prediction that goes beyond a standard 7-day forecast. Today you define what that prediction will be, get your hands on the data, and build a first quick model to test whether your idea is feasible.

## Learning Goals

- Define a clear, scoped prediction problem grounded in real weather data.
- Fetch and inspect data from the Open-Meteo historical and forecast APIs.
- Apply the supervised learning skills from Unit 4.1 to build quick baseline models.
- Evaluate whether the data and approach can support your chosen question.

## Prerequisites

- Python 3.9+
- Libraries: pandas, numpy, matplotlib, seaborn, scikit-learn, requests

```bash
pip install pandas numpy matplotlib seaborn scikit-learn requests
```

## Requirements

1. **Fork** this repository to your own GitHub account.
2. **Clone** the fork to your local machine.
3. Work in a single Jupyter Notebook called **`m4-05-assessment.ipynb`**.
4. **Commit regularly** — your commit history should show incremental progress.

## Tasks

### Task 1 — Define Your Prediction Problem

Discuss with your team and choose a research direction. Your prediction must go **beyond a standard weather forecast** — it should answer a question that a regular 7-day forecast does not.

#### Suggested directions

| Direction | Example questions |
|-----------|-------------------|
| **Long-term statistical prediction** | Will May be rainier than the climate norm? Will the majority of July days be above 25 °C? What is the probability that average summer temperature exceeds the 10-year mean? Report results with **confidence intervals** or **probabilities** — think **monthly or seasonal** questions, not next-Tuesday questions. |
| **Spatial refinement** | Take an existing city-scale 7-day forecast and refine it for a **specific location** — a rural area, a particular agricultural field, your neighbourhood — using interpolation, elevation adjustments, or local correction factors. |

Your team may also propose a different direction, as long as it goes beyond what a standard forecast already provides.

In a markdown cell, write:

1. **Problem statement** — One or two sentences describing the question you will answer.
2. **Why it matters** — Who would use this prediction and for what? (e.g., a tea farmer in Lankaran planning irrigation, an energy company forecasting summer demand.)
3. **Prediction target** — What exactly will your model predict? (e.g., "Monthly average temperature for June 2025 in Baku", "Daily precipitation probability for a specific rural coordinate".)
4. **Cities / locations** — List at least 3 cities (coordinates) you plan to use. At least one should be in Azerbaijan.
5. **Weather variables** — List at least 6 daily variables you will fetch (e.g., `temperature_2m_max`, `precipitation_sum`, `windspeed_10m_max`).

### Task 2 — Initial Data Inspection

Fetch sample data from both Open-Meteo endpoints and load it into pandas DataFrames.

**No API key is needed.** Open-Meteo is free and open.

1. **Historical data.** For one of your chosen cities, fetch at least 2 full years of daily data from the archive endpoint. Load the JSON response into a DataFrame. Report: shape, column names, data types, date range, and a quick check for missing values.

   ```
   https://archive-api.open-meteo.com/v1/archive?latitude=40.41&longitude=49.87&start_date=2022-01-01&end_date=2024-12-31&daily=temperature_2m_max,temperature_2m_min,precipitation_sum,windspeed_10m_max
   ```

2. **Forecast data.** For the same city, fetch the current 7-day forecast from the forecast endpoint. Load it into a DataFrame. Report the same summary.

   ```
   https://api.open-meteo.com/v1/forecast?latitude=40.41&longitude=49.87&daily=temperature_2m_max,temperature_2m_min,precipitation_sum,windspeed_10m_max
   ```

3. **Quick visualisation.** Plot at least one time-series chart from the historical data (e.g., daily max temperature over 2 years) and note any visible gaps, outliers, or seasonal patterns.

4. **Data quality notes.** In a markdown cell, list any issues you noticed (missing rows, suspicious values, gaps) and how they might affect your project.

### Task 3 — Baseline Model Experiment

Using the historical data from Task 2, build one or two quick models to test whether your prediction idea is feasible. Apply the supervised learning workflow from Unit 4.1.

1. **Create a simple target variable** related to your problem statement. For example:
   - Binary: "Was this day above the monthly climate average?" (classification)
   - Continuous: "Next-day maximum temperature" (regression)
   - Choose whatever makes sense for your direction — this is an experiment, not a final model.

2. **Feature engineering (minimal).** Create at least 2–3 simple features from the raw data (e.g., rolling averages, month indicator, lag features).

3. **Train at least two models.** Use a train/test split (`random_state=42`). Suggested models:
   - `LogisticRegression` or `LinearRegression` (depending on your target)
   - `RandomForestClassifier` or `RandomForestRegressor`

4. **Evaluate.** Report appropriate metrics (accuracy/F1 for classification, RMSE/R² for regression). Create a short comparison table.

5. **Feasibility verdict.** In a markdown cell, answer:
   - Do the results suggest your prediction idea is feasible?
   - What would you need to improve in the full project? (more data, more features, better cleaning, different model?)
   - Any changes to your problem statement based on what you learned?

## Submission

### What to submit

- `m4-05-assessment.ipynb` — your completed notebook with all code, outputs, and written analysis.

### Definition of done (checklist)

- [ ] Problem statement is clearly written with prediction target, cities, and variables.
- [ ] Historical and forecast data are fetched and loaded into DataFrames with summary stats.
- [ ] At least one visualisation of the historical data.
- [ ] Data quality issues are documented.
- [ ] At least two models are trained and evaluated with a comparison table.
- [ ] A feasibility verdict explains whether the idea works and what needs improvement.
- [ ] Commit history shows incremental progress.
- [ ] The notebook runs top-to-bottom without errors (`Kernel → Restart & Run All`).

### How to submit (Git workflow)

```bash
git add .
git commit -m "assessment: pre-flight check — problem definition and baseline models"
git push origin main
```

Then open a **Pull Request** on the original repository with a brief description of your work.

## Evaluation Criteria

| Criterion | Weight | Description |
|---|---|---|
| Problem Definition | 50% | Clear, specific problem statement that goes beyond standard forecasts; well-chosen cities, variables, and prediction target |
| Data Inspection | 20% | Both endpoints fetched and loaded correctly; summary stats reported; quality issues identified; at least one visualisation |
| Baseline Models | 20% | At least two models trained with proper train/test split; appropriate metrics; honest feasibility assessment |
| Communication & Code Quality | 10% | Clear markdown explanations at each step; clean code; notebook runs without errors; regular commits |

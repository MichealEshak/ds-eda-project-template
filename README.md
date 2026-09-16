# King County Housing EDA — Buyer Recommendation for Thomas Hansen

An exploratory data analysis (EDA) of King County (Seattle, USA) home sales, built to answer three concrete questions for a fictional home buyer, **Thomas Hansen**: can he afford a home big enough for his family, which neighborhood fits him best, and when should he buy.

> This repository started from the [`ds-eda-project-template`](https://github.com/neuefische/ds-eda-project-template). The original template instructions (learning objectives, generic setup walkthrough) have been kept at [**TEMPLATE_README.md**](TEMPLATE_README.md). This file replaces it as the map of the finished project.

## Client brief

| | |
|---|---|
| **Client** | Thomas Hansen (buyer, fictional) |
| **Household** | 5 kids — needs ≥ 4 bedrooms |
| **Budget** | "No money" — capped at the 25th percentile of all sale prices |
| **Wants** | A "nice" (above-average condition/grade), socially dense (family-friendly) neighborhood |
| **Open questions** | Best **location** and best **timing** to buy |

## Repository contents

Work through the analysis in this order:

| File | Description |
| --- | --- |
| [**01_assignment.md**](01_assignment.md) | The original project brief: dataset, tasks, deliverables, and the client roster this project's client (Thomas Hansen) was chosen from. |
| [**02_workflow.md**](02_workflow.md) | The recommended EDA workflow this analysis follows: understand → question → clean → explore relationships → present. |
| [**03_fetching_the_data_eda.ipynb**](03_fetching_the_data_eda.ipynb) | Connects to the PostgreSQL `eda` schema (psycopg2 / SQLAlchemy), joins the house-details and sale-price/date tables, and exports the combined dataset to `data/eda.csv`. |
| [**04_eda.ipynb**](04_eda.ipynb) | The main analysis notebook: data overview and cleaning, three research hypotheses, and the insights/recommendations for Thomas Hansen. See [Analysis walkthrough](#analysis-walkthrough) below. |
| [**column_names.md**](column_names.md) | Data dictionary describing every column in the King County housing dataset. |

### Supporting files

| File / Folder | Description |
| --- | --- |
| [**data/**](data/) | Holds `eda.csv`, the dataset exported by notebook 03. Tracked as a folder, but the CSV itself is git-ignored — re-run notebook 03 to regenerate it. |
| [**.env.example**](.env.example) | Template for the database credentials. Copy to `.env` and fill in your own values (see [Setup](#setup)). |
| [**pyproject.toml**](pyproject.toml) / [**uv.lock**](uv.lock) | Project dependencies, managed with [`uv`](https://docs.astral.sh/uv/). |
| [**TEMPLATE_README.md**](TEMPLATE_README.md) | The original template README: full step-by-step repo/environment setup instructions and learning objectives. Kept for reference. |
| [**presentation/**](presentation/) | The 10-minute, non-technical slide deck for Thomas Hansen: [Thomas_Hansen_Housing_Recommendation.pptx](presentation/Thomas_Hansen_Housing_Recommendation.pptx) and a [PDF export](presentation/Thomas_Hansen_Housing_Recommendation.pdf) of the same 11 slides. |

## Analysis walkthrough (`04_eda.ipynb`)

1. **Data overview & cleaning** — 21,597 sales, 21 columns, May 2014–May 2015, 70 zipcodes. Drops one 33-bedroom data-entry error and treats missing `waterfront` values as "not waterfront."
2. **Hypothesis 1 — Feasibility**: at Thomas's budget (≤ 25th percentile of price), are there enough 4+ bedroom homes? → Yes, over a thousand.
3. **Hypothesis 2 — Location**: which zipcode is both affordable/family-sized ("social" density) and "nice" (above-average condition/grade)? → **Zipcode 98023** is the 1st choice (strongest social density, lower avg price, better avg condition); **98092** is the 2nd choice / backup (marginally higher avg grade, but far fewer qualifying homes and pricier). Visualized on a geographic scatter plot with a colorblind-safe (blue/yellow) palette.
4. **Hypothesis 3 — Timing**: does price vary meaningfully by sale month? → Only ~8% swing across the year — location matters far more than timing, though December is marginally cheaper than November.
5. **Insights & recommendations** — the notebook closes with 3 insights and 3 client-facing recommendations for Thomas Hansen.

## Setup

> [!NOTE]
> Full step-by-step instructions (repo creation, collaborators, cloning, environment, credentials) live in [**TEMPLATE_README.md**](TEMPLATE_README.md). Quick version below.

```bash
git clone <this-repo-url>
cd ds-eda-project-template
uv sync                  # installs dependencies into .venv/
cp .env.example .env     # then fill in your DB credentials
```

Open the folder in VS Code (`code .`), open a notebook, and select the `uv`-managed Python environment as the kernel. Run notebook 03 first to populate `data/eda.csv`, then notebook 04.

## References & Further Reading

- [**House Sales in King County dataset**](https://www.kaggle.com/datasets/harlfoxem/housesalesprediction): The source dataset, with column descriptions and community notebooks.
- [**Pandas user guide**](https://pandas.pydata.org/docs/user_guide/index.html): The official guide to data manipulation with pandas.
- [**Seaborn tutorial**](https://seaborn.pydata.org/tutorial.html): Statistical data visualization in Python.
- [**SQLAlchemy documentation**](https://docs.sqlalchemy.org/en/20/): The database toolkit used to query PostgreSQL from Python.
- [**Hypothesis generation for EDA**](https://www.analyticsvidhya.com/blog/2020/11/an-efficient-way-of-performing-eda-hypothesis-generation/): How to form research questions and hypotheses before diving into the data.
- [**EDA Checklist**](https://github.com/neuefische/datascience-infographics/blob/main/EDA_Checklist.md): A phase-by-phase checklist for working through an exploratory analysis.
- [**Detailed EDA with Python**](https://www.kaggle.com/code/ekami66/detailed-exploratory-data-analysis-with-python): A worked example of a thorough EDA notebook on real data.
- [**Tips for data science presentations**](https://www.dataknowsall.com/storytelling.html): Storytelling techniques for presenting results to a non-technical audience.

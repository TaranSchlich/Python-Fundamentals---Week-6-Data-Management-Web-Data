# Sports Talent Analytics — Multi-Source Data Ingestion

A data-analysis notebook that pulls historic sports data from **four different source
types** into pandas DataFrames and answers concrete business questions for a fictional
sports-talent agency. Built in Google Colab for **GB885 — Python Fundamentals (Data
Management & Web Data)**.

**Author:** Taran Schlichtmann

---

## Business case

Jon Paul Sports Management Group (JPSMG) represents athletes with the support of
predictive modeling, and its model depends on aggressive data collection from many
sources. Acting as the firm's analyst, this notebook ingests data requested by four
internal teams, loads each source into a DataFrame, and answers the questions each team
needs to make decisions.

## Data sources — one per ingestion method

| Team | Source | Ingestion method |
|---|---|---|
| Olympic Account | `female_olympic_swimmers.csv` | Local file upload |
| Strategy | Ali-Ce `Athletes.csv` | Public GitHub raw URL |
| Basketball Account | nbaapi.com player totals | Live REST API (paginated) |
| Social Media | ESPN 2017 World Fame 100 | Kaggle API |

## Key findings

- **Olympic Account** — The USA produced the most female Olympic swimmers (2000–2016);
  Cierra Runge (193 cm, 2016 gold) is the tallest 2016 medalist and the recommended fit
  for a tall-women's swimwear endorsement.
- **Strategy** — Height and pay are essentially unrelated (r = −0.11); top earners cluster
  in a narrow ~5-year age band, and Boxing pays the most on average — recruit early and
  weight marketability over physical profile.
- **Basketball Account** — Across the full 2024 season, 6 players started all 82 games,
  and Daniel Gafford is the top *underused* defensive target (highest steals + blocks per
  game under 25 minutes) for value-driven contract negotiations.
- **Social Media** — Twitter following tracks endorsements most closely; Soccer leads in
  average total reach while Track and Field leads in average endorsements.

## Techniques demonstrated

- Reading data from a local upload, a GitHub-hosted CSV, a live REST API, and the Kaggle API
- Paginating a REST endpoint to assemble a complete dataset (the API caps each page at 50 rows)
- Cleaning and type-casting messy fields (stripping `$`/`,` from currency, handling nulls)
- Flattening nested JSON and engineering per-game features
- Answering questions with filtering, `groupby`, correlation, and interquartile range

## Repository structure

```
.
├── GB885_Assignment_6_Schlichtmann_T.ipynb   # the analysis notebook
├── README.md                                 # this file
└── .gitignore                                # excludes secrets and data files
```

## How to run

1. Open `GB885_Assignment_6_Schlichtmann_T.ipynb` in [Google Colab](https://colab.research.google.com/)
   (File → Upload notebook, or open it straight from GitHub).
2. Run the cells top to bottom (**Runtime → Run all**).
3. Two sections need a quick manual input; everything else loads automatically over the internet:
   - **Olympic section** — when `files.upload()` runs, upload `female_olympic_swimmers.csv`
     (provided in the course materials).
   - **Social Media section** — this uses the Kaggle API, so upload your own `kaggle.json`
     token when prompted (Kaggle → Account → *Create New API Token*). The token is a secret
     and is intentionally excluded from this repository via `.gitignore`.

Each section prints its answer inline — for example, the country that produced the most
female Olympic swimmers, the highest-paid sport, and the most underused defensive player
in the 2024 NBA season.

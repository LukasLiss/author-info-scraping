# Academic Paper Web Scraping — Scientometric Analysis

A hands-on introduction to fetching and enriching academic paper and author metadata using two popular APIs:

- **OpenAlex** — a free, open catalogue of the global research system (no API key needed)
- **SerpAPI** — a service that provides structured access to Google Scholar results

These tools are commonly used in **scientometric** and **bibliometric** analysis — for example, when conducting systematic literature reviews and wanting to enrich a paper list with citation counts, author affiliations, or career stage metrics.

---

## Repository Structure

```
author-info-scraping/
├── data/
│   └── example_papers.csv              10 papers from a Dimensions export (6 included, 4 excluded)
├── openalex/
│   ├── 01_fetch_paper_by_doi.ipynb     Fetch full metadata for a paper using its DOI
│   ├── 02_search_papers_by_keyword.ipynb  Search papers by keyword with filters & pagination
│   ├── 03_fetch_author_info.ipynb      Search for an author by name and get their profile
│   ├── 04_author_publication_history.ipynb  Get all publications, compute seniority metrics
│   └── 05_batch_enrich_papers.ipynb    Enrich a whole CSV of papers with OpenAlex data
├── serpapi/
│   ├── 01_search_author_by_name.ipynb  Find a Google Scholar author ID by name
│   ├── 02_fetch_author_metrics.ipynb   Retrieve h-index, citations, article list
│   ├── 03_compute_author_seniority.ipynb  Compute consecutive publishing years & seniority class
│   ├── 04_batch_enrich_first_last_authors.ipynb  Enrich papers with first/last author metrics
│   └── 05_visualize_seniority_distributions.ipynb  Plot seniority by author role and country group
├── inspiration/
│   └── EDA.ipynb                       Original exploratory notebook (full dataset, reference)
├── .env.example                        Template for API keys
├── requirements.txt
└── README.md
```

---

## Setup

### 1. Clone the repository

```bash
git clone <repo-url>
cd author-info-scraping
```

### 2. Create a virtual environment and install dependencies

```bash
python -m venv venv
source venv/bin/activate        # on Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Set up your API key

```bash
cp .env.example .env
```

Open `.env` and replace `your_serpapi_key_here` with your actual SerpAPI key.
The OpenAlex notebooks require no API key.

### 4. Launch Jupyter

```bash
jupyter notebook
```

Then navigate to the `openalex/` or `serpapi/` folder and open any notebook.

---

## Getting API Keys

### OpenAlex
No API key required. Optionally provide your email address in the `mailto` parameter of each request to get access to the faster "polite" pool and avoid rate limits.

**Documentation:** https://docs.openalex.org

### SerpAPI
Sign up at https://serpapi.com — the free tier includes **100 searches per month**.
After signing up, copy your API key from the dashboard into your `.env` file.

**Documentation:** https://serpapi.com/google-scholar-api

---

## Use Cases

### OpenAlex (no API key required)

| Notebook | What it demonstrates |
|----------|----------------------|
| `01_fetch_paper_by_doi.ipynb` | Fetch full metadata (title, abstract, OA status, concepts, authors) for a single paper by DOI |
| `02_search_papers_by_keyword.ipynb` | Keyword search with filters (open access, year range) and cursor-based pagination |
| `03_fetch_author_info.ipynb` | Search for an author by name, handle ambiguity, fetch h-index and affiliation |
| `04_author_publication_history.ipynb` | Retrieve all publications for an author, compute consecutive publishing years and seniority |
| `05_batch_enrich_papers.ipynb` | Loop over a CSV of papers, enrich each with OpenAlex data, export to CSV |

### SerpAPI (API key required)

| Notebook | What it demonstrates |
|----------|----------------------|
| `01_search_author_by_name.ipynb` | Search Google Scholar for an author by name, retrieve their profile ID |
| `02_fetch_author_metrics.ipynb` | Fetch h-index, i10-index, citation count and article list using a Scholar author ID |
| `03_compute_author_seniority.ipynb` | Compute consecutive publishing years and classify authors as early / mid / senior |
| `04_batch_enrich_first_last_authors.ipynb` | Enrich a paper list with first and last author metrics (h-index, seniority) |
| `05_visualize_seniority_distributions.ipynb` | Bar charts of seniority distributions by author role and country income group (HIC/LMIC) |

---

## Example Data

`data/example_papers.csv` contains 10 papers exported from [Dimensions](https://www.dimensions.ai/) as part of a systematic review on AI/ML in healthcare. It includes 6 papers marked `include` and 4 marked `exclude`, with columns for DOI, authors, affiliations, citation counts, and open access status.

The full export (670 papers) is available in `inspiration/example_dimension_export_with_additional_manual_inclusion_decision.csv`.

---

## Further Reading

- [OpenAlex documentation](https://docs.openalex.org)
- [SerpAPI Google Scholar API](https://serpapi.com/google-scholar-api)
- [Dimensions database](https://www.dimensions.ai/)
- [scholarly Python library](https://scholarly.readthedocs.io/) — a free alternative to SerpAPI for Google Scholar (no API key, but slower and less reliable)

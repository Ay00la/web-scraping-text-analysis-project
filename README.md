# Book Discovery: Web Scraping and Text Analysis

## Project overview
This project collects and analyses book product descriptions from **Books to Scrape**, a free public practice website for learning web scraping.

**Project topic:** Book discovery and reader appeal  
**Dataset:** 50 individual book product pages  
**Main deliverable:** A reproducible Jupyter Notebook that scrapes, cleans, analyses and presents text data.

The workflow:
1. Collect product pages using Requests and BeautifulSoup.
2. Clean the extracted text and metadata.
3. Analyse description sentiment with VADER.
4. Estimate topic relevance using TF-IDF and cosine similarity.
5. Generate concise extractive summaries.
6. Calculate a directional importance score and present results in tables and charts.

## Objectives
- Compare BeautifulSoup with Scrapy and justify the selected library.
- Collect at least 50 individual pages from a free website.
- Apply at least two text-analysis algorithms.
- Provide a summary and directional importance score for each page.
- Make the work reproducible in Jupyter Notebook.

## Technology stack

| Area | Library / tool | Purpose |
|---|---|---|
| Language | Python | Main implementation |
| HTTP | Requests | Retrieve web pages |
| HTML parsing | BeautifulSoup 4 | Extract page content |
| Data processing | pandas, NumPy | Clean and transform records |
| Text features | scikit-learn | TF-IDF and cosine similarity |
| Sentiment | VADER Sentiment | Positive/negative/neutral analysis |
| Visualization | Matplotlib | Result charts |
| Notebook | Jupyter Notebook | Interactive development and reporting |
| Environment | Anaconda / conda | Python environment and package management |

## Method summary

### Scraping
BeautifulSoup with Requests is used because the task is a bounded 50-page crawl and the implementation is straightforward to explain in a notebook. Scrapy is better suited to large concurrent crawls because it provides scheduling, retry handling and pipeline support. User-Agent variation and request delays are used as basic request-management practices, not to bypass restrictions.

### Text analysis
- **VADER:** produces a compound sentiment score from -1 to +1.
- **TF-IDF + cosine similarity:** compares each page's text with a book-discovery topic query. Similarities are converted to within-sample percentile relevance scores from 0 to 100.
- **Extractive summary:** selects up to two informative sentences using TF-IDF sentence weights.
- **Directional importance:** relevance percentile multiplied by VADER compound sentiment. Direction labels distinguish Positive, Negative, Neutral and Low relevance.

The score is an assignment-specific heuristic, not an objective measure of book quality. VADER reflects the tone of promotional copy; TF-IDF measures vocabulary overlap.

## Repository structure

```text
book-discovery-text-analysis/
├── web_scraping_text_analysis_project.ipynb
├── scraped_books_raw.csv
├── requirements.txt
├── README.md
└── outputs/
    ├── scraped_books_raw_cleaned.csv
    └── scraped_text_analysis_results.csv
```

The notebook writes generated CSV files to its current working directory unless output paths are changed.

## Environment: Jupyter Notebook and Anaconda

The project is designed for Python 3.11 in Jupyter Notebook, managed with Anaconda.

```bash
conda create -n book-text-analysis python=3.11 -y
conda activate book-text-analysis
pip install -r requirements.txt
python -m ipykernel install --user --name book-text-analysis --display-name "Python (book-text-analysis)"
jupyter notebook
```

Select the `Python (book-text-analysis)` kernel in Jupyter.

Alternatively, create a Python 3.11 environment through Anaconda Navigator, install the packages from `requirements.txt`, and launch Jupyter Notebook.

## How to run
1. Keep `scraped_books_raw.csv` in the same directory as the notebook.
2. Activate the conda environment.
3. Launch Jupyter Notebook and open `web_scraping_text_analysis_project.ipynb`.
4. Run the cells from top to bottom.

The default workflow analyses the existing 50-page dataset. An optional live crawl is included but disabled by default.

## Outputs
- `scraped_books_raw_cleaned.csv` — cleaned source records.
- `scraped_text_analysis_results.csv` — one row per page, with title, category, rating, summary, sentiment, relevance, importance score, direction and URL.

## Limitations and responsible use
- Product descriptions are promotional text; VADER does not represent verified reader reviews.
- TF-IDF is lexical and may miss semantic relationships expressed with different words.
- Percentile relevance is relative to this 50-page sample, not an absolute probability.
- Extractive summaries reuse source sentences and may not capture every nuance.
- User-Agent variation does not grant permission to bypass rate limits or access controls. Keep crawls modest and follow the website's policies.

## References
- [Books to Scrape](https://books.toscrape.com/)
- [Beautiful Soup documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [Scrapy documentation](https://docs.scrapy.org/)
- [scikit-learn TF-IDF documentation](https://scikit-learn.org/stable/modules/feature_extraction.html#tfidf-term-weighting)
- [VADER Sentiment](https://github.com/cjhutto/vaderSentiment)

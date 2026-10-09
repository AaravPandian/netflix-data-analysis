# Netflix Data Analysis

My first data analysis project, using **Python, pandas and Matplotlib** to explore a dataset of Netflix movies and TV shows.

The aim is to practise loading data, checking its quality, performing basic cleaning, creating charts and explaining the results.

## Questions explored

1. Are movies or TV shows more common in the dataset?
2. Which genres and categories appear most often?
3. Which maturity ratings are most common?
4. Which release years have the most titles?
5. Which countries are associated with the most titles?

## Tools used

- **Python:** writing the analysis.
- **pandas:** reading, cleaning and summarising the data.
- **Matplotlib:** creating bar charts and a line chart.
- **Jupyter Notebook or Google Colab:** running the code alongside explanations and results.

## Dataset

The dataset used contains **8,807 rows and 12 columns**. Each row represents one movie or TV-show title, rather than an individual TV episode.

Dataset reference: [Netflix Movies and TV Shows — Shivam Bansal, Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows).

The main columns used are:

| Column | Description |
| --- | --- |
| `type` | Movie or TV Show |
| `title` | Name of the title |
| `country` | Associated country or countries |
| `release_year` | Release year recorded in the dataset |
| `rating` | Maturity classification, such as TV-MA or PG-13 |
| `listed_in` | Genres and broader content categories |

This is a historical dataset. The latest recorded addition date is **25 September 2021**; it does not represent Netflix's current catalogue.

## Analysis process

### 1. Load and inspect the data

Loaded the CSV with `pd.read_csv()` and explored it using `head()`, `shape`, `columns` and `info()`. Used `isna().sum()` to check missing values.

### 2. Clean the data

- Used `drop_duplicates()` to remove identical rows; no identical rows were found in this dataset.
- Inspected the rating labels with `value_counts()` and identified three runtime values in the wrong column: `74 min`, `84 min` and `66 min`.
- Replaced these invalid ratings with `Unknown` and used `fillna()` to label missing ratings as `Unknown`.
- Excluded missing countries from the country analysis while retaining those titles for other analyses.

### 3. Prepare genres and countries

Some cells contain several labels, such as `India, United States`. To count each item separately, I used:

- `.str.split(',')` to separate the labels into lists.
- `.explode()` to place each list item on its own row.
- `.str.strip()` to remove spaces around each label.

A title with several genres or countries contributes to each associated group. Therefore, these counts can add up to more than the number of titles.

### 4. Count and visualise

Used `value_counts()` to calculate frequencies, `head(10)` to select leading categories and `sort_index()` to arrange release years chronologically.

Created five charts:

- Movies versus TV shows: vertical bar chart.
- Top 10 genres/categories: horizontal bar chart.
- Maturity ratings: vertical bar chart.
- Titles by release year: line chart.
- Top 10 associated countries: horizontal bar chart.

## Key findings

| Question | Finding |
| --- | --- |
| Movies or TV shows? | **6,131 movies** and **2,676 TV shows**. |
| Most common categories? | **International Movies: 2,752**, **Dramas: 2,427**, **Comedies: 1,674**. |
| Most common maturity rating? | **TV-MA**, appearing on **3,207 titles**. |
| Most represented release year? | **2018**, with **1,147 titles**. |
| Most frequently associated countries? | **United States: 3,690**, **India: 1,046**, **United Kingdom: 806**. |

These results describe how content is represented in the dataset. They do not measure how often people watched it.

## How to run the project

### Google Colab

1. Download `netflix_data_analysis.ipynb` from this repository.
2. Open [Google Colab](https://colab.research.google.com/) and upload the notebook.
3. Download the dataset from the Kaggle link above and extract `netflix_titles.csv` from the ZIP file.
4. Upload the CSV using Colab's Files panel.
5. Run the notebook cells from top to bottom.

If Colab starts a new session and the CSV is no longer present, upload it again.

### Jupyter Notebook on your computer

1. Download the notebook and dataset.
2. Place `netflix_data_analysis.ipynb` and `netflix_titles.csv` in the same folder.
3. Install the required tools in your terminal:

   ```bash
   python -m pip install pandas matplotlib jupyter
   ```

4. Open a terminal in that folder and start Jupyter:

   ```bash
   jupyter notebook
   ```

5. Open the notebook and run its cells in order.

The loading cell expects the filename `netflix_titles.csv`. If your filename or location is different, update the path in `pd.read_csv()`.

## Limitations

- The data is historical, and the final observed year may be incomplete.
- Catalogue counts do not establish audience popularity, viewing hours or revenue.
- Ratings are maturity classifications, not audience review scores.
- Release year is different from the year a title was added to Netflix.
- Genres and countries overlap because one title can have multiple labels.
- `listed_in` mixes genres with broader categories, such as International Movies.
- Some metadata is missing; country results exclude titles without country information.
- The file does not establish current availability in every region or provide a complete history of additions and removals.

## What I learned

- How to load and inspect a CSV file with pandas.
- Why values should be inspected before cleaning decisions are made.
- How to handle missing information without deleting every incomplete row.
- When to use `str.split()`, `explode()` and `str.strip()`.
- How to count categories and sort results.
- How to create and label simple charts with Matplotlib.
- How to distinguish a supported finding from an assumption.

## Acknowledgement

Dataset reference credited to Shivam Bansal on Kaggle. Refer to the dataset page for its usage and redistribution terms.

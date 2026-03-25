# Netflix Content Analysis

This repository presents comprehensive data cleaning, exploratory analysis, and visualization of Netflix content catalog from 2008-2021. The Jupyter notebook processes 8,800+ titles, addressing missing values, date parsing, duration standardization, and genre categorization.

## Project Overview

Analysis of `netflix.csv` covering movies and TV shows with variables: show_id, type, title, director, country, date_added, release_year, rating, duration, listed_in. Key transformations include date standardization, duration parsing (minutes/seasons), multi-label genre expansion, and temporal trend analysis. 

## Key Components

- **Data Cleaning**: Missing director/country imputation ("Not Given"), date parsing, duration standardization, duplicate removal.
- **Feature Engineering**: `listed_in` split into primary/secondary/tertiary genres, duration numeric conversion, type binary encoding.
- **EDA**: Content type distribution, top countries/directors, release year trends, rating analysis, duration patterns.
- **Visualization**: Bar charts (content type, top genres/countries), heatmaps (year-country matrix), histograms (release years, durations).

## Requirements

- Python 3.8+
- Pandas, NumPy
- Matplotlib, Seaborn

Install via:
```bash
pip install pandas numpy matplotlib seaborn
```

## Usage

1. Place `netflix.csv` in repository root.
2. Run: `jupyter notebook netflix-data-cleaning-analysis-and-visualisation.ipynb`.
3. Sequential execution produces cleaned dataset, summary statistics, and 15+ visualizations.

## Results Structure

| Analysis | Output Description |
|----------|-------------------|
| Dataset Overview | Info, describe, missing values table |
| Content Distribution | Movies (62%) vs TV Shows (38%) pie chart |
| Temporal Trends | Release year histogram, yearly additions |
| Geography | Top 10 countries bar chart (US dominant) |
| Genres | Top categories (Dramas, Comedies, Documentaries) |
| Duration Analysis | Minutes histogram (Movies), Seasons (TV Shows) |
| Ratings | Age rating distribution by content type |

Cleaned dataset shape: 8790 × 13 (added genre/duration features).

## Code Highlights

**Duration parsing**:
```python
def parse_duration(duration):
    if 'Season' in duration:
        return int(duration.split()[0]), 'seasons'
    else:
        return int(duration.split()[0]), 'minutes'
```

**Genre expansion**:
```python
df['listed_in1'] = df['listed_in'].str.split(', ').str[0]
df['listed_in2'] = df['listed_in'].str.split(', ').str.fillna('0')
df['listed_in3'] = df['listed_in'].str.split(', ').str.fillna('0')
```

**Temporal analysis**:
```python
df['date_added'] = pd.to_datetime(df['date_added'], format='%m/%d/%Y')
release_year_counts = df['release_year'].value_counts().sort_index()
```



## Key Findings

- US produces 70%+ content; India, UK follow.
- Movies average 100 minutes; TV shows peak at 1-2 seasons.
- Dramas/Comedies dominate; Documentaries growing.
- Release peak: 2018-2020; older catalog from 1990s.

## Limitations

- Single source (no viewership/runtime data).
- "Not Given" values (directors: 26%, country: 5%).
- Static snapshot (no longitudinal viewership).

## Author

Ting-Ying Lai  
National Taiwan University  
Data Science Portfolio

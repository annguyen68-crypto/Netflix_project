# Netflix Data Exploration

Data cleaning and exploratory data analysis (EDA) of the Netflix titles dataset, to understand how Netflix builds its content catalog over time, by genre and by region.

## Files

| File | Description |
|---|---|
| `Netflix_EDA_English.ipynb` | Full analysis notebook (English) |
| `Netflix_EDA_Vietnamese.ipynb` | Full analysis notebook (Vietnamese) |
| `netflix_titles.csv` | Raw dataset: 8,807 titles × 12 columns, titles added up to September 2021 |

Both notebooks contain the same code and analysis; only the language differs.

## Analysis questions

1. Which content type (Movie/TV Show) makes up the majority?
2. How is the duration of Movies and TV Shows distributed?
3. Which rating is the most common?
4. In which year did Netflix "boom" in the number of newly added titles?
5. Which genres does Netflix add the most in each month of the year? (seasonality)
6. Who are the top 10 directors with the most titles?
7. Which country has the most titles?
8. What are the most common keywords in the descriptions?

## Workflow

1. **Data overview** — size and data type of each column.
2. **Data cleaning**
   - Missing data: filled `director`, `cast`, `country` with "Unknown"; dropped 17 rows missing `date_added`, `rating` or `duration` (including 3 rows where the duration was entered in the `rating` column).
   - Duplicates: checked both full rows and content excluding `show_id`.
   - Format: parsed `date_added` to datetime (after stripping leading spaces); split `duration` into a number and a unit.
   - Logic checks: `date_added` vs. `release_year`.
   - Outliers: movie duration (IQR) and number of TV Show seasons — kept as real values.
   - Re-encoding: split multi-value columns (`listed_in`, `country`, `director`, `cast`); grouped the 14 rating codes into Kids / Teens / Adults following Netflix's US maturity levels.
3. **Feature engineering** — description length; year / month / day added.
4. **EDA** — one section per question: question → chart → insight.
5. **Conclusions, recommendations and data limitations.**

## Key findings

- **Movies dominate:** 69.7% of the catalog (6,126 titles), about 2.3× the number of TV Shows. Most TV Shows have only 1 season.
- **Mature audiences first:** TV-MA (36%) and TV-14 (25%) are the most common ratings; Adults content makes up 45.6%, while content for young children is only 6.5%.
- **Built from 2016 onwards:** 2016–2021 accounts for 98.4% of titles, peaking in 2019 (2,016 titles).
- **No clear seasonality:** each genre's monthly share stays close to the even 8.3% baseline.
- **US-led, Asia rising:** the US accounts for 46.2% of titles with country information; India ranks 2nd (13.1%), ahead of the UK.

## How to run

Requires Python 3 with Jupyter.

```bash
pip install pandas numpy matplotlib seaborn wordcloud
```

Open either notebook in Jupyter or VS Code, keep `netflix_titles.csv` in the same folder, then run all cells.

## Data limitations

- Data runs only to September 2021, so 2021 figures do not cover the full year.
- Movies are measured in minutes and TV Shows in seasons (no episode counts), so their durations cannot be compared directly.
- ~30% of rows are missing `director` and ~9% are missing `country` (filled with "Unknown").

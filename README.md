# FRI data engineering 1-hour work test

A 1-hour data engineering work test for candidates applying to the Forecasting Research Institute.

## Context

The Forecasting Research Institute (FRI) collects probabilistic forecasts on questions about future events. Our data comes from survey platforms and needs to be cleaned, modeled, and made queryable for research use.

This work test simulates a task you might encounter in the role of a data engineer at FRI.

We ask that you complete this work test using only your own writing, without the use of AI tools or outside assistance. This helps us evaluate your individual capabilities and thought process.

**Please do not spend more than 1 hour on the tasks below.**

In your solution, we're looking for correctness, clarity, and thoughtful modeling choices.

## Setup

1. Install the DuckDB Python library:
   ```bash
   pip install duckdb
   ```

2. (Optional) To query the database interactively from the command line, install the DuckDB CLI separately:
   ```bash
   # macOS
   brew install duckdb
   # Linux
   # See https://duckdb.org/docs/installation/
   ```

3. Load the data into a local DuckDB database:
   ```bash
   python setup.py
   ```

4. This creates `fri_worktest.duckdb` with three tables, all columns loaded as VARCHAR:
   - `raw_forecasts_export`: main denormalized forecast data;
   - `raw_forecaster_demographics`: demographics for each forecaster;
   - `raw_question_tags`: tags assigned to questions.

You can query the database interactively (assuming you have the DuckDB CLI from Step 2):
```bash
duckdb fri_worktest.duckdb
```

We prefer solutions in DuckDB SQL, but submissions in Python or other SQL variants are fine, too.

## Data description

The data represents forecasts on binary questions (probability in percent, 0-100) about AI-related topics.

- `forecasts_export.csv`: A denormalized export from a survey platform. Each row represents one forecast submission and includes forecaster metadata (name, type), question metadata (text), and free-text rationale. Forecasters may update their forecasts over time;

- `forecaster_demographics.csv`: Demographic data for each forecaster (e.g., experience, education);

- `question_tags.csv`: Domain tags assigned to questions in a many-to-many relationship (e.g., a question can have multiple tags like "artificial-intelligence" and "safety").

---

## Task 1: Data quality assessment (~10 minutes)

Review the three raw tables and document any data quality issues you find.

For each issue, note:
- Which table and column(s) are affected;
- What the issue is;
- How you would handle it (e.g., remove, correct, flag).

---

## Task 2: Dimensional model (~35 minutes)

Transform the raw tables into a clean dimensional model. Your model should include at least:

- `dim_forecasters`: One row per forecaster, incorporating relevant demographic data;
- `dim_questions`: One row per question;
- `fct_forecasts`: One row per forecast, with foreign keys to the dimension tables.

Your code must:
- Handle the quality issues you identified in Task 1;
- Cast columns to appropriate data types;
- Run successfully against the DuckDB database created by `setup.py`.

Briefly justify your key schema choices in comments or a short note.

---

## Task 3: Analytical queries (~15 minutes)

Using the model you built in Task 2, write queries to answer:

1. For each question, how many forecasters provided a prediction, and what is the median predicted probability?
2. How does the average predicted probability differ between superforecasters and other forecaster types?

---

## Submission

Submit a `.zip` file containing:
- A short document (any format) with your Task 1 data quality assessment; 
- Your code for Tasks 2 and 3.

Upload the `.zip` in the application form.

**Do not include your name anywhere in the submitted files** (submissions are reviewed blind).
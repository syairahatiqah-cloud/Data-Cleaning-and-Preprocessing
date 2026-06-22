# FSM Water Level / Streamflow Imputation App

A Streamlit web application for checking missing values and imputing water-level or streamflow time-series data using:

- Full Subsequence Matching (FSM)
- Linear interpolation
- Polynomial interpolation

The app is designed for hydrological telemetry data such as water level (WL) or streamflow (SF). It supports Excel and CSV upload, missing-data summaries, imputation plots, monthly seasonality comparison, and downloadable outputs.

---

## Main Features

### 1. Upload Data
Upload an Excel or CSV file and select:

- Date/time column
- Water level or streamflow value column

### 2. Raw Time-Series Plot
The app displays the original time series using Plotly and Matplotlib.

Available downloads:

- Interactive HTML plot
- PNG plot

### 3. Missing Data Summary
The app calculates missing data by:

- Monthly summary
- Yearly summary

Available downloads:

- Monthly or yearly missing summary CSV
- Missing percentage plot in HTML
- Missing percentage plot in PNG

### 4. FSM Imputation
The app supports two FSM modes:

- `FSM_scale`
- `FSM_diff`

Outputs:

- Full infilled CSV
- Time-series plot showing original data and FSM-imputed segments only
- PNG plot displayed in the app
- Monthly seasonality plot comparing original vs full infilled series

### 5. Linear Interpolation Imputation
The app fills missing values using linear interpolation.

Outputs:

- Full infilled CSV
- Time-series plot showing original data and linear-interpolated segments only
- PNG plot displayed in the app
- Monthly seasonality plot comparing original vs full infilled series

### 6. Polynomial Interpolation Imputation
The app fills missing values using polynomial interpolation.

Outputs:

- Full infilled CSV
- Time-series plot showing original data and polynomial-imputed segments only
- PNG plot displayed in the app
- Monthly seasonality plot comparing original vs full infilled series

---

## Expected Input Format

Your input file should contain at least two columns:

| DateTime | WL_or_SF |
|---|---:|
| 2020-01-01 00:00 | 1.23 |
| 2020-01-01 01:00 | 1.25 |
| 2020-01-01 02:00 | |
| 2020-01-01 03:00 | 1.32 |

Notes:

- Date/time column must be readable by `pandas.to_datetime()`.
- Missing values can be blank, `NaN`, or empty cells.
- The value column should be numeric.

---

## Repository Structure

Recommended structure:

```text
fsm-imputation-streamlit/
│
├── app.py
├── requirements.txt
├── README.md
└── data/
    └── sample_data.csv   # optional
```

When creating the GitHub repository, rename the Streamlit script to:

```text
app.py
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/fsm-imputation-streamlit.git
cd fsm-imputation-streamlit
```

Create and activate a virtual environment:

```bash
python -m venv .venv
```

For Windows:

```bash
.venv\Scripts\activate
```

For macOS/Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Run Locally

```bash
streamlit run app.py
```

The app will open in your browser, usually at:

```text
http://localhost:8501
```

---

## Deploy to Streamlit Community Cloud

1. Create a new GitHub repository.
2. Upload these files:
   - `app.py`
   - `requirements.txt`
   - `README.md`
3. Go to Streamlit Community Cloud.
4. Choose **New app**.
5. Select your GitHub repository.
6. Set the main file path as:

```text
app.py
```

7. Click **Deploy**.

---

## Notes for Deployment

This app uses Matplotlib to generate PNG images because Plotly PNG export may require Chrome/Kaleido support, which can be problematic on some cloud deployments.

For Excel upload support, the app uses:

- `openpyxl` for `.xlsx`
- `xlrd` for `.xls`

---

## Methods Included

### FSM: Full Subsequence Matching
FSM fills a missing gap by searching for the most similar historical subsequence in the same time series. It is especially useful when the data has repeating or cyclical behaviour, such as tidal water-level records.

### Linear Interpolation
Linear interpolation estimates missing values by drawing a straight line between known points before and after the missing gap. It is simple, fast, and suitable for very short gaps.

### Polynomial Interpolation
Polynomial interpolation estimates missing values using a curved function. It may be useful when the data trend is smooth and curved, but performance can weaken for large missing gaps.

---

## Suggested Citation

This app was developed based on the concept of Full Subsequence Matching for hydrological time-series imputation:

Khampuengson, T., & Wang, W. (2023). *Novel Methods for Imputing Missing Values in Water Level Monitoring Data*. Water Resources Management, 37, 851–878.

---

## License

You may add your preferred license, for example:

- MIT License
- Apache License 2.0
- Creative Commons license for documentation


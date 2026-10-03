# stc tv Data Analytics Project

Analysis, forecasting and personalized recommendations using the datasets supplied for the **stc Data Analysis Virtual Work Experience**, completed through the Misk Foundation on **3 October 2026**.

**Author:** Muhanna Almutairi

## Certificate

[![Certificate of completion](certificates/stc_data_analysis_certificate_preview.png)](certificates/stc_data_analysis_certificate.pdf)

This certificate confirms completion of the stc Data Analysis Virtual Work Experience through the Misk Foundation on 3 October 2026. Click the preview to open the original PDF.

This learning project covers four tasks. All code, comments and documentation are in English. The notebooks include saved results and charts, so readers can review the work without downloading the source datasets or running the code.

## Project overview

| Task | Question | Deliverable |
| --- | --- | --- |
| 1. Viewer behavior | How do movie and series viewing differ, including SD and HD usage? | [Analysis notebook](STC_TV_Task_1_Analysis.ipynb) |
| 2. Forecasting | How many watch hours should we expect in the next two months? | [Forecast notebook](STC_TV_Task_2_Forecast.ipynb) |
| 3. Recommendations | What can viewers discover from the histories of similar users? | [Recommendation notebook](STC_TV_Task_3_Recommendations.ipynb) |
| 4. Data storytelling | How can these findings guide service improvements? | [12-slide PowerPoint](Task_4/STC_TV_Task_4.pptx) |

**Tools:** Python, pandas, NumPy, Matplotlib, SciPy, scikit-learn, Jupyter and Google Colab.

## Key findings

### Task 1: Viewer behavior and streaming quality

The supplied sheet contains **1,048,575 viewing events** from **11,578 distinct viewers**.

- Series contribute **53.42% of viewing events** and **71.15% of watch hours**.
- **67.92% of movie events** use HD. **86.92% of series events** use SD.
- The mutually exclusive viewer segments are **7,677 movie-only viewers**, **3,678 viewers of both classes**, and **223 series-only viewers**.

The notebook checks missing values, describes numerical columns and compares event-level quality shares with viewer-level segments. Missing descriptions receive the label `Not provided`. Identical records are retained because the source lacks an event identifier that could confirm erroneous duplicates.

**Service proposal:** Investigate series HD availability and playback conditions. The observed SD usage alone does not establish a viewer preference or its cause.

### Task 2: Daily watch-time forecast

The source contains **86 business-day observations** from January to April 2018. It records watch hours rather than viewing counts.

A simple linear trend forecasts the next two historical calendar months:

| Forecast period | Business days | Estimated watch hours |
| --- | ---: | ---: |
| May 2018 | 23 | 13,974 |
| June 2018 | 21 | 11,290 |

The expected peak day is **1 May 2018**, at approximately **643 watch hours**. On a chronological holdout of 44 business days, the model achieves **63.72 hours/day mean absolute error**, compared with **85.86 hours/day** for a baseline that repeats the last observed week.

**Scope:** These are historical watch-hour estimates. The source cannot support a view-count forecast, weekend forecasts or hourly peak identification. The model has no holiday, promotion or content-release information.

### Task 3: Recommendations from similar viewers

The model uses **user-based collaborative filtering**, cosine similarity and up to **30 nearest neighbors**. Repeated user-title views collapse into **440,237 relationships**, covering **11,578 users** and **8,013 programs**. Personalized lists exclude titles the target viewer has already watched.

The aggregate ranking for **2,173 Moana viewers** is:

| Rank | Recommended program |
| --- | --- |
| 1 | The Jetsons & WWE: Robo-WrestleMania! |
| 2 | Surf's Up : WaveMania |
| 3 | Rings |
| 4 | The Mermaid Princess |
| 5 | Collateral Beauty |

In a reproducible hidden-title check on 200 users, the model recovers **56 titles in the top five (28.0%)**, compared with **21 titles (10.5%)** for a popularity baseline.

**Scope:** This random offline holdout is a demonstration, rather than a measure of future engagement. The group ranking can differ from each user's unseen-title list. The undocumented rating scale is not used in scoring.

### Task 4: Findings and proposed service improvements

The presentation combines the earlier findings, an anonymized viewer example and practical proposals:

- Audit HD availability and playback conditions for series.
- Test recommendations from similar viewers against popular available titles.
- Add hourly, weekend and holiday data, then refresh demand forecasts.

The slides include editable charts and tables. Speaker notes explain the evidence, cite the source notebooks and describe the limitations. Proposed improvements have not been deployed or measured in production.

## Run in Google Colab

1. Open the notebook for the task you want to explore:
   - [Task 1 in Colab](https://colab.research.google.com/github/muhanna32/stc-tv-data-analysis/blob/main/STC_TV_Task_1_Analysis.ipynb)
   - [Task 2 in Colab](https://colab.research.google.com/github/muhanna32/stc-tv-data-analysis/blob/main/STC_TV_Task_2_Forecast.ipynb)
   - [Task 3 in Colab](https://colab.research.google.com/github/muhanna32/stc-tv-data-analysis/blob/main/STC_TV_Task_3_Recommendations.ipynb)
2. Run the cells in order.
3. Upload the corresponding course workbook when prompted. Reading the larger workbooks can take a few minutes.

| Task | Required workbook | Sheet |
| --- | --- | --- |
| 1 | `stc TV Data Set_T1.xlsb` | `Final_Dataset` |
| 2 | `stc TV Data Set_T2.xlsx` | `Sheet1` |
| 3 | `stc TV Data Set_T3.xlsx` | `Sheet1` |

The course-provided source workbooks and starter notebooks are not included in this repository. Obtain the workbooks from the course materials. The completed notebooks include saved outputs for review.

## Run locally

Clone this repository, install the dependencies, and open Jupyter:

```bash
git clone https://github.com/muhanna32/stc-tv-data-analysis.git
cd stc-tv-data-analysis
python -m pip install -r requirements.txt
jupyter notebook
```

Place the required workbooks beside the notebooks, then run the cells in order.

## Interpretation notes

- Viewing events and unique users have different denominators. A person can watch both movies and series.
- Watching a title is an implicit signal, not proof that the viewer liked it.
- Tasks 1 and 3 each reach the Excel sheet row limit. Findings describe the supplied extracts and may not cover all viewing activity.
- Extreme duration values can affect averages. Median duration is more representative of a typical event in Task 1.
- This is a learning portfolio based on a virtual work experience, not an official stc report or an employment claim.

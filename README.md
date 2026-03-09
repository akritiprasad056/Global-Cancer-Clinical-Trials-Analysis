# 🔬 Global Cancer Clinical Trials Analysis — Power BI Dashboard

## Project Overview

This project is an end-to-end data analytics case study analyzing 10,000+ cancer clinical trial records sourced from ClinicalTrials.gov — the world's largest clinical trial registry maintained by the U.S. National Library of Medicine. The final output is a 3 page interactive Power BI dashboard covering trial status analysis, geographic distribution and drug pipeline analysis.

---

## Data Source

- **Source:** ClinicalTrials.gov — U.S. National Library of Medicine
- **Link:** https://clinicaltrials.gov
- **Records:** 10,000+ Cancer Clinical Trials
- **Last Updated:** 2025
- **Format:** CSV

---

## Tools Used

| Tool | Purpose |
|---|---|
| Power BI | Dashboard development and visualization |
| Power Query | Data transformation and custom column creation |
| DAX | Calculated measures and KPIs |
| Excel | Data exploration and preparation |
| AI Assistance | Data cleaning support |

---

## Project Workflow

### Step 1 — Data Collection
Downloaded 10,000+ cancer clinical trial records from ClinicalTrials.gov in CSV format. The dataset included information on trial status, phases, interventions, enrollment numbers, locations and more across 17 columns.

### Step 2 — Data Cleaning
The raw data had several quality issues that were addressed:
- Removed 3 columns with more than 60% missing values — Collaborators, Results First Posted and Study Documents
- Removed junk rows from Study Status, Sex and Age columns where location data had ended up in wrong columns
- Standardized all text values to proper case
- Extracted Start Year, Start Month, Completion Year and Country as separate columns
- Filled all blank cells with Not Specified

### Step 3 — Power Query Transformations
Performed 7 key transformations in Power Query after loading data into Power BI:

1. **Data Types** — Changed all column data types appropriately. Enrollment, Start Year, Start Month and Completion Year set as Whole Numbers. All text columns set as Text type.

2. **Outcome Group Column** — Created using Custom Column logic categorizing every trial into:
   - Successful — Completed trials
   - Unsuccessful — Terminated, Withdrawn and Suspended trials
   - Ongoing — All remaining active trials

3. **Trial Duration Column** — Calculated by subtracting Start Year from Completion Year giving number of years each trial ran.

4. **Cancer Type Column** — Created using Conditional Column logic mapping keywords in the Conditions column to specific cancer types including Breast Cancer, Lung Cancer, Colorectal Cancer, Pancreatic Cancer, Cervical Cancer, Ovarian Cancer, Lymphoma, Prostate Cancer, Leukemia and Brain Cancer.

5. **Tumor Type Column** — Created using Conditional Column categorizing trials as Malignant, Benign or Unspecified based on keywords in the Conditions column.

6. **Intervention Type Column** — Extracted intervention category from the Interventions column including Drug, Biological, Procedure, Device, Radiation, Behavioral, Dietary, Genetic and Combination Product.

7. **Age Group Column** — Created using Conditional Column with proper clinical terminology including Adults and Elderly, Pediatric Only, Pediatric and Adult and All Age Groups.

### Step 4 — DAX Measures
Created a dedicated Measures table in Power BI with 12 DAX measures:

```
Total Trials = COUNT('Clinical Trials Data'[NCT Number])
```
```
Completed Trials = CALCULATE(COUNT('Clinical Trials Data'[NCT Number]),'Clinical Trials Data'[Study Status] = "Completed")
```
```
Recruiting Trials = CALCULATE(COUNT('Clinical Trials Data'[NCT Number]),'Clinical Trials Data'[Study Status] = "Recruiting")
```
```
Terminated Trials = CALCULATE(COUNT('Clinical Trials Data'[NCT Number]),'Clinical Trials Data'[Study Status] = "Terminated")
```
```
Total Enrollment = SUM('Clinical Trials Data'[Enrollment])
```
```
Avg Enrollment = AVERAGE('Clinical Trials Data'[Enrollment])
```
```
Completion Rate % = DIVIDE([Completed Trials],[Total Trials],0)
```
```
Termination Rate % = DIVIDE([Terminated Trials],[Total Trials],0)
```
```
Early Stage Trials = CALCULATE(COUNT('Clinical Trials Data'[NCT Number]),'Clinical Trials Data'[Phases] IN {"Early Phase 1","Phase 1","Phase 1/2"})
```
```
Late Stage Trials = CALCULATE(COUNT('Clinical Trials Data'[NCT Number]),'Clinical Trials Data'[Phases] IN {"Phase 2","Phase 2/3","Phase 3","Phase 4"})
```
```
Total Countries = DISTINCTCOUNT('Clinical Trials Data'[Country])
```
```
Outcome Group = IF('Clinical Trials Data'[Study Status] = "Completed", "Successful", IF('Clinical Trials Data'[Study Status] IN {"Terminated","Withdrawn","Suspended"}, "Unsuccessful","Ongoing"))
```

### Step 5 — Dashboard Development
Built a 3 page interactive Power BI dashboard with slicers, KPI cards, donut charts, bar charts and a world map visual.

---

## Dashboard Pages

### Page 1 — Overview and Status
- 5 KPI Cards — Total Trials, Completed Trials, Recruiting Trials, Total Enrollment, Total Countries
- 2 KPI Performance Cards — Trial Completion Rate vs 60% target, Trial Termination Rate vs 10% threshold
- Trials by Outcome donut chart
- Trials by Study Type donut chart
- Total Trials by Gender bar chart
- Trials by Intervention Type bar chart
- Slicers — Start Year, Outcome Group, Study Type

### Page 2 — Geographic Analysis
- 3 KPI Cards — Early Stage Trials, Late Stage Trials, Total Countries
- Interactive world map showing global distribution of cancer trials
- Slicers — Outcome Group, Study Type, Phases

### Page 3 — Trial Trends and Pipeline
- 3 KPI Cards — Early Stage Trials, Late Stage Trials, Total Trials
- Total Trials vs Age Group area chart
- Total Trials vs Phases bar chart
- Total Trials vs Intervention Type bar chart
- Slicers — Phases, Country, Outcome

---

## Key Insights

1. Only 32% of cancer trials reach completion — highlighting the long and challenging journey of drug development
2. Phase 1 has the highest number of trials confirming the classic drug development funnel — very few drugs that enter Phase 1 ever reach patients
3. The United States dominates global cancer research — while Africa and South America have significantly fewer trials highlighting geographic inequality
4. Drug based interventions lead the pipeline with nearly 4,000 trials — followed by Biological treatments like immunotherapy
5. 70% of trials are Interventional — meaning doctors are actively testing new treatments — while 30% are Observational studies
6. Adults and Elderly patients make up 92% of trial participants — reflecting the age specific nature of cancer

---

## Dataset Columns

| Column | Description |
|---|---|
| NCT Number | Unique identifier for each clinical trial |
| Study Title | Full name of the clinical trial |
| Study Status | Current status — Completed, Recruiting, Terminated etc. |
| Conditions | Disease or condition being studied |
| Interventions | Treatment being tested — Drug, Procedure, Device etc. |
| Sex | Gender eligibility — All Genders, Female, Male |
| Age | Age group eligibility |
| Phases | Trial phase — Phase 1 to Phase 4 |
| Enrollment | Number of participants |
| Study Type | Interventional or Observational |
| Start Date | Trial start date |
| Primary Completion Date | Primary completion date |
| Completion Date | Final completion date |
| Locations | Trial locations worldwide |
| Start Year | Extracted from Start Date |
| Start Month | Extracted from Start Date |
| Completion Year | Extracted from Completion Date |
| Country | Extracted from Locations |
| Outcome Group | Custom column — Successful, Unsuccessful, Ongoing |
| Trial Duration | Calculated years of trial duration |
| Cancer Type | Extracted cancer type from Conditions |
| Tumor Type | Malignant, Benign or Unspecified |
| Intervention Type | Extracted intervention category |
| Age Group | Clinical age group terminology |

---

## Project Structure

```
Global-Cancer-Clinical-Trials-Analysis/
│
├── README.md
├── Data/
│   └── Clinical_Trials_Cleaned.xlsx
├── Dashboard/
│   └── Clinical_Trials_data.pbix
└── Screenshots/
    ├── Page1_Overview.png
    ├── Page2_Geographic.png
    └── Page3_Pipeline.png
```

---

## How to Use

1. Download the repository
2. Open Clinical_Trials_data.pbix in Power BI Desktop
3. The dashboard will load with all 3 pages
4. Use the slicers on the left side to filter and explore the data interactively

---

## Author

**Akriti Prasad**
Healthcare and Pharma Analytics
Connect on LinkedIn

---

## Acknowledgements

Data sourced from ClinicalTrials.gov — U.S. National Library of Medicine
https://clinicaltrials.gov

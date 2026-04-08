# 📊 Data Jobs Dashboard — Power BI Portfolio Project

> An interactive Power BI dashboard analyzing salary trends, skill demand, and job market insights across data roles globally.

---

## 📌 Project Overview

This dashboard provides a comprehensive view of the data job market, enabling users to explore job counts, salary benchmarks, and top in-demand skills — filtered dynamically by **Job Title** and **Country**.

The project is built on a structured star-schema data model and leverages DAX measures, calculated parameters, and dynamic slicer-driven visuals to deliver actionable insights.

---

<img width="1326" height="737" alt="image" src="https://github.com/user-attachments/assets/3a63a9b6-8a95-4346-82a4-532ae2e1389d" />


## 🖼️ Dashboard Preview

| Filter | Default Value |
|---|---|
| Job Title | Data Analyst |
| Job Country | India |

**Key KPIs (filtered view):**

| Metric | Value |
|---|---|
| Job Count | 5K |
| Skills Per Job | 3.7 |
| Median Yearly Salary | $74K |
| Median Hourly Salary | $25 |

---

## 🗄️ Data Model — Tables Used

### Fact Table

| Table | Description |
|---|---|
| `job_postings_fact` | Core fact table containing all job postings with salary, schedule type, and associated dimension keys |

### Dimension Tables

| Table | Description |
|---|---|
| `company_dim` | Company details linked to each job posting |
| `date_dim` | Date dimension for time-based analysis |
| `skills_dim` | Master list of all skills (e.g., SQL, Python, Tableau) |
| `skills_job_dim` | Bridge/junction table linking jobs to their required skills (many-to-many relationship) |
| `schedule_type_dim` | Categorizes job postings by schedule type (Full-time, Part-time, Contract, etc.) |

---

## 📐 DAX Measures

All custom measures are grouped under the `_Measures` table for clean organization.

### Core KPI Measures

| Measure | Description |
|---|---|
| `Job Count` | Counts total distinct job postings — `COUNTROWS(job_postings_fact)` |
| `Skill Per Job` | Average number of skills required per job posting |
| `Median Yearly Salary` | Median of the yearly salary column from the fact table |
| `Median Hourly Salary` | Median of the hourly salary column from the fact table |

### Chart Measures

| Measure | Description |
|---|---|
| `Job Percent` | Percentage share of each skill across all jobs — used in the Top Skills bar chart |
| `Select Measure` | Dynamic measure switcher for the Top Skills chart (toggles between Job Count and Job Percent) |
| `Select Salary Measure` | Dynamic measure switcher for the Most Paid Jobs chart (toggles between Yearly and Hourly salary) |
| `Deduction Rate` | Calculates deduction or tax-adjusted salary for net pay analysis |

---

## 🎛️ Parameters & Slicers

### Field Parameters

| Parameter | Description |
|---|---|
| `Select Category` | Controls the axis/grouping category displayed in visuals |
| `Select Measure` | Dynamically switches the Y-axis metric on the Top Demanding Skills chart between **Job Count** and **Job Percent** |
| `Select Salary Measure` | Dynamically switches the X-axis metric on the Most Paid Jobs chart between **Median Yearly Salary** and **Median Hourly Salary** |
| `Select Skill Measure` | Parameter to toggle skill-related metrics in skill visuals |

### Page-Level Slicers / Filters

| Slicer | Field | Type |
|---|---|---|
| Select Job Title | `job_postings_fact[job_title_short]` | Dropdown |
| Select Job Country | `job_postings_fact[job_country]` | Dropdown |

---

## 📊 Charts & Visualizations

### 1. KPI Cards (Top Row)
**Type:** Card Visuals × 4

Displays high-level summary metrics that update dynamically based on slicer selections:
- **Job Count** — Total job postings matching the selected filters
- **Skill Per Job** — Average skills required per posting
- **Median Yearly Salary** — Salary benchmark (annual)
- **Median Hourly Salary** — Salary benchmark (hourly)

---

### 2. What are the Top Demanding Skills?
**Type:** Horizontal Bar Chart

| Property | Detail |
|---|---|
| Y-Axis | Skill Name (from `skills_dim`) |
| X-Axis | Dynamic — Job Count or Job Percent (via `Select Measure` parameter) |
| Sort Order | Descending by selected metric |
| Filter | Scoped to selected Job Title and Country |

**Top Skills Visible (Data Analyst — India):**

| Rank | Skill | Approx. Job % |
|---|---|---|
| 1 | SQL | ~65% |
| 2 | Python | ~50% |
| 3 | Excel | ~40% |
| 4 | Tableau | ~38% |
| 5 | Power BI | ~32% |
| 6 | R | ~22% |
| 7 | Azure | ~15% |
| 8 | AWS | ~13% |
| 9 | SAS | ~10% |
| 10 | Snowflake | ~8% |

**Toggle Buttons (below chart):**
- `Job Count` — Shows absolute number of jobs requiring each skill
- `Job Percent` *(active)* — Shows percentage of jobs requiring each skill

---

### 3. What are the Most Paid Jobs?
**Type:** Horizontal Bar Chart

| Property | Detail |
|---|---|
| Y-Axis | Job Title (short) from `job_postings_fact` |
| X-Axis | Dynamic — Median Yearly or Median Hourly Salary (via `Select Salary Measure` parameter) |
| Filter | Filtered by selected country and date context |

**Toggle Buttons (below chart):**
- `Median Yearly Salary` *(active)* — Annual compensation view
- `Median Hourly Salary` — Hourly rate view

---

## 🔗 Data Model Relationships

```
job_postings_fact
    ├── company_dim         (Many-to-One on company_id)
    ├── date_dim            (Many-to-One on date)
    ├── schedule_type_dim   (Many-to-One on schedule_type_id)
    └── skills_job_dim      (One-to-Many via job_id)
                └── skills_dim  (Many-to-One on skill_id)
```

> The `skills_job_dim` acts as a **bridge table** to handle the many-to-many relationship between job postings and skills.

---

## ⚙️ Technical Details

| Property | Detail |
|---|---|
| Tool | Microsoft Power BI Desktop |
| Schema | Star Schema |
| Interactivity | Cross-filtering, drill-through enabled |
| Parameters | Field Parameters (Power BI native) |
| DAX Patterns | CALCULATE, MEDIAN, DIVIDE, COUNTROWS, SELECTEDVALUE |
| Drill Through | Cross-report drill-through toggle available |
| Keep All Filters | Enabled on drill-through |

---

## 💡 Key Insights

- **SQL** is the most in-demand skill for Data Analysts in India, appearing in over 60% of job postings.
- **Python** and **Excel** closely follow, highlighting the blend of programming and spreadsheet proficiency expected.
- The **Median Yearly Salary** for a Data Analyst in India sits at **$74K**, with an hourly equivalent of **$25**.
- Cloud tools like **Azure**, **AWS**, and **Snowflake** appear in a smaller but growing share of postings, indicating rising demand for cloud-savvy analysts.

---

## 📁 Repository Structure

```
📦 Data-Jobs-Dashboard
 ┣ 📊 DataJobs_Dashboard.pbix       # Power BI report file
 ┣ 🖼️  dashboard_preview.png        # Dashboard screenshot
 ┗ 📄 README.md                     # Project documentation (this file)
```




---

*Built with ❤️ using Power BI | Data sourced from public job postings datasets*

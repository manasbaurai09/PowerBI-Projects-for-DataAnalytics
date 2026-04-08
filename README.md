# 📊 Power BI Portfolio — Data Analytics Projects

> A collection of interactive Power BI dashboards analyzing real-world datasets across the **job market**, **ride-hailing**, and **food delivery** domains. Each project demonstrates end-to-end dashboard development — from data modeling and DAX to visual design and storytelling.

---

## 🗂️ Projects Overview

| # | Project | Domain | Key Metrics |
|---|---|---|---|
| 1 | [Data Jobs Dashboard](./PowerBI_Project_1-Data_Jobs_Dashboard) | Job Market & Salaries | Salary, Skills, Job Count |
| 2 | [Uber Analytics Dashboard](./PowerBI_Project_2-Uber_Dashboard) | Ride-Hailing & Revenue | Bookings, Revenue, Ratings |
| 3 | [Zomato Analytics Dashboard](./PowerBI_Project_3-Zomato_Dashboard) | Food Delivery & Orders | Orders, Amount, City Trends |

---

## 1. Data Jobs Dashboard

📁 [`PowerBI_Project_1-Data_Jobs_Dashboard`](./PowerBI_Project_1-Data_Jobs_Dashboard)

### 📌 About
An interactive dashboard analyzing the global data job market — exploring salary benchmarks, in-demand skills, and job distribution across countries and job titles. Designed for job seekers and recruiters to understand what skills pay the most and which are most sought after.

### 🔍 Key Highlights
- Filters by **Job Title** (e.g., Data Analyst) and **Job Country** (e.g., India)
- Identifies **Top 10 in-demand skills** (SQL, Python, Excel, Tableau, Power BI, etc.)
- Compares **Median Yearly vs. Hourly Salary** across roles
- Dynamic toggle between **Job Count** and **Job Percent** views

### 📊 Visuals
- KPI Cards — Job Count, Skills Per Job, Median Yearly Salary, Median Hourly Salary
- Horizontal Bar Chart — Top Demanding Skills
- Horizontal Bar Chart — Most Paid Jobs

### 🗄️ Tables
`job_postings_fact` · `company_dim` · `date_dim` · `skills_dim` · `skills_job_dim` · `schedule_type_dim`

### 💡 Key Insight
> SQL is the #1 demanded skill for Data Analysts in India, appearing in over 60% of job postings, with a median yearly salary of $74K.

---

## 2. Uber Analytics Dashboard

📁 [`PowerBI_Project_2-Uber_Dashboard`](./PowerBI_Project_2-Uber_Dashboard)

### 📌 About
A comprehensive operations dashboard analyzing Uber's ride bookings, revenue, trip distances, and customer/driver ratings. Features a vehicle-type image slicer that dynamically filters the entire report — from Auto to Uber XL.

### 🔍 Key Highlights
- Dynamic **Vehicle Type Image Slicer** (Auto, Bike, Go Mini, Go Sedan, Premier Sedan, Uber XL)
- Tracks **Completed vs. Lost vs. Incomplete** bookings with donut charts
- **Month / Quarter toggle** on both trend charts via field parameter
- Revenue breakdown by all 6 vehicle categories

### 📊 Visuals
- KPI Cards — Completed Bookings, Lost Bookings, Revenue, Total Distance, Avg. Distance
- Donut Charts × 3 — Completed / Cancelled / Incomplete booking shares
- Area Chart — Completed Booking Trend (Monthly/Quarterly)
- Column Chart — Revenue Trend (Monthly/Quarterly)
- Horizontal Bar Chart — Revenue by Vehicle Type
- Rating Cards — Avg. Customer Rating (4.40 ⭐) & Avg. Driver Rating (4.23 ⭐)

### 🗄️ Tables
`Uber` · `Calendar` · `Date Axis` · `IMG`

### 💡 Key Insight
> Auto is the top-revenue vehicle type at ₹13M (~25% of total), while the overall booking completion rate stands at ~62%, flagging cancellations as a key operational challenge.

---

## 3. Zomato Analytics Dashboard

📁 [`PowerBI_Project_3-Zomato_Dashboard`](./PowerBI_Project_3-Zomato_Dashboard)

### 📌 About
A food delivery analytics dashboard tracking Zomato's order trends, city-wise revenue performance, food category preferences, and year-over-year sales growth. Features a dynamic **Top N city slicer** (Top 5 to Top 50) built using a disconnected `RankTable` and `RANKX` DAX logic.

### 🔍 Key Highlights
- **Top N city filter** — dynamically rank and display Top 5 / 10 / 15 / 20 / 50 cities
- Toggle between **Amount** and **Quantity** views across all visuals
- Food category breakdown — **Veg**, **Non Veg**, and **Other** with image cards
- **Year-over-year sales trend** from 2017 to 2020

### 📊 Visuals
- KPI Cards — Total Amount (987M), Quantity (2M), Ratings (148K), Orders (150K)
- Horizontal Bar Chart — Top N Cities by Amount / Quantity
- Image Category Cards × 3 — Veg / Non Veg / Other (Amount + Ratings)
- Line Chart — Sales Amount by Year (2017–2020)

### 🗄️ Tables
`orders` · `food` · `restaurant` · `menu` · `users` · `RankTable`

### 💡 Key Insight
> Tirupati leads all cities with ₹43M in order value. Sales peaked in 2018 at ₹0.41bn before declining, with Veg food dominating both revenue (₹122M) and ratings (12K).

---

## 🛠️ Tech Stack

| Tool | Usage |
|---|---|
| **Power BI Desktop** | Dashboard development, data modeling, visuals |
| **DAX** | Measures, KPIs, RANKX, CALCULATE, SWITCH, time intelligence |
| **Power Query (M)** | Data transformation and cleaning |
| **Star / Snowflake Schema** | Relational data modeling across all projects |
| **Field Parameters** | Dynamic axis and metric toggling |

---

## 📁 Repository Structure

```
📦 PowerBI-Portfolio
 ┣ 📂 PowerBI_Project_1-Data_Jobs_Dashboard
 │   ┣ 📊 DataJobs_Dashboard.pbix
 │   ┣ 🖼️  dashboard_preview.png
 │   ┗ 📄 README.md
 ┣ 📂 PowerBI_Project_2-Uber_Dashboard
 │   ┣ 📊 Uber_Dashboard.pbix
 │   ┣ 🖼️  dashboard_preview.png
 │   ┗ 📄 README.md
 ┣ 📂 PowerBI_Project_3-Zomato_Dashboard
 │   ┣ 📊 Zomato_Dashboard.pbix
 │   ┣ 🖼️  dashboard_preview.png
 │   ┗ 📄 README.md
 ┗ 📄 README.md  ← You are here
```

---

*Built with ❤️ using Power BI | All dashboards are portfolio projects for analytical and learning purposes*

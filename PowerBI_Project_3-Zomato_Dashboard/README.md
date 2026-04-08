# 🍕 Zomato Analytics Dashboard — Power BI Portfolio Project

> An interactive Power BI dashboard tracking food trends, order volumes, revenue, and ratings across cities — with dynamic Top-N city filtering, food category breakdowns, and year-over-year sales trends.

---

## 📌 Project Overview

This dashboard delivers a comprehensive analysis of Zomato's food delivery operations across Indian cities. It enables stakeholders to explore total revenue, order quantities, customer ratings, and city-wise performance — all switchable between **Amount** and **Quantity** views. A dynamic **Top N slicer** (Top 5 / 10 / 15 / 20 / 50) controls the city ranking chart, making it highly interactive and portfolio-worthy. 

The Dataset used in this:- [Zomato Data](Zomato_Data_Source)

---

<img width="1308" height="736" alt="image" src="https://github.com/user-attachments/assets/9a2b2c3d-c118-4f18-97ae-68cfad6f5c79" />


## 🖼️ Dashboard Preview

**Overview KPIs (All Cities / Default View):**

| Metric | Value |
|---|---|
| Total Amount | 987M |
| Total Quantity | 2M |
| Total Ratings | 148K |
| Total Orders | 150K |

**Food Category Breakdown:**

| Category | Sales Amount | Ratings |
|---|---|---|
| Veg | 122M | 12K |
| Non Veg | 106M | 10K |
| Other | 24M | 927 |

---

## 🗄️ Data Model — Tables Used

### Fact Tables

| Table | Description |
|---|---|
| `orders` | Core transaction table — contains order-level data including amount, quantity, date, user, and restaurant references |
| `food` | Food item details — item name, category (Veg / Non Veg / Other), and pricing |

### Dimension Tables

| Table | Description |
|---|---|
| `restaurant` | Restaurant details — name, city, locality, cuisine type |
| `menu` | Menu items linked to restaurants and food items |
| `users` | Customer/user information — demographics and user ID |

### Calculated / Helper Tables

| Table | Description |
|---|---|
| `RankTable` | Helper table used to power the dynamic Top N slicer (stores values: 5, 10, 15, 20, 50) — drives RANKX-based city filtering |
| `_Measures` | Centralized table for all DAX measures (no raw data, purely organizational) |

---

## 📐 DAX Measures

All measures are grouped under the `_Measures` table for clean model organization.

### Core KPI Measures

| Measure | Description |
|---|---|
| `Total Amount` | Sum of order amounts — `SUM(orders[amount])` |
| `Total Quantity` | Sum of items ordered — `SUM(orders[quantity])` |
| `Total Orders` | Count of distinct orders — `COUNTROWS(orders)` |
| `Total Ratings` | Sum or count of ratings submitted — `SUM(orders[rating])` or `COUNT(...)` |

### Food Category Measures

| Measure | Description |
|---|---|
| `Veg Amount` | Total amount from Veg food items — `CALCULATE([Total Amount], food[category] = "Veg")` |
| `Non Veg Amount` | Total amount from Non-Veg food items |
| `Other Amount` | Total amount from Other category items |
| `Veg Rating` | Total ratings for Veg orders |
| `Non Veg Rating` | Total ratings for Non-Veg orders |
| `Other Rating` | Total ratings for Other category orders |

### Dynamic / Ranking Measures

| Measure | Description |
|---|---|
| `City Rank` | Ranks cities by selected metric using `RANKX(ALL(restaurant[city]), [Selected Metric])` |
| `Top N Filter` | Filters city chart to show only cities within the Top N rank — uses `RankTable` selection via `SELECTEDVALUE` |
| `Selected Metric` | Switches between `Total Amount` and `Total Quantity` based on the Amount / Quantity toggle button |

### Time Intelligence Measures

| Measure | Description |
|---|---|
| `Sales Amount by Year` | Total amount grouped by year — used in the line chart trend visual |

---

## 🎛️ Parameters & Slicers

### Dynamic Toggles (Button Slicers)

| Toggle | Options | Effect |
|---|---|---|
| **Amount / Quantity** | Amount *(active)* / Quantity | Switches all city and overview metrics between revenue (₹) and order quantity views |
| **Top N Selector** | Default / Top 5 / Top 10 / Top 15 / Top 20 / Top 50 | Filters the "Top Cities by Amount/Quantity" bar chart to show N cities using `RANKX` logic |

### RankTable Parameter

The `RankTable` is a manually created table with a single column of N values `{5, 10, 15, 20, 50}`. When a user clicks a Top N button:
1. `SELECTEDVALUE(RankTable[N])` captures the chosen number
2. The `Top N Filter` measure uses this to dynamically filter the city bar chart via `City Rank <= Selected N`

---

## 📊 Charts & Visualizations

### 1. Overview KPI Cards
**Type:** Card Visuals × 4

| Card | Metric | Value |
|---|---|---|
| Amount | `Total Amount` | 987M |
| Quantity | `Total Quantity` | 2M |
| Ratings | `Total Ratings` | 148K |
| Orders | `Total Orders` | 150K |

All cards respond to page-level filters and the Amount/Quantity toggle.

---

### 2. Top N Cities by Amount / Quantity
**Type:** Horizontal Bar Chart

| Property | Detail |
|---|---|
| Y-Axis | City name (from `restaurant[city]`) |
| X-Axis | `Selected Metric` (Amount or Quantity) |
| Dynamic Filter | Controlled by Top N button slicer via `RankTable` + `RANKX` |
| Labels | Revenue/Quantity values shown at bar ends |
| Active View | Top 5 (highlighted button) |

**Top 5 Cities by Amount (sample):**

| Rank | City | Amount |
|---|---|---|
| 1 | Tirupati | 43M |
| 2 | Electronic City, Bangalore | 29M |
| 3 | Baner, Pune | 27M |
| 4 | Raipur | 23M |
| 5 | Other | 22M |

---

### 3. Food Category Cards with Images
**Type:** Image Cards / Custom Visual Cards × 3

| Card | Category | Amount | Ratings |
|---|---|---|---|
| 🥗 Veg | Vegetarian | 122M | 12K |
| 🍗 Non Veg | Non-Vegetarian | 106M | 10K |
| 🍔 Other | Other / Mixed | 24M | 927 |

Each card displays a food image, category name, total sales amount, and total ratings side by side. Ratings are highlighted in gold/yellow for visual contrast.

---

### 4. Sales Amount by Year
**Type:** Line Chart

| Property | Detail |
|---|---|
| X-Axis | Year (2017 – 2020) |
| Y-Axis | `Sales Amount by Year` (₹ Billions) |
| Data Points | Labeled at each year node |
| Purpose | Shows year-over-year revenue trend |

**Year-wise trend:**

| Year | Sales Amount |
|---|---|
| 2017 | 0.09bn |
| 2018 | 0.41bn *(peak)* |
| 2019 | 0.34bn |
| 2020 | 0.14bn *(decline)* |

Peak in 2018 followed by a decline, likely reflecting market conditions or dataset scope for 2020.

---

### 5. Zomato Branding Banner (Left Header Panel)
**Type:** Image / Text Visual

Displays the Zomato logo, tagline **"Tracking Food Trends Across Cities"**, and a branded delivery illustration — used for professional portfolio presentation.

---

### 6. Navigation Icons (Left Sidebar)
**Type:** Button Visuals / Bookmarks Navigation

| Icon | Likely Page |
|---|---|
| 🏠 Home | Dashboard (current) |
| 📊 Chart | Analysis / Detail Page |
| 👤 User | User Analytics Page |
| ⚙️ Settings | Settings / Info Page |

The left sidebar uses Power BI buttons with icons for multi-page navigation within the report.

---

## 🔗 Data Model Relationships

```
orders (Fact)
    ├── restaurant   (Many-to-One on restaurant_id)
    ├── users        (Many-to-One on user_id)
    └── menu         (Many-to-One on menu_id)
            └── food (Many-to-One on food_id)

RankTable
    └── Used as disconnected parameter table (no join)
        Drives Top N filtering via SELECTEDVALUE + RANKX
```

---

## ⚙️ Technical Details

| Property | Detail |
|---|---|
| Tool | Microsoft Power BI Desktop |
| Schema | Snowflake / Star Schema |
| Top N Logic | Disconnected `RankTable` + `RANKX` over `ALL(restaurant[city])` |
| Metric Toggle | `SELECTEDVALUE` + `SWITCH` pattern for Amount vs. Quantity |
| Food Images | Embedded image URLs or base64 in visuals |
| Theme | Custom Zomato red/pink branding with light background |
| Navigation | Button-based multi-page navigation with bookmark actions |
| DAX Patterns | RANKX, CALCULATE, SWITCH, SELECTEDVALUE, SUM, COUNTROWS |

---

## 💡 Key Insights

- **Tirupati** leads all cities with ₹43M in order value — significantly ahead of the second-ranked Electronic City, Bangalore (₹29M).
- **Veg food** dominates both in sales (₹122M) and ratings (12K), followed closely by **Non-Veg** (₹106M, 10K ratings), suggesting a balanced but slightly veg-leaning customer base.
- Sales peaked in **2018 at ₹0.41bn**, then declined steadily through 2020 (₹0.14bn), which could reflect competitive pressures or pandemic impact.
- With **150K orders** but only **148K ratings**, the rating capture rate is nearly 99%, indicating strong post-order feedback engagement.
- The **"Other"** food category lags significantly (₹24M, 927 ratings), suggesting it is a niche segment with limited demand.

---

## 📁 Repository Structure

```
📦 Zomato-Analytics-Dashboard
 ┣ 📊 Zomato_Dashboard.pbix         # Power BI report file
 ┣ 🖼️  dashboard_preview.png        # Dashboard screenshot
 ┗ 📄 README.md                     # Project documentation (this file)
```



---

*Built with ❤️ using Power BI | Data represents Zomato food delivery operations for analytical and portfolio purposes*

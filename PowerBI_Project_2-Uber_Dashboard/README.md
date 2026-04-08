# 🚖 Uber Analytics Dashboard — Power BI Portfolio Project

> An interactive Power BI dashboard analyzing Uber's ride bookings, revenue performance, vehicle-type breakdown, and customer/driver satisfaction — with dynamic vehicle-level drill-down and time-period toggles.

---

## 📌 Project Overview

This dashboard presents a full-spectrum analysis of Uber's operations, covering booking volumes, revenue trends, trip distances, and ratings. Users can select a **vehicle type** (Auto, Bike, Go Mini, Go Sedan, Premier Sedan, Uber XL) via a visual image slicer, with all metrics and charts updating dynamically in response.

The design uses a sleek black-and-white aesthetic with Uber branding, and leverages a calendar table, DAX time intelligence, field parameters, and custom image integration for a polished, portfolio-ready output.

---

<img width="1343" height="740" alt="image" src="https://github.com/user-attachments/assets/ef93d1b7-96de-4c82-a3f4-a499388081cd" />


## 🖼️ Dashboard Preview

**Default View — Auto (selected vehicle):**

| KPI | Value |
|---|---|
| Completed Bookings | 93K |
| Lost Bookings | 57K |
| Revenue | ₹ 52M |
| Total Distance | 2.51M |
| Avg. Distance | 24.64 |
| Avg. Customer Rating | 4.40 ⭐ |
| Avg. Driver Rating | 4.23 ⭐ |

---

## 🗄️ Data Model — Tables Used

### Fact / Main Table

| Table | Description |
|---|---|
| `Uber` | Core data table containing all ride records — bookings, cancellations, revenue, distance, ratings, vehicle type, and date |

### Dimension / Supporting Tables

| Table | Description |
|---|---|
| `Calendar` | Date dimension table for time intelligence (used for Month, Quarter, Year slicing) |
| `Date Axis` | Field parameter or separate table to control the X-axis grouping (Month vs. Quarter toggle) on trend charts |
| `IMG` | Image URL table that stores vehicle images for the image slicer (Auto, Bike, Go Mini, Go Sedan, Premier Sedan, Uber XL) |

---

## 📐 DAX Measures

All measures are organized under the `_Measures` table.

### Booking Measures

| Measure | Description |
|---|---|
| `Completed Booking` | Count of rides with a "Completed" status |
| `Lost Booking` | Count of cancelled or incomplete rides (Cancelled by Customer + Cancelled by Driver + Incomplete rides) |
| `Cancelled Bookings` | Rides cancelled by either customer or driver |
| `In Completed Bookings` | Rides that were neither completed nor formally cancelled |
| `Completed Booking %` | Percentage of completed bookings out of total bookings |
| `Cancelled Booking %` | Percentage of cancelled bookings out of total bookings |
| `InCompleted Booking %` | Percentage of incomplete bookings out of total bookings |

### Revenue Measures

| Measure | Description |
|---|---|
| `Revenue` | Total revenue generated from all completed rides — `SUM(Uber[revenue])` |

### Distance Measures

| Measure | Description |
|---|---|
| `Total Distance` | Sum of all trip distances — `SUM(Uber[distance])` |
| `Avg. Distance` | Average distance per trip — `AVERAGE(Uber[distance])` |

### Rating Measures

| Measure | Description |
|---|---|
| `Avg. Customer Rating` | Average rating given by customers — `AVERAGE(Uber[customer_rating])` |
| `Avg. Driver Rating` | Average rating given to drivers — `AVERAGE(Uber[driver_rating])` |

---

## 🎛️ Parameters & Slicers

### Field Parameters

| Parameter | Description |
|---|---|
| `Date Axis` | Dynamically switches the X-axis on the Completed Booking and Revenue trend charts between **Month** and **Quarter** views |

### Visual Slicers

| Slicer | Type | Field | Description |
|---|---|---|---|
| Vehicle Type Image Slicer | Image Tile Slicer | `IMG[vehicle_image]` + `Uber[vehicle_type]` | Clicking a vehicle image (Auto, Bike, etc.) filters the entire dashboard to that vehicle type |

---

## 📊 Charts & Visualizations

### 1. KPI Cards (Top Row)
**Type:** Card Visuals × 5

Dynamic summary cards updating with vehicle and time filters:

| Card | Metric |
|---|---|
| Completed Booking | Total completed rides |
| Lost Booking | Total lost/cancelled rides |
| Revenue | Total revenue (₹) |
| Total Distance | Cumulative distance (km) |
| Avg. Distance | Average trip length (km) |

---

### 2. Vehicle Type Image Slicer (Left Panel)
**Type:** Image Tile Slicer / Custom Visual

| Property | Detail |
|---|---|
| Source | `IMG` table with vehicle image URLs |
| Function | Acts as the primary filter for the entire page |
| Vehicles | Auto, Bike, Go Mini, Go Sedan, Premier Sedan, Uber XL |

The selected vehicle name and image display prominently in the left panel (e.g., "Auto" with the auto-rickshaw image), providing clear visual context for the filtered data.

---

### 3. Booking Status Donut Charts (Left Panel)
**Type:** Donut Charts × 3

| Chart | Metric | Description |
|---|---|---|
| Completed | `Completed Booking %` | Share of rides successfully completed |
| Cancelled | `Cancelled Booking %` | Share cancelled by customer or driver |
| In Completed | `InCompleted Booking %` | Share of rides that were incomplete |

Each donut includes a text description below for user clarity.

---

### 4. Completed Booking Trend
**Type:** Area Chart

| Property | Detail |
|---|---|
| X-Axis | Month or Quarter (controlled by `Date Axis` parameter toggle) |
| Y-Axis | `Completed Booking` measure |
| Toggle Buttons | **Month** (active) / **Quarter** |
| Range Displayed | Jan – Dec |
| Purpose | Tracks ride volume fluctuation over time |

---

### 5. Revenue Trend
**Type:** Column (Bar) Chart

| Property | Detail |
|---|---|
| X-Axis | Month or Quarter (controlled by `Date Axis` parameter toggle) |
| Y-Axis | `Revenue` measure (₹) |
| Toggle Buttons | **Month** (active) / **Quarter** |
| Range Displayed | Jan – Dec |
| Purpose | Visualizes monthly/quarterly revenue performance |

---

### 6. Revenue by Vehicle Type
**Type:** Horizontal Bar Chart

| Property | Detail |
|---|---|
| Y-Axis | Vehicle Type (Auto, Bike, Go Mini, Go Sedan, Premier Sedan, Uber XL) |
| X-Axis | `Revenue` measure |
| Labels | Revenue values shown at end of each bar |
| Purpose | Compares revenue contribution across all vehicle categories |

**Revenue breakdown (approx.):**

| Vehicle | Revenue |
|---|---|
| Auto | ₹ 13M |
| Bike | ₹ 11M |
| Go Mini | ₹ 10M |
| Go Sedan | ₹ 9M |
| Premier Sedan | ₹ 6M |
| Uber XL | ₹ 2M |

---

### 7. Average Customer Rating Card
**Type:** Card Visual with Star Rating

| Property | Detail |
|---|---|
| Metric | `Avg. Customer Rating` |
| Display | Numeric value (4.40) + star visual |
| Purpose | Reflects overall customer satisfaction |

---

### 8. Average Driver Rating Card
**Type:** Card Visual with Star Rating

| Property | Detail |
|---|---|
| Metric | `Avg. Driver Rating` |
| Display | Numeric value (4.23) + star visual |
| Purpose | Reflects overall driver performance rating |

---

## 🔗 Data Model Relationships

```
Calendar
    └── Uber  (One-to-Many on Date)

IMG
    └── Uber  (One-to-Many on vehicle_type — drives image slicer)

Date Axis
    └── Used as Field Parameter for chart X-axis toggle
```

---

## ⚙️ Technical Details

| Property | Detail |
|---|---|
| Tool | Microsoft Power BI Desktop |
| Schema | Star-like Schema |
| Vehicle Filter | Image Tile Slicer (custom visual or native tile slicer) |
| Time Toggle | Field Parameter — Month / Quarter |
| DAX Patterns | CALCULATE, SUM, AVERAGE, DIVIDE, COUNTROWS, time intelligence |
| Image Integration | `IMG` table with image URLs rendered in tile slicer |
| Theme | Custom black & white with Uber branding |

---

## 💡 Key Insights

- **Auto** is the highest-revenue vehicle type at ₹13M, contributing ~25% of total revenue.
- **93K completed bookings** vs. **57K lost bookings** indicates a completion rate of ~62%, highlighting cancellation as a key area for operational improvement.
- Revenue and bookings peak mid-year (around **March–April**) before stabilizing, suggesting seasonal demand patterns.
- **Customer ratings (4.40)** are slightly higher than **driver ratings (4.23)**, both above the industry-standard satisfaction threshold of 4.0.
- **Uber XL** generates the least revenue (₹2M), possibly reflecting lower demand or limited supply for the premium large-vehicle segment.

---

## 📁 Repository Structure

```
📦 Uber-Analytics-Dashboard
 ┣ 📊 Uber_Dashboard.pbix           # Power BI report file
 ┣ 🖼️  dashboard_preview.png        # Dashboard screenshot
 ┗ 📄 README.md                     # Project documentation (this file)
```



---

*Built with ❤️ using Power BI | Data is representative of Uber ride operations for analytical purposes*

# 📊 Candidate Engagement and Follow-Up Analysis Dashboard

**Senior Research Analyst Project | U.S. Department of Labor (DOL)**  
*Powered by RStudio · OpenAI · xAI · Shiny*

---

## 📌 [Overview](#overview)

This interactive dashboard provides a comparative analysis of job candidate engagement across the U.S. and U.K., covering the entire candidate lifecycle—from initial interview to final offer acceptance. Built using **low-code/no-code principles**, this tool empowers policy analysts, labor economists, HR practitioners, and data scientists to visualize and download insights without writing code.

---

## 🧠 [How This Was Accomplished](#how-this-was-accomplished)

This dashboard was developed using:

- **RStudio + Shiny**: For rapid prototyping and visualizing multi-dimensional data.
- **OpenAI + xAI**: Used for generating insights, documentation, and automating code design.
- **Low-Code/No-Code Approach**: Pre-built datasets and modular UI components allow non-coders to interact and derive policy-driven insights.
- **Clean Code**: Modular and reusable; integrates drop-down menus, interactive plots, and data download capabilities.

---

## 🔍 [Key Features](#key-features)

- 📍 Region-based drill-down for U.S. and U.K. labor engagement.
- 📈 Compare metrics across regions (e.g., Midwest vs. London).
- 📊 Switch between **Bar** and **Line** plots dynamically.
- 📥 Export raw data by category and country in `.csv` format.
- 🧾 Tabular view of structured interview, follow-up, and satisfaction data.

---

## 🗂️ [Datasets](#datasets)

All data used in this project are **simulated representations** based on typical labor engagement KPIs. In a live production scenario, these would be ingested via APIs or SQL pipelines connected to verified data warehouses.

| Dataset Type          | Metrics Captured                                | Source |
|-----------------------|--------------------------------------------------|--------|
| Interview Process     | Success rates, rejection counts, satisfaction   | Simulated (based on EEOC reports) |
| Follow-Up Process     | Email/phone follow-ups, satisfaction            | Simulated (based on HR survey templates) |
| Satisfaction Survey   | Interview, communication, follow-up experiences | Custom simulation |
| Offer Acceptance      | Offer conversion rates                          | Simulated with regional variance |
| Demographics          | Gender and age breakdowns                       | Simulated (based on DOL age/gender ratios) |
| Conversion Funnel     | Leads → Interviews → Offers → Acceptances       | End-to-end candidate tracking |

---

## 🧪 [Working Code](#working-code)

The full Shiny app code is included in [`app.R`](./app.R). Below is the core logic used to load and visualize the dataset:

<details>
<summary>Click to Expand R Shiny Code Snippet</summary>

```r
# Load required libraries
library(shiny)
library(ggplot2)
library(dplyr)
library(tidyr)
library(viridis)
library(DT)

# ...full UI and server code available in app.R
```

</details>

---

## 🖼️ [UI Highlights](#ui-highlights)

- 📌 **Sidebar Inputs**: Select country, data type, and plot type.
- 📊 **Main Panel**:
  - Responsive plots using `ggplot2` and `viridis`.
  - Interactive data tables using `DT`.
- 💾 **Export Feature**: One-click `.csv` download of active dataset.

---

## 🌐 [Applications and Use Cases](#applications-and-use-cases)

This dashboard supports both **domestic and international labor policy analysis** and is applicable to:

- 🔹 Labor market researchers
- 🔹 Federal HR departments
- 🔹 International workforce benchmarking
- 🔹 DEI-focused recruitment optimization
- 🔹 DOL-funded policy pilot evaluations

---

## 🚀 [Future Enhancements](#future-enhancements)

- 🔗 Connect to live data via SQL or REST API endpoints
- 📍 Geospatial mapping with `leaflet`
- 🔍 Predictive modeling on offer acceptance trends using ML
- 🌍 Multi-language support for global HR teams

---

## 📥 [Getting Started](#getting-started)

To run locally:

```bash
# Clone repo
git clone https://github.com/your-org/candidate-engagement-dashboard.git

# Open in RStudio and run app.R
```

No advanced R knowledge required. Built for **analysts, not just developers**.

---

## 🧾 [Acknowledgements](#acknowledgements)

- U.S. Department of Labor Public Research Archives  
- OpenAI Codex + xAI for idea generation and documentation
- Tidyverse for clean data wrangling
- RStudio + Shiny for making dashboards that speak to everyone

---

## 📬 [Feedback or Collaboration](#feedback-or-collaboration)

If you’re a data scientist, policymaker, or labor economist interested in expanding this project, feel free to [open an issue](https://github.com/your-org/candidate-engagement-dashboard/issues) or connect on [LinkedIn](https://www.linkedin.com).

---

Let me know if you’d like the README saved as a `.md` file or want it styled for a specific GitHub theme (dark/light mode).

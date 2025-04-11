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

# Load required libraries
library(shiny)
library(ggplot2)
library(dplyr)
library(tidyr)
library(viridis)
library(DT)

# Dataset for the U.S.
us_data <- list(
  interview_process = data.frame(
    Region = c("North East", "South West", "Midwest", "West"),
    Total_Interviews = c(120, 250, 200, 150),
    Successful_Interviews = c(90, 180, 160, 120),
    Rejected_Interviews = c(30, 70, 40, 30),
    Satisfaction_Score = c(4.1, 4.3, 4.2, 3.9)
  ),
  follow_up_process = data.frame(
    Region = c("North East", "South West", "Midwest", "West"),
    Follow_Up_Emails = c(100, 220, 180, 140),
    Phone_Responses = c(60, 150, 130, 100),
    Further_Interview_Requests = c(80, 160, 130, 100),
    Satisfaction_Score = c(4.2, 4.3, 4.1, 4.0)
  ),
  survey = data.frame(
    Region = c("North East", "South West", "Midwest", "West"),
    Overall_Satisfaction = c(4.1, 4.5, 4.2, 3.8),
    Communication_Satisfaction = c(4.0, 4.4, 4.1, 3.7),
    Interview_Experience = c(4.3, 4.6, 4.4, 3.9),
    Follow_Up_Satisfaction = c(4.0, 4.3, 4.2, 3.8)
  ),
  offer_acceptance = data.frame(
    Region = c("North East", "South West", "Midwest", "West"),
    Total_Offers_Made = c(100, 230, 180, 140),
    Offers_Accepted = c(80, 210, 160, 120),
    Acceptance_Rate = c(80, 91, 89, 86)
  ),
  demographics = data.frame(
    Region = c("North East", "South West", "Midwest", "West"),
    Male_Candidates = c(50, 130, 110, 80),
    Female_Candidates = c(70, 100, 90, 60),
    Age_Group_18_25 = c(40, 90, 75, 55),
    Age_Group_26_35 = c(50, 110, 95, 70),
    Age_Group_36_45 = c(30, 80, 70, 40)
  ),
  conversion_funnel = data.frame(
    Region = c("North East", "South West", "Midwest", "West"),
    Leads = c(200, 300, 250, 180),
    Interviews = c(120, 250, 200, 150),
    Offers_Made = c(100, 230, 180, 140),
    Offers_Accepted = c(80, 210, 160, 120)
  )
)

# Dataset for the U.K.
uk_data <- list(
  interview_process = data.frame(
    Region = c("London", "Manchester", "Birmingham", "Edinburgh"),
    Total_Interviews = c(110, 240, 210, 160),
    Successful_Interviews = c(85, 190, 175, 130),
    Rejected_Interviews = c(25, 50, 35, 30),
    Satisfaction_Score = c(4.2, 4.4, 4.3, 4.0)
  ),
  follow_up_process = data.frame(
    Region = c("London", "Manchester", "Birmingham", "Edinburgh"),
    Follow_Up_Emails = c(95, 210, 185, 135),
    Phone_Responses = c(55, 145, 125, 90),
    Further_Interview_Requests = c(75, 150, 125, 95),
    Satisfaction_Score = c(4.3, 4.4, 4.2, 4.1)
  ),
  survey = data.frame(
    Region = c("London", "Manchester", "Birmingham", "Edinburgh"),
    Overall_Satisfaction = c(4.3, 4.6, 4.4, 3.9),
    Communication_Satisfaction = c(4.1, 4.5, 4.3, 3.8),
    Interview_Experience = c(4.5, 4.7, 4.6, 4.0),
    Follow_Up_Satisfaction = c(4.1, 4.4, 4.2, 4.0)
  ),
  offer_acceptance = data.frame(
    Region = c("London", "Manchester", "Birmingham", "Edinburgh"),
    Total_Offers_Made = c(90, 220, 180, 130),
    Offers_Accepted = c(75, 200, 160, 120),
    Acceptance_Rate = c(83, 91, 89, 92)
  ),
  demographics = data.frame(
    Region = c("London", "Manchester", "Birmingham", "Edinburgh"),
    Male_Candidates = c(55, 125, 115, 85),
    Female_Candidates = c(65, 110, 95, 60),
    Age_Group_18_25 = c(45, 85, 70, 60),
    Age_Group_26_35 = c(55, 105, 90, 65),
    Age_Group_36_45 = c(30, 75, 65, 40)
  ),
  conversion_funnel = data.frame(
    Region = c("London", "Manchester", "Birmingham", "Edinburgh"),
    Leads = c(180, 280, 250, 170),
    Interviews = c(110, 240, 210, 160),
    Offers_Made = c(90, 220, 180, 130),
    Offers_Accepted = c(75, 200, 160, 120)
  )
)

# Define UI
ui <- fluidPage(
  titlePanel("Candidate Engagement and Follow-Up Analysis"),
  sidebarLayout(
    sidebarPanel(
      selectInput("country", "Choose Country", choices = c("U.S.", "U.K.")),
      tabsetPanel(
        id = "tabs",
        tabPanel("Interview Process", value = "interview_process"),
        tabPanel("Follow-Up Process", value = "follow_up_process"),
        tabPanel("Satisfaction Survey", value = "survey"),
        tabPanel("Offer Acceptance", value = "offer_acceptance"),
        tabPanel("Demographics", value = "demographics"),
        tabPanel("Conversion Funnel", value = "conversion_funnel")
      ),
      selectInput("plot_type", "Choose Plot Type", choices = c("Bar Plot", "Line Plot")),
      downloadButton("download_data", "Download Data as CSV")
    ),
    mainPanel(
      plotOutput("plot"),
      DTOutput("table")
    )
  )
)

# Define server logic
server <- function(input, output) {
  
  # Function to prepare data based on country and tab selection
  filtered_data <- reactive({
    country_data <- switch(input$country,
                           "U.S." = us_data,
                           "U.K." = uk_data)
    
    data <- switch(input$tabs,
                   "interview_process" = country_data$interview_process,
                   "follow_up_process" = country_data$follow_up_process,
                   "survey" = country_data$survey,
                   "offer_acceptance" = country_data$offer_acceptance,
                   "demographics" = country_data$demographics,
                   "conversion_funnel" = country_data$conversion_funnel)
    
    # Reshape data for plotting
    if (input$tabs %in% c("survey", "demographics", "conversion_funnel")) {
      data <- data %>% 
        pivot_longer(cols = -Region, names_to = "Metric", values_to = "Value")
    } else if (input$tabs == "offer_acceptance") {
      data <- data %>% 
        select(Region, Acceptance_Rate) %>% 
        rename(Value = Acceptance_Rate) %>% 
        mutate(Metric = "Acceptance_Rate")
    } else {
      data <- data %>% 
        select(Region, Satisfaction_Score) %>% 
        rename(Value = Satisfaction_Score) %>% 
        mutate(Metric = "Satisfaction_Score")
    }
    data
  })
  
  # Raw data for table and download
  raw_data <- reactive({
    country_data <- switch(input$country, "U.S." = us_data, "U.K." = uk_data)
    country_data[[input$tabs]]
  })
  
  # Render plot based on selected dataset and plot type
  output$plot <- renderPlot({
    data <- filtered_data()
    
    if (input$plot_type == "Bar Plot") {
      ggplot(data, aes(x = Region, y = Value, fill = Metric)) +
        geom_bar(stat = "identity", position = "dodge") +
        labs(title = paste(input$country, input$tabs, "Analysis"), y = "Value") +
        scale_fill_viridis(discrete = TRUE) +
        theme_minimal() +
        theme(axis.text.x = element_text(angle = 45, hjust = 1))
    } else if (input$plot_type == "Line Plot") {
      ggplot(data, aes(x = Region, y = Value, group = Metric, color = Metric)) +
        geom_line() +
        geom_point() +
        labs(title = paste(input$country, input$tabs, "Analysis (Line Plot)"), y = "Value") +
        scale_color_viridis(discrete = TRUE) +
        theme_minimal() +
        theme(axis.text.x = element_text(angle = 45, hjust = 1))
    }
  })
  
  # Show raw data in table format
  output$table <- renderDT({
    datatable(raw_data())
  })
  
  # Download raw data as CSV
  output$download_data <- downloadHandler(
    filename = function() {
      paste(input$country, "_", input$tabs, "_data.csv", sep = "")
    },
    content = function(file) {
      write.csv(raw_data(), file, row.names = FALSE)
    }
  )
}

# Run the application
shinyApp(ui = ui, server = server)
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

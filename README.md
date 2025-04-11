# CandidateEngagementDashboard

A Shiny dashboard for analyzing candidate engagement and follow-up processes across U.S. and U.K. regions, built with R and deployable for actionable insights.

---

## Table of Contents

- [Summary](#summary)
- [Features](#features)
- [How It Works](#how-it-works)
- [Technical Details](#technical-details)
- [Installation](#installation)
- [Usage](#usage)
- [Why This Matters](#why-this-matters)
- [Conclusion](#conclusion)

---

## Summary

The `CandidateEngagementDashboard` is an interactive web application designed to track and visualize candidate recruitment metrics across regions in the U.S. and U.K. Developed using R Shiny, this project evolved from raw datasets into a polished tool with the help of xAI’s Grok AI. It started with basic dataframes for interview processes, follow-ups, satisfaction surveys, offer acceptance rates, demographics, and conversion funnels. Through iterative refinement, I addressed plotting errors (e.g., missing `Value` columns), added dynamic data reshaping with `tidyr`, and integrated bar/line plot options for flexibility. The app now offers downloadable CSV exports, interactive tables via `DT`, and a sleek UI—making it valuable for HR teams and data enthusiasts alike.

---

## Features

- **Multi-Region Analysis**: Compare candidate data across U.S. (e.g., North East, Midwest) and U.K. (e.g., London, Edinburgh) regions.
- **Diverse Metrics**: Covers interviews, follow-ups, satisfaction, offer acceptance, demographics, and conversion funnels.
- **Interactive Visuals**: Toggle between bar and line plots to spot trends or compare metrics.
- **Data Tables**: View raw data with searchable, sortable tables.
- **Exportable Insights**: Download datasets as CSV files for offline use.
- **User-Friendly Design**: Simple sidebar with country and category tabs for easy navigation.

---

## How It Works

For non-technical folks: Imagine a dashboard where you pick a country (U.S. or U.K.) and a category (like "Satisfaction Survey"). You’ll see colorful charts showing how candidates rate their experience across regions—bars for quick comparisons, lines for trends. Below that, a table lists all the numbers, and you can save it as a spreadsheet with one click.

For techies: The app uses `shiny` for the UI, `ggplot2` for plots, and `DT` for tables. Data is stored in nested lists (`us_data`, `uk_data`), reshaped with `pivot_longer` for multi-metric datasets (e.g., demographics), and plotted dynamically based on user input. Reactive expressions ensure seamless updates across tabs and plot types.

---

## Technical Details

- **Libraries**: `shiny`, `ggplot2`, `dplyr`, `tidyr`, `viridis`, `DT`.
- **Data Structure**: Six datasets per country, each with region-specific metrics (e.g., `Satisfaction_Score`, `Acceptance_Rate`).
- **Key Fixes**: Resolved plotting errors by reshaping data into `Metric`/`Value` pairs, added plot type selector (`Bar Plot`/`Line Plot`), and separated raw data for tables/downloads.
- **Code Highlights**: 
  - Reactive data prep with `switch` and `pivot_longer`.
  - Dynamic `ggplot` with conditional `fill`/`color` for multi-metric visualization.
  - CSV export via `downloadHandler`.

---

## Installation

1. **Install R**: Download from [CRAN](https://cran.r-project.org/).
2. **Install Libraries**: Run in R console:
   ```R
   install.packages(c("shiny", "ggplot2", "dplyr", "tidyr", "viridis", "DT"))
   ```
3. **Clone Repo**: 
   ```bash
   git clone https://github.com/your-username/CandidateEngagementDashboard.git
   ```
4. **Run App**: Open `app.R` in RStudio and click "Run App".

---

## Usage

- **Launch**: Start the app locally or deploy to shinyapps.io.
- **Explore**: Select a country and tab (e.g., "U.S." > "Offer Acceptance").
- **Visualize**: Choose "Bar Plot" for comparisons or "Line Plot" for trends.
- **Interact**: Scroll the table or search for specific values.
- **Download**: Click "Download Data as CSV" to save the current dataset.

Non-tech tip: Play with the tabs to see what’s working well in each region! Tech tip: Check the `server` function for reactive logic.

---

## Why This Matters

This dashboard bridges data and decisions. For HR teams, it reveals where candidate experiences shine or stumble—think higher satisfaction in London (4.6) vs. Edinburgh (3.9). For businesses, it’s a tool to optimize hiring, boost acceptance rates, and understand demographics—all in one glance. Technically, it’s a showcase of low-code analytics with R, proving you don’t need a PhD to turn numbers into insights. It’s about making recruitment smarter, faster, and fairer.

---

## Conclusion

The `CandidateEngagementDashboard` is more than code—it’s a story of turning data into action. From fixing bugs to adding polish, this project blends technical finesse with real-world value. Whether you’re an HR pro wanting better hires or a coder learning Shiny, dive in, fork it, and make it yours. Let’s keep improving how we connect talent with opportunity!

---

## Features

- Select country: U.S. or U.K.
- Analyze various stages:
  - Interview Process
  - Follow-Up Process
  - Satisfaction Survey
  - Offer Acceptance
  - Demographics
  - Conversion Funnel
- Choose between Bar Plot and Line Plot visualization
- View interactive data tables
- Download selected data as CSV

## Technologies Used

- R and Shiny
- ggplot2 for data visualization
- dplyr and tidyr for data manipulation
- viridis for color palettes
- DT for interactive data tables

## Screenshots

(Add screenshots of your app here)

## Installation

To run this app locally, you need to have R and RStudio installed.

Install the required packages if not already installed:

```r
install.packages(c("shiny", "ggplot2", "dplyr", "tidyr", "viridis", "DT"))
```

Then run the app using the code below.

## Full Shiny App Code

```r
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

    if (input$tabs %in% c("survey", "demographics", "conversion_funnel")) {
      data <- data %>% pivot_longer(cols = -Region, names_to = "Metric", values_to = "Value")
    } else if (input$tabs == "offer_acceptance") {
      data <- data %>% select(Region, Acceptance_Rate) %>% rename(Value = Acceptance_Rate) %>% mutate(Metric = "Acceptance_Rate")
    } else {
      data <- data %>% select(Region, Satisfaction_Score) %>% rename(Value = Satisfaction_Score) %>% mutate(Metric = "Satisfaction_Score")
    }
    data
  })

  raw_data <- reactive({
    country_data <- switch(input$country, "U.S." = us_data, "U.K." = uk_data)
    country_data[[input$tabs]]
  })

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

  output$table <- renderDT({
    datatable(raw_data())
  })

  output$download_data <- downloadHandler(
    filename = function() {
      paste(input$country, "_", input$tabs, "_data.csv", sep = "")
    },
    content = function(file) {
      write.csv(raw_data(), file, row.names = FALSE)
    }
  )
}

shinyApp(ui = ui, server = server)
```

---

## Author
Maurice McDonald - [Your GitHub](https://github.com/emcdo411)

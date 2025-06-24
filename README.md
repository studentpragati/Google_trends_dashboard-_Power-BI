# 📊 Google Trends Analysis Using Power BI

## 🚀 Overview

This project uses *Power BI* to import data from *Google Trends* via the *SerpAPI*. It allows users to track, analyze, and visualize the performance of up to five keywords over time, across regions, and discover related topics. The interactive dashboard offers insights into trends and regional interests, helping guide decision-making in areas such as marketing, content creation, and SEO optimization.

---

## 🔍 Project Components

### 1. 📅 Keyword Performance Over Time
- *All-Time Data*:
  - *🎯 Purpose*: To retrieve historical search interest for up to five keywords, from the start of Google Trends data collection to the present.
  - *⚙ Functionality*: Enables users to observe long-term trends in keyword popularity.
  
- *Past 7 Days Data*:
  - *🎯 Purpose*: Focuses on recent trends, identifying short-term changes or spikes in search interest.
  - *⚙ Functionality*: Helps users stay updated on immediate shifts in public interest.

### 2. 🌍 Geographical Analysis of Keywords
- *🎯 Purpose*: Provides a geographical breakdown of search interest for the specified keywords, showing where each keyword is most popular over the past 5 years.
- *⚙ Functionality*: 
  - Displays regional data, allowing users to compare search interest in different countries or regions.
  - Useful for identifying key markets for specific keywords.

### 3. 📈 Analysis of Related Topics (Rising and Top Keywords)
- *🎯 Purpose*: To discover related topics and keywords associated with the main keyword.
- *⚙ Functionality*:
  - *📈 Rising Keywords*: Highlights search terms related to the main keyword that are gaining popularity.
  - *📊 Top Keywords*: Lists the most consistently popular keywords associated with the main keyword.

---

## 🎯 Project Aim and Key Objectives

The goal of this project is to help users monitor keyword trends, analyze regional interest, and explore related topics in a user-friendly, visual manner. The project provides businesses, marketers, content creators, and analysts with actionable insights.

### ✨ Key Objectives:
1. *📊 Monitor Keyword Trends*:
   - Compare the popularity of up to five keywords (e.g., "Data Analyst," "The Developer," "Jobs," "India," "Power BI").
   - Track how public interest in these terms has evolved over time.
   
2. *🌍 Geographical Insights*:
   - Visualize search interest by region to identify where specific keywords are most popular.
   - Provide insights into regional demand and market interest.
   
3. *🔍 Discover Related Topics*:
   - *📈 Rising Keywords*: Identify emerging search terms gaining popularity related to the main keyword.
   - *📊 Top Keywords*: Highlight consistently popular search terms.
   
4. *⏳ Time-Based Keyword Performance*:
   - Fetch data for different time frames (e.g., past 7 days, last 5 years, or all-time data) for both short-term and long-term trends.

---

## 🛠 Features of the Dashboard

### 1. *📅 Keyword Performance Tracking (Over Time)*
   - *Feature*: Displays the popularity of up to five keywords over selected time periods (e.g., past 7 days, last 5 years, all-time).
   - *Visualization*: Line or area charts compare the search interest for each keyword.
   - *Use Case*: Observe how interest in different keywords fluctuates over time, identify trends, and detect events that triggered spikes in interest.

### 2. *🌍 Geographical Breakdown*
   - *Feature*: Shows where each keyword is most popular by region or country.
   - *Visualization*: Interactive Geo Maps highlight regions based on search volume.
   - *Use Case*: Analyze regional search trends and identify high-interest markets.

### 3. *📈 Rising and Top Keywords*
   - *Feature*: Identifies related keywords, categorized into rising and top.
   - *Visualization*: Tables or word clouds showing rising and top keywords.
   - *Use Case*: Discover emerging trends and adjust content strategies to stay ahead of competitors.

### 4. *⏳ Time-Based Data Selection*
   - *Feature*: Allows users to select different time frames for keyword analysis (e.g., last 7 days, last 12 months, all-time).
   - *Visualization*: Time-based filters dynamically update the graphs and metrics.
   - *Use Case*: Supports short-term and long-term trend analysis.

### 5. *🔢 Total Searches Overview*
   - *Feature*: Displays the total search volume for all selected keywords.
   - *Visualization*: A summary section shows the total number of searches.
   - *Use Case*: Provides a quick overview of overall interest.

### 6. *⚖ Keyword Comparison*
   - *Feature*: Compares the five selected keywords in terms of search volume, rising trends, and geographical performance.
   - *Visualization*: Combination of line graphs, bar charts, and tables.
   - *Use Case*: Compare how different keywords perform, aiding in decision-making.

### 7. *🔄 Auto-Refresh of Data*
   - *Feature*: Automatically updates the dashboard with the latest data from Google Trends API.
   - *Use Case*: Ensures the data is always current without manual updates.

### 8. *🔍 Customizable Filtering*
   - *Feature*: Provides filtering options by country, date range, or specific keyword.
   - *Visualization*: Drop-down menus or slider bars to adjust filters dynamically.
   - *Use Case*: Tailor the insights to specific regions or time frames.

---

## 🔧 How to Use the API

### 📅 API 1: Keyword Performance Over Time (Past 7 Days)

m
let
    BaseUrl = "https://serpapi.com/search",
    QueryParams = [
        engine = "google_trends",
        q = "Data Analyst,The Developer,Jobs,India,Power BI",
        data_type = "TIMESERIES",
        date = "now 7-d",
        tz = "-330",
        api_key = "Paste your key here"
    ],
    UrlWithParams = BaseUrl & "?" & Text.Combine(List.Transform(Record.FieldNames(QueryParams), 
        each _ & "=" & Uri.EscapeDataString(Record.Field(QueryParams, _))), "&"),
    JsonResponse = Json.Document(Web.Contents(UrlWithParams)),
    InterestOverTime = JsonResponse[#"interest_over_time"]
in
    InterestOverTime


---

### 🕰 API 2: All-Time Keyword Performance

m
let
    BaseUrl = "https://serpapi.com/search",
    QueryParams = [
        engine = "google_trends",
        q = "Data Analyst,The Developer,Jobs,India,Power BI",
        data_type = "TIMESERIES",
        date = "all",
        tz = "-330",
        api_key = "Paste your key here"
    ],
    UrlWithParams = BaseUrl & "?" & Text.Combine(List.Transform(Record.FieldNames(QueryParams), 
        each _ & "=" & Uri.EscapeDataString(Record.Field(QueryParams, _))), "&"),
    JsonResponse = Json.Document(Web.Contents(UrlWithParams)),
    InterestOverTime = JsonResponse[#"interest_over_time"]
in
    InterestOverTime


---

### 🌍 API 3: Geographical Analysis of Keywords

m
let
    apiUrl = "https://serpapi.com/search.json",
    queryParams = [
        engine = "google_trends",
        q = "Data Analyst,The Developer,Jobs,India,Power BI",
        data_type = "GEO_MAP",
        date = "today 5-y",
        tz = "-330",
        api_key = "Paste your key here"
    ],
    fullUrl = apiUrl & "?" & Uri.BuildQueryString(queryParams),
    response = Web.Contents(fullUrl),
    jsonResponse = Json.Document(response),
    dataTable = Table.FromRecords({jsonResponse}),
    comparedBreakdownByRegion = dataTable{0}[compared_breakdown_by_region]
in
    comparedBreakdownByRegion


---

### 🔍 API 4: Rising and Top Keywords

m
let
    apiUrl = "https://serpapi.com/search.json",
    queryParams = [
        engine = "google_trends",
        q = "The Developer",
        data_type = "RELATED_TOPICS",
        api_key = "Paste your key"
    ],
    fullUrl = apiUrl & "?" & Uri.BuildQueryString(queryParams),
    response = Web.Contents(fullUrl),
    jsonResponse = Json.Document(response)
in
    jsonResponse



---

## 🔚 Conclusion
- This Google Trends Analysis Dashboard provides an intuitive way to track keyword performance, analyze regional interest, and discover related topics. By integrating Google Trends data into Power BI, the dashboard offers actionable insights for marketing, content strategy, and business development.

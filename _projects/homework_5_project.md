---
name: Homework 5.1
tools: [Python, HTML, vega-lite, Altair]
image: assets/pngs/visualization.png
description: Bigfoot sighting data interactive plots using Vega-lite & Altair
custom_js:
  - vega.min
  - vega-lite.min
  - vega-embed.min
  - justcharts
---


# Daily Dew Point Distributions Across the Calendar Year

<vegachart schema-url="{{ site.baseurl }}/assets/json/heatmap.json" style="width: 100%"></vegachart>

## Write Up
This heatmap visualizes **average daily dew point patterns across the calendar year** using environmental data linked to Bigfoot sighting reports. The heatmap focuses on how dew points vary temporally. Each small square represents a specific day (e.g., March 15th or July 3rd). The color of the square shows the average dew point for that day across all years in the dataset. Darker colors mean more cooler temperatures and precipitation conditions, while lighter colors indicate drier air. 

Encoding Strategy
X-axis: Days of month 1, 31 (`date(date):O`) as ordinal, enforcing consistent 1-31 day labels despite varying month lengths
Y-axis: Month (`month(date):O`) as ordinal, formatted with 3-letter abbreviations (%b) for seasonal representation using short names like "Jan" or "Feb." 
Color: Mean dew point (`mean(dew_point):Q`) using a sequential blue scheme, intuitively mapping darker hues to higher moisture levels  


Color Semantics/Choice
The `blues` color scheme was chosen to represent dew points because people naturally associate blue with water and rain (precipitation). Darker blues represent higher dew points (muggier days), while lighter blues show drier conditions visualizing the contrast expected between typical dew point ranges (20°F-70°F). This makes it easy to see at a glance which days or months tend to be more humid over time.

Data Transformations
Before plotting, I cleaned the dataset, removing days with missing dew points and filtering of null dew points via `transform_filter` to avoid errors.  Date formatting was necessary, to convert raw dates into a format the chart could use to identify months and days, parsing via `format={'parse': {'date': 'utc:%Y-%m-%d’}}`.  Averaging, dew point values were averaged for each day (e.g., all January 1sts across multiple years are combined into one average value). Aggregate metrics in tooltips (UV index, temperature high, pressure) using (mean/max) methods.

The visualization showcases monthly moisture patterns while the interactive tooltips add extra context: hovering over a square reveals the month’s full name, the day, and related weather details like UV index, temperature highs and air pressure. By encoding time across both axes, it creates a calendar-like matrix that reveals possible correlations between specific date ranges and humidity levels (dew points). The choice of dew point rather than humidity as the target metric is dew point can provide a more detailed measure of actual air moisture measurements. By organizing the data in this way, the chart helps to identify trends.

# Monthly Precipitation Probabilities over 6 Years

<vegachart schema-url="{{ site.baseurl }}/assets/json/line.json" style="width: 100%"></vegachart>

## Write Up

This line chart visualizes **monthly precipitation trends from 2001 to 2006**, offering a clear comparison of how rain probabilities shift across seasons and years. Each colored line represents a single year, tracing the average likelihood of rain (% chance) month by month, with circular markers highlighting exact values. The x-axis organizes time seasonally (January to December), while the y-axis quantifies precipitation probability, creating a rhythm that reveals patterns like wetter springs or drier autumns in specific years. Years are distinguished using a qualitative color scheme which helps viewers track individual years’ trends without overwhelming the plot. The design intentionally limits the timeframe to six years to balance detail and readability—too many lines could clutter the view, but this range allows easy comparison of mid-2000s climate variations.  

Key data transformations include filtering out years outside 2001–2006 and aggregating daily probabilities into monthly averages. Interactive tooltips enhance exploration, letting users hover to see exact percentages, months, and years. By encoding time seasonally rather than chronologically, the chart answers questions like “Did summers grow drier in this period?” or “Which year had the rainiest winters?” The circular markers add precision, while the color choices ensure lines remain distinct yet harmonious. This balances simplicity and depth, making it accessible for spotting both annual anomalies and seasonal patterns.

<!-- these are written in a combo of html and liquid --> 

<div class="left">
{% include elements/button.html link="https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/bfro_reports_fall2022.csv" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://github.com/jnaiman/online_cv_public/blob/main/python_notebooks/test_generate_plots.ipynb" text="The Analysis" %}
</div>


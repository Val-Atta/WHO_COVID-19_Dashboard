# WHO_COVID-19_Dashboard
# Load required packages
library(tidyverse)
library(httr)
library(jsonlite)
library(ggplot2)
library(scales)

# Function to fetch data from WHO COVID-19 dashboard
fetch_who_data <- function() {
  url <- "https://covid19.who.int/region/afro/country"
  response <- httr::GET(url)
  content <- httr::content(response, "text", encoding = "UTF-8")
  data <- jsonlite::fromJSON(content)
  return(data)
}

# Fetch data
dashboard_data <- fetch_who_data()

# Extract required information
country_data <- dashboard_data$country

# Filter data for African countries
african_countries <- country_data[country_data$region == "AFRO", ]

# Plot confirmed cases by country
ggplot(african_countries, aes(x = name, y = total_cases)) +
  geom_bar(stat = "identity", fill = "#1f77b4") +
  labs(x = "Country", y = "Total Confirmed Cases",
       title = "COVID-19 Confirmed Cases in African Countries") +
  theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust = 1),
        plot.title = element_text(hjust = 0.5)) +
  scale_y_continuous(labels = comma)
===============================================================================
#CODE BRIEF DESC;
In this code, we start by loading the required packages, including tidyverse for data manipulation and visualization, httr for making HTTP requests, and jsonlite for working with JSON data.

Next, we define a function fetch_who_data() to fetch data from the WHO COVID-19 dashboard. This function sends an HTTP GET request to the dashboard URL and retrieves the JSON response. We then parse the JSON data using jsonlite::fromJSON().

After fetching the data, we extract the required information by filtering for the African countries. In this example, we assume the JSON structure of the WHO dashboard API remains the same as of my knowledge cutoff in September 2021. Please note that the actual structure may vary, so you might need to adapt the code accordingly if the API has changed.

Finally, we use ggplot2 to create a bar plot showing the total confirmed COVID-19 cases for each African country. The plot is customized with appropriate labels and titles, and the y-axis scale is formatted to use commas for better readability.

Please note that this code is based on assumptions about the structure of the WHO COVID-19 dashboard API, and it might need adjustments if the API has changed. Additionally, ensure that you have the necessary packages installed before running the code.

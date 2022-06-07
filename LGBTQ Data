---
title: "Tidy Tuesday - LGBTQ Data"
author: "Tim Mooney"
date: '2022-06-07'
output: html_document
---
```{r}
library(tidyverse)
library(showtext)
library(usefunc)
library(patchwork)
library(dplyr)
library(ggplot2)
library(janitor)
library(ggdark)
```
```{r}
# Load in the Data 
pride_data <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2022/2022-06-07/pride_aggregates.csv')
```

Wrangling:

```{r}
# Check variable names in the data
names(cleaned_data)

#Clean Variable names to snake_case
cleaned_data <- pride_data %>% 
  clean_names()

#Renaming variables for ease
cleaned_data <- rename(cleaned_data, states_contributed_to = number_of_states_where_contributions_made)
```
```{r}
# Select top 10 contibuters in terms of monetary value
biggest_contributors <- cleaned_data %>%
  dplyr::slice_head(n = 10)
  
```

Plotting:

```{r}
# Check the variable type
class(biggest_contributors$total_contributed)

# Simple Bar chart with specified colours
simple_bar <- ggplot(biggest_contributors, aes(x = company, y = total_contributed, fill = company)) +   
  geom_bar(stat = "identity") +
  scale_fill_manual(values = c("Toyota" = "red2",
                               "State Farm" = "orange",
                               "Jack Daniel's (Brown-Forman)" = "yellow",
                               "General Motors" = "green2",
                               "FedEx" = "navy",
                               "Enterprise" = "purple4",
                               "Comcast" = "white",
                               "Budweiser" = "plum1",
                               "AT&T" = "skyblue1",
                               "Amazon" = "sienna4")) +
  labs(title = "Companies Contributing To Anti-LGBTQ Political Campaigns", subtitle = "Each year, in June companies take part in the annual celebration of the LGBTQ community. However, data reports show that some of these companies are bigoted and simply just pose as LGBTQ allies,\nhere are just the top 10 in terms of monetary contributions toward Anti-LGBTQ political campaigns.", caption = "Author: @TimMooneyShare | Data provided by Data for progress & TidyTuesday", x = "Companies Contributing", y = "Total of Contributions Made") +
  scale_y_continuous("Total of Contributions Made", 
                       breaks = scales::breaks_extended(20),
                       labels = scales::label_dollar()) +
  dark_theme_light()

simple_bar

```

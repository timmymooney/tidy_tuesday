library(shiny)
library(ggplot2)
library(tidyr)
library(dplyr)

squirrel_data <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2023/2023-05-23/squirrel_data.csv') %>% 
  janitor::clean_names()

am_data <- squirrel_data %>% pivot_longer(cols = running:foraging, names_to = "activities") %>% 
  filter(shift == "AM") %>% 
  filter(value == TRUE) %>% 
  count(activities, sort = TRUE) %>% 
  mutate(activities = str_to_title(activities))

pm_data <- squirrel_data %>% pivot_longer(cols = running:foraging, names_to = "activities") %>% 
  filter(shift == "PM") %>% 
  filter(value == TRUE) %>% 
  count(activities, sort = TRUE) %>% 
  mutate(activities = str_to_title(activities))

ui <- fluidPage(
  titlePanel("Interchangeable Spidergraph Plot"),
  fluidRow(
    column(width = 5,
           sidebarPanel(
             selectInput(
               inputId = "plotType",
               label = "Select Plot",
               choices = c("Morning Data", "Afternoon Data"),
               selected = "Morning Data"
             )
           )
    ),
    column(width = 9,
           mainPanel(
             plotOutput("plot", height = "600px")  # Adjust the height as needed
           )
    )
  )
)

server <- function(input, output) {
  output$plot <- renderPlot({
    if (input$plotType == "Morning Data") {
      max_value <- 850
      ggplot(am_data, aes(x = activities, y = n)) +
        geom_polygon(aes(fill = n)) +
        geom_point(size = 4, color = "steelblue") +
        coord_polar(start = -pi/2) +
        labs(title = "Morning Squirrel Activities", x = "", y = "", color = "") +
        theme_minimal() +
        theme(legend.position = "none",
              title = element_text(size = 17),
              axis.text.x = element_text(size = 15)) +
        ylim(0, max_value)
    } else {
      max_value <- 850
      ggplot(pm_data, aes(x = activities, y = n)) +
        geom_polygon(aes(fill = n)) +
        geom_point(size = 4, color = "steelblue1") +
        coord_polar(start = -pi/2) +
        labs(title = "Afternoon Squirrel Activities", x = "", y = "", color = "") +
        theme_minimal() +
        theme(legend.position = "none",
              title = element_text(size = 17),
              axis.text.x = element_text(size = 15)) +
        ylim(0, max_value)
    }
  })
}

shinyApp(ui, server)

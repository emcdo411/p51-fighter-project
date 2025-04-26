# P-51 Mustang vs F-35A vs Su-57: Evolution of Fighter Aircraft

### A Shiny Application to Compare Three Iconic Fighter Jets

This Shiny app compares three fighter aircrafts across multiple performance metrics, including speed, range, service ceiling, thrust, and weight. The three jets compared are:
- **P-51 Mustang** (World War II legend)
- **F-35A Lightning II** (Modern multirole stealth fighter)
- **Su-57 Felon** (Russia’s fifth-generation fighter)

### Key Features:
- **Aircraft Summary**: Detailed specifications and history of each aircraft.
- **Interactive Aircraft Build Map**: Location markers for the manufacturers of each aircraft.
- **Radar Comparison**: An interactive radar chart to compare the performance metrics.
- **Speed and Range Comparison**: Bar charts comparing the max speed and range of the jets.

### Table of Contents:
- [Tech Stack](#tech-stack)
- [Installation Instructions](#installation-instructions)
- [Aircraft Data](#aircraft-data)
- [UI and Server Code](#ui-and-server-code)
- [Interactive Features](#interactive-features)
- [Acknowledgements](#acknowledgements)

---

## Tech Stack

![Tech Stack](https://img.shields.io/badge/R-%23E1A2A6?style=flat&logo=r&logoColor=white) ![Shiny](https://img.shields.io/badge/Shiny-%23F03D47?style=flat&logo=r&logoColor=white) ![Leaflet](https://img.shields.io/badge/Leaflet-%23007A7A?style=flat&logo=leaflet&logoColor=white) ![Plotly](https://img.shields.io/badge/Plotly-%23637D8C?style=flat&logo=plotly&logoColor=white)

This application was built using the following tools:
- **R** for the programming language
- **Shiny** for the interactive web app framework
- **Leaflet** for map visualization
- **ggplot2** for static plotting
- **Plotly** for interactive radar charts
- **dplyr** for data manipulation

---

## Installation Instructions

To run this project locally, follow these steps:

1. **Install R**: If you don't have R installed, you can download it from [here](https://cran.r-project.org/).
2. **Install RStudio**: Recommended for an integrated development environment (IDE) from [here](https://posit.co/download/rstudio-desktop/).
3. **Install the required R packages**:
    ```R
    install.packages(c("shiny", "leaflet", "ggplot2", "plotly", "dplyr"))
    ```
4. **Clone the repository**:
    ```bash
    git clone https://github.com/yourusername/fighter-aircraft-comparison.git
    ```
5. **Run the app**:
    - Open the project folder in RStudio.
    - Open the `app.R` file and click the "Run App" button in RStudio.

---

## Aircraft Data

The dataset includes performance specifications for three fighter jets:

- **P-51 Mustang**
- **F-35A Lightning II**
- **Su-57 Felon**

### Sample Data:
```R
plane_data <- data.frame(
  Plane = c("P-51 Mustang", "F-35A Lightning II", "Su-57 Felon"),
  Max_Speed = c(437, 1200, 1320), # mph
  Range = c(1650, 1380, 2200), # miles
  Service_Ceiling = c(41900, 50000, 66000), # feet
  Thrust = c(1490, 43000, 77000), # lbf
  Weight = c(12000, 29000, 39300), # lbs
  First_Flight = c(1940, 2006, 2010),
  Description = c(
    "The P-51 Mustang was a long-range, single-seat fighter and fighter-bomber used during World War II and the Korean War.",
    "The F-35A Lightning II is a modern multirole stealth fighter designed for ground attack and air superiority missions.",
    "The Su-57 Felon is Russia's fifth-generation stealth multirole fighter jet designed for air superiority and attack roles."
  )
)
```

---

## UI and Server Code

The app is built using **Shiny** for interactivity. The **UI** section organizes the features into tabs for easy navigation, and the **Server** section contains the logic for rendering the different components.

### UI:
```R
ui <- fluidPage(
  theme = bslib::bs_theme(version = 5, bootswatch = "darkly"),
  titlePanel("P-51 Mustang vs F-35A vs Su-57: Evolution of Fighter Aircraft"),
  tabsetPanel(
    tabPanel("Plane Summary", tableOutput("planeSummary")),
    tabPanel("Aircraft Build Map", leafletOutput("planeMap", height = 600)),
    tabPanel("Radar Comparison", plotlyOutput("radarPlot", height = 600)),
    tabPanel("Speed Comparison", plotOutput("speedPlot")),
    tabPanel("Range Comparison", plotOutput("rangePlot"))
  )
)
```

### Server:
```R
server <- function(input, output) {
  # Render the plane summary
  output$planeSummary <- renderTable({ plane_data %>% select(Plane, Description) })
  # Render the map
  output$planeMap <- renderLeaflet({
    leaflet(build_locations) %>%
      addProviderTiles("CartoDB.DarkMatter") %>%
      setView(lng = -40, lat = 40, zoom = 2) %>%
      addCircleMarkers(~Lon, ~Lat, label = ~Plane, popup = ~Info, radius = 8, color = "white", fillColor = "red")
  })
  # Render radar chart
  output$radarPlot <- renderPlotly({
    plot_ly()  # Radar plot code as shown above
  })
  # Render speed comparison chart
  output$speedPlot <- renderPlot({
    ggplot(plane_data, aes(x = Plane, y = Max_Speed, fill = Plane)) + geom_bar(stat = "identity")
  })
  # Render range comparison chart
  output$rangePlot <- renderPlot({
    ggplot(plane_data, aes(x = Plane, y = Range, fill = Plane)) + geom_bar(stat = "identity")
  })
}
```

---

## Interactive Features

- **Radar Comparison**: The radar chart is interactive, allowing users to explore how each plane compares on various performance metrics.
- **Aircraft Map**: The map shows the locations where each plane's manufacturer is based, with clickable markers for additional details.
- **Speed and Range Comparison**: Bar charts display side-by-side comparisons of the planes' maximum speed and range, respectively.

---

## Acknowledgements

- **Data**: The aircraft data is sourced from various public resources including aviation history archives.
- **Libraries**: This project uses several libraries from the R ecosystem: Shiny, ggplot2, Plotly, Leaflet, and dplyr.
- **Contributors**: Developed by [Your Name] for all aviation and military history enthusiasts.

---

### [Link to Project Repository](https://github.com/yourusername/fighter-aircraft-comparison)
```

This README layout will give your GitHub project a polished, professional look, and it’s designed to attract a wide audience, from tech enthusiasts to military history buffs. The tech stack is highlighted with colorful badges, and the sections are organized for easy navigation. Let me know if you need further tweaks!

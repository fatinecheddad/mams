
library(shiny)
library(htmltools)

# Exemples de données similaires à votre DataFrame

# Fonction pour générer un tableau HTML avec des styles personnalisés
generate_table_html <- function(data) {
  rows <- apply(data, 1, function(row) {
    alert_color <- if (row["Alert"] == "Red") {
      "background-color: red; color: white;"
    } else if (row["Alert"] == "Amber") {
      "background-color: orange; color: white;"
    } else if (row["Alert"] == "Green") {
      "background-color: green; color: white;"
    } else {
      ""
    }
    tags$tr(
      tags$td(row["Axes"]),
      tags$td(row["KRI"]),
      tags$td(row["Variable"]),
      tags$td(style = alert_color, row["Alert"])
    )
  })
  tags$table(
    class = "styled-table",
    tags$thead(
      tags$tr(
        tags$th("Axes"),
        tags$th("KRI"),
        tags$th("Variable"),
        tags$th("Alert")
      )
    ),
    tags$tbody(rows)
  )
}

# UI de l'application
ui <- fluidPage(
  tags$head(
    tags$style(HTML("
      .styled-table {
        border-collapse: collapse;
        margin: 25px 0;
        font-size: 0.9em;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        min-width: 400px;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
      }
      .styled-table thead tr {
        background-color: #009879;
        color: #ffffff;
        text-align: left;
      }
      .styled-table th, .styled-table td {
        padding: 12px 15px;
      }
      .styled-table tbody tr {
        border-bottom: 1px solid #dddddd;
      }
      .styled-table tbody tr:nth-of-type(even) {
        background-color: #f3f3f3;
      }
      .styled-table tbody tr:last-of-type {
        border-bottom: 2px solid #009879;
      }
    "))
  ),
  titlePanel("Tableau de Monitoring"),
  mainPanel(
    uiOutput("table")
  )
)

# Serveur de l'application
server <- function(input, output) {
  output$table <- renderUI({
    generate_table_html(data)
  })
}

# Lancement de l'application Shiny
shinyApp(ui = ui, server = server)

library(shiny)

# Define UI for application
ui <- fluidPage(
  
  # Application title
  titlePanel("Import Data"),
  
  # Description
  tags$hr(),
  tags$h4("Import Data Description"),
  tags$p("This section aims to import the summary table, then define the customer scope to access the explanation of the columns constituting the table and visualize some relevant statistics on the quality of the data."),
  tags$p("Press the Browse button to open the file explorer, then import the summary table."),
  
  # File input
  fluidRow(
    column(12, align = "center",
           box(
             title = "Upload File",
             status = "danger",
             fileInput("file", label = NULL),
             verbatimTextOutput("value")
           )
    )
  ),
  
  # Select client scope
  tags$hr(),
  fluidRow(
    column(12,
           selectInput("client_scope", "Sur quel périmètre client voulez-vous appliquer l'OGM:",
                       choices = c("Choix 1", "Choix 2", "Choix 3"))
    )
  ),
  
  # HTML file integration
  tags$hr(),
  fluidRow(
    column(12,
           HTML("<h4>Explications supplémentaires</h4>"),
           includeHTML("path/to/your/file.html")
    )
  ),
  
  # Plots
  tags$hr(),
  fluidRow(
    column(6,
           h1("Plot 1"),
           textOutput("plot1_text")
    ),
    column(6,
           h1("Plot 2"),
           textOutput("plot2_text")
    )
  ),
  fluidRow(
    column(6,
           h1("Plot 3"),
           textOutput("plot3_text")
    ),
    column(6,
           h1("Plot 4"),
           textOutput("plot4_text")
    )
  )
)

# Define server logic
server <- function(input, output) {
  
  # Function to render file input
  output$value <- renderPrint({
    # Print file input details
    input$file
  })
  
  # Render text for plot 1
  output$plot1_text <- renderText({
    "Texte temporaire pour le plot 1"
  })
  
  # Render text for plot 2
  output$plot2_text <- renderText({
    "Texte temporaire pour le plot 2"
  })
  
  # Render text for plot 3
  output$plot3_text <- renderText({
    "Texte temporaire pour le plot 3"
  })
  
  # Render text for plot 4
  output$plot4_text <- renderText({
    "Texte temporaire pour le plot 4"
  })
}

# Run the application
shinyApp(ui = ui, server = server)


 # Code Accompanying Master’s Thesis: *Sexist Rhetoric in the Spanish Congress: a Machine Learning-Based Approach*

> By Maria Carda 

![Static Badge](https://img.shields.io/badge/R_code-%23276DC3?logo=R&labelColor=white&logoColor=%23276DC3) ![Static Badge](https://img.shields.io/badge/HTML-grey?logo=htmx&logoColor=gray&labelColor=white) ![Static Badge](https://img.shields.io/badge/CSS-blue?logo=htmx&logoColor=gray&labelColor=white) ![Static Badge](https://img.shields.io/badge/tidyverse-R_package-%23276DC3?logo=Tidyverse&logoColor=black&labelColor=white&color=%23276DC3)

## At a glance

The objective of this project is to detect and analyze the presence of sexist discourse in Spanish parliamentary debates between 2019 and 2023, using a combination of automated data extraction, language processing, and machine learning models.

## Project Overview

The thesis project consists of the following components:

1.  <u>Data Harvesting Processing</u>: extraction of parliamentary intervention data from official Spanish Congress and government websites using web scraping techniques. This included gathering official transcripts from the XIV Legislature legislative sessions.
2.  <u>Data Processing & Interventions Extraction</u>: cleaning of raw text data (removal of HTML, normalization, etc.) and extraction of relevant variables such as speaker gender, political party, interventor name, full intervention text, session agenda, and date. 
3.  <u>Data Annotation</u>: usage of OpenAI's gpt-4o-mini model via API to annotate 30,924 interventions. For each, the model identified (1) whether sexist content was present, (2) the specific sexist fragment, and (3) the type of sexism according to the theoretical framework of the thesis.
4.  <u>Data Analysis</u>: descriptive analysis of sexist interventions, including frequency by party and gender, typology distributions, and temporal patterns. 
4.  <u>Machine learning models</u>: development and evaluation of models using NNET, Random Forest, XGBoost, LSTM, and Keras, which were assessed using standard performance metrics (accuracy, F1, AUC).

## Required packages

```{r}

# Web Scraping and API Interaction
library(RSelenium)     # Automated web browsing and dynamic scraping
library(rvest)         # HTML/XML scraping from static web pages
library(httr)          # HTTP methods for web communication
library(jsonlite)      # JSON parsing for API responses and data interchange

# Data Manipulation 
library(tidyverse)     # Collection of packages for data manipulation, cleaning, and transformation
library(tidyr)         # Data tidying 
library(forcats)       # Working with categorical variables 
library(purrr)         # Functional programming 
library(stringr)       # String manipulation 
library(stringi)       # Advanced string processing

# Visualization and Reporting
library(scales)        # Scale functions for ggplot2 
library(RColorBrewer)  # Color palettes for visualization
library(vip)           # Variable importance plots for ML models

# NLP (Natural Language Processing)
library(tidytext)      # Text mining using tidy data principles
library(stopwords)     # Multilingual stopword lists
library(udpipe)        # Tokenization, POS tagging, lemmatization
library(textrecipes)   # Text preprocessing steps for ML pipelines

# AI and Language Models
library(openai)        # Interface to OpenAI API for LLM tasks
library(reticulate)    # Integrating Python code and models

# Machine Learning Framework
library(caret)         # Unified interface for training and evaluating ML models
library(nnet)          # Feed-forward neural networks
library(randomForest)  # Ensemble learning using decision tree forests
library(xgboost)       # Gradient boosting algorithm for classification/regression
library(keras)         # Deep learning using TensorFlow backend
library(ranger)        # Fast implementation of Random Forests

# Model Evaluation and Metrics
library(pROC)          # ROC curves and AUC computation
library(yardstick)     # model performance metrics
library(lime)          # Local Interpretable Model-Agnostic Explanations

# Preprocessing
library(recipes)       # Data preprocessing pipelines for ML models
library(tidymodels)    # Unified modeling framework for machine learning
library(themis)        # Techniques for addressing class imbalance (SMOTE)
library(rsample)       # Resampling infrastructure (train/test splits, bootstraps)
library(ROSE)          # Synthetic data generation for imbalanced classification
```

## Installation and Setup

To successfully run the project, follow these steps:

1.  Install R: Install the programming language on your machine.

2.  Install "RSelenium": this package requires a web driver and browser automation setup. It is needed to install the following outside of R:

    -   [Java](https://www.java.com/es/download/manual.jsp): Ensure that Java is installed and properly configured.
    -   [Docker](https://www.docker.com/products/docker-desktop/): Install Docker from Docker's official website.
    -   [VNC Viewer](https://www.realvnc.com/es/connect/download/viewer/): Download and install VNC Viewer from RealVNC.

3.  Setup Rselenium: following the previous installation, it is required to open docker before running the code and log in with a user. Then, run the following commands in the R terminal:

    -   docker info
    -   docker run hello-world
    -   docker pull selenium/standalone-firefox-debug:latest
    -   docker run -d -p 4449:4444 -p 5901:5900 --platform linux/amd64 selenium/standalone-firefox-debug:latest

4.  Run the application: Once all dependencies are installed and configured, the project can be run by opening R and executing the main script.

5. Pyhton 3.10 installation: Install from the official [Python site](https://www.python.org/downloads/release/python-3100/)
and make sure to check “Add Python to PATH”.

To verify the installation, please execute the following in your terminal/bash: python3.10 --version

6. Creation of virtual environment: Once the program is install, it is required to set up a virtual environment to manage Python dependencies independently.

```{bash}
# Navigate to your project directory
cd /path/to/project

# Create a virtual environment using Python 3.10
python3.10 -m venv venv

# Activate the environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Upgrade pip
pip install --upgrade pip

# install packages
pip install tensorflow numpy h5py scipy

```

## Usage

Once the project is set up and running, users can utilize the various data processing and visualization features seamlessly. The project enables web scraping to collect book cover images and extract dominant colors, allowing for an in-depth analysis of color trends across different authors and genres. Users can explore the most frequently used colors for different authors, genres, and sources, comparing trends.

## Features

This project offers the following features:

1.  Data Collection (`scrap_books)`: Load book metadata, including title, author, and cover image.
2.  Color Extraction (`extract_colors)`: Identify dominant colors from book cover images.
3.  Clustering & Cleaning: Group similar colors and remove duplicates.
4.  Visualization: Generate plots and applications ([shiny](https://mariacarda.shinyapps.io/data_harvesting_books/)) showing color distribution by author, webpage and category.

## Note on data availability

Due to size and storage limitations, the text (*textos.csv*) and interventions (*completado.csv*) datasets included in this repository contain **only sample subsets** of the full data. **The complete databases are not publicly included here**.

If you require access to the full datasets for your research or project, please contact the project administrator at: 100419840@alumnos.uc3m.es

## Future Enhancements

Some future enhancements for the project include:

-   <u>Machine Learning improvement</u>: Leverage higher computational capacity to explore more complex models such as transformer-based architectures, and improve classification performance through advanced feature engineering and hyperparameter tuning.
-   <u>Expanded Data Sources</u>: Extend data collection to cover the entire democratic period in Spain (post-1978) to provide a longitudinal analysis.
-   <u>Advanced Visualizations</u>: Enhance data visualization with interactive dashboards to enable dynamic exploration of sexist discourse patterns and incorporating time-series and network visualizations for deeper insights.

## Conclusion

This project offers a meaningful exploration of sexism within parliamentary discourse, combining data scraping, natural language processing, and machine learning techniques. It serves as a foundation tool for further academic inquiry into the intersection of language, politics, and gender. Future enhancements like integration of more sophisticated models and real-time data monitoring have the potential to deepen the scope and impact of the research.

## Disclaimer

This project was developed exclusively for academic purposes as part of my final thesis for the Master in Computational Social Science at Carlos III University. The code and materials provided are intended for research and educational use only. **Commercial use is strictly prohibited**. For permissions or inquiries, please contact the project administrator.

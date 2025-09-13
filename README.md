Ethnic Diversity and Prosocial Behavior in Early Childhood
Project Summary
This project investigates the relationship between ethnic diversity in German kindergartens and the prosocial behavior of children. Using a field study, the research aims to understand how ethnic heterogeneity within a group of peers influences a child's willingness to engage in cooperative, helpful behavior, specifically measured by a giving game.

The study is based on a bachelor's thesis by Mohammed El-Zein and uses data collected from a sample of German kindergartens. The analysis employs fixed-effects models to account for unobserved differences between kindergartens and to isolate the effect of ethnic diversity on prosocial behavior. The findings contribute to the ongoing discussion about the social benefits and challenges of diverse early childhood environments.

Files
Ethnic Diversity and Prosocial Behavior in Early Childhood.pdf: This PDF contains the complete bachelor's thesis. It includes the introduction, literature review, theoretical framework, data and methodology, results, and conclusion of the study. This document provides the full academic context for the project.

Ethnic Diversity and Prosocial Behaviour El-Zein .R: This R script contains the code used to analyze the data and generate the results presented in the thesis. The script is structured into several sections for clarity and reproducibility:

1. Load Required Libraries: Installs and loads the necessary R packages (haven, dplyr, lfe, Matrix).

2. Load Data: Reads the raw data from a .dta file.

3. Clean and Prepare Data: Performs data cleaning, variable creation, and preparation for analysis.

4. Descriptive Statistics: Calculates and presents summary statistics of the key variables.

5. Main Regressions: Runs the primary fixed-effects regressions to estimate the effect of diversity on prosocial behavior.

6. Robustness Checks: Contains additional regressions to test the stability of the main findings using different model specifications.

7. Results and Outputs: Presents the regression summaries and prepares the output for the thesis document.

How to Use the R Script
To run the analysis, you will need to:

Ensure you have R installed on your system.

Open the .R file in an R environment (e.g., RStudio).

Install the required packages by running the first section of the script.

Update the setwd() path to the location of your data file.

Run the script line by line or in sections to replicate the analysis.

Important Note on Data

Due to confidentiality and data privacy reasons, the original dataset used in this analysis cannot be made public. This repository is intended solely to showcase the methodology and analysis performed in R, as described in the accompanying thesis.

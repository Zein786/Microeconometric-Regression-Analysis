microeconometric-regression-analysis

This repository contains the replication materials for the bachelor thesis “Ethnic Diversity and Prosocial Behavior in Early Childhood: Evidence from a Field Study in German Kindergartens” (University of Konstanz, 2025).
The project investigates whether the ethnic and migrant composition of German kindergartens is associated with greater prosocial behavior, measured through a coin allocation experiment among native German children. Using data from the KIDS’n’GROUPS field study, the analysis examines the relationship between heritage diversity (language-based) and visible diversity (skin/hair color) and children’s generosity, with fixed effects and multiple robustness checks.
Key Features
R Analysis Script (analysis.R)
Cleans and prepares raw data from the KIDS’n’GROUPS dataset.
Constructs measures of heritage diversity and visible diversity at the group level.
Runs descriptive statistics, correlation analysis, and fixed-effects regressions.
Performs robustness checks at both the group level and the kindergarten level.
What Makes This Code Extra Interesting
Multi-Level Design: Goes beyond individual-level regressions by incorporating peer-group (kigaid × id_group) diversity and testing at the kindergarten average level for robustness.
Dual Operationalization of Diversity: Distinguishes between heritage-based (linguistic/cultural) and visible (skin/hair) diversity, allowing for nuanced analysis of social mechanisms.
Fixed-Effects Strategy: Uses kindergarten fixed effects (felm) to control for unobserved institutional differences such as teaching style, local norms, or socio-economic context.
Behavioral Measure of Generosity: Prosocial behavior is measured via a coin allocation experiment, operationalized both continuously (coins given) and categorically (generosity dummies).
Robustness and Transparency: Includes multiple cross-checks (correlation matrices, aggregated regressions, fixed-effects models) to strengthen the credibility of results.

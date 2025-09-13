# ==============================================================================
# R Script for Bachelor Thesis: Ethnic Diversity and Prosocial Behavior
# Author: Mohammed El-Zein
# Description: Estimates effect of group-level diversity within kindergartens
#              on prosocial behavior using fixed effects and robustness checks.
# ==============================================================================

# ------------------------------------------------------------------------------
# 1. Load Required Libraries
# ------------------------------------------------------------------------------
if (!requireNamespace("haven", quietly = TRUE)) install.packages("haven")
if (!requireNamespace("dplyr", quietly = TRUE)) install.packages("dplyr")
if (!requireNamespace("lfe", quietly = TRUE)) install.packages("lfe")
if (!requireNamespace("Matrix", quietly = TRUE)) install.packages("Matrix")

library(haven)
library(dplyr)
library(lfe)

# ------------------------------------------------------------------------------
# 2. Load Data
# ------------------------------------------------------------------------------
setwd("~/Desktop/bachelorarbeit/data")
kids_data <- read_dta("Kidsngroups_Bachelorarbeit.dta")

# ------------------------------------------------------------------------------
# 3. Clean and Prepare Data
# ------------------------------------------------------------------------------
kids_data_clean <- kids_data %>%
  # Replace "." or " " in 'otherl' and 'motherl' with empty string ""
  mutate(
    otherl = ifelse(otherl %in% c(".", " "), "", otherl),
    motherl = ifelse(motherl %in% c(".", " "), "", motherl)
  ) %>%
  # Filter out rows where both motherl and otherl are empty after replacement
  filter(!(motherl == "" & otherl == "")) %>%
  mutate(
    # Calculate 'migrant' based on cleaned 'motherl' and 'otherl'
    migrant = ifelse((motherl != "Deutsch") | (otherl != ""), 1, 0),
    is_german = ifelse(migrant == 0, 1, 0),
    visibly_migrant = ifelse(c2_skinc >= 3 & c2_hairc >= 3, 1, 0)
  )

# ------------------------------------------------------------------------------
# 4. Calculate Diversity at the (kigaid, id_group) Level
# ------------------------------------------------------------------------------
group_diversity <- kids_data_clean %>%
  group_by(kigaid, id_group) %>%
  summarise(
    heritage_div_group = mean(migrant, na.rm = TRUE),
    visible_div_group = mean(visibly_migrant, na.rm = TRUE),
    .groups = "drop"
  )

# Merge back
kids_data_clean <- kids_data_clean %>%
  left_join(group_diversity, by = c("kigaid", "id_group"))

# ------------------------------------------------------------------------------
# 5. Prepare Regression Dataset
# ------------------------------------------------------------------------------
regression_data <- kids_data_clean %>%
  filter(is_german == 1) %>%
  mutate(
    coins_given = 4 - c2_dict,
    generosity_dummy1 = ifelse(coins_given > 2, 1, 0),
    generosity_dummy2 = ifelse(coins_given >= 1, 1, 0)
  )

# Dataset: Visibly Migrant Children
visibly_migrant_data <- kids_data_clean %>%
  filter(visibly_migrant == 1)

# Dataset: Heritage Migrant Children
heritage_migrant_data <- kids_data_clean %>%
  filter(migrant == 1)

# ------------------------------------------------------------------------------
# 6. Descriptive Stats
# ------------------------------------------------------------------------------
cat("\n--- Descriptive Statistics ---\n")
summary(regression_data %>%
          select(coins_given, generosity_dummy1, generosity_dummy2,
                 heritage_div_group, visible_div_group,
                 age))

# ------------------------------------------------------------------------------
# 7. Correlation Analysis
# ------------------------------------------------------------------------------
cat("\n--- Correlation Matrix ---\n")
cor_matrix <- regression_data %>%
  select(coins_given, generosity_dummy1, generosity_dummy2,
         heritage_div_group, visible_div_group, age) %>%
  cor(use = "complete.obs")
print(round(cor_matrix, 3))

# ------------------------------------------------------------------------------
# 8. Main Regressions (Group Diversity w/ Kindergarten Fixed Effects)
# ------------------------------------------------------------------------------
cat("\n--- Regressions: HERITAGE Diversity ---\n")
model1_cont <- felm(coins_given ~ heritage_div_group + age + c2_female + factor(c2_skinc) | kigaid | 0 | 0,
                    data = regression_data)
model1_d1 <- felm(generosity_dummy1 ~ heritage_div_group + age + c2_female + factor(c2_skinc) | kigaid | 0 | 0,
                  data = regression_data)
model1_d2 <- felm(generosity_dummy2 ~ heritage_div_group + age + c2_female + factor(c2_skinc) | kigaid | 0 | 0,
                  data = regression_data)

summary(model1_cont)
summary(model1_d1)
summary(model1_d2)

cat("\n--- Regressions: VISIBLE Diversity ---\n")
model2_cont <- felm(coins_given ~ visible_div_group + age + c2_female + factor(c2_skinc) | kigaid | 0 | 0,
                    data = regression_data)
model2_d1 <- felm(generosity_dummy1 ~ visible_div_group + age + c2_female + factor(c2_skinc) | kigaid | 0 | 0,
                  data = regression_data)
model2_d2 <- felm(generosity_dummy2 ~ visible_div_group + age + c2_female + factor(c2_skinc) | kigaid | 0 | 0,
                  data = regression_data)

summary(model2_cont)
summary(model2_d1)
summary(model2_d2)

# ------------------------------------------------------------------------------
# 9. Robustness Check: Kindergarten-Level Regressions (Average at kigaid level)
# ------------------------------------------------------------------------------
cat("\n--- ROBUSTNESS: Kindergarten-Level Regressions ---\n")
kiga_level_data <- regression_data %>%
  group_by(kigaid) %>%
  summarise(
    avg_coins = mean(coins_given, na.rm = TRUE),
    heritage_div_kiga = mean(heritage_div_group, na.rm = TRUE),
    visible_div_kiga = mean(visible_div_group, na.rm = TRUE),
    avg_age = mean(age, na.rm = TRUE),
    pct_female = mean(c2_female, na.rm = TRUE),
    .groups = "drop"
  )

kiga_model <- lm(avg_coins ~ heritage_div_kiga + visible_div_kiga + avg_age + pct_female,
                 data = kiga_level_data)
summary(kiga_model)

# ------------------------------------------------------------------------------
# 11. Done
# ------------------------------------------------------------------------------
cat("\n✅ Analysis complete with robustness checks and correlation analysis.\n")


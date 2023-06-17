# US-Bankruptcy-Data
#installing_R_packages
install.packages("tidyverse")
library("tidyverse")
install.packages("ggplot2")
library("ggplot2")
install.packages("dplyr")
library("dplyr")
install.packages("lubridate")
library("lubridate")
install.packages("hms")
library("hms")
library("data.table")
install.packages("readr")
library("readr")
install.packages("anytime")
library("anytime")
install.packages("parsedate")
library("parsedate")

#Renaming_the_data_frame
data <- read.csv("american_bankruptcy.csv")

#renaming_the_columns
data <- data %>%
  rename("Current assets" = X1,
         "Cost of goods sold" = X2,
         "Depreciation and amortization" = X3)

data <- data %>%
  rename("EBITDA" = X4,
         "Inventory" = X5,
         "Net Income" = X6)

data <- data %>%
  rename("Total Receivables" = X7,
         "Market Value" = X8,
         "Net Sales" = X9)

data <- data %>%
  rename("Total Assets" = X10,
         "Total Long-term Debt" = X11,
         "EBIT" = X12)

data <- data %>%
  rename("Gross Profit" = X13,
         "Total Current Liabilities" = X14,
         "Retained Earnings" = X15)

data <- data %>%
  rename("Total Revenue" = X16,
         "Total Liabilities" = X17,
         "Total Operating Expenses" = X18)

#making_sure_the_column_names_are_correct
column_names <- colnames(data)
print(column_names)

#Cleanning_the_data
#removing_the_dublicates
data <- distinct(data)

#removing_the_NA_values
data <- na.omit(data)

#calculating_profitability_ratios
#calculated_ROA_ratio
result <- sum(data$`Net Income` / data$`Total Assets`) 
print(result)

#calculating_liquidity_ratios
#current_ratio
result_1 <- sum(data$`Current assets` / data$ `Total Current Liabilities`) 
print(result_1)

#time_interest_ratio
result_2 <- sum(data$EBIT / data$`Total Operating Expenses`)
print(result_2)

#Exporting_the_data
write.csv(data, "fin_data.csv", row.names = FALSE)

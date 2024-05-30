# CBTC

DESCRIPTION:

Our project, "Unraveling Unemployment," takes a deep dive into unemployment data to uncover meaningful insights. We start by ensuring the data is clean and reliable through meticulous cleaning and preprocessing.

Using advanced analytical techniques and insightful visualizations, we explore unemployment trends over time and across regions. Our visualizations, including line plots, bar graphs, and heatmaps, provide clear insights into unemployment dynamics, making complex data easy to understand.

The value of our project lies in its ability to empower decision-makers with actionable insights. By understanding unemployment trends and regional disparities, stakeholders can make informed decisions about policy formulation, resource allocation, and economic development.

Key features of our project include rigorous data cleaning, advanced exploratory data analysis, compelling visualizations, and actionable insights. Through our efforts, we aim to provide stakeholders with the tools they need to navigate the complexities of the job market and drive positive change in their communities.
............................................................
QUESTIONS

Q1. What is the trend of the unemployment rate over time?
Answer: By analyzing the line plot , we can observe the fluctuation in the unemployment rate over different time periods. From the visualization, we can infer whether the unemployment rate has been increasing, decreasing, or remaining relatively stable over time.

Q2. What is the distribution of the unemployment rate across different regions?
Answer: The bar plot visualizes the average unemployment rate by region. By examining this plot, we can identify which regions have higher or lower unemployment rates on average compared to others.

Q3. Is there any relationship between the unemployment rate and the labor participation rate?
Answer: The scatter plot illustrates the relationship between the unemployment rate and the labor participation rate. By analyzing this plot, we can determine whether there is a correlation between these two variables. Additionally, the color mapping to regions helps in identifying any regional patterns in this relationship.

Q4. Are there any correlations among different numeric variables in the dataset?
Answer: The heatmap of the correlation matrix provides insights into the relationships between different numeric variables such as the unemployment rate, labor participation rate, etc. By examining the correlation coefficients, we can identify which variables are positively or negatively correlated with each other.

Q5. How does the unemployment rate vary across different regions?
Answer: The pair-plot visualizes multiple relationships within the dataset, including the unemployment rate across different regions. By examining the pair-plot, we can observe how the unemployment rate varies within each region and whether there are any notable patterns or outliers.
............................................................

Conclusion
The analysis of the unemployment data reveals fluctuating trends in the unemployment rate over time, indicating its dynamic nature. 
Regional disparities exist, with some regions exhibiting higher average unemployment rates.
 The scatter plot suggests a potential negative correlation between unemployment rate and labor participation.
 Additionally, the correlation matrix highlights relationships among variables. Overall, the analysis underscores the need for targeted interventions to address regional disparities and promote labor market participation for economic stability.

 .................................................................................
code

# Importing necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
# Load the data
unemployment_data = pd.read_excel("C:/Users/acs/OneDrive/Desktop/Unemployment project/unemployment_data.xlsx")
# Display the first few rows of the DataFrame
print(unemployment_data.head())
# Data Cleaning and Preprocessing
# Check for missing values
print(unemployment_data.isnull().sum())


# Handling missing values
# Drop rows with missing values
unemployment_data.dropna(inplace=True)

# Check if missing values are removed
print(unemployment_data.isnull().sum())

# Check data types
print(unemployment_data.dtypes)

# Convert Date column to datetime with dayfirst=True
unemployment_data['Date'] = pd.to_datetime(unemployment_data['Date'], dayfirst=True)

# EDA
# Summary statistics
print(unemployment_data.describe())

# Visualizations
# 1. Line plot of Unemployment Rate over time
plt.figure(figsize=(10, 6))
sns.lineplot(data=unemployment_data, x='Date', y='Estimated Unemployment Rate (%)', marker='o')
plt.title('Unemployment Rate over Time')
plt.xlabel('Date')
plt.ylabel('Unemployment Rate (%)')
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()

# 2. Histogram of Unemployment Rate
plt.figure(figsize=(8, 6))
sns.histplot(data=unemployment_data, x='Estimated Unemployment Rate (%)', bins=20, kde=True)
plt.title('Histogram of Unemployment Rate')
plt.xlabel('Unemployment Rate (%)')
plt.ylabel('Frequency')
plt.grid(True)
plt.tight_layout()
plt.show()

# 3. Bar plot of Average Unemployment Rate by Region
plt.figure(figsize=(10, 6))
sns.set_palette("pastel")  # Set color palette
average_unemployment_by_region = unemployment_data.groupby('Region')['Estimated Unemployment Rate (%)'].mean().sort_values()
average_unemployment_by_region.plot(kind='barh')
plt.title('Average Unemployment Rate by Region', fontsize=16, fontweight='bold', color='blue')  # Title styling
plt.xlabel('Average Unemployment Rate (%)', fontsize=14, fontweight='bold', color='green')  # X-axis label styling
plt.ylabel('Region', fontsize=14, fontweight='bold', color='green')  # Y-axis label styling
plt.xticks(fontsize=12, fontweight='bold', color='purple')  # X-axis ticks styling
plt.yticks(fontsize=12, fontweight='bold', color='purple')  # Y-axis ticks styling
plt.grid(axis='x', linestyle='--', alpha=0.5)  # Grid styling with reduced opacity
plt.tight_layout()  # Adjust layout to prevent overlap
plt.show()

# 4. Scatter plot of Unemployment Rate vs. Labour Participation Rate with color mapping to Region
plt.figure(figsize=(10, 10))
sns.scatterplot(data=unemployment_data, x='Estimated Labour Participation Rate (%)', y='Estimated Unemployment Rate (%)', hue='Region', palette='bright')
plt.title('Unemployment Rate vs. Labour Participation Rate', fontsize=16, fontweight='bold', color='blue')  # Title styling
plt.xlabel('Labour Participation Rate (%)', fontsize=14, fontweight='bold', color='green')  # X-axis label styling
plt.ylabel('Unemployment Rate (%)', fontsize=14, fontweight='bold', color='green')  # Y-axis label styling
plt.xticks(fontsize=12, fontweight='bold', color='purple')  # X-axis ticks styling
plt.yticks(fontsize=12, fontweight='bold', color='purple')  # Y-axis ticks styling
plt.grid(True, linestyle='--', alpha=0.5)  # Grid styling with reduced opacity
plt.legend(loc='upper right', fontsize=12)  # Add legend with fontsize
plt.tight_layout()  # Adjust layout to prevent overlap
plt.show()

# 5. Heatmap of Correlation Matrix
plt.figure(figsize=(8, 6))

# Select only numeric columns
numeric_columns = unemployment_data.select_dtypes(include=['float64', 'int64'])

# Calculate correlation matrix
corr = numeric_columns.corr()

# Plot heatmap
sns.heatmap(corr, annot=True, cmap='coolwarm', fmt=".2f", linewidths=0.5)
plt.title('Correlation Matrix', fontsize=16, fontweight='bold', color='blue')  # Title styling
plt.tight_layout()  # Adjust layout to prevent overlap
plt.show()

# 6. Pairplot to visualize relationships between multiple variables
sns.pairplot(unemployment_data, hue='Region', palette='bright')
plt.suptitle('Pairplot of Unemployment Data', fontsize=16, fontweight='bold', color='blue')  # Title styling
plt.tight_layout()  # Adjust layout to prevent overlap
plt.show()

...............................................................................................................

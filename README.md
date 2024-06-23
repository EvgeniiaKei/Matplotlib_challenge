# Matplotlib_challenge
Data Visualization

![Laboratory](https://github.com/EvgeniiaKei/Matplotlib_challenge/assets/166274251/dcd8d19c-47cd-43c3-991b-6be44b67c698)
# Background
You've just joined Pymaceuticals, Inc., a new pharmaceutical company that specialises in anti-cancer medications. Recently, it began screening for potential treatments for squamous cell carcinoma (SCC), a commonly occurring form of skin cancer.

As a senior data analyst at the company, you've been given access to the complete data from their most recent animal study. In this study, 249 mice who were identified with SCC tumours received treatment with a range of drug regimens. Over the course of 45 days, tumour development was observed and measured. The purpose of this study was to compare the performance of Pymaceuticals’ drug of interest, Capomulin, against the other treatment regimens.

The executive team has tasked you with generating all of the tables and figures needed for the technical report of the clinical study. They have also asked you for a top-level summary of the study results.

# Instructions
This assignment is broken down into the following tasks:

Prepare the data.
Generate summary statistics.
Create bar charts and pie charts.
Calculate quartiles, find outliers, and create a box plot.
Create a line plot and a scatter plot.
Calculate correlation and regression.
Submit your final analysis.
# Prepare the Data
1. Run the provided package dependency and data imports, and then merge the mouse_metadata and study_results DataFrames into a single DataFrame.
2. Display the number of unique mice IDs in the data, and then check for any mouse ID with duplicate time points. Display the data associated with that mouse ID, and then create a new DataFrame where this data is removed. Use this cleaned DataFrame for the remaining steps.
3. Display the updated number of unique mice IDs.
# Generate Summary Statistics
# Create Bar Charts and Pie Charts
1. Generate two bar charts.
2. Generate two pie charts.
# Calculate Quartiles, Find Outliers, and Create a Box Plot
1. Calculate the final tumour volume of each mouse across four of the most promising treatment regimens: Capomulin, Ramicane, Infubinol, and Ceftamin. Then, calculate the quartiles and IQR, and determine if there are any potential outliers across all four treatment regimens.
2. Using Matplotlib, generate a box plot that shows the distribution of the final tumour volume for all the mice in each treatment group. Highlight any potential outliers in the plot by changing their color and style.
# Create a Line Plot and a Scatter Plot
# Calculate Correlation and Regression

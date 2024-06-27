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
     # Calculate statistics use group by Drug Regimen	
       mean = clean_df['Tumor Volume (mm3)'].groupby(clean_df['Drug Regimen']).mean()
       median = clean_df['Tumor Volume (mm3)'].groupby(clean_df['Drug Regimen']).median()
       var = clean_df['Tumor Volume (mm3)'].groupby(clean_df['Drug Regimen']).var()
       std = clean_df['Tumor Volume (mm3)'].groupby(clean_df['Drug Regimen']).std()
       sem = clean_df['Tumor Volume (mm3)'].groupby(clean_df['Drug Regimen']).sem()

    # Assemble the resulting series into a single summary DataFrame.
       summary_stat = pd.DataFrame({"Mean Tumor Volume":mean, 
                                    "Median Tumor Volume":median, 
                                    "Tumor Volume Variance":var, 
                                    "Tumor Volume Std. Dev.":std, 
                                    "Tumor Volume Std. Err.":sem})
    # Display the Summary statistics table grouped by 'Drug Regimen' column
      summary_stat

    # A more advanced method to generate a summary statistics table of mean, median, variance, standard deviation,
    # and SEM of the tumor volume for each regimen (only one method is required in the solution)

    # Using the aggregation method, produce the same summary statistics in a single line
     agg_drug_reg_sum_df = clean_df.groupby(["Drug Regimen"])[["Tumor Volume (mm3)"]].agg(["mean","median","var","std","sem"])
     agg_drug_reg_sum_df

<img width="343" alt="image" src="https://github.com/EvgeniiaKei/Matplotlib_challenge/assets/166274251/04dfe7ad-289d-4628-9084-7cc29c716755">


# Create Bar Charts and Pie Charts
1. Generate two bar charts.

   <img width="391" alt="image" src="https://github.com/EvgeniiaKei/Matplotlib_challenge/assets/166274251/968fc9e2-6e15-4a76-a5b0-db885f20eeef">

2. Generate two pie charts.
   
   <img width="296" alt="image" src="https://github.com/EvgeniiaKei/Matplotlib_challenge/assets/166274251/05cf88bc-9f77-4dde-a40b-f7df307d075e">

# Calculate Quartiles, Find Outliers, and Create a Box Plot
1. Calculate the final tumour volume of each mouse across four of the most promising treatment regimens: Capomulin, Ramicane, Infubinol, and Ceftamin. Then, calculate the quartiles and IQR, and determine if there are any potential outliers across all four treatment regimens.
       # Create empty list to fill with tumor vol data (for plotting)
       tumor_volume_data = []

       # Calculate the IQR and quantitatively determine if there are any potential outliers. 
       # Locate the rows which contain mice on each drug and get the tumor volumes
       for drug in treatment_list:
             volume_df = greatest_tp_df.loc[greatest_tp_df["Drug Regimen"]==drug]["Tumor Volume (mm3)"]
             tumor_volume_data.append(volume_df)
    
       # Determine Quartiles, IQR, Lower Bound, Upper Bound    
         quartiles = volume_df.quantile([0.25,0.5,0.75])

        iqr = quartiles[0.75] - quartiles[0.25]

        lower_bound = quartiles[0.25] - (1.5*iqr)
        upper_bound = quartiles[0.75] + (1.5*iqr)

       # Determine outliers using upper and lower bounds
        outliers = volume_df.loc[(volume_df > upper_bound) | (volume_df < lower_bound)]
    
        print(f"{drug}'s potential outliers: {outliers}")


- Capomulin's potential outliers: Series([], Name: Tumor Volume (mm3), dtype: float64)
- Ramicane's potential outliers: Series([], Name: Tumor Volume (mm3), dtype: float64)
- Infubinol's potential outliers: 31    36.321346 Name: Tumor Volume (mm3), dtype: float64
- Ceftamin's potential outliers: Series([], Name: Tumor Volume (mm3), dtype: float64)
   
3. Using Matplotlib, generate a box plot that shows the distribution of the final tumour volume for all the mice in each treatment group. Highlight any potential outliers in the plot by changing their color and style.

        # Generate a box plot that shows the distrubution of the tumor volume for each treatment group.
           red_dot = dict(marker="o", markerfacecolor='red', markersize=12)
           fig1, ax1 = plt.subplots()
           ax1.boxplot(tumor_volume_data, flierprops=red_dot)
           ax1.set_title("The tumor volume for each treatment group")
           ax1.set_ylabel("Final Tumor Volume (mm3)")
           plt.show()

<img width="416" alt="2" src="https://github.com/EvgeniiaKei/Matplotlib_challenge/assets/166274251/03ca09be-8dc6-47dc-9dc1-27208fddbec3">


# Create a Line Plot and a Scatter Plot

    # Generate a line plot of tumor volume vs. time point for a single mouse treated with Capomulin
     capomulin_df = clean_df.loc[clean_df["Mouse ID"] == "l509",:]
     capomulin_df

    #get values ready for plotting
    time = capomulin_df["Timepoint"]
    vol = capomulin_df["Tumor Volume (mm3)"] 

     #graph build and display
     line, = plt.plot(time, vol, markersize=12)
     plt.xlabel("Timepoint")
     plt.ylabel("Tumor Volume (mm3)")
     plt.title("Capomulin treatmeant of mouse l509")
     plt.show()

<img width="435" alt="image" src="https://github.com/EvgeniiaKei/Matplotlib_challenge/assets/166274251/5c19b687-ee79-4808-ac7f-2cd0876261a1">
     

# Calculate Correlation and Regression

     # Calculate the correlation coefficient
     print(f"The correlation between mouse weight and average tumour volume is {round(st.pearsonr(weight, avg_tumor_vol)[0],2)}")

      # Use scipy stats to find values for linear regression
      reg_model = linregress(weight, avg_tumor_vol)
      (slope, intercept, rvalue, pvalue, stderr) = reg_model
      co_plot = weight * slope + intercept
      line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))

     # Plot main data
     plt.scatter(weight, avg_tumor_vol, marker="o")
     plt.plot(weight, co_plot, color="red")
     # Plot output and styling
     plt.xlabel("Weight (g)")
     plt.ylabel("Average Tumor Volume (mm3)")
     plt.title("Average Tumor vs Mouse Weight - Capomulin")
     plt.annotate(line_eq,(20,36), fontsize=18, color="red")
     plt.show()

<img width="426" alt="image" src="https://github.com/EvgeniiaKei/Matplotlib_challenge/assets/166274251/a501252e-f6fe-44ed-9c63-faf1018b2b4b">

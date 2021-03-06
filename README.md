# pymaceuticals_challenge

 I was able to complete this homework, but it was honestly pretty frustrating. The readme instructions and starter document were not at all clear, and there were a lot of places where I wasn't even sure exactly what you were asking for. When I went to my tutor, TAs, ask BCS, and the instructor for clarification, I got more uncertainty when they also didn't know, or gave me competing answers.

  - First, I imported dependancies and read in the data from both csvs.

  - I then merged the data on Mouse ID, creating the dataframe called merged_data and displayed a preview to show the columns I would be working with.



* Before beginning the analysis, check the data for any mouse ID with duplicate time points and remove any data associated with that mouse ID.

  - I first checked the number of mice by finding the len of unique Mouse IDs using .value_counts on merged_data.
  - I then identified mice with duplicate data by using .loc for Mouse ID on .duplicated, searching  Mouse ID and Timepoint in merged_data. 
  - This returned that the ID 'g989' contained duplicate data.
  - I printed out all data for the ID 'g989' to see for myself the duplication.
  - I created a new dataframe called cleaned_df without any data associated with the mouse 'g989' using .isin on merged_data. 
  - I checked to be sure the drop was complete by checking the number of mice again by finding the len of unique Mouse IDs using .unique on cleaned_df.



* Generate a summary statistics table consisting of the mean, median, variance, standard deviation, and SEM of the tumor volume for each drug regimen.

  - First I used .groupby for Drug Regimen on cleaned_df, storing it as drug_group.

  - Then I manually calculated the mean (with .mean), median (with .median), variance (with .var), standard deviation (with .std), and SEM (with .sem), storing each as its own variable.
  - I used those variables to create a new dataframe called tumor_summary.

  - I then used the .agg function to calculate the mean, median, variance, standard deviation, and sem again, storing the result in a variable called summary_table. 



* Generate a bar plot using both Pandas's `DataFrame.plot()` and Matplotlib's `pyplot` that shows  the number of total mice for each treatment regimen throughout the course of the study.

  - I used .value_counts on cleaned_df for Drug Regimen and stored the results as the variable drug_counts.
  - On the matplotlib chart I used .index.values on drug_counts for the y, and .values on drug_counts for the x.
  - For the pandas .plot I did not need to set the axis. 
  - I formatted both charts to look nice, be easily understood, and match.



* Generate a pie plot using both Pandas's `DataFrame.plot()` and Matplotlib's `pyplot` that shows the distribution of female or male mice in the study.

  - I used .value_counts on cleaned_df for Sex and stored the results as the variable sex_counts.
  - On the matplotlib chart I used stored the counts for Male and Female as separate variables called males and females, and used them to create the list sex_nums, which I then put in the pie chart using plt.pie.
  - For the pandas .plot I did not need any additional initialization. 
  - I formatted both charts to look nice, be easily understood, and match.



* Calculate the final tumor volume of each mouse across four of the most promising treatment regimens: Capomulin, Ramicane, Infubinol, and Ceftamin. Calculate the quartiles and IQR and quantitatively determine if there are any potential outliers across all four treatment regimens.

  - I used .groupby on cleaned_df for Drug Regimen and Mouse ID, and used .max on the Timepoint column of the resulting groups to find the final tumor volume for each mouse, storing the result as max_tumor.
  - I used .drop on max_tumor to drop the drug treatments we did not want to look at, leaving only Capomulin, Ramicane, Infubinol, and Ceftamin.
  - I used .reset_index on max_tumor to turn it into a mergeable object.
  - I merged max_tumor with cleaned_df on Mouse ID and Timepoint, storing the result as latest_data.

  - I used .unique on Drug Regimen in latest_data, storing the result as treatments (a list of the four drugs).
  - I initialized an empty list called tumor_volume_list for plotting later.

  - I used a for loop for the following:
      - I read through latest_data using .loc for Drug Regimen, storing the Tumor Volume (mm3) invalues as tumor_vol.
      - I added each tumor_vol value to tumor_volume_list.
      - I calculated the quartiles and iqr for each drug using tumor_vol and .quantile, setting the quartiles, and manually calculating iqr.
      - I printed the results for each drug treatment.
      - I set that if a given volume was greater than the upper bound of less than the lower bound it should be added to an empty list I called outliers. 
      - I printed those calculations. 

  - Outside of the for loop I calculated the qurtiles, upper/lower bounds, and iqr for the total off all drug treatments the same way as I had for them individually. 
  - I printed those calculations.

  
* Using Matplotlib, generate a box and whisker plot of the final tumor volume for all four treatment regimens and highlight any potential outliers in the plot by changing their color and style.
  - I created a box and whisker plot using tumor_volume_list for the content and treatments for the labels.


* Select a mouse that was treated with Capomulin and generate a line plot of tumor volume vs. time point for that mouse.
  - I created a new dataframe called id_index from the dataframe merged_data, and set the index to Mouse ID so I could easily find data for my chosen mouse.
  - I chose a mouse (shown is 'u364', but I tried with several to be sure it was working properly), and set its ID equal to the variable mouse_id.
  - I found my mouse's timepoints using .loc on id_index, and stored them as the variable individual_time.
  - I found my mouse's tumor volumes using .loc on id_index, and stored them as the variable individual_volume.
  - I plotted individual_time as my x axis and individual_volume as my y axis.
  - I formatted the chart to look nice and be easily understood.

* Generate a scatter plot of mouse weight versus average tumor volume for the Capomulin treatment regimen.
  - I used .set_index on cleaned_df to set the index to Drug Regimen, and stored it as drug_index.
  - I used .loc for Capomulin on drug_index to pull out just the Capomulin data, storing it as just_capomulin.
  - I used .groupby Mouse ID on just_capomulin to get data for each mouse isolated.
  - I used .mean on the Tumor Volume (mm3) column of the grouped data, storing the result as avg_tumor_vol.
  - I used .mean on the Weight (g) column of the grouped data, storing the result as mouse_weight.
  - I created a scatter plot using avg_tumor_volume as the y axis and mosue_weight as the x axis.
  - I formatted the chart to look nice and be easily understood.

* Calculate the correlation coefficient and linear regression model between mouse weight and average tumor volume for the Capomulin treatment. Plot the linear regression model on top of the previous scatter plot.
  - I used linregress on mouse_weight and avg_tumor_vol to find the slope, intercept, rvalue, pvalue, and stderr.
  - I multiplied mouse_weight by slope plus intercept and stored it as regress_values.
  - I used the same scatter plot as before to show the relationship between mouse_weight and avg_tumor_vol.
  - I calculated the correlation coefficient and stored it as cc.
  - I calculated the r-squared valued and stored it as rsquared.
  - I formatted the chart to look nice and be easily understood.


* Look across all previously generated figures and tables and write at least three observations or inferences that can be made from the data. Include these observations at the top of notebook.

Here are some final considerations:

* You must use proper labeling of your plots, to include properties such as: plot titles, axis labels, legend labels, _x_-axis and _y_-axis limits, etc.

* See the [starter workbook](Pymaceuticals/pymaceuticals_starter.ipynb) for help on what modules to import and expected format of the notebook.

## Hints and Considerations
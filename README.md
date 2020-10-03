# pymaceuticals_challenge

I have never had a very strong background in math, so I was a little worried about this homework going in. I was able to complete it, but I feel like for the later sections (correlation, linear regression, box and whisker plots), being able to complete and show the calculations did not necessarily mean I understand the how or why. 

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
  - I formatted both charts to look nice and match.



* Generate a pie plot using both Pandas's `DataFrame.plot()` and Matplotlib's `pyplot` that shows the distribution of female or male mice in the study.

  - I used .value_counts on cleaned_df for Sex and stored the results as the variable sex_counts.
  - On the matplotlib chart I used stored the counts for Male and Female as separate variables called males and females, and used them to create the list sex_nums, which I then put in the pie chart using plt.pie.
  - For the pandas .plot I did not need any additional initialization. 
  - I formatted both charts to look nice and match.



* Calculate the final tumor volume of each mouse across four of the most promising treatment regimens: Capomulin, Ramicane, Infubinol, and Ceftamin. Calculate the quartiles and IQR and quantitatively determine if there are any potential outliers across all four treatment regimens.

  - I used .loc on the Drug Regimen column in merged_data to isolate the mice treated with each of the four drug types, and stored the result as big_four.
  - I used .groupby on cleaned_df for Mouse ID, and used .max on the  Timepoint column of the resulting groups to find the final tumor volume for each mouse, storing the result as max_tumor.
  - I used .reset_index on max_tumor to turn it into a mergeable object.
  - I merged max_tumor with cleaned_df on Mouse ID and Timepoint, storing the result as latest_data

  

* Using Matplotlib, generate a box and whisker plot of the final tumor volume for all four treatment regimens and highlight any potential outliers in the plot by changing their color and style.

  **Hint**: All four box plots should be within the same figure. Use this [Matplotlib documentation page](https://matplotlib.org/gallery/pyplots/boxplot_demo_pyplot.html#sphx-glr-gallery-pyplots-boxplot-demo-pyplot-py) for help with changing the style of the outliers.

* Select a mouse that was treated with Capomulin and generate a line plot of tumor volume vs. time point for that mouse.

* Generate a scatter plot of mouse weight versus average tumor volume for the Capomulin treatment regimen.

* Calculate the correlation coefficient and linear regression model between mouse weight and average tumor volume for the Capomulin treatment. Plot the linear regression model on top of the previous scatter plot.

* Look across all previously generated figures and tables and write at least three observations or inferences that can be made from the data. Include these observations at the top of notebook.

Here are some final considerations:

* You must use proper labeling of your plots, to include properties such as: plot titles, axis labels, legend labels, _x_-axis and _y_-axis limits, etc.

* See the [starter workbook](Pymaceuticals/pymaceuticals_starter.ipynb) for help on what modules to import and expected format of the notebook.

## Hints and Considerations
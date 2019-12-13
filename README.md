 # MachineLearning-and-Statistics-Project

#Overview...


# Project Sections

## 1. Introduction
In this section I give a brief introduction to the dataset and the paper it was sourced from: *"Hedonic housing prices and the demand for clean air. Journal of Environmental Economics and Management"*. 
I give an overview of the variables in the dataset and describe what each of them are and their assumed relationship / effect (positive or negative) on the housing prices.
Finally, I renamed the variables to give them names that are more easily understandable for the rest of the project.

## 2. Descriptive Analysis
In this section I calculated various statistics for the dataset and engaged in some initial data exploration. The main elements in this section are:

### 2.1 Basic Information
Here I checked the variables data types and whether there are any null values in the dataset that I would have had to deal with. 

### 2.2 Measures of Central Tendency and Measures of Spread / Dispersion
Here I:
* Calculated the measures of central tendency for the variables in the dataset e.g. mean, mode, median
* Calculated the measures of spread / dispersion for the variables e.g. range, standard deviation 

This revealed a cohort of 16 records where the Median House price was at the max value of 50,000. It also, showed that there was evidence of some of the variables data being highly unevenly distributed.

### 2.3 Distribution of Variables
 This section contains plots of the distributions of the variables. First I looked at the distribution of the Median House Prices using a KDE and Boxplot. This again highlighted a large number of outlier values in the upper range.
 I then looked at the distribution of all the variables and plotted them side by side. This showed that only the number of Rooms, % of Lower Status People and Median Value had a roughly normal distribution, but did not highlight any annomalies in the data that I felt required further investigation.
 
 ## 2.4 Relationships between the Variables
 In this section I created a correlation table of all the variables. This showed that a number of variables were strongly positively or negatively correlated. Looking at the correlation with the Median House Prices in particular I found that the average number of Rooms, and % of Lower Status people were most strongly correlated with it.  
I then created scatter plots showing each variable plotted against the Median Value. This gave further evidence of "Rooms" and "% Lower Status" variables having the strongest relationship with the Median Value.


## 3. Inferential Statistics
In the section of the project I performed a t-test to determine if there was significant difference between Median House Prices in areas that are by the Charles River in Boston vs areas that are not by the river.

### 3.1 Looking more closely at the "By River" variable
Before jumping into performing a t-test I first took a closer look at the "By_River" variable to get the counts of the number of observations in each group ("Next to" and "Away from" the river. 
I also compared the distribution of the two groups and looked at their descriptive statistics. I noted the large difference in the size of both groups and that both had a large cohort of datapoints at the near the max of both ranges.

### 3.2 T-test
In the T-Test section itself I:
* First described what a T-Test is and why it was an appropriate  test.
* Stated the Null and Alternative Hypothesis for the test.
* Checked to see if the dataset met the requirement for a T-Test and noted that it that outliers, the distribution of each group, and homogeneity of variances needed to investigated further. 
* Removed outliers from the dataset - using the definition of 1.5 times the Interquartile range above or below the 1st and 3rd quartiles. 
* Confirmed that both group were roughly normally distributed using the stats.normaltest() function.
* Confirmed there was homogeneity of variances using stats.Levene(). 

### 3.3 T-Test Results
Once I had confirmed all requirements for a T-Test had been met I went ahead with the test and confirmed there was a significant difference between the two groups. 


## 4 Predicting House Prices Using a Neural Network

## 5. References 
This section contains the references used in the project. All references are noted in line using a "[1]" in next to the relevant text. 
Code that has been adapted from other sources is referenced with the link to the source in a comment at the top of the code
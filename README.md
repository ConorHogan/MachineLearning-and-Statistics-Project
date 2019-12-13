 # MachineLearning-and-Statistics-Project

# Overview
This README file gives an overview of the sections contained in the "Machine-Learning-and-Statistics-Project-Notebook" Jupyter Notebook contained in this repository. 
The notebook contains more detailed commentary on each of the areas listed below along with accompanying tables and charts and the code used to generate them. 
Also contained in this repository are:

1. A PDF copy of the academic paper that the dataset was originally sourced from.
2. A "requirements.txt" listing the packages (with version numbers) that need to be installed on your computer in order to run the code in the Jupyter Notebook. 


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
I then looked at the distribution of all the variables and plotted them side by side. This showed that only the number of Rooms, % of Lower Status People and Median Value had a roughly normal distribution, but did not highlight any anomalies in the data that I felt required further investigation.
 
## 2.4 Relationships between the Variables
In this section I created a correlation table of all the variables. This showed that a number of variables were strongly positively or negatively correlated. Looking at the correlation with the Median House Prices in particular I found that the average number of Rooms, and % of Lower Status people were most strongly correlated with it.  
I then created scatter plots showing each variable plotted against the Median Value. This gave further evidence of "Rooms" and "% Lower Status" variables having the strongest relationship with the Median Value.


## 3. Inferential Statistics
In the section of the project I performed a t-test to determine if there was significant difference between Median House Prices in areas that are by the Charles River in Boston vs areas that are not by the river.

### 3.1 Looking more closely at the "By River" variable
Before jumping into performing a t-test I first took a closer look at the "By_River" variable to get the counts of the number of observations in each group ("Next to" and "Away from" the river). 
I also compared the distribution of the two groups and looked at their descriptive statistics. I noted the large difference in the size of both groups and that both had a large cohort of datapoints at the near the max of both ranges.

### 3.2 T-test Set-up
In the this section I:
* First described what a T-Test is and why it was an appropriate  test.
* Stated the Null and Alternative Hypothesis for the test.
* Checked to see if the dataset met the requirement for a T-Test and noted that it that outliers, the distribution of each group, and homogeneity of variances needed to be investigated further. 
* Removed outliers from the dataset - using the definition of 1.5 times the Interquartile range above or below the 1st and 3rd quartiles. 
* Confirmed that both groups were roughly normally distributed using the stats.normaltest() function.
* Confirmed there was homogeneity of variances using stats.Levene(). 

### 3.3 T-Test Results
Once I had confirmed all requirements for a T-Test had been met I went ahead with the test and confirmed there was a significant difference between the two groups. 

## 4 Predicting House Prices Using a Neural Network
This section contains a finalised model for a neural network to predict the Median House Price based on the other variables in the dataset. 
It also contains the research that went into the creation of the model and the several testing configurations and models that I went through before arriving at the final model.

**NOTE** 
There a several test models in this section that can take quite a long time to run. This is because I tested most of the models by running them 5 times and getting the average of the 5 results.
In order to prevent a person from running "All Cells" in the accompanying Jupyter Notebook and having to wait a long period of time to get to the final model I have "commented out" some of the code to used to test the models. However, I have manually recorded the results achieved in the cell following the code.   

### 4.1 Preprocessing
Here I prepared the data to be fed into the model by going through a preprocessing checklist of:
1. Checking for null values - there were none. 
2. Checking for categorical variables - there was only one; "By_River", but this had already been converted into a boolean value. 
3. Standardizing the data.

Before standardizing I also shuffled the data and split it into training and tests sets. 

### 4.2 Baseline Prediction Test
Once the data has been preprocessed, I created a model with a basic configuration to act as a baseline for further iterations to be measured against. Ironically and a little frustratingly this baseline model produced some of the best predictions when compared to the subsequent "improved" models. 

### 4.3 Factors to Consider When Creating Further Models
Before continuing to create updated models I researched what the different elements of a model do. The elements I looked at included:
1. Model Selection
2. Density 
3. Number of Layers
4. Number of Units (Neurons) per layer
5. Activation Functions 
6. Optimizers 
7. Epochs
8. Batch Sizes

### 4.4 Model Tuning 
Now that I had a better idea of what each of the elements of a model did, I attempted to test changes to these elements in turn in order to see what effect they would have on the performance of the model.
The test I performed included:
1. Various Batch Sizes (32, 16, 4, 2) - I found that smaller batch sizes tended to perform better
2. Increasing the number of epochs - After testing 500 epoch I found that the model prediction stopped improving at around the 250 epoch mark so I set the standard number of epochs at 300 and introduced early stopping. 
3. Number of Units per Layer - There was no conclusive result showing that increasing the size of the hidden layer beyond the size of the inputs led to better predictions.
4. Number of Units per Layer - Here I added second and third layers of various sizes. Having just 1 additional hidden layer seemed to perform better than three. 

### 4.5 Further Tuning 
Next I attempted to improve the results of the model further by Whitening the data, and then engaging in Feature Selection. 

#### 4.5.1 Whitening / Dimensionality Reduction 
Using Principle Component Analysis I aimed to reduce the number of features by 2 and then tested the whitened dataset using various model configurations to test performance.
However, it seemed to consistently make the results worse. 

#### 4.5.2 Feature Selection
I then discarded the whitened dataset and tried to see if removing the features / variables that had a less obvious relationship to the Median Value of House Prices would improve performance. 
Using Correlation and F_Regression I identified the average number of Rooms in an area, and the % of Lower Status People in an area to have the strongest relationship with the Median Value.
I then tested this dataset in various model configuration with reduced numbers of units in each layer to take account of the reduced number of input, but the testing using just these two features produced consistently worse results.

### 4.6 Final Model
Finally, I performed some follow-up testing of a selection of the best performing models from the previous sections, before choosing a final model with the following configuration:

|Model Element|Configuration|
|:------------------------|:---------|
|Number of Hidden Layers|2|
|Number of Units per Layer |13, 13|
|Hidden Layer Activation Functions|ReLU|
|Optimizer|Adam|
|Epochs|300 with early stopping after 20 with no improvement|
|Batch Size|4|

This model achieved a MSE score of 7.22. 

To finish a created a table of "Predicted" and "Real" values along with percentage difference between the two value and then plotted the Predicted and Real values side by side. 

## 5. References 
This section contains the references used in the project. All references are noted in line using a "[1]" in next to the relevant text. 
Code that has been adapted from other sources is referenced with the link to the source in a comment at the top of the code.
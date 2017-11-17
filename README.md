# Business-Analytics

### Intro
>“We’re onboarding a new client next month as part of a very large deal. It’s critical that we support them with our excellent service levels. I need to know how many tickets per week on average we can expect from this client so we can ensure we have enough help desk resources in place.”

>**What decisions need to be made?**
The decision the sales manager needs to make is, “Do we have enough capacity on the support team to handle the support tickets from the new customer?” and “If not, how many people do we need to add to the support team to reach the desired capacity?”

>**What information do we need to inform this decision?**
We need to calculate the average number of tickets per customer per week. We can then aggregate the average number of tickets for each customer to get a total average number of support tickets that we predict will be submitted per week. Once we have this information, we need to compare the predicted average number of tickets with the current capacity of the support staff, specifically, the average number of tickets each team member can handle. **What type of analysis is needed to get the information needed to make that decision?**

**2 key analytical concepts** to understand business situation and analyze data.
  - A. Problem Solving Framework: CRISP-DM(Cross Industry Standard Process for Data Mining) 
  - B. Methodology Map

**[A. CRISP-DM]** was originally developed by data miners in order to generalize the common approaches to defining and analyzing a problem. CRISP-DM is the "Problem Solving Framework". Let's have a mental model! The framework is made up of 6 steps:
  - 1)Business Issue Understanding
  - 2)Data Understanding
  - 3)Data Preparation
  - 4)Performing Analysis + Modeling
  - 5)Validation
  - 6)Presentation + Visualization
  
>ex> How much electricity capacity does the company need to supply for any given hour tomorrow in a utility company? 
  
**1) Business Issue Understanding** 
  - What decisions needs to be made?
  - What information is needed to inform those decisions?
  - What type of analysis can provide the information needed to inform those decisions?
    - >Research: How do we supply the power we need? 
    - >Prediction: How much electricity will be demanded in each hour of the day tomorrow?   

**2) Data Understanding** 
  - What data is needed and available?
  - What are the important characteristics of the data?
    - >Data Collecting: What factors drives electricity demand tomorrow? 

**3) Data Preparation**
  - Gathering - Cleansing - Formatting - Blending - Sampling
   
*Formatting* refers to format the data by changing the way a date field appears, renaming a field, or even rotating the data, similar to using a pivot table. *Blending* refers to combine the data with other datasets to enrich it with additional variables, similar to using the vlookup function in Excel. *Sampling* refers to sample the dataset and work with a more manageable number of records.

**4) Performing Analysis + Modeling**
  - Various modeling techniques are selected and applied, and their parameters are calibrated to optimal values. Typically, there are several techniques for the same data mining problem type. Some techniques have specific requirements on the form of data. Therefore, stepping back to the data preparation phase is often needed.
    - >After creating a model, we repeat the process to predict electricity usage for a given hour on the next day. This includes the number of electricity plants we need for any given temperature, as well as the thresholds when we need to activate additional plants or purchase it on the market. 
    
**5) Validation**
  - Before proceeding to final deployment of the model, it is important to more thoroughly evaluate the model, and review the steps executed to construct the model, to be certain it properly achieves the business objectives. 

**6) Presentation + Visualization**
  - Determine the best method of presenting insights based on the audience
  - Make sure the amount of information shared is not overwhelming
  - Use the results to tell a story to the audience
-----------------------------------------------------------------------------------------------
## Ok, which methodology will we use? 

**[B. Methodology Map]** is a guide to determine the appropriate analytical technique(s) to solve a particular business question or problem. The map outlines two main scenarios for a business problem:

  - **Non Predictive Analysis**
refers to the more standard approaches of blending together data and reporting on trends and statistics and helps answer business questions that involve understanding more about the dataset such as "On average, how many people order coffee and a donut per transaction in my store in any given week?"

  - **Predictive Analysis**
help businesses predict future behavior based on existing data such as "Given the average coffee order, how much coffee can I expect to sell next week if I were to add a new brand of coffee?"

<img src="https://user-images.githubusercontent.com/31917400/32698915-d8ea47ea-c7a4-11e7-9059-b190b5216afd.jpg" width="600" height="300" />

1)*Non Predictive Analysis
  - Geospatial (using location based data to drive conclusion - by Geographic dimension: zip-code,country,etc)
  - Segmentation (grouping data together) 
  - Aggregation (calculating a value across a group or dimension)
  - Descriptive (providing simple summaries of a data sample - Mean, Median, Mode, SD, and Interquartile range)

2)*Predictive Analysis
  - Step1. Investigate the data (Rich/Poor)...if "data poor" ? 
    - => Setting up an experiment called "A/B testing" 
  - Step2. Expecting outcomes if it is Numeric/Non-Numeric (categorical)
    - Numeric Types: 1)continuous(taking all values in a range), 2)Time-Based, 3)discrete(count)
    - Non-Numeric Types: 1)binary, 2)Non-binary
  - Step3. Model Selection 
--------------------------------------------------------------------------------------------------------------------------------------  

### 1) For Numeric & continuous outcome, [Linear Regression]
>Imagine we have the data displayed in the scatter plot. It appears that we have a linear relationship between the number of employees and the number of tickets. The relationship appears to be linear since it seems like we can draw a straight line through the data. If we know the **equation** of the line, we can predict values for tickets given a certain number of employees. 

__A. Linear Regression Validation:__ 

#correlation coefficient: cov(x,y)/sqrt(var(x)*var(y)) shows how much x and y are correlated. This value is often referred to as r. The range of r is from -1 to +1  (Explained variation / Total variation)

#cov(x,y): E[(x-E[x])(y-E[y])] or E[xy]-E[x]E[y] is a measure of the joint variability - how x and y move together with the point [mean(x), mean(y)] as a center  (moving similarly(+), being independent(0), moving differently(-)...but the value is meaningless..)  

#Calculating R-squared: While a strong correlation is good, we need to know how well the data fits our line. R-squared is a coefficient between 0 and 1. R-squared is interpreted as the percent of variance in observations that is explained by the model, or the explanatory power of the model. In general, the higher the R-squared, the better the model fits your data. However, there are important conditions we need to concern about. Of course, 

> significance of predictor by P-value..we want high

> explaining variablilty by R-squared-value..we want high

But first, R-squared cannot determine whether the coefficient estimates and predictions are biased, which is why we must assess the residual plots. Second, the low P value with high R-squared combination also indicates that changes in the predictors are related to changes in the response variable and that our model explains a lot of the response variability, but what if we have significant predictors but a low R-squared value(R-squared represents the scatter around the regression line)???? This is because of a prediction interval. A prediction interval is a range that is likely to contain the response value of a single new observation given specified settings of the predictors in our model. Narrower intervals indicate more precise predictions. When the data points are spread out further, the predictions must reflect that added uncertainty. In this case, then we need to add more variables to the model. 

<img src="https://user-images.githubusercontent.com/31917400/32923154-e19c1f8a-cb2d-11e7-9737-255e74e372c5.jpg" width="600" height="150" />

#
























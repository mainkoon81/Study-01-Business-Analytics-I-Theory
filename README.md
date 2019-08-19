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
# Predictive Analysis

## 1) [Linear Regression]
>Imagine we have the data displayed in the scatter plot. It appears that we have a linear relationship between the number of employees and the number of tickets. The relationship appears to be linear since it seems like we can draw a straight line through the data. If we know the **equation** of the line, we can predict values for tickets given a certain number of employees. 

```
Linear Regression is a statistical method used to predict numeric outcomes by analyzing the outcome’s relationship with one or more predictor variables.
```

__Issue A. Validation:__ a good fit of our data? 

#correlation coefficient: cov(x,y)/sqrt(var(x)*var(y)) shows how much x and y are correlated. This value is often referred to as r. The range of r is from -1 to +1  (Explained variation / Total variation)

#cov(x,y): E[(x-E[x])(y-E[y])] or E[xy]-E[x]E[y] is a measure of the joint variability - how x and y move together with the point [mean(x), mean(y)] as a center  (moving similarly(+), being independent(0), moving differently(-)...but the value is meaningless..)  

#Calculating R-squared: While a strong correlation is good, we need to know how well the data fits our line. R-squared is a coefficient between 0 and 1. R-squared is interpreted as the percent of variance in observations that is explained by the model, or the explanatory power of the model. In general, the higher the R-squared, the better the model fits your data. However, there are important conditions we need to concern about. Of course, 

> significance of predictor by P-value..we want low 

> degree of explained variablilty by R-squared-value..we want high

But first, R-squared cannot determine whether the coefficient estimates and predictions are biased, which is why we must assess the residual plots. Second, the low P value with high R-squared combination indicates that changes in the predictors are related to changes in the response variable and that our model explains a lot of the response variability, but what if we have significant predictors but a low R-squared value(R-squared represents the scatter around the regression line)???? This is because of a prediction interval. A prediction interval is a range that is likely to contain the response value of a single new observation given specified settings of the predictors in our model. Narrower intervals indicate more precise predictions. When the data points are spread out further, the predictions must reflect that added uncertainty. In this case, then we need to add more variables to the model. 

The p-value is the probability that the coefficient is zero. The lower the p-value the higher the probability that a relationship exists between the predictor and target variable. If the p-value is high, we should not rely on the coefficient estimate. When a predictor variable has a p-value below 0.05, the relationship between it and the target variable is considered to be statistically significant.

<img src="https://user-images.githubusercontent.com/31917400/32923154-e19c1f8a-cb2d-11e7-9737-255e74e372c5.jpg" width="600" height="150" />

__Issue B. Multiple Predictors:__ Using more data to strengthen the Correlation Coefficient

Y=β0+β(X) is to become Y=β0+β1(x1)+β2(x2)+β3(x3)+β4(x4)....

#Step.1 Cleaning up the data so that the dataset does not have any bias to any of our variables. 

#Step.2 Graphing a scatter-plot between each predictor variable and the response variable than select good predictors.
  - Our numerical values of predictors are normally distributed?
  - Our numerical predictors have a linear relationship with the response variable ? (high P-value?) (E[RES]=0) (E[Y-βX]=0)
  - Our numerical predictors share the same variance? (homoscedasticity) (var[RES]=σ^2)
  - RES are uncorrelated with our model? 

As for categorical variables, we cannot use a scatterplot to see whether a linear relationship exists. The best way to check for this is to see if the coefficients turn out to be significant with a high multiple-R-squared. If there is a linear relationship, then the coefficients should be significant and the multiple-R-squared should be relatively high. 

#Step.3 Checking Adjusted R-squared.
  - In a nutshell, the more variables that are included, the higher the r-squared value will be - even if there is no relationship between the additional variables and the response variable.  

__Issue C. Categorical Predictors:__ what will happen in linear regression when we add a categorical variable to the mix of predictor variables? Simply assign a integer to each category and plug it into the model?  If we transform a category into a numeric variable, we are assuming a linear relationship exists between the response variable and the category number. Since the category number is generally assigned arbitrarily, this doesn't make sense. Instead we use "dummy" variable. 

A dummy variable can only take on two values 0/1. We would add dummy variables for one less than the number of unique values in the categorical variable. So if there are four categories, you'd add three dummy variables. For example, in Y=β0+β1(x1)+β2(x2), we add categorical variable 'C' that consists of 4 categories (c1,c2,c3,c4)-(0/1,0/1,0/1,0/1), then Y=β0+β1(x1)+β2(x2)+β3(c1)+β4(c3)+β5(c4). We don't create a variable for 'c2' because the equation needs a 'baseline value' that is not coded into a dummy variable. If a variable is in 'c2', then the value for all three of the dummy variables would be zero. The interpretation of the coefficient of 'c3', the dummy variable above, is that it represents the **"average difference"** between the response value in c3, compared to in c2. 

__Issue D. Variable transformation:__ People often transform in hopes of achieving normality prior to using some form of the general linear model (e.g., t-test, ANOVA, regression, etc). But I fear that in many cases, people make two mistakes when doing so:
 - 1. They look at normality of the outcome variable rather than normality of the errors. For OLS models, it is the errors that are assumed to be independently and identically distributed as normal with mean = 0. (Some people also assume that explanatory variables in regression models must be normally distributed. But that is clearly incorrect. For example, an OLS linear regression model with one dichotomous explanatory variable is equivalent to an unpaired t-test, which is a perfectly good model.)
 
 - 2. They overestimate the importance of the normality assumption. Or putting it another way, they underestimate the robustness of OLS models to non-normality of the errors. (And in reality, they are never truly normal anyway. As George Box noted, normal distributions and straight lines don't exist in nature; but they are still useful approximations to the statistician.)
In the context of OLS models, transformations are more often about stabilizing the variance, it seems to me--e.g., the log transform when the SD is proportional to the mean. But in some contexts, one may transform to obtain a test statistic that has an approximately normal sampling distribution--e.g., the sampling distribution of the odds ratio (OR) is not normal, but the sampling distribution of ln(OR) is asymptotically normal with SE = SQRT(1/a + 1/b + 1/c +1/d) where a-d are the 4 cell counts in the 2x2 table.

http://fmwww.bc.edu/repec/bocode/t/transint.html






## 2) [Classification Model]
 - >Logistic Regression (Binary-classification)
 - >Decision Trees (Binary-classification) 
 - >Random Forests (Multi-classification)
 - >Boosted Models (Multi-classification)

So which model the data fit the best? 

### Binary-Classification (Binary Response variable)
__1. Logistic Regression:__ Logistic Regression is a statistical method used to predict binary outcomes by analyzing the outcome’s relationship with one or more predictor variables. It’s part of a family of "GLM" for short. The formula is very similar to that of a linear regression; however, since the target variable is binary, instead of a continuous numeric variable, the target variable has to be modified to fit this GLM formula. 

<img src="https://user-images.githubusercontent.com/31917400/34130015-3f9f4d40-e43e-11e7-9ea7-adabfa544d58.jpg" width="400" height="125" />

 - Issue A. **Selecting Variables for the `Stepwise tool`:** 
   - The `Stepwise tool` takes one input from the **model object**, and the other input from our **original training set.**
   - The `Stepwise tool` needs to figure out all of the possible variables it can calculate first and it takes this list of possible variables from the Logistic Regression Tool output. 
   - A choice of two different adjusted fit measures are provided to the user:
     - the Akaike information criterion (or **AIC**)
     - the Bayesian information criterion (or **BIC**)
     - These two measures are similar to one another, but the BIC places a larger penalty on the number of variables included in the model, typically resulting in a final model with fewer variables than is the case when the AIC is used.
   - Steps to Build the Model in Alteryx
     - Use a `Select tool` to set the each variable to the correct data type.
     - Use the `Create Samples tool` to create samples of dataset and set 70% for the estimation sample and 30% for the validation sample.
     - Use the `Logistic Regression tool` and set the target variable as Redeemer
     - Select all variables besides Customer Key, First Name, Last Name, and Redeemer as predictor variables.
     - Add a `Stepwise tool`
   - The `Stepwise tool` helps us reduce and figure out which predictor variables have a good chance of being in the model, but it is not a tool that can automatically find all of the appropriate predictor variables in one run.
   - so we need `Model comparison tool` 

__2. Decision Tree:__ It analyzes the data as if it was a series of decisions. It does this by splitting the data and creating the largest difference at the percent b/w the target group. This results in a comparison b/w each of the different possible outcomes. For example, let's see if we can predict whether specific M&M will get eaten. 
 - Split (one predictor) - 'color': this split is choosen because it produces the `*largest difference*` in percent eatean b/w two groups. 
 - Split (add the second predictors) - 'flavour': Only possible split is 'W_Peanuts' vs 'W/O_Peanuts'. 
 - so which split would happen first? Since 'flavor' has a larger gap, it would cause the first split.
 - Once the first split has happened, **each split is treated separately**. 
 - Considering only the 'W_Peanuts' group for the second split and the 'W/O_Peanuts' group separately, how would the tree predict the actual result? What is the chance the 'blue M&M' is eaten? If we trace along the path for the 'blue', we can see that at the terminal node, there is 90% chance of being eaten. 
<img src="https://user-images.githubusercontent.com/31917400/34521746-4fcf16fa-f087-11e7-89af-179764cffa14.jpg" /> 
<img src="https://user-images.githubusercontent.com/31917400/34543709-41b59c58-f0da-11e7-893e-b97d3dd2146b.jpg" /> 

 - Issue A. `DecisionTree tool` requires parameter-setting and model-customization.
   - reading the output report: 
     - **Root Node Error:** A percentage of how many of the data points went to the incorrect terminal node (predicted incorrectly) when all of the data points are validated against themselves within the entire training set (the Estimation dataset). When we cross-validate out data against our model, How many errors occur? Within that estimation sample (model) and within that validation sample, how many are correctly predicted or how many are errored out? 
     - **Pruning table:**  Lists out the levels in the decision tree with their related error terms with cross-validation samples. It shows how many levels there are to the decision tree and some error charms with cross-validation sample. 
   - reading the output Interactive:
     - we can see how the model is created and where it decides to split and how many records fall within each 'Yes/No' at each split.  
     - **confusion matrix:** A matrix (or table) that lists out all of the possible prediction results when we validate our model against our validation set. This confusion matrix is one of the best methods to review the accuracy and precision of your model as well as to understand any model bias in classifying your data points. It shows how many of the data point fall within the correct terminal node. Here 97% of the nodes are classified correctly while 68% of the Yes's are correct, and ... so When classifying all Yes's against the Cross Validation sample, it tells the overall accuracy-68%. This matrix helps determine whether there might be biases within our data or if it's too skewed to one side or the other. 
<img src="https://user-images.githubusercontent.com/31917400/34523838-039c5f2c-f091-11e7-9ac3-cd88ea977acd.jpg" width="700" height="400" />    
 
 - Issue B. `Model Comparison tool` compares models against each other: 
   - Apply the model to the validation sample and observe how accurately the model predicts the outcomes. This step helps avoid overfitting and helps you understand how accurate your predictions will be on new data.
   - Lift is a measure of the performance of a predictive model calculated as the ratio b/w the results obtained with and w/o the predictive model. The lift chart is based on aggregating data into several groups. These groups are ordered based on the predicted probability of a favorable response for each model. For example, the lift chart shows how much more likely we are to receive respondents than if we contact a random sample of customers - by contacting only 10% of customers based on the model we will reach 3 times as many respondents as if we use no model. The greater the area between the lift curve and the baseline, the better the model. 
   - In the gain chart, y-axis shows the percentage of positive responses.
   - The Precision vs Recall chart is 
   - The ROC curve is (http://www.dataschool.io/roc-curves-and-auc-explained/) 
<img src="https://user-images.githubusercontent.com/31917400/34531390-01e32102-f0aa-11e7-81b5-5525deb26c60.jpg" /> 

 - Issue C. `Score tool` 
   - Apply the model to a new dataset to make predictions. This dataset should have all the predictor variable values, which are passed through the model to predict the unknown target variable value. The prediction will be a number between 0 and 1, representing the likelihood of positive outcome.
   - We have our model chosen so the only thing we have to do is to predict who is going redeem a future marketing campaign. When we put a model into production it is referred to as scoring the model. Which simply means taking each individual record and applying the model to them which gives their probability to redeem the offer.
   - Now we can answer to:
     - Create a dataset that contains only the individuals who have a greater than 50% probability of redeeming an offer.
     - Only include the Customer Key, First and Last Names, and the likelihood they will redeem an offer.
     - Sort the data with the highest likelihood individuals are at the top.
 
 
 
 
 
 
 
### Non-Binary-Classification (Non-Binary Response variable)
>For example, in our company, the insurance policy has a reward based benefit offer. This benefit varies depending on what mode of transportation an employee takes to work. Our company ran a survey to understand the mode of transportation of our employees and only 60% responded. What our management would like to do is **predict the mode of transportation of the other 40% of employees.** This would help us better estimate what benefits we can offer.

__1. RandomForest Model:__ Of course we can use 'DecisionTree' for Non-binary classification as well, 'DecisionTree' is prone to an error called over-fitting, where the model fits the sample data too well, and as a result, does not predict future results as well as it should. A technique that helps to eliminate this issues is the RandomForest Model.
 - A Forest Model creates hundreds of trees, called an ensemble of decision trees.
 - The first tree will be created with a random subset of the original data. We will also use the different combination of predictors to assist the splits. Its splits are choosen at places to produce the largest differences in percent of the mode of transportation.
 - The second tree will then do the same thing with different random subset of data and with different predictors. This will continue to occur until the number of trees specified has been created(default = 500).  
 - Each tree is created by different randomly generated chunks of the original data.
 - It looks at the results as a whole to make a prediction.
 - Each individual tree created still has overfitting issues, but when you look at the results as a whole, the overfitting gets averaged out by all of the other trees.
<img src="https://user-images.githubusercontent.com/31917400/34543354-4efece18-f0d8-11e7-9168-29710e567562.jpg" /> 

 - For example, if applying to this model to a particular employee who is 1.5 miles away from work (one of the predictors). This is how we average it out ! 
<img src="https://user-images.githubusercontent.com/31917400/34544108-3fa2d3de-f0dc-11e7-9ba3-bddf146c6056.jpg" /> 

 - Issue A. `Forest Model tool` 
<img src="https://user-images.githubusercontent.com/31917400/34544525-ac949d72-f0de-11e7-95d5-11cad480983c.jpg" width="240" height="150" /> 

 - reading the output report: 
   - **Out of the Bag Error Rate:** Explains how well the model performed with the cross-validation set in the estimation data. This gives a good understanding of how solid the model performs with just the estimation data. You can think of it in the same terms as an R-squared.
   - **Confusion Matrix:** Shows again how well the model performed on the original, estimation data. Compared to the "Out Of The Bag Error Rate", the confusion matrix does a better job at representing where errors occurred in classifying the data. This confusion matrix is one of the best methods to review the accuracy and precision of your model as well as to understand any model bias in classifying your data points.
   - **The Percentage Error for Different Number of Trees graph:** Helps us see what the correct number of trees is to use, so we can avoid over computing. What we are looking for is the number of trees it takes to minimize the error of each of the items, so basically, where does it flatline? After we determine the ideal number of trees, we can change subsequent Forest Models and run our data with the smaller number of Decision Trees.
   - **Predictor Variables importance:** Which predictor variables matter the most in relation to this model? This is very helpful in determining which variables are most associated with our data on and we can focus on for future analysis.
<img src="https://user-images.githubusercontent.com/31917400/34545792-21bfe4fa-f0e7-11e7-9a5a-7563e550916c.jpg" width="600" height="450" /> 

__2. Gradient-tree boosted Model:__ Forest Models might give us a better estimate than decision trees, but they're computationally intensive. What we need is a model that can be both accurate AND fast. What we'll use to achieve this balance is known as the Boosted Model. How it works? 
 - Instead of creating a bunch of random trees, the boosted model makes one tree.
 - Algorithm performs an analysis on the errors of the tree to identify the biggest source of error.
 - Changes the tree to reduce that error.
 - Does the analysis again to find the next biggest error.
 - Makes a change to reduce it.
 - Does this over and over until it can’t make the tree any better and we have our finished Boosted Model.
 - Issue A. `Boosted Model tool`
   - reading the output report:
     - **Predictor Variables importance:** Which predictor variables matter the most in relation to this model? This is very helpful in determining which variables are most associated with our data on and we can focus on for future analysis.
     - **No.of Iteration assessment:** shows the amount of variance-'Deviance'(distance between two probabilistic models) that is captured with more iterations. It shows how the deviance (loss) changes with the number of trees included in the model. The more trees added, the smarter the prediction became. The vertical blue dashed line indicates where the minimum deviance occurs using the specfied assessment criteria (cross validation, the use of a test sample, or out-of-bag prediction).This helps answer 'How many trees are needed to creat the optimal result?' The Estimation sample and In-Model sample estimate that are built into this model are very close, meaning this model performs well on an independent sample.
<img src="https://user-images.githubusercontent.com/31917400/34563118-2cfca602-f149-11e7-8136-4e5083de0473.jpg" width="600" height="350" /> 

 - 'validation step' required: `Model Comparison tool`
   - applying the modelsss to the validation set and observing the accuracy
   - Overall Accuracy of the Model, Overall Accuracy of different categories, Confusion Matrix
     - If we look at the model accuracy we see that the Forest Model performed best, followed up by a very close second with the Decision Tree model. And coming in 3rd was the Boosted model. The Forest Model provides the highest accuracy, and there are now 2 reasons to pick the Forest Model:
       - It has the highest overall accuracy
       - The averaged results from the forest model helps deal with the decision tree model's bias to overfit the data

------------------------------------------------------------------------------------------------------------
## Segmentation & Clustering
> Let's say a retail business has thousands stores. We want to create models to determine what is the best product mix (heater ? or AC ?) in each of these? It would be great if we could email individually to each of our customers that is customized considering each customer's needs or interests. How to do this? Dividing the entities into smaller set of objects called 'segments'. 
 - want to deal with the group as a whole? Use 'Standardization' (simplifying logistics)
 - want to deal with each entity individually, differently? Use 'Localization' with their own product mix that works for the specific stores(custumizable based on specifics)
<img src="https://user-images.githubusercontent.com/31917400/34650107-22dd6c58-f3b3-11e7-8cce-1705e0a20378.jpg" />    
 - How to balance b/w Standardization / Localization? Clustering is a statistical methodology that groups similar objects into clusters(segments) in a multi-dimension, Using 'Distance'- measuring similarity.
 - This unsupervised algorithm creates segments and make their objects in each segment as similar as possible, but make each segment as far away from each other as possible. 
<img src="https://user-images.githubusercontent.com/31917400/34650267-efeb943e-f3b5-11e7-9a48-af9d06e8fb63.jpg" width="400" height="200" /> 
<img src="https://user-images.githubusercontent.com/31917400/34650461-a3dcf642-f3b9-11e7-9851-3504820ac403.jpg" />    

### Data Preparation for clustering
 - Objectives behind creating segments determine the data or variables to use for our model. 
<img src="https://user-images.githubusercontent.com/31917400/34651586-041e8a92-f3ca-11e7-9d6b-3e8ac5a333ad.jpg" />    

 - Predetermined bias: Consider how the business was run over the time our data was collected. Sth abnormal happened? 
 - Datatype: 
 - Data Quality: outliers, missing, How far out the outliers are? can have an hugh impact on the clustering processs.
 - Scaling(standardizing): A 'z-score' (aka, a standard score) indicates how many standard deviations an element is from the mean. 

### Variable Reduction
 - PCA analyses all of the variance within all of the variables selected. It focuses on accounting for the total variation. It tries to answer how it can summarise the variables. 
 - FA analyses variance that are shared or common within the variables. It focuses on accounting for just the correlations b/w variables. It tries to answer what fundamentally might be causing the responses.  
<img src="https://user-images.githubusercontent.com/31917400/34652092-8d0d02f0-f3d1-11e7-9aff-df0fd1c95799.jpg" width="400" height="100" /> 










-------------------------------------------------------------------------------------------
# Extra Tip_1: Statistical-knowledge

1> **Measures of Spread** are used to provide us an idea of how spread out our data are from one another.
 - Range
 - Interquartile Range (IQR)
 - Standard Deviation
 - Variance
When we have data that follows a normal distribution, we can completely understand our dataset using the 'mean' and 'SD'. However, if our dataset is skewed or when we have outliers, the 5 number summary (min,IQR,max) might be better to summarize our dataset.

2> Simpson's Paradox
 - the way we choose to look at our data can lead to the different result.
<img src="https://user-images.githubusercontent.com/31917400/34156013-515bc6ec-e4b3-11e7-82ba-38e1f7a49784.jpg" width="400" height="125" /> 
<img src="https://user-images.githubusercontent.com/31917400/34170221-f0ad18a8-e4e1-11e7-9517-056f9c4b5bbf.jpg" width="500" height="180" /> 

3> Discrete Random Variable "P(X=x)=f(x): y-value"
 - x: outcome (whether **Numeric** or Non-numeric) just like "bins"
 - P(X=x): probability of x: freq/total_freq...it's a ratio.
 - f(x): probability function, thus... sum(f(x)) = 1
 - E[x] = sum(x*f(x))
 - var(x) = E[x^2]-E[x]^2
 - E[xy] = sum(xy*f(x,y)) = sum(x*f(x))*sum(y*f(y))
 - cov(x,y) = E[xy]-E[x]E[y]
 - Popular Discrete Distribution
   - **Bernoulli: B(p)**
     - x: freq or NO.of success or NO.of failure, thus x=1 or 0
     - N = 1 :coin-size
     - P(X=1)=f(x) = **p**, P(X=0)=f(x) = **1-p** = q
     - E[x] = p
     - var(x) = pq
   - **Binomial: B(n,p)**
     - x: freq or NO.of success or NO.of failure, thus x=0,1,2,3,4.....
     - N = n (independent) :coin-size
     - P(X=x*success)=f(x) = nCx * p^x * q^(n-x)
     - E[x] = n*p
     - var(x) = n*pq
   - Poisson
   - Geometric
   - Generalized Geometric(Negative Binomial)
   - Hyper Geometric
   - **Uniform: U(n)**
     - x: freq or No.of any outcome of the "dice"
     - N = n (independent)
     - P(X=x)=f(x) = 1/n
     - E[x] = (n+1)/2

4> Continuous Randome Variable "P(X<=x)=F(x): area"
.....




# Study-01-Business-Analytics-II
Cloud Computing

-----------------------------------------------------------------------------------
> What is the Operating System? 
 - For big device: Windows, Linux, Unix, MacOS-X... 
 - For small device: Android(google), iOS(apple)...

OS offers a **user_interface** to multiple hardwares(devices). It runs a special piece of codes called a **device driver** so that OS can manage these different resources(so that we don't need to care how each divices interact with each other). Aside form this, it schedules tasks, allocates storage, and shows a default interface to human users when no application is running. 

> What is the Distributed System?
 - A collection of multiple machine that appears as a single machine? It is in contrast to a network where the user is ware that machine's location, storage replication, load balancing, unknown functionality? It has 3 characteristics: 
   - 1)multiple machine 
   - 2)interconnections
   - 3)shared state? 
 - In a more technical term, it is a collection of entities, each of these entities being autonomous, programmable, **asynchronous** and failure-prone, and these entities communicate through an unreliable communication medium. 
   - Each entity is essentially a process running on a single device: stand-alone **autonomus** 
   - Each has written code running underneath inside the process: **programmable** (you cannot program humanbeings to interact)
   - *Each process runs according to its own clock that are not always synchronized with each other: **asynchronous**
     - which distinguishes this from parallel systems such as supercomputer with huge number of processors sharing the same motherboard. 
   - Each may crash arbitrarily at any point in time: **failure-prone**
   - When communicating each other, the data might be able to be dropped or delayed: **unreliable communication**
<img src="https://user-images.githubusercontent.com/31917400/44532050-1f26e180-a6ea-11e8-89e0-dd3234952dfd.jpg" />

> So...What do we need to know? 
 - P2P system: BitTorrent, Kazza
 - Infrastructure: AWS, AZURE, GoogleCloud
 - Storage: NoSQL, Cassandra
 - Programming: MapReduce, Storm
 - Coordination: Paxos, Snapshots
 - Management: Concurrency(accessing the same data), Replication Control

> 5 Essential Characteristics in Cloud
 - 1.On Demand Self-Service: Provision them by ourselves
<img src="https://user-images.githubusercontent.com/31917400/44717773-e2763400-aab5-11e8-9686-ed67b5ccb476.jpg" />

 - 2.Broad Network Access: Access them using the network
<img src="https://user-images.githubusercontent.com/31917400/44718426-f02cb900-aab7-11e8-8670-e414d06a3f9b.jpg" />
 
 - 3.Resource Pooling: Allocate specific resources from a pool
<img src="https://user-images.githubusercontent.com/31917400/44720973-5ddce300-aac0-11e8-99b7-56fd3c6d7f1e.jpg" />

 - 4.Rapid Elasticity:
<img src="https://user-images.githubusercontent.com/31917400/44722628-887d6a80-aac5-11e8-8216-7486c6c16394.jpg" />

ex) All over the night until around 08:00 morning time the load on the server is quite low, then people are coming to the office, connecting to their email accounts, so the load will keep increasing as more people are using the system up to some pick workload. Around 4:00 PM people are starting to leave the office and the load is going down again.
 
 - 5.Measured Service:
<img src="https://user-images.githubusercontent.com/31917400/44723064-df377400-aac6-11e8-8ba4-2af779fcfb5d.jpg" />
 
> 3 Service Model
 - 1.IaaS
 - 2.PaaS
 - 3.SaaS
 
> 4 Deployment Model
 - 1.Public Cloud
 - 2.Private Cloud
 - 3.Hybrid Cloud
 - 4.Community Cloud

-----------------------------------------------------------------------------------
## Overview
__Q0. What is a server?:__
 - A server is a **computer program** or a **device** that provides functionality for other programs or devices, called "clients" (client-server model). Because of this, a single overall computation can be distributed across multiple processes or devices. 
 - Servers can provide various functionalities, often called "services", such as sharing data or resources among multiple clients, or performing computation for a client.
 - A single server can serve multiple clients, and a single client can use multiple servers. A client process may run on the same device or may connect over a network to a server on a different device.
 - Client–server systems are today most frequently implemented by (and often identified with) the **request–response model**: a client sends a request to the server, which performs some action and sends a response back to the client, typically with a result or acknowledgement. Designating a computer as "server-class hardware" implies that it is specialized for running servers on it. Servers are often referred to as **dedicated** because they carry out hardly any other tasks apart from their server tasks. Server computers often have special operating systems not usually found on personal computers.
## what;s the difference b/w host and server? 

__Q1. Define Cloud Computing:__
 - `Cloud` means a **network** delivering **requested virtual resources** as a SERVICE. 
 - Cloud_Computing is a model for enabling **on-demand** network access to a `shared pool of configurable computing resources`(:Network, Server, Storage, Application, etc) that can be rapidly provisioned and released with minimal management effort(service provider interaction).    
 
__Q2. Describe the key characteristics of CC:__   
 - Using the cloud, we can rent the hardware, software w/o purchasing outright. It offers a consistent deployment configuration(prebuilt-solution stack). 
 - It enables `Self-Service`, `Sourcing options`(so many services..development environment? platform? IaaS, PaaS, SaaS), `Economies of scale`(as ur business grows,..?)
 
 - 1.**On-demand Self-Service**:
   - delivering IT services driven by user requests w/o human interaction
 - 2.**Ubiquitous network access**:
   - delivering IT services anytime, anywhere via user-choosen devices
   - Just like electricity from a wall outlet
 - 3.**Pool of virtualized resources**:
   - delivering IT services via resource pool that can expand/contract based on the required underlying workload, characteristics  
 - 4.**Utility-based pricing**: 
   - delivering IT services that can be metered for usage
 
__Q3. Describe the benefits of using CC:__
 - 1.Better capital utilization
   - the unit cost of on-demand capacity may be higher than that per time unit of fixed capacity, this is offset by not having to pay for the resources when not in use. 
 - 2.accelerate software development
   - faster provisioning of resources is a key benefit (instead of taking weeks to set up the environment, it can be provisioned in minutes). 
 - 3.elasticity of resources
   - access to a pool of a virtualized resources that expanding/contracting, thus pay only for the resources you used. 
 - 4.access to complex infrastructure and resources w/o internal resources
   - provisioning of infrastructure and application services can be outsourced to CC. 
 - 5.support for geographically distributed users
   - access are based on standard internet transports and protocols 
 - 6.New business opportunities
   - for providers to host cloud services and vendor applications
   
__Q4. Describe some driving factors towards using CC:__ 
 - 1.**poorly utilized resource** driving up hardware, labor costs
   - setting up a new environment is pricey
   - obtaining new hardware for new project is pricey
 - 2.**too long lead time** (a month) to create middleware infrastructure(new application environment)
   - Approvals - procurement - shipment - installation - license_procurement - OS_installation - configuration - application_ installation
 - 3.**error-prone manual process** to create middleware infrastructure
   - emerging when moving from test to production
 - 4.**under-utilized, Idle resources** during non-peak times(off-peak periods)
   - Each application must be sized to support peak load
 - 5.**degraded quality of service** during periods of exceptional load  
   - need more resources. need sth that can be provisioned and deprovisioned on demand
   
__Q5. Describe some of the concerns:__
 - 1.**Maturity**: ..Is it hype? Ready for producion-level deployment? Ready for prime-time? 
 - 2.**Standards**: ..in progress. See OpenCloudMenifesto
 - 3.**Security**: ..Many sharing the same resources. Mitigated via encryption? Only making public domain data available in public clouds?
 - 4.**Interoperability**: ..vendor APIs are different. Can we write code supported across lots of different cloud_providers? 
 - 5.**Data_Control**: ..what does a company do to be in control of their own data? The use of provate clouds? 
  
__Q6. Compare Grid_Computing with CC:__
 - There are several situations where Grids and Clouds can be used together. **Grids offer automatically scalable resources??** made available over a network. From this point, there is a convergence with clouds. Grids involve applying the resources of many machines in a network, working in parallel to solve a single problem at the same time while Clouds offer resources for many independent tasks.
 - If positioning CC to a Grid infrastructure, Grids link disparate computers to form one large virtual infrastructure, leveraging unused resources. Grid sizes vary from forming a 'super virtual computer'(loosely coupled machines??) to a smaller redundant dual machine system, but because of fixed network connection, we ourself should do all configurations(including load balancing) as we add extra machine, thus in Grids, we should know where the network is located(physical location).  
   - **Arch** 
     - Grids: Service-Oriented
     - Clouds: User-Specified
   - **Platform_Awareness**
     - Grids: Client software must be Grid_enabled
     - Clouds: Works in a customized environment provided by the service provider
   - **Scalability**
     - Grids: Nodes
     - Clouds: Nodes + Infrastructure
   - **Standardization**
     - Grids: Interoperability and Standards
     - Clouds: Lack of standards for interoperability
 
__Q7. Examples of CC:__
 - Commercial Public Clouds:
   - Made available via the Internet, offering services across open networks 
   - (almost) Free to use
 - Private Clouds: TBD

-----------------------------------------------------------------------------------
## Concepts
__Q1. Describe how CC leverages the Internet:__
 - CC is Internet-based computing whereby shared resources, software, information are offerred to computers on-demand. As a new consumption and delivery model inspired by `Consumer Internet Services`, simply CC is an **online environment for access** to computer resources: computing power, Storage, Management, Applications.
   
__Q2. Describe elasticity & scalability:__
<img src="https://user-images.githubusercontent.com/31917400/46347089-37234680-c642-11e8-8296-33eb7744c96c.jpg" />

 - **Elasticity(both direction) & Scalability(one direction)** is the ability to expand/shrink a computing resources in real time based on user's need. CC does always **"right-sizing"** to what is required and can measure usage by uptime(this usage must meet SLA_serviceLevelAgreements while minimizing cost). CC scale up to meet demand, scale down when higher demand is not required.
   - Why prefer VM Server Scaled up/down over physical Server Scaled up/down? -> speed, energy consumption

__Q3. Define Virtualization:__
 - Take one machine and split it up into multiple machine.  
 - Virtualization involves: Hardware, Networks, Storage, OS, Applications, Desktop??, **DATA**??
 - (+): the software is decoupled from the hardware(being independent of the hardware), which allows hosting an individual application in the environment isolated from underlying OS. It improves **IT resource utilization:** treating IT physical resources as logical resources, it consolidates the resources into a virtual environment(virtual CPU, virtual RAM, virtual HardDrive, virtual Networks). With it, one physical resource can look like multiple resources that have functions, features that are not available in their underlying physical resources(but when it comes to the performance it can't do outside of the physical, sth might have to lose out). 
   - `Reduced hardware cost`
     - enables to have a 'single server' function as 'multiple virtual server'.
     - You can manage resources to reduce operation, system management costs.
   - `Optimization of workload`
     - increases the usage of existing resources by enabling dynamic sharing of resource pool.
   - `IT flexibility and responsiveness`
     - enables to have a single, consolidated view of all available resources in the **network which are easily accessible regardless of location**.
     - enables to reduce the **management of your environment** by providing 
       - `emulation for compatibility` ??? while migrating from old environment, we can still use the old one.
       - `improved interoperability` ??? 
       - `transparent change windows` ???

__Q4. List the characteristics of virtualized environment:__
 - **Partitioning**: makes it possible to run multiple applications and OSs in a single machine.
 - **Isolation**: VMs are completely isolated from hosts and other VMs
   - crash of a VM does not affect other VMs
   - data is not shared b/w VMs
   - only communicate via specifically configured network connections 
 - **Encapsulation**: it is possible to encapsulate entire state of VM in `hardware-independent files`.
   - the `hardware-independent files` contain the OS, application files, and VM configuration.  

__Q5. Define Hypervisors:__
 - 'OS' would be called 'supervisor'. With the ability to run OS on other OS, the term 'hypervisor' resulted. It's a piece of code.
 - For example, VMware ESX(type_1), it is a virtualization software allowing multiple OS to run concurrently.
 - it uses a `thin layer of code` in software or firmware to achieve fine-grained, dynamic resource sharing(your OS consumes all resources of your machine while Hypervisor allocates the part of the resources of the machine to each OS). 
 - it provides the greatest level of flexibility in **how virtual resources are defined and managed** (coz it controls exact what size each VM will be) thus it is a primary technology of choice for system virtualization (it becomes industry standard)
 - it may mediate access to CPU, RAM, Hard, Network. ????
 
__Q6. Virtualized VS NonVirtualized systems(servers):__ 
<img src="https://user-images.githubusercontent.com/31917400/46361578-f3423880-c665-11e8-9163-55730ca9d016.jpg" />

 - NonVirtualized System: Because each system(server) has its own separate hardware, the amount of processing power available to each application is fixed. For example, application_A comes under heavy use while application_B is idle thus, the processing capacity on B might be underused.    
 - Virtualized System: By running both applications A, B on the same hardware `through a hypervisor`, you can direct resources to the system thus, hypervisor can offer more processing capacity and memory to the application being used more heavily.   

__Q7. Describe the types of Hypervisors:__
<img src="https://user-images.githubusercontent.com/31917400/46363862-153eb980-c66c-11e8-98bd-84be11b15240.jpg" />

 - **type_I**(native, bare metal): runs directly on the system hardware.
   - Iy is typically the preferred approach coz they achieve higher performance efficiency, availability, security. 
 - **type_II**: runs on a host OS providing virtualization services such as I/O device support, memory management.
   - mainly used on client systems where efficiency is less critical.
   - mainly used on a host OS or systems where support for a broad range of I/O devices is important ????

__Q8. Provisioning VS Deprovisioning:__ main benefit is scalability?
 - **provisioning** refers to the processes for the deployment and integration of cloud computing services within an enterprise IT infrastructure. From a provider’s standpoint, cloud provisioning can include the supply and assignment of required cloud resources to the customer. For example, the creation of virtual machines, the allocation of storage capacity and/or granting access to cloud software. So it offers 'resources availability' to USERS, SOFTWARE.
   - it controls 'applications available to users. 
   - it controls 'servers_resources' available to applications.
   
 - **deprovisioning** offers 'resources reduction' to USERS, SOFTWARE while deallocating 'back_end' resources. It refers the process of removing access of an individual user to an organization’s resources. This can include removing user accounts on individual machines or servers, or from authentication servers. It can also include removing a user’s machine entirely. De-provisioning is usually done when a user leaves an organization. 
   - Freeing up hardware, software associated with those application. 
 - Self_Service provisioning allows customers to request the 'amount of computer services' w/o going through a lengthy process.
   - computing, storage, software, process, other resources.
 - fast provision, fast decommission show the maturity of the hosting provider.   

__Q9. Describe Multitenancy:__
 - CC must enable multitenancy(different companies sharing the same underlying resources).
 - Multitenancy is the ability to deliver an application to multiple clients from a single instance of software. 
 - When building SaaS applications, or PaaS, ORGANIZATIONS? should design applications with multitenancy in mind to minimize the '/tenant' cost of delivery. Technical challenges associated with **building a multitenants application** include: access control, customization(data, user interface, business logic), and isolation of data.
<img src="https://user-images.githubusercontent.com/31917400/46371899-80df5180-c681-11e8-9274-f7db769d7408.jpg" />
 
 - 1)SaaS modes of multitenancy
   - Simple multitenancy(Single-tenancy):
     - Each customer has his own resources segregated from other customers
     - relatively inefficient
   - Fine_grain multitenancy(Multi-tenancy):
     - All resources are shared, but the customer data and access capabilities are segregated within the application
     - It's more efficient, offering superior economies of scale
 - 2)PaaS mode of multitenancy
     - it allows multiple customers to run their copy separately from other customers through virtualization.
     - Each customers code is isolated from each other.
 - The key technical challenge of multitenancy is how to support multiple client organizations from shared instances of the software solution.      
__Extra:__
 - API: refers a collection of interfaces providing access from one system into another's software. CC service should have standardized API defining how multiple 'applications' and 'data sources' communicate each other. It allows customers infrastructure, applications to plug into the cloud. Cloud APIs haven't been standardized yet.   
 - Metering of Services: cloud usage is tracked via metered services (No.of user, capacity used, services leveraged). Note SLA coz too many incidental charges. 
 - Economies of scale: refering the cost advantages that an IT vender obtains due to expansion.
   - AVG_cost/unit decreases as the scale of input increases.
   - The more resources used, the cheaper the price per resources. 
   - It's reducing the cost over time, which leads to greater adoption of the technology.
   
__Q10. Describe management(governance, tooling, automation):__
 - 1)**Governance:** a process(including principle, rules) of applying policies relating to using services. It tells a shared responsibility b/w users and the provider(understanding boundaries of the USER and Cloud is critical).
   - Ensure the IT assets are implemented in accordance with the agreement
   - Ensure the IT assets are properly maintained 
   - Ensure the IT assets are offering proper value, supporting the customer's goal
   
   - > Some Risk moving into a Cloud Environment
     - Audit and compliance Risk(data access ctrl, jurisdiction, audit trail, etc)
     - Billing Risk(accurate billing?)
     - Contract Risk(provider out of business?)
     - Security Risk
     - Information Risk(protecting intellectual property?)
     - Interoperability Risk
     - Performance, Availability Risk(KPI being maintained?)
   - > Management
     - Desktops in the Cloud
       - In a `virtualized desktop`(in the cloud), the applications, data, files, graphics are separate from the physical desktop and stored in the data center(cloud). 
       - The popular approach is VDI(virtual desktop infrastructure). The `virtual client desktop` is created on the server. VDI hosts a desktop OS on a centralized server in a data center(cloud). VDI is a variation on the `client-server computing model`, sometimes referred to as `server-based computing`. 
       - There are 4 types of `virtual client desktop`:
         - Session_based Computing: the user is running a session on the server.
         - OS streaming: the client OS software is passed to the device but only as much as needed. Some of the processing is occurring on the local machine. The application, data, files, graphics are split b/w client and server, streamed to the client when needed. 
         - VDI: VMwareESX, Citrix have these.
         - PC Blade: an entire PC can be contained on a single blade slotted into a blade cabinet. A server blade can contain lots of PC blades. The desktop is a thin client used to access the PC blade. ?? fuck. pc and desktop is different???
     - Devices in the Cloud
       - managing assets 
       - monitoring services
       - change management
       - security
       
 - 2)**Tooling:** Each layer of the cloud environment(application, platform, infrastructure) contains tools.  
   - it guides users via the physical makeup of the cloud (based on the expected demand characteristics) ?????
   - it assists: 
     - allocation of physical resources
     - asset management
     - resource virtualization
 
 - 3)**Automation:** it goes hand in hand with virtualization. As you know cloud environment implies dynamic scaling based on demand. Implementing a manula process is too time-consuming. Automation realizes the value of virtualization: `dynamic scaling`
   - Why? "scale, speed, cost" of deployment, dynamics of the environment..
   - Automation can be used for security as well...(such as policies, licensing..) 
 
 - 4)**Security:** CC presents an added level of risk because essential services are outsourced to a third party. CC shifts CTRL over data and operation from client to provider. 
   - What's the issue? Do I need to know? 

-----------------------------------------------------------------------------------
## Cloud Service Delivery Models
__Q1. Describe CSDM:__
 - There are three models deployed on the top of an `cloud infrastructure that has key characteristics of clouds`. Having access to all three gives the most flexibility for optimizing your environment. 
   - **SaaS**: Use of software(application) delievered via a network
     - The software no longer reside resides on the customer's machine.
     - Instead, the user access the applications running on a cloud infrastructure using various devices via a `thin-client interface` such as a web-browser. 
     - EX> web-based email running on a cloud  
   - **PaaS**: the middleware plarform and solution stack?? accessible on the cloud
     - Customers can develop, test, deploy their applications.
     - middleware means "software acting as an intermediate layer b/w applications or b/w client and server. It is used to support distributed applications in heterogeneous environment???? 
   - **IaaS**: provision servers, storage, networking resources
<img src="https://user-images.githubusercontent.com/31917400/46614029-b619f280-cb0c-11e8-9f30-1ab8c1c162b2.jpg" />

> Notice that each service model builds on the cloud infrastructure, and each model higher up on this diagram is more restrictive in the resources it makes available to the client. These services model architectures can be used together, in which case, the client has access to all resources of the **service model stack**. 
 - SaaS delivers only applications. It may conceivably be used as part of PaaS, IaaS, in which case, the user has access to the platform and infrastructure respectively.
 - On its own, SaaS is the least flexible. If you add PaaS, you can create, deploy, test the application (then can get more flexibility in how the application performs). 
 - Adding IaaS gives the ability to add or remove system resources(servers, storage, firewall, etc).  
<img src="https://user-images.githubusercontent.com/31917400/46670627-93e6aa00-cbca-11e8-82b8-c169dda5dde2.jpg" />

__Q2. SaaS:__
 - Under the SaaS model, `SP(service_provider)` **is responsible for creation, updating, maintenance of the application** including the licensing the software?? Users rent the software on a per usage basis or buy a subscription. The service is accessed as a web application or as a wrappered web services application invoked using web services APIs. 
 - WTF SERVICE PROVIDER IS A SOFTWARE PROVIDER? platform provider? 
 - Service user accesses the service through Internet_based interfaces. ???????????????
<img src="https://user-images.githubusercontent.com/31917400/46670547-61d54800-cbca-11e8-9637-c2095cf96306.jpg" />

__Q3. PaaS:__
 - Under the PaaS model, SP(service_provider) supplies the software platform or middleware where the applications run. `User` **is responsible for creation, updating, maintenance of the application**. The sizing of the hardware required for the execution of the software is made in a transparent manner. Platforms in the cloud are an interesting offering that takes the pain away from having to set up the software platform or middleware.
 - Ex) Google App Engine, IBM smart business development, Test Cloud
<img src="https://user-images.githubusercontent.com/31917400/46667878-db693800-cbc2-11e8-9832-0c779cdf0c34.jpg" />
<img src="https://user-images.githubusercontent.com/31917400/46669813-6a2c8380-cbc8-11e8-9cbc-a3bd311de192.jpg" />

__Q4. IaaS:__
 - `IP` uses the **cloud** to outsource the provision of computing infrastructure to host service. IP(infra_provider) makes entire computing infrastructure available "as a service". It manages a large pool of computing resources and use virtualization to assign and resize the resources required by customers. Rather than purchasing servers, customers rent processing capacity, memory, data storage, networking resources provisioned over a network. Supporting this service is through a combination of some special features of CC such as dynamic provisioning, fine_grained measurement(metering), virtualization, broadband access, flexible billing.  
<img src="https://user-images.githubusercontent.com/31917400/46665107-c688a680-cbba-11e8-9a62-b7a035d1fe0f.jpg" />

__Q5. Describe additional Cloud Service:__
 - A number of other service candidates have identified by market trends. These includes DaaS(data), TaaS(testing), IaaS(integration). 
 - However, they could fall into the SaaS, PaaS models.  

__Q6. Describe a Reference Arch for the PaaS model:__
<img src="https://user-images.githubusercontent.com/31917400/46671394-8b8f6e80-cbcc-11e8-97af-3f5f79ab6074.jpg" />

 - Cloud_provider(AWS) makes its service available(via APIs) to the users.  
 - BSS layer enables capabilities such as subscription services for a pay-per-usage model.
 - OSS layer is reponsible for making resources available on demand and for the security of the environment. 
 - To instantiate an new cloud instance, the user sends a request to the cloud_provider. The request is delegated to OSS that initiates and manages cloud service instances. 
 
 - cloud management platform enables to manage, deploy, automate business applications on the cloud. 
 - OSS manages the creation of cloud service instances. 
 - BSS manages the business aspects of cloud service instances - metering, reporting, analytics, etc.
 - Depending on the environment, the user interface to the cloud management platform can be anything; and this interface manages the virtual machine images and the virtualized infrastructure.  
   - from a comprehensive portal interface? 
   - to API
 
-----------------------------------------------------------------------------------
## Cloud Deployment Scenarios






























































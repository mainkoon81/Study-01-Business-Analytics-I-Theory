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
## Predictive Analysis
## 1) [Basic Linear Model]: For Numeric & Continuous outcome
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

## 2) [Classification Model]: for Non-numeric & Discrete outcome (identifying what "group" a data point belong to)
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

2> Descriptive statistics is about describing our collected data.
 - measures of center 
 - measures of spread 
 - shape of distribution
 - outliers and plots of data
 
3> Inferential Statistics is about using our collected data to draw conclusions to a larger population.
 - Population: our entire group of interest.
 - Parameter: numeric summary about a population
 - Sample: subset of the population
 - Statistic: numeric summary about a sample
The way we perform inferential statistics is changing as technology evolves. Many career paths involving Machine Learning and Artificial Intelligence are aimed at using collected data to draw conclusions about entire populations at an individual level. 

4> Simpson's Paradox
 - the way we choose to look at our data can lead to the different result.
<img src="https://user-images.githubusercontent.com/31917400/34156013-515bc6ec-e4b3-11e7-82ba-38e1f7a49784.jpg" width="400" height="125" /> 
<img src="https://user-images.githubusercontent.com/31917400/34170221-f0ad18a8-e4e1-11e7-9517-056f9c4b5bbf.jpg" width="500" height="180" /> 

5> Discrete Random Variable "P(X=x)=f(x): y-value"
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

6> Continuous Randome Variable "P(X<=x)=F(x): area"

7> Examples
















































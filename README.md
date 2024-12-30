# R-Language_rental_analysis
Descriptive statistics
After defining the new data frame (Rent.df) descriptive statistics was studied for each of the variables using R studio:

Price	Bedroom	Bathroom	Area
Min.   :    1200  	Min.   : 1.00 	Min.   : 1.00  	Min.  :    3  
1st Qu.:  13000  	1st Qu.: 1.00 	1st Qu.: 1.00  	1st Qu.: 650  
Median :  21000  	Median : 2.00	Median : 2.00	Median : 1000  
Mean   :  44337  	Mean   : 2.08	Mean   :   2.06 	Mean   : 1265  
3rd Qu.:  36000  	3rd Qu.: 3.00	3rd Qu.: 3.000  	3rd Qu.: 1440  
Max. : 5885000  	Max. : 15.00	Max. :  19.00  	Max.   :19800  

4.3 Data Cleaning or Preprocessing
Data cleaning nearly comprises of handling the following three types of values:
1. Duplicate observations
2. Null Values
3. Outliers
Using the unique() command in Rstudio, duplicate values were checked, but no duplicate observation found, then using is.na() command null values were checked and no null values found, For checking the outliers histogram and boxplot were plotted , then extreme values were omitted , histogram and boxplots plotted after removing the outliers are attached below :
Price: Rent prices less than Rs 1,00,000 used
  

Bedroom: less than 4 bedrooms used 
   

Bathrooms: less than  4 used

   
Area: less than 3000 used
   

After eliminating the outliers, 176513 observations remain, and 16,498 observations have been removed.
Conversion of categorical variable to numeric variables 
For the city variable , as it is a categorical variable , it was converted into numeric one hot encoding using as.numeric(as.factor()) command in Rstudio.

4.4 Multiple Linear Regression
a) Assumption check for Linearity

i) Price vs Bedrooms                                                              ii) Price vs Bathrooms
 ![image](https://github.com/user-attachments/assets/b91dbbe7-07af-411d-96cd-7b9ff14bffbb)  ![image](https://github.com/user-attachments/assets/b9b3cc24-707b-48c5-a2bb-2b5de9f299d2)

  
iii) Price vs rent
 ![image](https://github.com/user-attachments/assets/ae86fda7-d75a-4c86-a345-7efdb8168433)


b) Assumption check for Normality of residuals


Normality of residuals of MLR model can be  checked by plotting a histogram:
 ![image](https://github.com/user-attachments/assets/8c8da3bf-0208-4d17-aaa1-5f628cb80c02)



As the histogram looks a bit skewed, therefore to ascertain the normality of residuals, Q-Q plot is plotted and the values in plot predominantly follow a straight line, therefore it can be assumed that condition of normality is met.
![image](https://github.com/user-attachments/assets/43b4db25-15d7-4614-8c92-c7f09c1a83bd)

 

c) Assumption check for multicollinearity
![image](https://github.com/user-attachments/assets/ddcc591b-07b3-466f-a8c1-e79b01823df7)

To check the multicollinearity assumption, Correlation analysis needs to be done , On 
completing the correlation, it can be seen that there is high correlation seen in between 
bedroom and bathroom as well as area and bedroom, therefore to rule out
multicollinearity and for the purpose of comparison, another MLR model needs to be
built by removing the Bedroom variable, afterwords through Hypothesis testing using
ANOVA, It can be ascertained which model is better fit for the data.

 

Below are the descriptive statistics attached for both the 
Models:

MLR 1
 
![image](https://github.com/user-attachments/assets/a9ce3600-7789-4cff-802f-5b92c5f4cf20)




MLR 2 
 
![image](https://github.com/user-attachments/assets/d6c75bd9-0fb9-44ea-8bbc-210adb03fb9b)

Q-Q plot for MLR 1   
![image](https://github.com/user-attachments/assets/4d80a6e0-8a40-4344-89c2-dc78292fc819)

Q-Q plot for MLR 2
![image](https://github.com/user-attachments/assets/2f422763-b196-4a95-8bd4-5702783fb043)
  
The Q-Q plot for both the models seems similar Therefore ANOVA test need to be done to ascertain which MLR model is better fit for the analysis .

4.5) ANOVA

To ascertain whether the selected model has multicollinearity or not, VIF factor test will be conducted later in this section, additionally ANOVA test is also being conducted to determine the significance of the bedroom variable the Null Hypothesis and alternate hypothesis are stated below:
Null Hypothesis ( Ho): The “bedroom” variable has no significant effect on the dependent variable.
Alternate Hypothesis ( H1): The “bedroom” variable has a significant effect on the dependent variable.

Anova has provided the following outcome:
	Res.Df	RSS	Df	Sum of Sq	F	Pr(>F)
1	176508	3.5986e+13	NA	NA	NA	NA
2	179509	3.6066e+13	-1	-7.9259e+10	388.75	2.2e-16 

Since the p value is less than 0.05, therefore Null Hypothesis is rejected , therefore Bedroom is significant variable and MLR 1 Model is a better model
Additionally, after running the vif factor check for all 5 variables in MLR 1, it can be seen that all vif factor values are below 5 for all 5 variables, thereby confirming that no multicollinearity is seen in MLR 1
 

Assumption check for Homoskedasticity
In the Homoskedasticity check the residuals are plotted against the fitted values and from the plot it can be observed that the residuals are almost proportionately spread across the fitted values, this shows that homoskedasticity is met, therfore MLR model is acceptable .
 
![image](https://github.com/user-attachments/assets/345e7b06-863f-4c12-a675-482c78e4806b)



Evaluation (Interpretation of Result)
MLR 1:
 ![image](https://github.com/user-attachments/assets/0e6ff555-3115-4c7e-8fd7-dc207aa66779)


The above output for MLR 1 can be described as below:
Bedroom: if all other factors remain constant and the no. of bedrooms in an apartment increases by one unit then the rental price of the apartment goes up by INR 1759.
Bathroom: if all other factors remain constant and the no. of bathrooms in an apartment increases by one unit then the rental price of the apartment goes up by INR 5036
Area: if all other factors remain constant and the area of the apartment increases by one unit then the rental price of the apartment goes up by INR 12.25.
City: if all other factors remain constant and the city increases by one ( Alphabetically in the sequence of A to Z) then the rental price of the apartment goes up by INR 2219
Adjusted R-squared: the adjusted R-squared is 0.3475 or 34.75%, which implies that 34.75% of the rental price of an apartment can be explained by all the above 4 predictor variables ( no of bedrooms, no of bathrooms, area, city), that is all these 4 variables exert a moderately strong influence on the rental price.

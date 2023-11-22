# ECON-487-Lab-3
1)	Let’s focus on two variables HHLARGE (“fraction of households that are large”) and EDUC (“fraction of shoppers with advanced education”). 
a.	What are the means and percentiles of each of these variables?
HINT: summary(oj$EDUC)
b.	Using your coefficient estimates from the regression in Q9 of the previous problem set (if you did not include HHLARGE and EDUC, rerun the regression with them included):
i.	If we move from the median value of HHLARGE to the 75th percentile (3rd quartile), how much does log(quantity) change each week on average?
HINT: using coef(reg_output)["var_name"] exports the coefficient on “var_name” from the regression model “reg_output”.  
Similarly, summary(df$var_name)  will output a bunch of summary statistics for the variable var_name in data frame df.  Using summary(df$var_name)["3rd Qu."] will take the level of the 3rd quantile from the summary of var_name.  
Note: if we wanted to assess the changes in levels, you’d want to take the exponent of everything.
ii.	If we move from the median value of EDUC to the 75th percentile (3rd quartile), how much does log(quantity) change each week on average?
iii.	Base on this analysis, which is the more important predictor of demand?
c.	Now let’s see if these variables impact price sensitivity. Add two interaction terms (with logprice) to the model to test this. 
i.	What are the coefficients on the interaction terms? 
ii.	Does the sign of your estimates make sense based on your intuition?
iii.	What are the coefficient estimates on the variables EDUC and HHLARGE that aren’t part of the interaction term? How do they compare to your regression from 1b?
iv.	Similar to 2b, if we move from the median value of each variable to the 3rd quartile, how much does elasticity change? Based on this, which is more important to price sensitivity?
d.	You should notice that the coefficients on EDUC and HHLARGE have flipped sign once we include interaction terms with price. HHLARGE now appears to be a positive demand shifter and increases price sensitivity. Explain in words or pictures what is going on.
2)	Create make a new dataframe which takes the previous week’s prices as a variable on the same line as the current week.  This would enable you to see if there is intertemporal substitution. 
a.	There are going to be a couple of steps.  First is creating a new dataframe which is like the old one except that the week variable will change by a single week
i.	Df1 <- oj
ii.	Df1$week <- Df1$week+1
1.	This will replace week with week+1
iii.	The next step will use the merge function.  
1.	Df2 <- merge(oj, df1, by=c("brand","store","week"))
2.	Investigate the Df2 and rename the lagged store values needed for a lagged price within the same store
b.	Now run a regression with this week’s log(quantity) on current and last week’s price.
c.	What do you notice about the previous week’s elasticity?  Does this make sales more or less attractive from a profit maximization perspective?  Why?
3)	In the last assignment you calculated the MSE on a test set.  Let’s expand that code to include 5-fold cross validation.  
a.	Create 5 partitions of the data of equal size.
b.	Create 5 training datasets using 80% of the data for each one.  This could be done by “appending” the data together using rbind or via sampling.
c.	Estimate a complex model using OLS which includes price, featured, brand, brand*price and lagged price, all the sociodemographic variables and interactions of EDUC and HHSIZE with price on each of the training sets then the MSE on the test sets using the predict command.
i.	Calculate the MSE for the model on the test set for each fold (e.g., there will be five sets of model parameters and five test set MSEs with 5-fold cross validation).  
ii.	Average across the MSEs to get the cross validated MSE for an OLS model run on that particular set of features.

Advance DAX Visualization with Coupon Redemption Data https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms
Introduction
To create advance DAX functions, a suitable data ‘Coupon Redemption’ data set is used. The data set is used for predicting coupon redemption and the data set includes information on campaign data, items, customer demographics. 
Based on the data set, there are 6 tables. Train, campaign data, customer demographics, coupon item mapping, customer transaction data and item data. The data set is available on Kaggle. 
As the first step the data set is loaded to power bi and created relationship across all tables.
Since the data set is based on coupon redemption, there are details of customers and demography and purchased items and value and discount information. Along with the item purchase information, the data set can be analyzed categorical information on customer details and understanding the basket value. 
3.1 Family Type (SWITCH Advance DAX Function)
Under the customer demographic information, the column family size provides information on number members in the family. The data starts from 1 and to a maximum number 5. This count provides the total family member count. Therefore, the numerical values can be segregated by different categories. In categorize it the following breakdown is created.



Member Count	Category Name
Between 0-2	Small Family
3	Medium Family
Between 4-5	Large Family

Based on the above breakdown a new column is created and the switch function is used. To assign the new column, it is name under ‘Family Type’. After calling the SWITCH function based on the above table the condition ‘SWITCH’ function takes several conditions and returns corresponding values. In the above table, if the member count is 3 it will assign the category name as medium family and if the condition is ‘TRUE’.
 
Figure 1 SWITCH Advance DAX Function

3.2 Ranking Income Bucket (RANKX Advance DAX Function)
The RANKX function is used to determine which income bracket consists of 1 to 12. Based on that the RANKX function allows to calculate rank of each level of income and ‘ALLSELECTED’ allows to select all the attributes from customer demographics table and ‘DESC’ ensures the ranking must be in descending order. Therefore, when higher the income is higher the rank. The final argument ‘DENSE’ will meet a condition if two values are the same it will skip. 

 
Figure 2 RANKX Advance DAX Function
3.3 Customer Basket Value by customer ID (GROUPBY & CALCULATE Advance DAX Functions)
The data set includes purchases for customer IDs. However, the table which includes the customer id does not include the total value of sale after discount. Therefore, the values should be grouped by from the customer transaction table on the purchases. In order to create a new total sale value after total discount, a DAX function is created with ‘CALCULATE’ and added the final selling price and used ‘GROUPBY’ function to group all values by customer ID.
 
Figure 3 CALCULATE and GROUPBY Advance DAX Function

3.4 Visualization of the three New Advance DAX Function
Based on the 3 advance DAX function the following visualization is created. The bar chart represents the three family groups based on the number of family members and the y axis represents the calculated basket value by customer id. The use of these two DAX functions (SWITCH & GROUPBY and CALCULATE) allow categorize the visual simpler with just three bars rather than 5.
The stacked column chart plot has the x axis as the ranking of income bracket (RANKX) function and the y axis with the quantity and the legend, family type (SWITCH) function. This allows to understand the visual better based on a ranking and the family type. 
The tree map includes the family type, with the use of (SWITCH) function to divide the three-family type customer basket value and quantity. 
The final visualization decomposition tree includes the calculated total customer basket value (GROUPBY) function and explained by the family size and age range and by the ranking of income (RANKX) function. 

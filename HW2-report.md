### Kris Seekford
### CS625-HW2
### 03/09/25

##### <ins>Initial Data Cleaning
To start the project, I first downloaded the data and uploaded it to OpenRefine. I then removed duplicate rows by sorting the data based on the movie name and "blanking down" all rows. This removes any duplicate row from the table. Next, I went through the genre column and replaced any data that did not make sense. For example, there were rows that said "add plot" or had the plot instead of the genre. I then repeated this process for the rest of the columns. Lastly, I nnoticed that the likes column had rows that were nnot considered a number because of the comma in them so I removed the commas and changed the values to numbers.

##### <ins>Refilling Empty Values
Continuing with the tasks outlined in the instructions, I changed all blank values in the rating, votes, and run times column by selecting the column as a numeric facet, including only blank cells, and then used the custom transformation to change the value to 0. I then repeated this process for the columns with text values, but instead of channging the value to 0, I changed it to N/A.

##### <ins>Fixing the Year Column
To start the cleaning process of the year column, I first removed the parentheses and "--" by using a replace function to delete the items. An example code is value.replace("(",""). Next I split the column into multiple columns by spaces. This removes all the text after the year number/numbers. However, doing this will shift the year values with a roman numeral to the second row. To fix this, I created a numeric facet for the second year column, selected numeric values, then transformed the original year column to the values of the second year column, and lastly deleted the other year columns. Lastly, we still have one issue, in the first step I removed "–" because they were at the end of some years instead of only in between a range of years. To add this value back to the years that are in a range format, I converted the column back to the text format. This converted some of the values to a value such as 2000.0 so I used a replace function to remove the ".0" first. Finally, I used an if statement to select every value thats length was greater than 4 and added "--" in between the fourth number and fifth number in the value. 

##### <ins>Refilling Empty Values

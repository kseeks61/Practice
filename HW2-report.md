### Kris Seekford
### CS625-HW2
### 03/09/25

##### <ins>Initial Data Cleaning
To start the project, I first downloaded the data and uploaded it to OpenRefine. I then removed duplicate rows by sorting the data based on the movie name and "blanking down" all rows. This removes any duplicate row from the table. Next, I went through the genre column and replaced any data that did not make sense. For example, there were rows that said "add plot" or had the plot instead of the genre. I then repeated this process for the rest of the columns. Lastly, I nnoticed that the likes column had rows that were nnot considered a number because of the comma in them so I removed the commas and changed the values to numbers.

##### <ins>Refilling Empty Values
Continuing with the tasks outlined in the instructions, I changed all blank values in the rating, votes, and run times column by selecting the column as a numeric facet, including only blank cells, and then used the custom transformation to change the value to 0. I then repeated this process for the columns with text values, but instead of channging the value to 0, I changed it to N/A.

##### <ins>Cleaning the Year Column


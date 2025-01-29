### Kris Seekford
### CS625-HW2
### 03/09/25

#### <ins>Initial Data Cleaning
To start the project, I first downloaded the data and uploaded it to OpenRefine. I then removed duplicate rows by sorting the data based on the movie name and "blanking down" all rows. This removes any duplicate row from the table. Next, I went through the genre column and replaced any data that did not make sense. For example, there were rows that said "add plot" or had the plot instead of the genre. I then repeated this process for the rest of the columns. Lastly, I nnoticed that the likes column had rows that were nnot considered a number because of the comma in them so I removed the commas and changed the values to numbers.

#### <ins>Refilling Empty Values
Continuing with the tasks outlined in the instructions, I changed all blank values in the rating, votes, and run times column by selecting the column as a numeric facet, including only blank cells, and then used the custom transformation to change the value to 0. I then repeated this process for the columns with text values, but instead of channging the value to 0, I changed it to N/A.


#### <ins>Fixing the Year Column
To start the cleaning process of the year column, I first removed the parentheses and "--" by using a replace function to delete the items. An example code is value.replace("(",""). Next I split the column into multiple columns by spaces by clicking the "Split column" button in the "Edit column" tab. This removes all the text after the year number/numbers. However, doing this will shift the year values with a roman numeral to the second row. To fix this, I created a numeric facet for the second year column, selected numeric values, then transformed the original year column to the values of the second year column, and lastly deleted the other year columns. Lastly, we still have one issue, in the first step I removed "–" because they were at the end of some years instead of only in between a range of years. To add this value back to the years that are in a range format, I converted the column back to the text format. This converted some of the values to a value such as 2000.0 so I used a replace function to remove the ".0" first. Finally, I used an if statement to select every value thats length was greater than 4 and added "--" in between the fourth number and fifth number in the value. The last step to clean the year column was to split the column by "--" into a start year and end year column. I did this by seletcing the "Split column" button under the year column and split it by "--". After this I created a numeric facet for the end year column, selected all blank rows and replaced it with the start year's value. Lastly, I noticed that there were still some blank values since they did not have a value in the start year columns as well and switched them to "N/A".

The following is the Python if statemnt mentioned above (assuming you switched the values to text and removed the .0):

    if len(value) > 4:
        return value[0,4] + "--" + value[4:]


#### <ins>Creating Verdict Column
The task of the cleaning process was to create a new column called Verdict, that returned "Not known" if the rating value was 0, "Flop" if the rating value was greater than zero but less than or equal to 4.5, "Average" if the value was greater than 4.5 but less than or equal to 6.5, "Hit" if the value was greater than 6.5 but less than or equal to 8.0, and "Super Hit" if the value was greater than 8.0. To complete this task I first selected the ratings columns and selcted the "Add column based on this column..." button in the "Edit column" tab. Once I clicked this, I named the new column "Verdict" and went into the transformation space where it stated "return value". I switched the code to Python since I am most famliar with it and wrote an if-elif-else statement for the conditions (elif stands for else if). Lastly, I created the column and checked the cells in a text facet to ensure the process went how I expected.

The following is the Python code to execute the conditional statement:


    if value == 0:
      return "Not known"
    elif 0 < value <= 4.5:
      return "Flop"
    elif 4.5 < value <= 6.5:
      return "Average"
    elif 6.5 < value <= 8.0:
      return "Hit"
    else:
      return "Super Hit"


#### <ins>Links to Data
If you would like to see more about my data cleaning process I am providing the links below.

CSV of the cleaned data: 
[https://github.com/kseeks61/Practice/blob/main/HW2-Movies.csv]

JSON of Executions:
[https://github.com/kseeks61/Practice/blob/main/HW2-Movies.json]


#### <ins>Analysis of the Cleaned Data
The first task of my data anlysis is to finnd how many movies were listed as "Super Hits" in the year 2021. To find this I first swithced both the "Fist Year" and "Last Year" column's cells to text by going to "Edit cells", "Common transforms", and then clicked the "To text" button. I then created a text facet of the Start Year column by clicking the "TExt facet" button under the "Facet" tab and selected the year 2021. Since we only want to find the movies and shows from the year 2021, I repeated the above "Text facet" task for the "Last Year" column as well. After this, I created a text facet for the "Verdict" column and viewed the the total number next to the "Super Hit' values, which was 38.

The next task is to find the movies that got the highest ratings from 2018 to 2020 by genre. This task is similar to the one above. I first select the year 2018 in a text facet of the "Start Year" column, then included the years 2018, 2019, and 2020 in the text facet for the "Last Year" column. By doing so we now have a subsection of the movies that started in 2018 and ended in 2018, 2019, or 2020. I then created a new text facet based on the "GENRE" column, which effectively gives us a list of genres of the movies in those years. However, since we did not clean the "GENRE" column, the genres can fall into one or more categories, resulting in lots of unique genres such as "Comedy, Romance, Thriller" resulting in very low numbers of values in the same genre. Since the question asks us to find the data and not clean it, we will move on, but it is still important to note that one would want to change that for a more accurate analysis. Once you have completed these steps, you can click on the genre you want to observe and compare the ratings of the movies in said genre. I found that the highest rated movie in the Action genre was "Nohzdyve" with a rating of 7.5. The highest rated movie in the Comedy genre was "Daniel Sloss: Live Shows" with a rating of 8.6. (Since there were 100 rows for the Comedy genre, I created a numeric facet for the "Rating" column and used the slider to highlight the top values.) Following this process, I found that the highest rated movie in the Drama genre was "Castle & Castle" with a rating of 8.6.

The next task is to find the top 3 genres that got the lowest number of votes. To do so, we can close out of all previous facets except the text facet for the "GENRE" column (however make sure to deselect the "Drama" genre). Next we created a numeric facet of the "VOTES" column. However, since we do not want to include the values that are zero (since we changed this earlier to represent no data given), we can write an if staement in the "VOTES" column's numeric facet. To do this, first click change on the top of the numeric facet. Then we can write the following code:

    if value > 0:
        return value

This code will effectively turn any zero value in the numeric facet to a blank column. Next we can click on numeric to only keep the numeric values and then adjust the slider all the way to the left. Finally, I sorted the data from lowest to largest values in the "VOTES" column by clicking on the column, clicking "Sort", then selecting "Sort values cells as" "numbers", clicking "smallest to largest", and finally, clicking the button to "Sort based only on this column". Now we have our data sorted and can view the genres of the movies with lowest number of votes. I found that the genres of the 3 movies that have the lowest number of votes are "Drama", "Comedy", and "Animation, Short".


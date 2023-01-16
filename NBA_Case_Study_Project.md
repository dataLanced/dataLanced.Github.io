# NBA Case Study Project

<img src="images/Massachusetts Education Project.png?raw=true"/>

For this project I am going to assume the role of an entry-level data analyst interviewee for my hometown NBA team, the Minnesota Timberwolves. My goal is to display how we can use data to try to add potential talent to our team and we will display how that we can using Tableau.

This project is something that I feel personally excited about is because I throughly love all things sports and seeing how integral that data science has become across all across sports. It has actually led to teams improvement by acquiring players and even aiding in individual player development. Since I'm interested in this domain, I'd like to continue doing hobby projects and maybe work for some team's front office perhaps!

Here are just some of the things that I took away from my interactions with the data:

- Tyrese Haliburton, Nikola Jokic, Jayson Tatum, Josh Giddey and Draymond Green are very interesting and productive outliers considering the position that they play.
- Anthony Edwards is very similar to Zach Lavine and Donovan Mitchell but at least 5 years younger!
- Sacramento Kings have the best 3-point shooting power forwards in the league!
- Joel Embiid and Demar Derozan stand out a lot! Find out why!
- Some shooting guards actually have more assists than some point guards!

In the upcoming data analyis section, I'll explain how I came away with these insights! If you're a hard core hoops fan though, I'll warn you in advance, but your favorite all-star caliber players might not stand out as much as you think—at least in this brief analytics project!

## The What and The Where of this Dataset

This dataset can be found here at this popular hoops website called [Basketball Reference](https://www.basketball-reference.com/leagues/NBA_2022_totals.html). The data is already clean and all we have to do is feed it as it is to Tableau.

The dataset itself encompasses the total stats (not per game split) entirety of the NBA players who played at least one game in the 2021-22 NBA season. Since we know it's from a trusty source and cross-checked the numbers with other trustworthy NBA sources. 

### Data Dictionary

There are over 20 columns of data, but we only need few columns to find the answers we're looking for:
- Player : A player's name
- Pos: Player position
- Age: A player's age
- Tm: A player's team during the 2021-22 season
- G: Total games played
- 3P%: Three-point shot percentage
- TRB: Total Rebounds
- AST: Total Assists
- PTS: Total Points

Now let's begin the data analysis section!!

## Data Analysis

First, we're going to create a scatter plot featuring all the players featuring the PTS, AST, TRB, Pos. This is how it looks like below:


As we cam see,

---

### Try to find out which medical specialties have the highest number of procedures on average.

Now with this line of code we're going to check out the distinct values (or fields) in the `medical_specialty` column using the following query.
<img src="images/SQL Healthcare Project/query2.png?raw=true"/>
<img src="images/SQL Healthcare Project/output1.png?raw=true"/>

I also counted the unique values in the `medical_specialty` column and it turns out that we have 73 distinct values.

Now that we know what those are, let's create a query that groups all the values of `medical_specialty` together and find the average `num_procedures` per specialty. We also want to count how many patients there are per specialty (please note that one row in this dataset represents one patient).

<img src="images/SQL Healthcare Project/query3.png?raw=true"/>

And here are a few lines of the output

<img src="images/SQL Healthcare Project/output2.png?raw=true"/>

Not only does it look more organized now, but we are closer to our next goal of answering which specialties have the highest number of procedures on average. So let's say that our supervisor instructs us to filter down to specialties that have at least 50 patients and an average of at least 2.5 procedures per patient for a given specialty. With this we should have a great idea on what specialties to focus on! 

So let's put this concept into a query and see what we get.

<img src="images/SQL Healthcare Project/query4.1.png?raw=true"/>
<img src="images/SQL Healthcare Project/output3.png?raw=true"/>

Just as planned! We now have 5 specialties that were able to meet our rigorous criteria and as we can see from both the `avg_procedures` and `rows_count` columns, a lot of patients are treated in these specialties and they get at least 2.5 procedures too. These are amazing results and I'm quite sure that the supervisor will be delighted with these results!

---

### Are there any racial discrepancies? (based on the number of lab procedures done)

Next, our supervisor has asked us to check to see if there are any discrepancies in treatment based on race. For this purpose, we will use the `num_lab_procedures` that patients from all racial backgrounds are receiving the highest quality treatment. The table that we have been using until now, `patient`, doesn't have any information that outlines a person's racial background. Therefore, we will use another table called `demographics` employing the SQL inner join technique along the shared `patient_nbr` column to ensure that we can properly align the demographic info of the new table to the parent table. The `patient_nbr` column is our primary key for both tables, so we know that the values present are all unique.  

<img src="images/SQL Healthcare Project/query5.png?raw=true"/>

For this query, we created a CTE and used it in a view to use for future reference and set up our join and the columns to be displayed from said join. Next we want to take that view and create a query that categorizes our database by race and uses the average of `num_lab_procedures`and we can determine whether all of our patients are getting equal treatment.

Here is the query:

<img src="images/SQL Healthcare Project/query6.png?raw=true"/>

And the output:

<img src="images/SQL Healthcare Project/output4.png?raw=true"/>

From these results, we can determine that there aren't any outliers that would indicate the presence of preferential treatment due to racial makeup. Now let's move further in our analysis.

---

### Do patients who get a lot of procedures/tests done stay longer in the hospital?

Next we were asked to see if patients that have a lot of procedures done tend to have longer stay times in the hospital. First, we run a query that gives a sense of the data distribution for the `num_lab_procedures` column.

<img src="images/SQL Healthcare Project/query7.png?raw=true"/>


<img src="images/SQL Healthcare Project/output5.png?raw=true"/>

From the output, we can see that `num_lab_procedures` has an average value of around 43 procedures. With this knowledge, we can use a series of `CASE` statements to categorize our patients based on their `num_lab_procedures` value. If a value for `num_lab_procedures` falls within 0-24 it will be assigned the tag of "few", for 25-54: "average", for over 55: "many".

Now we are going to create a query that creates these tags for every patient, groups all of them by these tags and looks at the average hospital stay per group. Now, let's look at that query and its output together

<img src="images/SQL Healthcare Project/query7.png?raw=true"/>
<img src="images/SQL Healthcare Project/output6.png?raw=true"/>

From what we have seen, we can now draw a positive correlation between time spent in the hospital and how many procedures that they have. The longer a patient stays at a hospital the more procedures they have and the shorter their stay, the fewer procedures they have.

---
### We want to perform a medical test on any patient who is either African-American or had an "Up" value for metformin. Please help us compile a list of patients who   meet this criteria

Next, I've been tasked to compile a list of patients who are either African-American or have a value of "Up" for the `metformin` column. Here is a simple query that we can use, making use of the `UNION` function. Some lines of the output will also be displayed.

<img src="images/SQL Healthcare Project/query8.png?raw=true"/>
<img src="images/SQL Healthcare Project/output7.png?raw=true"/>

---

### Find "success stories" where patients who came into the hospital with an emergency (`admission_type_id` is 1), but stayed less than the average time in the hospital 

To find these success stories, we have to have something in our query like this: `WHERE time_in_hospital < AVG(time_in_hospital)`. But actually, this wouldn't work and it would produce an error because we can't use `AVG` in a `WHERE` clause, only in a `SELECT` clause. So we have to use a subquery to work around this. Here is an example of how we can get what we want:

<img src="images/SQL Healthcare Project/query10.png?raw=true"/>
<img src="images/SQL Healthcare Project/output10.png?raw=true"/>

Subqueries are a useful tool, but they can make things look messy if we have a lot of them to manage. Therefore, we can once again use a CTE to make things more neat. Last time we created a `VIEW`, so this time we're going to use `WITH`. We'll update the query and confirm that the output is still the same as our previous query.

<img src="images/SQL Healthcare Project/query10.1.png?raw=true"/>
<img src="images/SQL Healthcare Project/output11.png?raw=true"/>

With the help of the `WITH` CTE our subquery has now been condensed from `(SELECT AVG(time_in_hospital) FROM health)` to just `(SELECT * FROM avg_time)`. 

And we also have a nice list of "success story" patients to provide to our supervisor too!

---
Next we've been asked to generate a query that will summarize the results of the top 50 medicated patients along with the number of lab procedures that they had(table will be ordered by `num_medications`and afterwards `num_lab_procedures`). The output of our queries should produce values in this format: 

### We are asked to write a summary for the top 50 medical patients in a format like this: "Patient 2383 was Caucasian and was readmitted. They had 21 medications and 32 lab procedures."

Using a combination of `CONCAT` and `CASE`, we will be able to generate multiple summaries like this. Here is the query and the output below:

<img src="images/SQL Healthcare Project/query11.png?raw=true"/>
<img src="images/SQL Healthcare Project/output9.png?raw=true"/>


---

## Recap/Conclusion

In conclusion, we set out to complete the tasks that our supervisor instructed us to and we've done just that. To review what was asked of us, let's refresh our memories with the below tasks:

- What does the time spent in the hospital look like? Are the majority of our patients spending less than 7 days?
- Try to find out which medical specialties have the highest number of procedures on average.
- Are there any racial discrepancies? (based on the number of lab procedures done)
- Do patients who get a lot of procedures/tests done stay longer in the hospital?
- We want to perform a medical test on any patient who is either African-American or has an "Up" value for metformin. Please help us compile a list of patients who   meet this criteria
- Find "success stories" where patients who came into the hospital with an emergency (`admission_type_id` is 1), but stayed less than the average time in the hospital 
- We are asked to write a summary for the top 50 medical patients in a format like this: "Patient 2383 was Caucasian and was readmitted. They had 21 medications and 32 lab procedures."

From my own standpoint, the most interesting insights that we can come away with are that we weren't able to find any racial favoritism amongst the patients, the cardiology department had by far the highest amount of admitted patients and that we were able to find a strong correlation between the number of lab procedures done and length of time spent for our patients in the hospital.

I didn't know much about our patients going into this dataset, but now I have a much firmer understanding of them thanks to this brief analysis! I'll stop here for now, but I'd definitely like to jump back into this dataset sometime in the near future.

Thank you so much for your time and reading all of this! This was an absolute pleasure to do and if you have any questions, please comment below or please contact me at lance.inimgba@gmail.com or on [LinkedIn](https://www.linkedin.com/in/lance-inimgba-65a23a50/)!

I'm actively looking for new opportunities in the data science field, so please don't hesitate to contact me if you know of anything out there!







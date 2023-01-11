## Massachusetts School Project

<img src="images/Massachusetts Education Project.png?raw=true"/>

In this project, I will be assuming the role of a new hire on the Massachusetts Department of Education data team. I've been asked with doing the following:
  - A report to show the school board the state of the school system 
  - How does class size affect college admission?
  - What are the top math schools in the state?
  - What schools are struggling he most?

This project is something that hits somewhat close to me since I also worked as an educator overseas. Therefore, I was quite curious in the contents of this dataset and the relationships between the columns that could possibly be discovered.

This time, I'll be using Tableau to work with our already cleaned dataset and will provide the answer the questions that I've been assigned to uncover. Stay tuned!

### Data Analysis

Now we're going to look at our data and begin our analysis of it by answering one of the questions that we are were assigned:

#### What schools are struggling the most?

To answer this question we'll need to look at the "% Graduated" column and organize our rows by the "School Name". Since we know that only the high schools will have non-null values in this column, we then filter out the null values and sort the values in ascending order. We'll just include the bottom 10 high schools in our analysis. These schools will be highlighted by the blue rectangle in the image below.

<img src="images/LowGrad1.png?raw=true"/>

Looking at our selection of schools, since the "% Graduated" column denotes the graduation rate percentage for a given school, we can probably conclude that some of these schools are worth taking a closer look as the values. Upon looking up these schools on Google, the vast majority of these schools are alternative charter schools or low-income schools and in my opinion, shouldn't be viewed with the same lenses as a traditional public high schools. To account for thesese possible misleading red flags I decided to filter the above output by the "TOTAL Enrollment" column and set so that "TOTAL Enrollment" was equal or greater than 200 students. This was the result as displayed below:

<img src="images/LowGradRev.png?raw=true"/>

While it's not perfect, I think it portrays a somewhat more realistic picture than our first display. But in a real job setting, I think that it would be wise to communicate closely with officials in the DoE as well as individual school administration staff, so that we actually ensure that we're choosing the right schools when determining which schools are "struggling" the most.




Be sure to follow *The Interesting Project Template* as shown in [**The Data Science Project Studio**](https://www.datacareerjumpstart.com/products/the-data-science-project-studio/categories/2150357707/posts/2158441592). 

### 1. You can have sections and text.

Just like this. And you can even add internal coding blocks

```python
print('this is the python code I used to solve this problem')
```

### 2. You can add any images you'd like. 

<img src="images/dummy_thumbnail.jpg?raw=true"/>



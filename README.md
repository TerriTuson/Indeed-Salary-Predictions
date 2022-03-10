# Indeed-Salary-Predictions

Project 4 at General Assembly's London Data Science Immersive.  

We were asked to use web scraping to collect data from Indeed to address the question: You're working as a data scientist for a contracting firm that's rapidly expanding. Now that they have their most valuable employee (you!), they need to leverage data to win more contracts. Your firm offers technology and scientific solutions and wants to be competitive in the hiring market. Your principal wants you to determine the industry factors that are most important in predicting the salary amounts for these data.

### Scraping

Scraping was done using Beautiful Soup and requests libraries and information scraped included: 
job title, summary, location, company name and salary. 

Locations included major cities in the UK, and job titles included Data Scientist and Data Analyst.

### Cleaning

Initially there were a lot of duplicates and null values, especially in the salary category, and these were dropped. 

Salaries were edited to make sure that they were consistent throughout, for example all being provided as a yearly figure. 

Regex was used to ensure that the text of the cities were easier to parse in the modelling phase. 

# EDA

CountVectorizer and TfidfVectorizer were employed to better understand the text in the summary paragraph.

### Modelling

As a classification model to predict salary as either high or low, the first port of call was to convert the salary into one of these two categories. I chose to convert them via the median figure. 

Modelling was initially undertaken with just location as a feature variable to understand whether the location had an effect on the salary. Surprise, surprise, London had the most effect, giving a 38% increase.

More features were then added to the model, which also increased the result - the best estimator on the mean cross validated training score increased to 75.4 compared to the original logistic regression score of 60.75 and a baseline accuracy of 52.89.

Features that made a specific difference primarily included the type of role e.g. analyst and the level of the role e.g. manager. 

<img width="954" alt="features" src="https://user-images.githubusercontent.com/93994809/157727778-c64edbd4-ada3-4d7f-8b4c-29e0e126c2e8.png">

### Model Evaluation
The second part of the project stated ‘Your boss would rather tell a client incorrectly that they would get a lower salary job than tell a client incorrectly that they would get a high salary job. Adjust one of your models to ease his mind, and explain what it is doing and any tradeoffs.’

In this way, the threshold for the predicting class was increased to 0.6. This led to more low salaries being predicted as low salary (634 vs 602) however it also led to more high salaries being predicted as low salary (299 vs 382) and the accuracy decreased to 0.67.

### Limitations

Limitations of the project include the fact that only 13 UK cities were scraped. An increase in our number of datapoints by either investigating more areas in the UK or further afield, would generate more accurate findings.
Other features were not included in our model which could have been looked at. These include the industry the job posting is in and the requirements needed for the job.

Lastly, data was only scraped over a short time period of a week, and therefore was not reflective of the UK job market as a whole. Scraping over the course of a month or a year could generate different findings.

### Risks

Risks include the fact that we only ultimately used job listings that had salary information. This may have caused a bias in our model as it may be the case that job listing without salary information incur a higher or lower salary distribution.

Secondly, using the median for our threshold of low versus high salary may not have been the most appropriate, especially as the boss was worried about telling clients they were going to receive a high salary when they were not. A more appropriate approach may have been to divide the salaries into the 25% quartile and 75% quartile range, where 25% of the salaries are defined as high and 75% of the salaries are defined as low.

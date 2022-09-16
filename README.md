Travis County Graduates and Their Affluence 

Project Intro
Our interest is in the field of education.  Success of an educational institution is frequently measured by the graduation rate of their students. Success of an individual student can be affected by multiple factors including access to certain resources that higher incomes can provide. We are interested in exploring the relationship between income and graduation rates in Travis County, Texas. 

Group Members 
•	Sierra Gomez
•	Sierra Quevedo 
•	Austin Calvo

Technologies/Languages Used 
•	Python
•	HTML
•	BeautifulSoup
•	WebDriver
•	SQL
•	Pandas

Questions we’ll ask of the Data:
1.Are higher income zip codes more likely to have higher graduation rates? 
2.What is the median income and median graduation rate for Travis county?
3. What is the difference in percentage between the 1st and last quartile graduation rates?


Project Report - ETL
 
Extract:

Sources of Data:
1.	Publisher data.austintexas.gov. (2022, June 2). Travis County 4-year high school graduation rates by campus. Catalog. Retrieved September 12, 2022, from https://catalog.data.gov/dataset/travis-county-4-year-high-school-graduation-rates-by-campus-b2c05 
This data was collected via CSV file. The dataset source is originally from Texas Education agency (TEA) which is a state agency that oversees education in Texas, and found on Data.Gov. This dataset was collected over 4 years, annually (2016-2019). The data set includes ~40 schools in Travis County with 28 columns including details regarding their location, type of school, district, graduation rate, and graduation rate broken down by ethnicities and sex of their students. This dataset was chosen due to having a large amount of details regarding each high school in our target county being looked into. The data was extracted from the website via CSV file. 

2.	Travis County Demographics. Point2. (n.d.). Retrieved September 12, 2022, from https://www.point2homes.com/US/Neighborhood/TX/Travis-County-Demographics.html#MedianIncomeByZipcode 
This data was collected via webscraping. The dataset sources is originally gathered from the U.S Census Bureau release, found on Point2Homes.come. This dataset displayed a table titled “What is the median and average household income in Travis County by zipcode?” It included a table with 5 columns including ZipCode, Population of that ZipCode, Number of Households, Median Income, and Average Income of 54 ZipCodes in Travis County. This dataset was chosen due to it having financial information regarding our target county we were looking into. The data table was extracted via webscraping using BeautifulSoup.  

Transform:
For the income demographic dataset, after being scraped, it was transformed into a Pandas DataFrame. 3 columns (Zip Codes, Median Income, and Average Income) were kept. The other 2 columns regarding the population size and number of households in each zip code were deleted as those details are not relevant to the main relationship we are analyzing. A row was dropped in which the median income and average income of that ZipCode was reported as $0.00. The Pandas DataFrame was then converted and exported as a CSV file. We then created a table in pgAdmin and imported the CSV file. From here, we created a new table with just the 3 columns from this dataset that we deemed necessary.

Since our demographic dataset was from 2020, we decided that it would be advantageous to use only 2019 data because this would most closely match. For this analysis we were focused on graduation rates regarding income levels. This meant that there were many columns in the education dataset that were not relevant. In all, we pared the data down from 29 columns to the 7 that we thought would be essential to this analysis. We deleted all columns in regarding graduation rate by ethnicities and sex. To do this, we created a table in pgAdmin and imported the CSV file. From here, we created a new table with just the columns that we deemed necessary and filtered out all rows that were not from the year 2019. At this point the data was ready to be joined on Zip Code with our demographic set.

Load: 
Type of Final Production Database: Relational Database. Out final data is stored in a SQL database. 
The advantages of a non-relational database are vertical scalability, dynamic schema flexibility and the ability handle large amounts of unstructured data. However, we knew that our ending dataset would be small and simple, so that level of complexity would be unnecessary. It is for these reasons that we chose to load our data into a relational database.

The two datasets were joined on the Zip Code column to ensure only the Travis County Zip Codes that had both graduation data and income data were including in the final dataset to prepare for the analyzation of this data. 
At first glance with the joined table, a large income disparity between Zip Codes was seen (~140k difference between the lowest and highest reported income) This shows there is a large economic inequality throughout Travis County. In addition, the graduation data set also had a large disparity between the highest and lowest graduation rates (~50%). This shows there is a large educational inequality between zip codes. We hypothesize the correlation between higher graduation rates and higher income will be statistically significant. 

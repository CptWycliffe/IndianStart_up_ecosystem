#**Introduction**
While it's reported that only 1 in every five startup businesses fail within the first year, the situation in India is not any different. A recent study of the Indian startup economy indicated that whereas India has 105 unicorn startups, surprisingly only 23 of them are profitable. 
This shocking trend is compounded by the fact that only 10% of Indian startups live to see their 5th anniversary, thereby sinking in billions in funding from venture capitalists and investment firms around the world.

It's therefore imperative that Venture Capitalists make a number of considerations before committing resources in any startup venture. 

This project aims to explore and gain insight into the Indian startup funding ecosystem through an in-depth data analysis. We will try to understand the venture capital funding trends as observed in the year 2018-to-2021. Some of the factors we will consider are; 

- The Location/headquarters of the Business startup
- The Sector/Industry of the business venture
- The Startup year
- The stage at which the business is in when seeking funding

The Null hypothesis in this projects suggests that Indian Start-ups in the technology industry are likely to receive funding. The alternative hypothesis argues that no factor will affect the probability or amount of funding received by an Indian start-up.

To understand these factors, we will research on the following questions:

1. What are the top five startup-sectors which are investor's favorites'?
2. Can the success of obtaining finance from investors be impacted by location?
3. Which stages receives more investment from investors for start-ups?
4. What Sectors have the maximum amount of funding?
5. What is the total amount of funds each year?

##***Data Handling***
Using python scripts, we will explore four datasets with information about Indian startups funding for the years, 2018,2019,2020 and 2021. 
We will go through the following processes in a bid to validate out hypothesis 

- Load our data
- Process each dataset
- Merge the datasets 
- Evaluate the data using univariate and multivariate analysis 
- Visualize our findings 
- Draw a conclusion
 
First we will import the libraries that will enable us analyze the data. These libraries include 
pandas and NumPy: for data manipulation
seaborn and matplotlib: for visualization

```
# Data handling
import pandas as pd
import numpy as np

# Vizualisation (Matplotlib, Plotly, Seaborn, etc. )
import matplotlib.pyplot as plt
import seaborn as sns
import re

# Other packages
import os
```
##Data Loading
Using pandas.read_csv, we can load all our four datasets and be able to read the .csv files. 

```
# For CSV, use pandas.read_csv to import the data files
data_2018 = pd.read_csv('startup_funding2018.csv')
data_2019 = pd.read_csv('startup_funding2019.csv')
data_2020 = pd.read_csv('startup_funding2020.csv')
data_2021 = pd.read_csv('startup_funding2021.csv')
```

#Data Processing 
In this section, we will explore each dataset separately. We will undertake three main tasks i.e

- Understand the data contained in them
- Identify the issues with the data
- Determine how to handle each of the issues identified 
To do this we will use the code:

data.columns - To see what columns are contained in the data set 
data.head() - to preview the data contained in the dataset
data.info() - to get a summary of data in each column
pandas.isnull() - to check for the null values in each column 

##Processing 2018 Dataset

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p0q6kd84xmiimrikqke4.jpg)

**_From the above, we notice the following_**
-The amount columns contains different currencies as well as cells with "-"
-The Industry columns is described using more than one phrase
-The Location is described using more than one physical address.

**To clean these;** 
_We will assume the Amounts without any signs are in dollars; thus convert the values in INP to USD and replace "-" with NaN._
_Split and pick the first part of the phrase to describe the physical address/headquarter._
_Pick only one phrase to describe the industry._

## Processing 2019 - 2021 Datasets
By repeating the process with the other datasets, we make the following observations 

###  Observations from previewing the datasets
**The 2018 DataFrame**
- The columns in 2018 are different from those of 2019 - 2021, meaning they have to be renamed for concatenation.
- The amounts in the 2018 DataFrame are a mix of Indian Rupees (INR) and US Dollars (USD), meaning they have to be converted into same currency.
- The industry and location columns have multiple information. A decision is to be made between selecting the first value before the separator(,) as the main value.

**The 2019 DataFrame**
- The datatype of the "Founded" column is set to float64. It should be set to a string for uniformity.
- The headquarter column has multiple information. A decision is to be made between selecting the first value before the separator(,) as the main value.

**The 2020 DataFrame**
- There is an extra column called "Unnamed:9", giving it a total of 10 columns. It should be dropped to ensure complete alignment with the other DataFrames for ease of concatenation.

**The 2021 DataFrame**
- The datatype of the "Founded" column is set to float64. It should be set to a string for uniformity.
- There are some cells that have null values, "Amount" has 3 null cells

**General Observations**
- The currency signs and comma separator have to be removed from each of amount column for each DataFrame to allow numerical manipulation and analysis.

- The 2022 average INR/USD rate will be used to convert the Indian Rupee values to US Dollars in the 2018 DataFrame.
- First values of industry and location in the 2018 data will be selected as the primary sector and headquarters respectively.
- Amounts without currency symbols are assumed to be in USD ($)
- Financial analysis will be narrowed to transactions whose amounts are available in the loaded data

##Merging the Datasets

Once the cleaning of the data is completed, we combine all the four .csv files into one dataframe using the pandas.concat() syntax as demonstrated below. We can also view a summary of the new dataset contents as seen

```
#Joining all the four files using concatenate
data = pd.concat([data_2018,data_2019,data_2020,data_2021])

#Preview a summary of the data in the new combined file 
data.info()
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/or4txy8rpzkyb6jidss3.jpg)


You can view more [Visualization of the findings here.](https://azubiafrica-my.sharepoint.com/:u:/g/personal/wycliffe_omondi_azubiafrica_org/EcYf9kq8OylHuBxXU2tTjLcBqADv6qLZjASA3NV0H9drOQ?e=vk0xZH)

By conducting multivariate analysis on the combined dataset, we are able to answer the research questions and put our findings on the visualization as shown. 

What are the top five startup-sectors which are investor's favorites'?

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v6vpxtd7czaqe79aei0k.jpg)


Can the success of obtaining finance from investors be impacted by location?

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/drtsyhw6kua37g7kaau9.jpg)

Which stages receives more investment from investors for start-ups?

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4tr4tk3oxodj9ielyq7c.jpg)


What Sectors have the maximum amount of funding?

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ovjma7t95j3iqw7xiedp.jpg)

What is the total amount of funds each year?

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/s475sdv4u54srknrw59w.jpg)


Exploring the Indian Startup funding provides insight into the vibrant and ever-growing venture capitalist ecosystem. From this analysis, we gain a better understanding of the characteristics associated with Indian startups.
We are able to draw the following observations;
_The Top sectors that are favorites' to investors are in FinTech and EdTech_¶
_The highest Amount received by a start-up are also in the FinTech and EdTech sectors_
_The startup with the highest amount of funding is also in the Edtech industry._ 

We can therefore affirm the null hypothesis; **_Indian Startups in the technology industry are likely to receive funding._**

 If you're interested in exploring this project further, please check out my [GitHub](https://github.com/CptWycliffe/IndianStart_up_ecosystem) repository for more information, suggestions and input.

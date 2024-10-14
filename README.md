 ## Project Title
 Analysis of Google Play Store Apps: Insights into Ratings, Downloads, and App Performance

### 1. Objective
The primary goal of this project is to analyze Google Play Store app data to identify key factors that influence app performance, including downloads, ratings, revenue, and user engagement. This analysis will provide insights into app market dynamics, helping developers, marketers, and stakeholders optimize app design, pricing, and marketing strategies.

### 2. Scope of Work
The project will focus on key performance metrics such as:

- App Downloads
- User Ratings
- Category-wise Analysis
- Pricing Model
- Content Rating
- Size of the App
- Sentiment Analysis of User Reviews
- Impact of Updates

### 3. Data Source
Google Play Store Dataset: A publicly available dataset from [kaggle](https://www.kaggle.com) with features such as app name, category, rating, reviews, size, installs, type (free/paid), price, content rating, genres, last update, and current version. [Download here](https://www.kaggle.com/datasets/gauthamp10/google-playstore-apps)


### 4. Tools and Technologies
- Programming Language: Python for data manipulation and analysis.
- Libraries:
Pandas: For data manipulation and cleaning.
Matplotlib/Seaborn: For visualizations.
- Jupyter Notebooks: For documentation and step-by-step analysis.

### 5. Problem Statements
- What factors influence the number of downloads for apps across different categories?
- How do app size and update frequency affect user ratings and reviews?
- What trends can be observed from the sentiment analysis of user reviews?
- How does the pricing model (free, paid) impact the performance and revenue of apps?
- What categories show the highest user engagement, and what characteristics contribute to this success?


### 6. Data Collection and Preprocessing

- ### Data Collection
The dataset utilized for this analysis has been sourced from Kaggle, a prominent platform for data science and machine learning resources. Below is a preview of the dataset,

![Google Play Store Raw Data .img](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Excel%20Data/Data%20Excel%20ss.jpg)

- ### loading Data into Python:
Importing the required library
``` Python

import numpy as np
import pandas as pd
df= pd.read_csv("Google_Play_Store.csv")
df.head()

```
![df.head()](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/df.head().png)

- ### Data Cleaning and processing

Fixed null values

``` python
df = df[~df.Rating.isnull()]
```

Filling na values with average values
``` python
df["Android_Ver"] = df["Android_Ver"].fillna(df["Android_Ver"].mode()[0])
```


Converting some objects types to floating type

```python
#Reviews
df.Reviews = df.Reviews.astype("int32")

#Installs
df.Installs = df["Installs"].str.replace(",", "").str.replace("+", "").astype("int")

#Price
df.Price = df.Price.apply(lambda x : 0 if x=="0"  else float(x[1:]))
```

 Sanity Check - The reviews should be less than the no of installs
```python
df[df.Reviews > df.Installs].head()
```


### 7. Data Visualisation

Data is visualized using Matplotlib and Seaborn, two powerful Python libraries that enable the creation of comprehensive and aesthetically pleasing visual representations.

## Matplotlib
Importing the library
```python
import matplotlib.pyplot as plt
%matplotlib inline
```
### Boxplot

### 1.Boxplot of apps and prices
```python
plt.boxplot(df.Price)
plt.title("Boxplot of apps and Prices")
plt.xlabel("Apps")
plt.ylabel("Price $")
plt.show()
```
![Apps & Price](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Box%20Plot%20-%20Apps%20%26%20Price.png)

 - Apps having price less then 50$
```python
df = df[df.Price < 50]
```

![plt.show](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Box%20Plot%20-%20Price%20less%20than%2050.png)

### Histogram

### 2. Histogram for the reviews
```python
plt.hist(df.Reviews)
plt.title("Histogram for the reviews.")
plt.xlabel("Reviews")
plt.ylabel("No of Apps")
plt.show
```
![Reviews](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Hist%20-Reviews.png)

### 3. Histogram for the size
```python
plt.hist(df.Size)
plt.title("Histogram for the size.")
plt.xlabel("Size")
plt.ylabel("No of Apps")
plt.show
plt.show
```
![Size](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Hist%20-%20Size.png)


### 4. Distribution for Rating
```python
df.Rating.plot.hist()
plt.title("Distribution of Rating")
plt.xlabel("Ratings")
plt.ylabel("No of Apps")
plt.show()
```
![Rating](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Hist%20-%20Rating.png)


## Seaborn
Importing the library
``` python
import seaborn as sns
```
### Bar Chart

### 1. Bar Chart of Content Rating Distribution
```python
df["Content_Rating"].value_counts().plot.barh()
plt.title("Content Rating Distribution")
plt.xlabel("Installs")
plt.ylabel("Category")
plt.show()
```
![Content Rating Distribution](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Bar%20-%20Content%20Rating.png)

### 2. Android Version Distribution
```python
df["Android_Ver"].value_counts().plot.bar()
plt.title("Android Version Distribution")
plt.xlabel("Version")
plt.ylabel("No of Apps")
plt.show()
```
![Android Version](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Bar-%20Android%20ver.png)

### Scatter Plot

### 3. Size Rating Distribution
```python
plt.scatter(df.Size, df.Rating)
plt.title("Size-Rating Distribution")
plt.xlabel("Size")
plt.ylabel("Rating")
plt.show()
```
![Size & Rating](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Sea%20-%20Size%20Rating.png)

### Joint Plot

### 4. Joint plot of Size & Rtaing
```python
sns.jointplot(x="Size", y="Rating", data=df)
plt.show()
```
![Joint - Size & Rating](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Joint%20-%20Size%20%26%20Rating.png)


### Reg Plot

### 5. Reg Plot of Price & Rating
```python
sns.regplot(x="Price", y='Rating', data=df)
plt.show()
```
![Price & Rating](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Reg%20-%20Price%20%26%20Rating.png)

### Pair Plot

### 6. Pair Plot of Review, Size, Rating & Price
```python
sns.pairplot(df[["Reviews", "Size", "Rating", "Price"]])
plt.show()
```
![Pair Plot](https://github.com/itsmanishjoshi/Google_Play_Store-Analysis/blob/main/Python/ScreenShots/Pair%20Plot.png)

# Seaborn and Linear Regression Analysis
# Question: Do higher film budgets lead to more box office revenue?
# Dataset scraped from the-numbers.com on May 1st, 2018.

import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

# Read the Data
data = pd.read_csv('cost_revenue_dirty.csv')

# 1. Explore and Clean the Data
#    - Check the number of rows and columns
#    - Check for NaN values
#    - Check for duplicate rows
#    - Identify data types of each column
print(data.shape)  # Shape of the data
print(data.head())  # Display first few rows
print(data.info())  # Data types and missing values
print(data.isna().values.any())  # Any missing values?
duplicated_rows = data[data.duplicated()]
print(f'Number of duplicated rows: {len(duplicated_rows)}')

# 2. Data Type Conversions
#    - Remove '$' signs and commas from the budget and revenue columns
#    - Convert the `Release_Date` column to datetime format
chars_to_remove = [" ", ',', '$']
columns_to_clean = ['USD_Production_Budget', 'USD_Worldwide_Gross', 'USD_Domestic_Gross']

for col in columns_to_clean:
    for char in chars_to_remove:
        data[col] = data[col].astype(str).str.replace(char, "")
    data[col] = pd.to_numeric(data[col])

data['Release_Date'] = pd.to_datetime(data['Release_Date'])

# 3. Descriptive Statistics
#    - Calculate the average production budget
#    - Find the minimum and maximum revenues
#    - Check profitability of the bottom 25% of films
print(data.describe())

# 4. Investigating Zero Revenue Films
#    - Count films that grossed $0 domestically
#    - Count films that grossed $0 worldwide
zero_domestic = data[data.USD_Domestic_Gross == 0]
print(f'Number of films that grossed $0 domestically: {len(zero_domestic)}')
print(zero_domestic.sort_values('USD_Production_Budget', ascending=False))

zero_worldwide = data[data.USD_Worldwide_Gross == 0]
print(f'Number of films that grossed $0 worldwide: {len(zero_worldwide)}')
print(zero_worldwide.sort_values('USD_Production_Budget', ascending=False))

# 5. Filter on Multiple Conditions
#    - Find films that grossed $0 domestically but had some international revenue
international_releases = data.query('USD_Domestic_Gross == 0 and USD_Worldwide_Gross != 0')
print(f'Number of international releases: {len(international_releases)}')

# 6. Unreleased Films
#    - Identify films not released as of May 1st, 2018
#    - Create a clean dataset without these unreleased films
scrape_date = pd.Timestamp('2018-5-1')
not_released = data.query('Release_Date >= @scrape_date')
print(f'Number of movies not released within {scrape_date}: {len(not_released)}')
data_clean = data.drop(not_released.index)

# 7. Films that Lost Money
#    - Calculate the percentage of films where production costs exceeded worldwide gross revenue
loss = data_clean[data_clean.USD_Worldwide_Gross < data_clean.USD_Production_Budget]
percentage_of_movie_in_loss = (len(loss) / len(data_clean)) * 100
print(f'Percentage of films that lost money: {percentage_of_movie_in_loss:.2f}%')

# 8. Visualization with Seaborn: Budget vs Revenue
#    - Scatter plot: USD Production Budget vs Worldwide Gross Revenue
plt.figure(figsize=(8, 4), dpi=200)
ax = sns.scatterplot(data=data_clean,
                     x='USD_Production_Budget',
                     y='USD_Worldwide_Gross')
ax.set(ylim=(0, 3000000000),
       xlim=(0, 450000000),
       ylabel='Revenue in $ billions',
       xlabel='Budget in $100 millions')
plt.show()

# 9. Release Date vs Budget Bubble Chart
#    - Visualize the relationship between release date and budget
plt.figure(figsize=(8, 4), dpi=200)
with sns.axes_style("darkgrid"):
    ax = sns.scatterplot(data=data_clean,
                         x='Release_Date',
                         y='USD_Production_Budget',
                         hue='USD_Worldwide_Gross',
                         size='USD_Worldwide_Gross')
    ax.set(ylim=(0, 450000000),
           xlim=(data_clean.Release_Date.min(), data_clean.Release_Date.max()),
           xlabel='Year',
           ylabel='Budget in $100 millions')
plt.show()

# 10. Converting Years to Decades
#    - Create a new column for the decade of the film's release
dt_index = pd.DatetimeIndex(data_clean.Release_Date)
years = dt_index.year
decades = years // 10 * 10
data_clean['Decade'] = decades
print(data_clean.head())

# 11. Separate Old and New Films
#    - Create two new DataFrames: old_films (before 1970) and new_films (1970 onwards)
old_films = data_clean[data_clean.Decade <= 1960]
new_films = data_clean[data_clean.Decade > 1960]
print(f'Number of films released before 1970: {len(old_films)}')

# 12. Seaborn Regression Plot: Old Films
#    - Visualize the regression line for old films
plt.figure(figsize=(8, 4), dpi=200)
with sns.axes_style("whitegrid"):
    sns.regplot(data=old_films,
                x='USD_Production_Budget',
                y='USD_Worldwide_Gross',
                scatter_kws={'alpha': 0.4},
                line_kws={'color': 'black'})
plt.show()

# 13. Seaborn Regression Plot: New Films
#    - Scatter plot and linear regression for new films
#    - Customize chart style and color
plt.figure(figsize=(8, 4), dpi=200)
with sns.axes_style("darkgrid"):
    ax = sns.regplot(data=new_films,
                     x='USD_Production_Budget',
                     y='USD_Worldwide_Gross',
                     scatter_kws={'alpha': 0.3, 'color': '#2f4b7c'},
                     line_kws={'color': '#ff7c43'})
    ax.set(ylim=(0, 3000000000),
           xlim=(0, 450000000),
           ylabel='Revenue in $ billions',
           xlabel='Budget in $100 millions')
plt.show()

# 14. Linear Regression using Scikit-Learn
#    - Fit a linear regression model on the new films
regression = LinearRegression()
X = pd.DataFrame(new_films, columns=['USD_Production_Budget'])
y = pd.DataFrame(new_films, columns=['USD_Worldwide_Gross'])
regression.fit(X, y)

#    - Output the slope and intercept
print(f'Intercept: {regression.intercept_}')
print(f'Coefficient: {regression.coef_}')
print(f'R-squared: {regression.score(X, y)}')

# 15. Prediction for a $350 million budget film
budget = 350000000
revenue_estimate = regression.intercept_[0] + regression.coef_[0, 0] * budget
revenue_estimate = round(revenue_estimate, -6)
print(f'Estimated revenue for a $350 million film: ${revenue_estimate:.10}.')

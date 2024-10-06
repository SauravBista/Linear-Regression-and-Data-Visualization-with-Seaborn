🎬 Seaborn and Linear Regression Analysis

This project investigates the relationship between movie budgets and box office revenue. Using a dataset scraped from the-numbers.com on May 1st, 2018, the analysis answers the question:

Do higher film budgets lead to more box office revenue?
📝 Project Overview

The project is built using Pandas, Seaborn, Matplotlib, and Scikit-Learn for data analysis and visualization. The dataset contains details on film production budgets, domestic and worldwide revenue, and release dates.
Key Steps:

    Data Exploration & Cleaning
        Checked for missing values and duplicates
        Cleaned currency data by removing commas and dollar signs
        Converted data types to ensure consistency

    Descriptive Statistics
        Examined trends in movie production budgets and revenue
        Analyzed profitability and zero-revenue films

    Data Visualization
        Scatter plots and bubble charts to visualize relationships between budget, revenue, and release dates
        Regression analysis for older (before 1970) and newer films (after 1970)

    Linear Regression with Scikit-Learn
        Applied linear regression on new films to predict box office revenue based on production budget
        Calculated model's accuracy with R-squared and predicted revenue for a $350M budget film

🔧 Tools & Libraries

    Python 3
    Pandas for data manipulation
    Seaborn and Matplotlib for data visualization
    Scikit-Learn for linear regression modeling

📈 Visualizations

Key visualizations include:

    Budget vs. Revenue Scatter Plot: Visualizing the relationship between production budgets and box office performance.
    Release Date vs. Budget Bubble Chart: Showing how budgets have changed over the years.
    Linear Regression Plots: For both old and new films, including regression lines to demonstrate trends in the data.

💡 Key Insights

    Films with higher production budgets tend to earn more at the box office, but the relationship is not linear across all eras.
    A significant percentage of films fail to recover their production costs, with lower-budget films being at greater risk.
    Modern films (post-1970) show a clearer correlation between budget and revenue compared to older films.

📊 Predictive Model

Using a linear regression model, we predict that a film with a $350M budget would generate around $2.78 billion in worldwide revenue.
📁 Dataset

The dataset contains the following columns:

    Release_Date: Date of the film's release.
    USD_Production_Budget: The production budget of the film in USD.
    USD_Worldwide_Gross: Worldwide box office gross in USD.
    USD_Domestic_Gross: Domestic box office gross in USD.

🚀 How to Run the Project

    Clone the repository:

    bash

git clone https://github.com/your-username/seaborn-linear-regression-analysis.git
cd seaborn-linear-regression-analysis

Install the required Python libraries:

bash

pip install -r requirements.txt

Run the Jupyter notebook or Python script to execute the analysis:

bash

    jupyter notebook analysis.ipynb
    # or
    python analysis.py

📚 Further Improvements

    Investigate additional variables like genre, cast, or critical ratings to enhance the predictive model.
    Explore advanced regression models or machine learning algorithms for better accuracy.

🔗 Links

    Dataset Source: the-numbers.com
    Python Documentation: python.org
    Seaborn Documentation: seaborn.pydata.org
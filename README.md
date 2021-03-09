# Opening a Real Estate Agency in King County/Seattle

In this project, I'm working for a Real Estate Agency firm that considers entering the King County/Downtown Seattle market. However, since they don't know the area very well, the Agency hired me to study the market.

My mission is to help them understand how houses are valued, which factors matter the most for buyers, and provide ideas/strategies for entering the market given their commission-based business model.

## Commission-based Business Model

The firm charges a commission of **5%** based on a minimum price agreed with the owner and **7%** if sold above the agreed minimum price, and _there's no reduction on commission if they sell below minimum_. `¯\_(ツ)_/¯`

For example, if they agreed with the owner to sell the house at a minimum of **_USD 1,000,000.00_** and they sold it at **_USD 1,200,000.00_** , the commission will be:

- **_USD 1,200,000.00 * 7% = USD 84,000.00_

If **_USD 1,000,000.00_**:

- **_USD 1,000,000.00 * 5% = USD 50,000.00_

Moreover, based on historical data, their agents have a **30% success rate in selling houses and 10% of selling above the minimum price.**

> **_Disclamer: I invented all of these assumptions. I have no accurate understanding of how Real Estate Agents work._**

## Goals

1. Show some insights about the market.
2. Analyze which features are the most/least valued.
3. Come up with ideas/strategies to enter the market given their commission-based business model.

## The Dataset

All the analysis will be done using the King County House Sales dataset, which contains information regarding house sales + some specifications about the sold houses.

[You can find more about it here (Kaggle)](https://www.kaggle.com/harlfoxem/housesalesprediction)
[Column Definitions here](https://github.com/renoneto/second_module_project/blob/main/data/kc_house_data_column_names.md)

## Navigation

You can find the following files/folders in my repository:

### [`Real Estate Market Analysis.ipynb`](https://github.com/renoneto/second_module_project/blob/main/Real Estate Market Analysis.ipynb)

- **Content:** Main Jupyter Notebook with the whole analysis.

- **What I'm doing:**

1. Dataset Exploration and Cleaning.
2. Asking Questions to understand the Housing Market.
3. Running Revenue Simulations given the Business Model, trying to find the best combination of No. of Agents and Zip Codes that will increase Net Income/ROI.
4. Creating a Linear Regression Model to predict the Sale Price of Houses.
5. Analyzing the final model, understanding the weights given to each feature.
6. Presenting Conclusions/Recommendations.

### [`presentation.pdf`](https://github.com/renoneto/second_module_project/blob/main/presentation.pdf)

- **Content:** Non-technical presentation to stakeholders talking about the approach and recommendations.

## Market Insights

Given the Business Problem and Goals, I decided to start the analysis by exploring the dataset, trying to understand and get some insights about the market.

The questions and the Business-Context for each are the following:

**When were houses built? Is the Number of New Houses growing over time?**
> **Business Context:**
> A good sign of a Healthy Market would be to see the No. of New Houses growing over the years. I assume that in a declining region, with not jobs/companies, people would likely move to different regions instead of building new houses. New houses could mean:
>
> - High demand: more people are moving to Seattle, because the good job market.
> - Residents are building new houses: residents are looking for new houses, and they end up building their own.
>
> Either way, it would be good to look at an upward trend if you are a Real Estate Agency firm. Nobody would like to sell houses in a region with no buyers.

**What's the impact of `date` in `price`? Have prices changed over time?**
> **Business Context:**
> A Real Estate Agency would not enter a market where houses are losing value (_unless they know something that nobody knows, of course_). Growing prices would be a good indication of a healthy real estate market.

**What's the importance of Zipcode and Coordinates in `price`?**
> **Business Context:**
> It's essential for the Agency to understand which regions have higher prices and if there's something specific to the area that justifies that price difference.
>
> This information might help the company to decide in which regions to focus on/allocate more resources. Of course, `price` is not the only data point relevant to this question. However, it would be an important one.

**Is the dataset evenly distributed in terms of houses by Zip Code?**
> **Business Context:**
> It would not be entirely wrong to imply that certain Zip Codes sell more than others, and given that I'm looking at a dataset of sold houses, I can check if my hypothesis is correct.
>
>  Even though I might not necessarily know the reason for that. It's important for the Agency to consider that when allocating agents to Zip Codes/Regions.

**What's the Average Sold Price by Zip Code?**
> **Business Context:**
> Again, following the same logic that the Agency would allocate Agents based on Price/Demand, it would be interesting to see many sold houses in areas where the average price is high.

**What's the Total Sold by Zip Code?**
> **Business Context:**
> By Summing the Sold Price of all houses by Zip Code, I can identify which Zip Codes sell more in Absolute Value. In other words, the total amount of dollars sold in houses, which does not translate to actual revenue. However, it can be an excellent metric to analyze.

**Would the distance from Downtown Seattle be a good proxy for coordinates and Zip Code?**
> **Business Context:**
> Just like Zip Code, the distance from Downtown Seattle might be a good way to choose which Houses to sell.

## Revenue Simulation

After exploring the dataset, I'm running simulations built on top of assumptions about the Market Size + Costs + Agent Conversion Rate + Zip Codes.

The outcome is questionable since I don't have all the inputs necessary to build such model. However, the goal is to show some recommendations and, in a real-world scenario, I'd work closely with stakeholders to understand all variables and constraints.

The steps taken were the following:

1. **Define Average Success Rate by Agent:** % Success Rate on selling houses by Agent = Sold Houses / Listings, by Agent.
2. **Remove Outliers:** I found that some houses are outliers, and were negatively impacting the outcomes.
3. **Define the Housing Market Size:** To effectively calculate the No. of Sold Houses, I need to consider all Listed Houses that were not sold. Therefore, I'm estimating the Market Size based on the Success Rate by Rate and assuming that the dataset is representative of the whole market.
4. **Run Simulations and estimate Revenue:**
    1. Define No. of Houses Agents will manage per year.
    2. Total No. of Listings and Sold Houses.
    3. Simulate Sales on Different Pairs of Zip Code.
5. **Impact of No. of Agents in Net Income in Top 5 Most Profitable Zip Codes:** Based on the results above, I take the Most Profitable Zip Codes and run simulations using different No. of Agents. The goal is to find the best combination of Zip Code + No. of Agents.
6. **Analyze results in different scenarios:** Given the results of the simulations, I find the best combination.
## Linear Regression Model to estimate Sold Price

As the last step of the project, I'm creating a Linear Regression Model to predict the Sold Price.

One of the benefits of such model is the interpretability of the coefficients. Each feature will have a different weight and signal. Therefore, it's possible to compare the impact on price by adding/removing one unit of a feature.

With that information, the Agency can focus on features that matter to buyers. Moreoever, it's a way to understand the market as well, which will help them to decide the best Houses to sell.

The following steps were taken during the process:

**1. Feature Transformation:**
    - Deal with null values and boolean fields
    - Create new features/Feature Engineering
    - Reduce bias in model towards Zip Codes with more records by oversampling
    - One-Hot Encoding of Features
    - Percentage of Zero/Null in Variables
    - Check for Normality of continuous variables
    - Feature Scaling: Z-Score

**2. Model Training**
    - Build Baseline Model
    - Remove features where p-value > 0.05
    - Look at QQ Plot and Scatter Plot of Residuals
    - Deal with outliers
    - Investigate Multicolinearity
    - Final Model Performance Analaysis

**3. Model Interpretation**

## Conclusions

**1. Relative Healthy Market:** Based on the growing number of Newer Sold Houses, it's possible to say that people are investing in the Real Estate Market. If there was no interest in the area, the data would show older sold houses. However, the Average Built Year is 1970, and it's possible to see an upward trend. <br> Probably there are healthier markets out there, but I'd have to compare Seattle with other places.

**2. Houses near Downtown Seattle and Washington Lake have higher prices:** Based on the price of sold houses and the coordinates, it's easy to see which areas are the most expensive. <br> It might be of interest of the Agency to focus on luxury/expensive houses, so it's useful information.

**3. 'Zip Code' is the most impactful feature:** After analyzing all features, the conclusion is that _Zip Code_ has a significant impact on the price. Therefore, for an Agency, a good strategy could be to define the market they will operate based on the Zip Code.

**4. Putting the Zip Code on the side, Waterfront and Square Footage add more value to a house:** Whether a house has a Waterfront is the most price-relevant feature after Zip Code. Houses with a Waterfront adds 177,850 dollars to the price. In second place comes the Square Footage, with 32 dollars added per unit.

**5. Distance from Downtown Seattle and Houses with Three Floors are the features that most reduce value:** On the other end of the spectrum, the farthest a house is from Downtown Seattle, the lower its price will be. More specifically, 1,520 dollars per kilometer. Moreover, interestingly, houses with Three Floors have their price reduced by 43,279 dollars.

**6. After running simulations on different Numbers of Agents and Combinations of Zip Codes, the most profitable solution was 25 Agents selling 98004 Houses:** Given the business model and some assumptions, I found the best combination of Zip Codes and No. of Agents. <br> Moreover, I was able to find which Zip Codes tend to bring higher revenue numbers: 98004, 98040, 98112, 98039, and 98006.

**7. Rethink the Business Model:** After running the simulations, I realized that the Return on Investment was pretty low relative to the risk that investors were taking. Therefore, another suggestion would be to rethink the business model and optimize it.
## Next Steps

**The Simulation Machine:** Given the results achieved after running simulations, one of my concerns was that my assumptions were entirely wrong or the business model doesn't make sense. However, the exercise of creating this 'simulation machine' is the main goal here. <br> The idea is to show how to take a data-driven approach to make strategic decisions. Ideally, I'd work directly with stakeholders to make sure that assumptions are realistic, and I'm taking into consideration all inputs in my model. <br> Besides that, I'd like to test different scenarios. As I said before, it's hard to analyze something without business understanding. Maybe the strategy is to focus on Luxury houses, or maybe there's a funding limit, or perhaps the business-owner already has a team with 30 Agents. Without that information, the model becomes too generalistic and maybe not realistic.

**Gather more data on houses that were not sold:** The dataset contains only successful cases, or sold homes. I'd also like to understand if there's some pattern in houses that did not sell. Maybe certain features make it harder to sell a house.

**Create different models for each Zip Code:** To achieve higher accuracy, a good idea would be to create one model for each Zip Code. That would bring a more granular understanding of the most/least valuable features within Zip Codes.

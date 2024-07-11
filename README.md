# Zomato Dataset Analysis

Practice Analysis on Zomato Dataset, which entails data from hotels and the services they offer from all over the world.

### Project Overview

The Zomato Data Analysis project aims to provide actionable insights for restaurant owners, food enthusiasts, and potential business partners by analyzing a comprehensive dataset obtained from Zomato. The analysis addresses various aspects of restaurant performance, customer preferences, and strategic business decisions. Key objectives include identifying high-performing restaurant categories, understanding customer engagement, and exploring cost factors across different locations and cuisines.

### Data Sources

The primary dataset used in this project was sourced from Zomato, a leading online food delivery platform. The dataset includes information about restaurants, their locations, cuisines, cost for two, ratings, votes, and facilities such as table booking and online delivery. The data was accessed via the Zomato API and comprises 9551 entries with 21 attributes.

### Tools

The following tools and libraries were utilized for data analysis and visualization:
- **Python**: The core programming language used for data manipulation and analysis.
- **Pandas**: For data cleaning, preparation, and analysis.
- **NumPy**: For numerical operations.
- **Matplotlib and Seaborn**: For data visualization and plotting.
- **SciPy**: For statistical analysis and hypothesis testing.
- **Jupyter Notebooks**: As the interactive development environment for writing and running code, as well as documenting the analysis process.

### Data Cleaning and preparation

Data cleaning and preparation were critical steps to ensure the accuracy and reliability of the analysis. The following actions were taken:

1. Handling missing Values
   - The Cuisines column had 9 missing values, which were filled with the placeholder "Unknown".
   ```python
   df['Cuisines'].fillna('Unknown', inplace=True)
   ```
2. Removing Duplicates
   - The dataset was checked for duplicate entries, and any found duplicates were removed.
   ```python
   df = df.drop_duplicates()
   ``` 
3. Data Type Conversion
   - Ensured that all columns had appropriate data types for analysis.
   ```python
   df['Average Cost for two'] = df['Average Cost for two'].astype(int)
   ```

### Exploratory Data Analysis
   
Exploratory Data Analysis (EDA) was conducted to uncover patterns, trends, and relationships within the data. Key findings included:
1. Average Ratings
   - Restaurants with table booking and online delivery facilities had higher average ratings compared to those without these facilities.
   ```python
   avg_rating_with_table_booking = df[df['Has Table booking'] == 'Yes']['Aggregate rating'].mean()
   avg_rating_with_online_delivery = df[df['Has Online delivery'] == 'Yes']['Aggregate rating'].mean()
   ```
2. Restaurant Categories and Costs
   - Identified cuisines that were more expensive or cheaper on average.
   ```python
   average_cost_by_category = df.groupby('Cuisines')['Average Cost for two'].mean().reset_index()
   ```
3. Location and Votes
   - Analyzed the distribution of votes across different locations and their correlation with the number of restaurants.
     ```python
     total_votes = df.groupby('City')['Votes'].sum().reset_index()
     num_restaurants = df.groupby('City')['Restaurant ID'].nunique().reset_index()
     votes_and_restaurants = pd.merge(total_votes, num_restaurants, on='City')
     votes_and_restaurants['Votes per Restaurant'] = votes_and_restaurants['Total Votes'] / votes_and_restaurants['Number of Restaurants']
     ```
4. High Rating Cuisines
   - Identified cuisines that received the most positive ratings.
     ```python
     average_rating_by_cuisine = df.groupby('Cuisines')['Aggregate rating'].mean().reset_index()
     ```
5. Impact of Social Activities
   - Assessed the impact of social activities (using table booking as a proxy) on restaurant ratings.
     ```python
     avg_rating_with_social = df[df['Has Table booking'] == 'Yes']['Aggregate rating'].mean()
     avg_rating_without_social = df[df['Has Table booking'] == 'No']['Aggregate rating'].mean()
     ```

**Visualizations**

Visualizations were created to enhance understanding and communication of the analysis:
1. Box plot
   ```python
   plt.figure(figsize=(10, 6))
   sns.boxplot(x='Has Table booking', y='Aggregate rating', data=df)
   plt.title('Distribution of Ratings for Restaurants with and without Social Activities')
   plt.xlabel('Has Table Booking Facility')
   plt.ylabel('Aggregate Rating')
   plt.show()
   ```
2. Box Plot
   ```python
   plt.figure(figsize=(10, 6))
   sns.barplot(x='Both Facilities', y='Aggregate rating', hue='Both Facilities', palette='rocket', data=average_ratings, dodge=False)
   plt.title('Average Ratings for Restaurants with and without Both Facilities')
   plt.xlabel('Has Both Online Delivery and Table Booking Facilities')
   plt.ylabel('Average Aggregate Rating')
   plt.legend().set_visible(False)
   plt.show()
   ```

**Hypothesis Testing**

Hypothesis tests were conducted to validate key assumptions:
1. Hypothesis 1: Restaurants with Online Order and Table Booking Perform Better:
   ```python
   t_stat, p_value = ttest_ind(
    df[df['Both Facilities'] == 'Yes']['Aggregate rating'],
    df[df['Both Facilities'] == 'No']['Aggregate rating'],
    equal_var=False
   )
   ```


   
2. Hypothesis 2: Restaurants with Social Activities are Rated More Positively:
   ```python
   t_stat_social, p_value_social = ttest_ind(
    df[df['Has Table booking'] == 'Yes']['Aggregate rating'],
    df[df['Has Table booking'] == 'No']['Aggregate rating'],
    equal_var=False
   )
   ```

### Results/Findings

- **Higher Ratings with Facilities**: Restaurants offering both online order and table booking facilities tend to receive higher average ratings compared to those without these features.

- **Expensive and Affordable Cuisines**: Fine dining and specialty cuisines are more expensive on average, while fast-food and common cuisines are cheaper.

- **Customer Engagement**: Locations with a higher number of restaurants receive more votes, indicating higher customer engagement. However, the number of votes per restaurant can vary widely.

- **Preferred Cuisines**: Certain cuisines consistently receive high ratings, highlighting customer preferences for these types of food.

- **Positive Impact of Social Activities**: Restaurants that offer table booking facilities, which can be associated with social dining experiences, tend to have higher ratings.

- **Cost Variation by Location**: The average dining cost varies significantly by location and type of cuisine, reflecting regional differences in pricing and dining culture.

- **Correlation between Facilities and Ratings**: A positive correlation exists between the availability of customer convenience facilities (online order and table booking) and higher restaurant ratings.

### Recommendations

1. **Enhance Customer Convenience**: Restaurants should consider offering online ordering and table booking facilities to improve customer satisfaction and ratings.

2. **Focus on High-Rating Cuisines**: Restaurants could focus on offering cuisines that are highly rated by customers to attract more business and improve their reputation.

3. **Target High Engagement Locations**: For expansion, Zomato and restaurant owners should consider locations with high customer engagement, as indicated by the number of votes and ratings.

4. **Optimize Pricing Strategies**: Restaurants should optimize their pricing strategies based on the type of cuisine and the location to attract more customers and increase profitability.

5. **Promote Social Dining Experiences**: Enhancing social dining experiences by offering table bookings and other social activities can lead to higher customer satisfaction and ratings.

### Limitations

1. **Data Representation**: The dataset may not represent all geographical regions equally, leading to potential biases in the analysis.

2. **Feature Limitations**: Some important features influencing customer ratings, such as service quality, ambiance, and hygiene, are not included in the dataset.

3. **Proxy Assumptions**: Assumptions made about proxies for social activities (e.g., table booking) may not fully capture the complexity of customer dining preferences.

### References

1. *Seaborn and Matplotlib Documentation*: For data visualization methods.
2. *Zomato API Documentation*: For detailed information on the data fields and how the data was obtained.
3. *ChatGPT - Python* [Check here](chat.openai.com)

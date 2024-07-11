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

   

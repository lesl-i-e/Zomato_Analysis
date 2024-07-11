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
   

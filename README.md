# Upliance

### Objective

This project aims to analyze and visualize user behaviors, cooking sessions, and order patterns. The analysis identifies relationships between cooking session participation and order trends, explores demographic factors influencing user activity, and highlights popular dishes and meal types. The insights provide actionable recommendations for improving business operations and customer satisfaction.

### Datasets:

####  Order Details Table:
- Columns: Order ID, User ID, Order Date, Meal Type, Dish Name, Order Status, Amount (USD), Time of Day, Rating, Session ID
- Provides information about user orders, meal preferences, and order status.

#### Cooking Sessions Table:

- Columns: Session ID, User ID, Dish Name, Meal Type, Session Start, Session End, Duration (mins), Session Rating
- Details the cooking sessions, including duration, user participation, and session ratings.

#### User Details Table:
- Columns: User ID, User Name, Age, Location, Registration Date, Phone, Email, Favorite Meal, Total Orders
Contains demographic information about users

### Data Cleaning and Preparation

#### 1. Handling Missing Values

- Rating: Replaced missing (N/A) values in the "Rating" column with Blanks for calculations and analysis.
- Session Rating: Checked for consistency and ensured missing ratings were treated as neutral or zero.
  
#### 2. Data Type Adjustments
- Converted dates to the appropriate datetime format for accurate sorting and time-based analysis.
- Changed numeric fields (e.g., Amount, Session Rating) to numeric data types for aggregation.

#### 3. Duplicate Removal
- Checked for duplicate entries in all datasets and removed redundant rows to ensure data consistency.

#### 4. Data Validation
- Cross-verified the relationships between tables using primary and foreign keys:
- Matched User ID across all three tables.
- Matched Session ID in the Order Details and Cooking Sessions tables.
  
### New Measures and Calculated Columns

#### Calculated Columns

``` Session-Order Match = 
IF(
    ISBLANK(OrderDetails[Session ID]),
    "False",
    "True"
)```

``` Session-Order Time Gap = 
DATEDIFF(
    RELATED(CookingSessions[Session End]), 
    OrderDetails[Order Date], 
    MINUTE
) ```

``` Dish Popularity Rank = 
RANKX(
    ALL(OrderDetails[Dish Name]), 
    CALCULATE(COUNT(OrderDetails[Order ID])), 
    , 
    DESC
) ```

```Age_Group = 
SWITCH(
    TRUE(),
    UserDetails[Age] >= 18 && UserDetails[Age] <= 25, "18-25",
    UserDetails[Age] >= 26 && UserDetails[Age] <= 35, "26-35",
    UserDetails[Age] >= 36 && UserDetails[Age] <= 45, "36-45",
    UserDetails[Age] > 45, "46+",
    "Unknown"
)```

#### Measures:

Order Frequency:

Formula: COUNTROWS(Order ID grouped by User ID)
Captures how often a user places an order.
Dish Popularity:

Formula: COUNT(Dish Name)
Tracks the frequency of each dish being ordered.
Measures
Total Orders:

Formula: SUM(Order Status Indicator)
Calculates the total completed orders.
Average Session Rating:

Formula: AVERAGE(Session Rating)
Provides insights into user satisfaction with cooking sessions.
Total Revenue:

Formula: SUM(Amount)
Shows total earnings from completed orders.
Average Order Value:

Formula: SUM(Amount) / COUNT(Order ID)
Calculates the average revenue per order.
Retention Rate:

Formula: (Active Users in Last 30 Days) / Total Users
Indicates user engagement over time.
Visualizations
Key Visuals in Power BI
Total Orders by User (Bar Chart):

Illustrates order frequency per user.
Revenue Over Time (Line Chart):

Tracks revenue trends based on order dates.
Dish Popularity (Pie Chart):

Highlights the most frequently ordered dishes.
User Engagement (Stacked Bar Chart):

Combines session ratings and order counts to evaluate user engagement.
Demographics and Meal Preferences (Clustered Bar Chart):

Explores correlations between age, location, and favorite meal types.
Findings
User Engagement
Users with higher session participation (e.g., Alice, Charlie) place more orders, highlighting the connection between engagement and revenue.
Meal Preferences
Dinner is the most preferred meal type, with Spaghetti and Grilled Chicken as the top dishes.
Breakfast and lunch orders are less frequent but favored by specific age groups.
Demographics
Younger users prefer dinner, while older users lean toward breakfast or lunch.
Urban areas like New York and Chicago show diverse meal preferences.
Business Recommendations
Enhance User Retention

Implement loyalty programs targeting users with high order frequency and session participation.
Focus Marketing on Popular Dishes

Promote dishes like Spaghetti and Grilled Chicken, offering discounts to drive repeat orders.
Age-Based Campaigns

Tailor marketing campaigns for different age groups. For instance, dinner promotions for younger users and breakfast deals for older users.
Region-Specific Offers

Develop location-based campaigns to cater to regional preferences.
Improve Cooking Sessions

Increase session duration for popular dishes and enhance user satisfaction by addressing feedback.


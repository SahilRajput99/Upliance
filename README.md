# Upliance

### Objective

This project aims to analyze and visualize user behaviors, cooking sessions, and order patterns. The analysis identifies relationships between cooking session participation and order trends, explores demographic factors influencing user activity, and highlights popular dishes and meal types. The insights provide actionable recommendations for improving business operations and customer satisfaction.

### Data Overview

The project involves the following datasets:

### 1. OrderDetails.csv

#### Columns:

Order ID

User ID

Order Date

Meal Type

Dish Name

Order Status

Amount (USD)

Time of Day

Rating

Session ID

### 2. CookingSessions.csv

#### Columns:

Session ID

User ID

Dish Name

Meal Type

Session Start

Session End

Duration (mins)

Session Rating

### 3. UserDetails.csv

#### Columns:

User ID

User Name

Age

Location

Registration Date

Phone

Email

Favorite Meal

Total Orders

### Data Cleaning and Transformation

To ensure the datasets were ready for analysis, the following data cleaning and transformation steps were performed:

#### Handling Missing Values:

- Missing values in the Rating column were replaced with 0 to maintain numeric integrity.

- Missing values in non-numeric fields (if any) were handled using appropriate placeholder values or were removed if irrelevant.

#### Merging Datasets:

- The datasets were merged using common columns:

User ID: To link user details with orders and cooking sessions.

Session ID: To establish relationships between cooking sessions and orders.

#### Derived Columns:

- Session Duration: Calculated as the difference between Session Start and Session End.

- Order Frequency: Aggregated orders per user over specific time periods.

- Dish Popularity: Counted the number of times each dish appeared in completed orders.

- Average Session Rating per User: Computed as the mean of session ratings for each user.

#### Data Type Corrections:

- Ensured that date fields (e.g., Order Date, Session Start, Session End) were correctly formatted as datetime objects.

- Converted categorical fields like Meal Type and Order Status to appropriate data types for analysis.

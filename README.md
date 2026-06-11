Customer Shopping Behavior Analysis
Uncovering Spending Patterns, Segmentation & Strategic Insights from 3,900 retail transactions.

Project Overview

A retail company observed shifts in customer purchasing patterns across demographics, product categories, and channels. This project explores those patterns through end-to-end data analysis — from raw data cleaning and ETL to SQL-based querying and Power BI visualization.

Key Business Question:
How can shopping data be leveraged to improve customer engagement and optimize marketing & product strategies?"

🎯 Objectives
1.Analyze spending patterns by gender, age group, and season
2.Identify high-value products and top-rated items
3.Compare subscriber vs. non-subscriber behavior
4.Segment customers into New, Returning, and Loyal groups
5.Evaluate the impact of discounts on revenue
6.Rank top products within each category using window functions

 Dataset Overview

MetricValueTotal Records3,900Features18 columnsProduct Categories4 (Clothing, Accessories, Footwear, Outerwear)Geographic Coverage50 US StatesNull Values37 (Review Rating only

Feature Groups

GroupColumnsDemographicsAge, Gender, LocationPurchase DetailsItem, Category, Amount, Season, Size, ColorBehaviorDiscount, Frequency, Previous Purchases, Review RatingPayment / ShippingPayment Method, Shipping Type, Subscription StatusEngineeredAge Group, Purchase Frequency Days
 
 Tech Stack

ToolPurposePython (Pandas, NumPy, Seaborn)Data cleaning, EDA, feature engineeringPostgreSQL + SQLAlchemyETL pipeline, SQL analysisPower BIInteractive dashboard & visualization

Data Cleaning & Feature Engineering

 SQL Analysis — Key Queries & Findings

Q1 · Revenue by Gender

SELECT gender, SUM(purchase_amount) AS revenue
FROM customer
GROUP BY gender;

Finding: Male customers generated $157,000 vs. female customers at $76,000 — males drive ~67% of total revenue.

Q2 · Discount Buyers Above Average Spend

SELECT customer_id, purchase_amount
FROM customer
WHERE discount_applied = 'Yes'
AND purchase_amount >= (SELECT AVG(purchase_amount));

Finding: ~1,850 discount buyers still exceeded the average spend of $59.76 — strong candidates for loyalty programs.

Q3 · Top 5 Products by Average Review Rating

SELECT item_purchased, ROUND(AVG(review_rating), 2) AS avg_rating
FROM customer
GROUP BY item_purchased
ORDER BY avg_rating DESC
LIMIT 5;

Finding: Blouse, Jacket, Dress, Shirt, and Boots all scored an average rating of 4.0.

Q4 · Standard vs. Express Shipping Impact

Finding: Average spend under Standard shipping ≈ $60 vs. Express ≈ $59 — shipping type has minimal impact on purchase amount.

Q5 · Subscriber vs. Non-Subscriber Spend

GroupCustomersAvg SpendRevenueSubscribed1,860$60.5$112,530Not Subscribed2,040$59.1$120,564

Finding: Subscribers spend slightly more per transaction, but non-subscribers generate higher total revenue due to volume.

Q6 · Top 5 Products by Discount Rate

SELECT item_purchased,
ROUND(100.0 * SUM(CASE WHEN discount_applied = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS discount_rate
FROM customer
GROUP BY item_purchased
ORDER BY discount_rate DESC
LIMIT 5;

Finding: Jeans (50%), Blouse (48%), Dress (47%), Sneakers (46%), Jacket (45%) — all heavily discounted items.

Q7 · Customer Segmentation (CTE-Based)

WITH segments AS (
  SELECT customer_id,
    CASE
      WHEN previous_purchases = 1 THEN 'New'
      WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
      ELSE 'Loyal'
    END AS segment
  FROM customer
)
SELECT segment, COUNT(*) AS customers FROM segments GROUP BY segment;

Finding:
New: 220 (6%)
Returning: 1,980 (51%)
Loyal: 1,700 (43%)

Q8 · Top 3 Products Per Category (Window Function)

SELECT category, item_purchased, order_count, rank
FROM (
  SELECT category, item_purchased,
         COUNT(*) AS order_count,
         RANK() OVER (PARTITION BY category ORDER BY COUNT(*) DESC) AS rank
  FROM customer
  GROUP BY category, item_purchased
) ranked
WHERE rank <= 3;

Q9 · Repeat Buyers & Subscription Status

Finding: Of buyers with >5 purchases, 1,640 are non-subscribers vs. 1,220 subscribed — a major opportunity to convert loyal customers into subscribers.


Q10 · Revenue by Age Group

Age GroupRevenueMiddle-aged$68,900Adult$62,500Senior$58,800Young Adult$42,700

Finding: Middle-aged customers (45–57) are the top revenue contributors.

Key Insights & Takeaways

InsightAction💰 Males drive 67% of revenueLaunch targeted campaigns for female segments🎁 Discount buyers still spend above averageUpsell them into loyalty & premium subscription programs👥 Middle-aged customers lead in revenueFocus marketing budgets on the 45–57 age bracket🔄 Loyal customers are largely non-subscribersOffer retention deals to convert repeat buyers📦 Clothing dominates all categoriesPrioritize Blouse & T-Shirt in inventory & promotions⭐ Product ratings are narrow (3.78–3.88)Low ROI on quality improvement; focus elsewhere

 Project Structure

 customer-shopping-behavior-analysis/
│
├── data/
│   └── customer_shopping_data.csv        # Raw dataset
│
├── notebooks/
│   └── shopping_analysis.ipynb           # EDA, cleaning & feature engineering
│
├── sql/
│   └── queries.sql                       # All 10 SQL analysis queries
│
├── powerbi/
│   └── shopping_dashboard.pbix           # Power BI dashboard file
│
├── reports/
│   └── Customer_Shopping_Behavior_Report.docx
│
└── README.md

How to Run

1. Clone the Repository

bashgit clone https://github.com/Mehnaz14/customer-shopping-behavior-analysis.git
cd customer-shopping-behavior-analysis

2. Install Dependencies

bashpip install pandas numpy matplotlib seaborn sqlalchemy psycopg2

3. Run the Notebook

Open notebooks/shopping_analysis.ipynb in Jupyter and run all cells for data cleaning, EDA, and ETL to PostgreSQL.

4. Run SQL Queries

Connect to your PostgreSQL instance and run sql/queries.sql after the ETL step loads the data.

5. View the Dashboard

Open powerbi/shopping_dashboard.pbix in Power BI Desktop.

Project Overview
A retail company observed shifts in purchasing behavior across demographics, product categories, and sales channels. This project builds a complete analytics pipeline to uncover what drives consumer decisions and repeat purchases — and translates those findings into concrete business recommendations.
Central Question: How can consumer shopping data be used to identify trends, improve customer engagement, and optimize marketing and product strategies?
Repository Structure
customer-shopping-behavior/
│
├── data/
│   └── customer_shopping_data.csv        # Raw dataset
│
├── notebooks/
│   └── shopping_behavior_analysis.ipynb  # Full EDA + preprocessing + SQL ETL
│
├── sql/
│   ├── q1_revenue_by_gender.sql
│   ├── q2_discount_buyers_above_avg.sql
│   ├── q3_top_products_by_rating.sql
│   ├── q4_shipping_vs_spend.sql
│   ├── q5_subscriber_spending.sql
│   ├── q6_top_discount_products.sql
│   ├── q7_customer_segmentation_cte.sql
│   ├── q8_top_products_per_category.sql
│   ├── q9_repeat_buyers_subscription.sql
│   └── q10_revenue_by_age_group.sql
│
├── dashboard/
│   └── customer_behavior_dashboard.pbix  # Power BI file
│
├── reports/
│   └── Customer_Shopping_Behavior_Report.pdf
│
└── README.md
 SQL Analysis — 10 Business Questions
Q1 · Revenue by Gender
Male customers account for ~67% of total revenue ($157K vs $76K), revealing an untapped opportunity in female-focused marketing.
Q2 · Discount Buyers Spending Above Average
~1,850 customers used discounts and spent above the $59.76 average — prime candidates for loyalty program conversion.
Q3 · Top 5 Products by Review Rating
Ratings are tightly clustered (3.78–3.88), indicating uniformly positive satisfaction. Quality improvement has low incremental ROI.
Q4 · Shipping Type vs Spend
Only a $1.10 difference between Standard ($60.20) and Express ($59.10) buyers. Shipping preference ≠ purchase value.
Q5 · Subscribers vs Non-Subscribers
Subscribed customers have a slightly higher avg spend ($60.50 vs $59.10), but non-subscribers make up the larger base. Converting frequent buyers to subscribers is a key LTV opportunity.
Q6 · Top Products by Discount Rate
Jeans lead with a 50% discount rate — nearly every other purchase uses a discount. Margin compression risk is highest here.
Q7 · Customer Segmentation (CTE)
Only 6% new customers → acquisition strategy needs attention.
Q8 · Top 3 Products Per Category (Window Function)
Blouse leads all products with 171 orders. Clothing dominates volume across all categories.
Q9 · Repeat Buyers & Subscription Status
1,640 repeat buyers are non-subscribers vs 1,220 subscribers — a major retention opportunity. Subscription incentives (discounts, early access) could drive meaningful growth.
Q10 · Revenue by Age Group
Middle-aged customers (45–57) are the top revenue segment at $68,900. Young Adults (18–31) have the most headroom for digital campaign growth.

 Future Enhancements

 Time-series analysis of seasonal purchasing trends
 Customer Lifetime Value (CLV) modelling
 Cohort retention analysis
 Churn prediction using machine learning

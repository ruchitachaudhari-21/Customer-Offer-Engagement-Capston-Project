# Customer-Offer-Engagement-Capston-Project
"The project is about analyzing customer engagement with marketing offers using Power BI. The client wanted to understand how customers interact with different types of offers, which offers drive higher engagement, and how demographics affect response rates."

Build an interactive Power BI dashboard using the Customer, Events, Offers, and Offers Metadata datasets to enable marketing teams and analysts to:
● Understand customer engagement with promotional offers (received, viewed, completed)
● Calculate offer redemption rates and analyze transaction behavior post-offer
● Segment customers by demographics (age, gender, income) and engagement levels
● Identify most effective offer types, channels, and reward strategies
● Enable ad hoc analysis of coverage, conversion, and spend metrics to inform marketing strategies

Data Sources
 Event.csv - All customer interactions and transactions
 Offer.csv - Marketing offer types and distribution channels
 Data_dictionary.csv - Field-level metadata for all tables
 Customer.csv - Customer demographics and signup date

Data Transformation:
🔹 Customers Table
Purpose: Holds demographic information for each customer.
Key Fields: customer_id, age, gender, income, became_member_on.
Cleaning Performed:
o Removed duplicates.
o Handled missing income by replacing with "not disclose".
o Corrected age outliers (removed invalid ages like 0 or >100).
o Created Age Group column for segmentation.
🔹 Offers Table
Purpose: Stores details of marketing offers.
Key Fields: offer_id, offer_type, difficulty, reward, duration, channels.
Cleaning Performed:
o Parsed channels JSON into list and expanded to rows.
o Created Offer Category column (BOGO, Discount, Informational).
o Verified logical consistency (difficulty = 0 and reward = 0 → Informational).
🔹 Events Table
Purpose: Records customer interactions (offer received, viewed, completed, transaction).
Key Fields: customer_id, event, time, value.
leaning Performed:
o Parsed value JSON to extract offer_id and amount.
o Steps Select Value column – Parse – Json- Extract value – Rename column Offer_id_extract
🔹 Offer Channels Table (derived from Offers)
Purpose: Normalized table for offer distribution channels.
Key Fields: offer_id, channel.
Cleaning Performed:
o Extracted each channel from channels JSON array.
o Removed duplicates.

Relationships:
1. customers[customer_id] ↔ events[customer_id] (One-to-Many)
2. offers[offer_id] ↔ events[value.offer id] (One-to-Many after parsing value)
3. offers[offer_id] ↔ offer_Channel[offer_id_extracted]
4. All are one-to-many relationships.
5. This star schema keeps fact data (Events) in the center, surrounded by dimension tables (Customers, Offers, Offer Channels).

Page 1 – Overview Dashboard
Purpose:
"Gives top-level KPIs of customer engagement and transactions in one glance."
What to Say in Exam:
•	"We used KPI cards for key measures — Total Customers, Offers Sent, Offers Viewed, Offers Completed, Redemption Rate, Avg. Transaction Amount — so decision makers can quickly see overall performance."
•	"This page acts as the executive summary, showing trends and highlights without needing to go deep into detail."
________________________________________
Page 2 – Offer Funnel
Purpose:
Here we highlight customer offer gerney
What to Say:
•	"We used a Funnel chart to clearly show drop-offs between stages — Sent → Viewed → Completed → Transaction."
•	"This helps marketing identify at which stage customers disengage, so they can optimize messaging or targeting."
________________________________________
Page 3 – Customer Segmentation
Purpose:
"Analyzes engagement by demographics like age, gender, and income."
What to Say:
•	"We added slicers for age group, gender, and income to allow dynamic filtering."
•	"A bar chart shows Redemption Rate by Age Group to identify the most responsive segments."
•	"A heatmap of Age vs Income vs Completion % reveals combined demographic insights for more precise targeting."
________________________________________
Page 4 – Offer Performance
Purpose:
"Compares performance across different offer types, rewards, and channels."
What to Say:
•	"We used bar charts to compare Redemption by Offer Type, Reward, and Channel — this shows which strategies work best."
•	"A scatter plot maps Difficulty vs Completion Rate, with bubble size representing reward. This helps find the right balance between difficulty and attractiveness of an offer."
________________________________________
Page 5 – Transaction Behavior
Purpose:
"Analyzes spending patterns over time and how they differ between engaged vs. non-engaged customers."
What to Say:
•	"We used a line chart for Avg. Spend Over Time, segmented by customers who completed offers vs. those who didn’t."
•	"This reveals whether offers lead to sustained higher spending or just short-term boosts."


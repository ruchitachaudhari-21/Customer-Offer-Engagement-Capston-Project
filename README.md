# Customer-Offer-Engagement-Capston-Project
 This project delivers an interactive Customer Offer Engagement Dashboard in Power BI, integrating customer demographics, offer details, and event transactions. The dashboard provides end-to-end visibility into the marketing offer lifecycle — from distribution, to viewing, to completion, and finally to transaction impact. 
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
 Purpose: Holds demographic information for each customer.
 Key Fields: customer_id, age, gender, income, became_member_on.
 Cleaning Performed:
o Removed duplicates.
o Handled missing income by replacing with "not disclose".
o Corrected age outliers (removed invalid ages like 0 or >100).
o Created Age Group column for segmentation.
🔹 Offers Table
 Purpose: Stores details of marketing offers.
 Key Fields: offer_id, offer_type, difficulty, reward, duration, channels.
 Cleaning Performed:
o Parsed channels JSON into list and expanded to rows.
o Created Offer Category column (BOGO, Discount, Informational).
o Verified logical consistency (difficulty = 0 and reward = 0 → Informational).
🔹 Events Table
 Purpose: Records customer interactions (offer received, viewed, completed, transaction).
 Key Fields: customer_id, event, time, value.
 Cleaning Performed:
o Parsed value JSON to extract offer_id and amount.
o Steps Select Value column – Parse – Json- Extract value – Rename column Offer_id_extract
🔹 Offer Channels Table (derived from Offers)
 Purpose: Normalized table for offer distribution channels.
 Key Fields: offer_id, channel.
 Cleaning Performed:
o Extracted each channel from channels JSON array.
o Removed duplicates.

Relationships:
1. customers[customer_id] ↔ events[customer_id] (One-to-Many)
2. offers[offer_id] ↔ events[value.offer id] (One-to-Many after parsing value)
3. offers[offer_id] ↔ offer_Channel[offer_id_extracted]
4. All are one-to-many relationships.
5. This star schema keeps fact data (Events) in the center, surrounded by dimension tables (Customers, Offers, Offer Channels).

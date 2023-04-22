# Hotel Revenue Analysis
[Dataset sourced from blog: Absent Data](https://absentdata.com/data-analysis/where-to-find-data/)

NOTE: For data analysis, I utilized SQL to combine and organize the data, and DAX in Power BI to calculate metrics and generate insights. This project was undertaken as a personal challenge to enhance my skills in working with financial and date data types in DAX, and to create more effective data visualizations.

# Resources Used for this Project: #
- Stack Overflow and other online forums to research SQL and DAX queries.
- Cole Nussbaumer Knaflic's book, *Storytelling with Data*, to reference best practices for data visualization. 
- Absent Data blog for the dataset and inspiration for the potential business problems. 
- The following Youtube channel for DAX calculation: [Calculate Growth over Last Year by Fiscal Year in Power BI](https://www.youtube.com/watch?v=iqUTHlfHomg&list=PLD27DiVmJtrSwEORvUXQgj2im_NP_uSC7&index=4), [Creating a simple date table in Power BI
](https://www.youtube.com/watch?v=-li7sxUxEqA&list=PLD27DiVmJtrSwEORvUXQgj2im_NP_uSC7&index=3), [Previous year up to a certain date
](https://www.youtube.com/watch?v=bAOs5LTP0I0&list=PLD27DiVmJtrSwEORvUXQgj2im_NP_uSC7&index=5)

# Objectives: #
Conduct a thorough analysis of a hotel revenue dataset to identify trends and insights related to revenue growth, hotel occupancy rates, guest parking requirements, distribution channels, and customer characteristics. The primary objective is to provide insights and answers to pertinent business questions within the hospitality industry.

# Business Questions: #
- Q1. Is our hotel revenue growing by year?
- Q2. Should we increase our parking lot size? 
- Q3. What trend can we see in the data?

# Discovery: #
- The original data source was an Excel Worksheet with 5 sheets containing 2018-2020 revenues, meal cost table, and market segment table.
- The worksheet consisted of 32 columns with attributes related to hotel type, customer information, booking information, meal information, and market segment.
- The combined rows totaled over 170,000, providing information on the attributes mentioned above.
- The data structure was consistent, enabling me to load the data into Microsoft SQL Server Management Studio for further structuring and transformation.

# Joining: #
- Loaded the dataset using the import wizard from SSMS.
- Used a SQL query to combine the 5 tables together and connect each table with their relevant keys.
- Created a backup of the merged dataset to ensure data safety during further transformations.

# Cleaning, Structuring, and Validating: #
- Converted month column from month name to month number for easier querying.
- Combined date columns together to use as a key later to create a relationship with a custom date dimension table in Microsoft Power BI.
- Organized each hotel revenue table by year, but dataset lacked consistency, which may impact date comparisons.
- Created a revenue calculation using various columns such as stays_in_weekend_nights, stays_in_week_nights, adults, children, babies, adr, discount, meal cost, is_canceled, and deposit type.
- Calculated total nights a guest stayed using stays_in_weekend_nights and stays_in_week_nights columns.
- Determined total number of guests using adults, children, and babies columns. 
- Multiplied total number of guests with meal cost to calculate total meal cost spent by guests.
- Used is_canceled column to determine if the guest actually stayed in the hotel and deposit_type to determine if the hotel made revenue from non-refundable deposits from canceled reservations.
- Used CASE expression in SQL to factor in revenue based on cancellation and deposit type.
- The logic behind revenue calculation:
  - If guest canceled reservation and deposit is refundable, then revenue is 0. 
  - If guest canceled and deposit is non-refundable, then revenue is $250 
    - Note: $250 is just a random number I created to replicate a non-refundable security deposit in some real hotels. 
  - If guest did not cancel reservation, then revenue is: 
    - (total nights * (ADR * (1 - discount rate)) + total meal cost
- Validated data and determined if there was anything out of the ordinary using custom query in SQL before loading query into Microsoft Power BI.

# Presenting: #
- Validated dataset loaded into Power BI
- Four card visualizations created to analyze Total Revenue, Average Daily Rate, Average Hotel Occupancy, and Total Parking Required
- Line chart created for each card to represent overall trend (inspired by Absent Data's blog)
- Line and clustered column chart used to visualize correlation between revenue growth and average daily rate, and negative correlation between hotel occupancy and average daily rate.
- Line and column chart used to compare current and past parking requirements and revenue growth. 
- Horizontal bar chart used to show which countries bring in the most revenue and which distribution channels are most profitable.
- Matrix added to provide deeper insight into revenue growth and parking requirement, with Month over Month and Year over Year growth highlighted.
- Slicer added to enable filtering by hotel type, year, and month for deeper insight into the report.

# Dashboard: #
![image](https://user-images.githubusercontent.com/28738970/233811688-68e34032-6800-4c5e-9918-fc978cc61cbc.png)

# My Analysis: #

- *Q1. Is our hotel revenue growing by year?*

- Answer: The revenue of the hotel appears to be increasing over the years, with 2019 showing a particularly high amount that could be considered an outlier. To gain more insights into why 2019 had such high revenue, additional data from the source may be necessary. Nonetheless, the trend indicates a positive growth in revenue.

  ![image](https://user-images.githubusercontent.com/28738970/233808997-99366179-5237-48bd-8e03-bb2b873fde4e.png)

- *Q2. Should we increase our parking lot size?*

- Answer: Based on the data, it doesn't appear that the parking requirements are increasing significantly to warrant an expansion of the parking lot size, particularly if the hotel was able to accommodate the guest parking needs during the high-revenue year of 2019.

  ![image](https://user-images.githubusercontent.com/28738970/233810262-40263b70-7642-4d7e-8f52-8ed415837c22.png)

- *Q3. What trend can we see in the data?*

- Answer: Based on my analysis, it appears that there is an inverse relationship between the average daily rate and hotel occupancy. As the average daily rate increases, hotel occupancy decreases. However, despite the lower hotel occupancy, there is an increase in revenue associated with the higher rate. Therefore, finding a balance between the average daily rate and hotel occupancy is important in maximizing revenue. By finding the optimal rate, the hotel can attract more customers while still generating sufficient revenue.

  ![image](https://user-images.githubusercontent.com/28738970/233810386-1133d586-3103-4b4d-90b0-32cb7641682d.png)

- Answer: Based on the analysis of the hotel revenue dataset, the following insights were uncovered:
  - Portugal is the top revenue-generating country for the hotel, followed by Great Britain, France, and Spain.
  - The most effective distribution channel for generating revenue is through travel agencies, followed by direct bookings and then corporate bookings.

  ![image](https://user-images.githubusercontent.com/28738970/233810413-56c69dc5-f762-47ac-a288-9cfae27c23bf.png)

- Answer: August is the most profitable month in all three years (2018, 2019, and 2020). We should investigate what draws guests during this month. Additionally, I noticed that April, August, and October require the most parking space. It would be wise to plan for this to avoid issues. However, the data for 2018 and 2020 are incomplete, and having complete data may provide better insights.

  ![image](https://user-images.githubusercontent.com/28738970/233810565-ce51455b-6039-4924-af37-f464e85fab4c.png)

  ![image](https://user-images.githubusercontent.com/28738970/233810915-86458cf0-7412-4586-9627-5f4852b4348d.png)

  ![image](https://user-images.githubusercontent.com/28738970/233810598-9708c1f2-262b-4ba9-95ee-07d91f425077.png)


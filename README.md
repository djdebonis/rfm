# RFM Analysis

This data was collected between November, 2021 and April, 2026 for a Health and Wellness Ecommerce small business. Although the total revenue for the business is relatively small, there is a large repurchase rate over the course of years, so the data is worth evaluating. These analyses may support making recommendations for how the business can approach future endevours.

All data analysis and visualization was conducted using the Python language (Python Software Foundation [2025]; henceforth “Python”), leveraging a Jupyter Notebook to scaffold and break down the different components of the analysis. This demonstrates the group’s competency in the learned skills from the course. The Jupyter Notebook can be accessed and visualized here.

### Summary of Data
Timeline of Data
The first order in this dataset was placed 2021-11-26 
The latest order in this dataset was placed 2026-04-18 
Meaning this dataset spans approx: 
4 years, 4 months, and 24 days of sales data.

### Summary statistics of Revenue
Total Revenue and Orders
The total revenue in the period is $135,022.53
There is a total of 1973 orders in this period contributing to the total revenue number.

### Data by Customer
These orders were placed by a total of 843 customers.
On average, a customer for this company places 2.34 (sd = 4.14) orders over their customer lifetime. The median number of orders per customer is 1.0
These data suggest that most customers place only an order or two, but some customers place a lot of orders.
The Average Order Value (AOV) is $68.44 (sd = $51.55), including shipping and taxes. The median order value is $50.0.
These data suggest that there is a large variance in the size of order values.

### Revenue Data by Day
The average daily revenue for this small ecomm business is $157.55 with a median daily revenue of: $92.4.
These data suggest that there is a large variance in the daily revenue, ranging from 0 to $1750+ on any given day.

### RFM Segmentation
Recency (R), Frequency (F), and Monetary (M) scores were assigned to each customer independently based on their purchase behavior during the period. Recency and Monetary scores were calculated by quintiles in accordance with the method suggested by Hughes (2019). 

**Recency scores**
Recency scores were sorted by date of last order, broken into equal quintiles, then assigned a score based on their rank; the most recent 20% of customers were assigned a 5, the second most recent 20% of customers were assigned a 4, and so on.

**Monetary scores** 
Monetary scores were sorted from highest to lowest by customer total lifetime order revenue, broken into even quintiles, then assigned as score based on their rank; the customers of the highest 20% total lifetime order revenue were assigned a 5, the second highest 20% of total lifetime order revenue were assigned a 4, and so on.

**Frequency scores**
Frequency scores had to be assigned differently than suggested by Hughes (2019) due to the disproportionate number of customers who only had a frequency value of 1 (i.e. the customer only placed one order ever). Breaking into quintiles would have resulted in customers with only one order being arbitrarily assigned to groups of 1, 2, or 3, which would misrepresent a significant difference in their past purchase behavior in the F score. To overcome this obstacle, thresholds for groups were manually assigned to better represent customer frequency (loyalty) groups. Although this process may lead to different sizes of F score groupings, it ensures that the F scores accurately represent customer behavior—especially for customers with only one order and customers with large order quantities (i.e. 10+). F scores were assigned as follows:

Let the Frequency score F(n) be defined as:

$$
F(n) =
\begin{cases}
1 & \text{if } n = 1 \\
2 & \text{if } n = 2 \\
3 & \text{if } 3 \leq n \leq 4 \\
4 & \text{if } 5 \leq n \leq 9 \\
5 & \text{if } n \geq 10
\end{cases}
$$

Where *n* is the number of orders in the period.


Each customer was then assigned a compiled RFM coded score, which was a simple concatenation of the string format of their R score + F score + M score. For example, if a customer had an R Score of 5, an F Score of 3, and an M score of 5, their RFM coded score would be 535. 

## R(FM) Segmentation
RFM cannot be easily displayed in a 2D format, as it is a three-dimensional plot. Ecommerce Platform Shopify (2026) has implemented a creative strategy for overcoming this, where the Frequency (F) and Monetary (M) scores are averaged into a composite score, a score that theoretically would suggest a crude depiction of customer lifetime value. Here we will call this the composite FM score, or, simply, the FM score. Shopify (2026) has also created thresholds and labels representing a customer segments ‘relationship’ to the business for the period based on R and FM scores. An example can be seen here:

![depiction of shopify's RFM visualization and segmentation graph](shopify_r_fm_example.png)

For the present study, a R x FM segmentation was adapted from Shopify (2026). The FM composite score was calculated as the average of the F score and the M score, represented as:

FM composite scores were calculated as:

$$
FM = \frac{F + M}{2}
$$

Where F is Frequency Score and M is Monetary Score. 

Groups were segmented according to the segment labels adapted from Shopify (2026). Individual .csv documents were made for each customer segment label, which would allow for targeted advertising efforts (obviously here the data was deidentified, but in a true use-case the data would have been identified). After this, Python’s matplotlib.pyplot module was used to depict the size of these segments based on number of customers and percentage of customer population.


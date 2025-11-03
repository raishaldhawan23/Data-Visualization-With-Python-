# From Sourcing to Revenue: An In-depth Analysis of Supply Chain for a Fashion and Beauty Startup

## 1. Project Background
The startup operates in a fast-moving retail environment where demand is volatile, SKUs are diverse (skincare, haircare, cosmetics), and inventory ties up cash very quickly. The leadership team wanted a single analytical view of the supply chain to answer the following strategic questions:

- Are we stocking the right products in the right quantities?
- Are we moving inventory fast enough to protect margins?
- Where in the chain (manufacturing, transport, delivery) are we losing time or money?
- Are production and shipping processes meeting delivery promises?
- How can we align supply-chain decisions with revenue performance?

This project uses an interactive Python Dash dashboard to analyse the startup’s end-to-end supply chain data (inventory, SKUs, transport, manufacturing, customer segment) and turn it into decision-grade insights for senior managers. The focus is on improving operational efficiency, reducing logistics costs and preventing stockouts for high-velocity products.

### Business objectives
- Optimise inventory levels without hurting availability.
- Improve supply chain efficiency by tracking lead times, shipping performance and transport modes.
- Link supply chain execution to revenue by analysing which products/segments actually drive sales(revenue, SKU profitability).

### Key Links
A short video walk-through of the dashboard: https://drive.google.com/file/d/14H6E1DJoKgrToBqJ-90M06jrtEzZf8sW/view?usp=drivesdk

## 2. Data Structure & Initial Checks
Each row in the dataset represents a unique SKU entry with commercial and operational attributes.
| Dimension      | Key Fields                                                   |
| -------------- | ------------------------------------------------------------ |
| **Product**    | SKU, Product Type, Price, Revenue Generated                  |
| **Inventory**  | Stock Levels, Order Quantities, Production Volumes           |
| **Operations** | Manufacturing Lead Time, Shipping Times, Transportation Mode |
| **Quality**    | Defect Rates, Inspection Results                             |
| **Customer**   | Customer Demographics, Location                              |
| **Finance**    | Costs, Revenue, Lead Time                                    |

### Key Stats
**Mean stock level**: 47.8 units
**Average manufacturing lead time**: 14.8 days
**Average shipping time**: 5.8 days
**On-time delivery rate**: 86%
**Average inventory turnover**: 28.9

### Data Integrity Checks
No missing data in key numeric columns.
Outliers reviewed for shipping and manufacturing times.
On-time delivery calculated as (Shipping Times ≤ Lead Time) and validated for all SKUs.

## 3. Executive Summary
**A. Business Problem**
The startup faced inventory imbalance, overstocking slow-moving products while running out of high-demand items. Simultaneously, lead-time variability and inconsistent transport allocation were hurting delivery performance and inflating costs.
The dashboard consolidates fragmented supply-chain data into one view, helping managers prioritise SKUs, optimise logistics, and align stock levels with real sales trends.

**B. Overview of Findings**
- **Revenue Concentration**: Skincare drives 45% of sales, haircare 29.5%, and cosmetics 25.5%. Cosmetics achieve the highest revenue per SKU (~£6.2K): making them the most efficient category.
- **Delivery Reliability**: On-time delivery rate is 86%: acceptable but below target. Delays stem from long manufacturing lead times.
- **Lead Time Spread**: Manufacturing times range from 2–30 days, introducing unpredictability into the fulfilment cycle.
- **Inventory Mismatch**: High sales occur even with low stock; correlation between stock levels and units sold is near zero.
- **Transport Cost Mix**: Spend distributed across Road (30.3%), Rail (28.7%), Air (27.6%), and Sea (13.4%). Road has the highest defect rate (2.6%) despite similar cost share to Air.
  
## 4. Methodology & Insights
### 4.1 Methodology
**1. Data ingestion & prep:** CSV loaded into Pandas; basic KPI fields were engineered in Python:
- Average stock level
- Inventory turnover = Number of products sold / Stock levels
- On-time delivery flag
- Category-level aggregations (revenue by product type, sales by SKU)

**2. Analytical dashboard build:** Dash + Plotly Express used to create an interactive dashboard with a dropdown for switching views (stock, sales, SKU revenue, transport costs, defect rates, delivery performance).

**3. Analytics approaches:**
- **Descriptive analytics** to profile current inventory, categories, transport and customer segments.
- **Diagnostic analytics** to spot mismatches (e.g. high stock but low sales, high shipping cost but high defect).
- **Light predictive orientation** using trendlines in scatter plots to show revenue behaviour by price and to support demand-driven stocking.

**4. Visualisation design:** Each chart was selected to answer a management question (e.g. “Which category should we prioritise?”, “Where are we losing money in transport?”, “Are we meeting delivery promise?”).

### 4.2 Insights
### **1. Product Category Performance: Skincare Dominates, Cosmetics Punch Above Their Weight**

<img width="948" height="407" alt="image" src="https://github.com/user-attachments/assets/0aebeba1-9cd3-44e6-a043-5410d1bc2d06" />

The donut chart for Sales by Product Type shows that skincare products account for 45 % of total sales, followed by haircare (29.5 %) and cosmetics (25.5 %).
At first glance this suggests skincare drives the company’s top-line revenue, but looking deeper at revenue per SKU reveals a more nuanced story. Cosmetics, despite representing the smallest share of SKUs, generate the highest revenue per SKU (~£6.2 k).
This means that skincare fuels volume, while cosmetics deliver efficiency. Both categories are vital, but for different reasons.

**Business implication:** Protect cosmetics from stockouts through higher safety stock, while maintaining skincare as the brand’s growth engine.


### **2. Inventory Health: Stock Fluctuations Reveal Poor Replenishment Discipline**

<img width="917" height="412" alt="image" src="https://github.com/user-attachments/assets/da2bef85-4293-4b46-a965-cabad380a099" />

<img width="945" height="427" alt="image" src="https://github.com/user-attachments/assets/261902e0-7a41-4e61-953d-b7815decad0a" />

The Stock Levels Distribution histogram shows an erratic pattern with peaks at both 10–20 units and 80–100 units, meaning several products are either perpetually short or heavily overstocked.
The Stock Levels by SKU line chart mirrors this chaos, jumping wildly across the SKU range with no consistent level of coverage.
This means that the company isn’t following a structured replenishment rule; some items sit idle, locking up working capital, while others repeatedly hit zero stock.

**Business implication:** Introduce dynamic reorder points based on real-time demand and turnover. A simple ABC inventory classification could trim total stock by ~15 % without hurting availability.


### **3. Demand vs. Inventory: High Sales Occur Even at Low Stock Levels**

<img width="973" height="417" alt="image" src="https://github.com/user-attachments/assets/7bb82c20-bbd1-409e-aaa0-640f9816bb5d" />

The scatter plot comparing Number of Products Sold vs. Stock Levels reveals almost no correlation (r ≈ 0.02). Several SKUs sold 700–900 units while maintaining stock below 20 units, proving that demand isn’t being met by planned stock.
This means that the startup’s capital is parked in the wrong places, too much in slow-moving items, too little where demand is real.

**Business implication:** Switch from “equal stock for all SKUs” to demand-weighted replenishment. Automating this with a forecast model could lift stock availability for high-velocity SKUs by 25 % while freeing tied-up cash.


### **4. Revenue Concentration: 20 % of SKUs Drive Nearly 70 % of Revenue**

<img width="947" height="443" alt="image" src="https://github.com/user-attachments/assets/091af3d5-38ac-44c0-96ed-bbb695d7d3d9" />

The Revenue by SKU line chart shows distinct spikes where roughly one-fifth of SKUs contribute most of the earnings. This 80/20 Pareto pattern means management attention should be laser-focused on these top performers.
This means when everything is treated equally, resources get diluted.

**Business implication:** Implement tiered service levels: faster production, premium transport, and higher safety stock for A-class SKUs; lean policies for B/C-class SKUs.


### **5. Price vs. Revenue: Skincare Can Hold a Premium, Cosmetics Is Price-Sensitive**

<img width="957" height="408" alt="image" src="https://github.com/user-attachments/assets/5a16bfdb-c9cc-41cf-976c-9514f3d9788f" />

The Price vs. Revenue scatter plot with trendlines by category shows skincare’s line gently sloping upward, haircare roughly flat, and cosmetics downward.
This suggests that customers tolerate higher prices for skincare but respond negatively to price hikes in cosmetics.

**Business implication:** Maintain premium pricing for skincare; run promotional bundles or loyalty offers for cosmetics to stabilise its elasticity. Targeted pricing could improve overall gross margin by 3–5 %.


### **6. Lead-Time Variability: Manufacturing Delays Create Supply-Chain Uncertainty**

<img width="920" height="395" alt="image" src="https://github.com/user-attachments/assets/4aa6f723-8660-4293-a770-09d311a5a3dc" />

The Manufacturing Lead Time Distribution histogram spans 2 to 30 days, showing extreme variation with no clear mode.
It means inconsistent supplier performance causes unpredictable replenishment cycles and directly threatens the 86 % on-time delivery rate.

**Business implication:** Standardise supplier SLAs, monitor lead-time deviation as a KPI, and enforce penalties or bonuses for consistency. Reducing variability by even 25 % could push on-time delivery above 92 %.


### **The Full Supply-Chain Story**
When viewed together, the visuals show a connected narrative: 
- Demand is strong, particularly for cosmetics and skincare.
- Inventory control is weak, with mismatched stock to sales.
- Operations are inconsistent, with variable lead times and unoptimised transport.

The business isn’t suffering from a sales problem, it’s a coordination problem. Better forecasting, targeted stocking, and process standardisation would immediately convert operational chaos into profitable growth.

## 5. Recommendations
1. Implement a demand-driven replenishment model. The analysis clearly shows that stock levels have no real correlation with sales, meaning inventory is being distributed without reference to actual demand patterns. By replacing static stock targets with dynamic reorder points that update automatically based on sales history and lead-time variability, the company can reduce excess stock by roughly a quarter while improving the availability of fast-moving SKUs.

2. Classify SKUs and assign differentiated service levels. About 20 % of products generate almost 70 % of total revenue, so treating every item equally wastes both capital and attention. Segmenting SKUs into A, B and C classes would let managers maintain higher safety stock and faster transport for top performers, while limiting production and holding costs for slow movers. This simple Pareto-based control could release cash tied up in non-essential inventory while guaranteeing service continuity for high-value products.

3. The company should rationalise its transport mix. Although spending across road, rail and air is similar, road transport delivers the highest defect rate and longer lead times. Redirecting premium and fragile goods from road to air or rail, and using sea freight for non-urgent shipments, would align cost with reliability. This reallocation could lower logistics expenses by two to three percent per quarter while cutting defect-related losses and improving delivery quality.

4. Standardise the manufacturing lead times. The data shows a wild variation from two to thirty days, which undermines planning accuracy and customer confidence. Introducing supplier SLAs, benchmarking performance and enforcing penalties for delays would make production more predictable. Even a modest 25 % reduction in lead-time variability could lift on-time delivery from the current 86 % to above 92 %, directly improving customer satisfaction.

5. Align pricing strategy with demand elasticity. The scatter plot reveals that skincare customers tolerate higher prices while haircare demand declines when prices rise. Maintaining premium pricing for skincare and running targeted promotions for haircare would protect margins without sacrificing volume. This shift, supported by data, could raise overall gross margin by 3-5%.

## 6. Summary
This dashboard translates complex operational data into a clear story of performance. It shows that the startup’s main obstacle is not demand but inefficiency, too much stock in the wrong places, inconsistent production, and misallocated transport spending. By acting on these insights, leaders can keep inventory lean yet responsive, stabilise lead times, reduce waste, and ensure that every operational decision supports revenue growth. The result is a supply chain that finally works in harmony with the business strategy rather than against it.

## 7. Tech Stack Used
- **Python (Dash Framework, Pandas, Plotly Express)**: Built an interactive web dashboard with real-time updates and dynamic chart switching.


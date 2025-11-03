# From Sourcing to Revenue: An In-depth Analysis of Supply Chain for a Fashion and Beauty Startup

## 1. Project Background
The startup operates in a fast-moving retail environment where demand is volatile, SKUs are diverse (skincare, haircare, cosmetics), and inventory ties up cash very quickly. The leadership team wanted a single analytical view of the supply chain to answer three things:

Are we stocking the right products in the right quantities?
Are we moving inventory fast enough to protect margins?
Where in the chain (manufacturing, transport, delivery) are we losing time or money?

This project uses an interactive Python Dash dashboard to analyse the startup’s end-to-end supply chain data (inventory, SKUs, transport, manufacturing, customer segment) and turn it into decision-grade insights for senior managers. The focus is on improving operational efficiency, reducing logistics costs and preventing stockouts for high-velocity products.

### Business objectives
Optimise inventory levels without hurting availability.
Improve supply chain efficiency by tracking lead times, shipping performance and transport modes.
Link supply chain execution to revenue by analysing which products/segments actually drive sales.

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
**a. Business Problem**
The startup faced inventory imbalance, overstocking slow-moving products while running out of high-demand items. Simultaneously, lead-time variability and inconsistent transport allocation were hurting delivery performance and inflating costs.
The dashboard consolidates fragmented supply-chain data into one view, helping managers prioritise SKUs, optimise logistics, and align stock levels with real sales trends.

**b. Overview of Findings**
**Revenue Concentration**: Skincare drives 45% of sales, haircare 29.5%, and cosmetics 25.5%. Cosmetics achieve the highest revenue per SKU (~£6.2K): making them the most efficient category.
**Delivery Reliability**: On-time delivery rate is 86%: acceptable but below target. Delays stem from long manufacturing lead times.
**Lead Time Spread**: Manufacturing times range from 2–30 days, introducing unpredictability into the fulfilment cycle.
**Inventory Mismatch**: High sales occur even with low stock; correlation between stock levels and units sold is near zero.
**Transport Cost Mix**: Spend distributed across Road (30.3%), Rail (28.7%), Air (27.6%), and Sea (13.4%). Road has the highest defect rate (2.6%) despite similar cost share to Air.
  
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

### 4.1 Detailed Insights
**1. Product Category Performance: Skincare Dominates, Cosmetics Punch Above Their Weight**
<img width="948" height="407" alt="image" src="https://github.com/user-attachments/assets/0aebeba1-9cd3-44e6-a043-5410d1bc2d06" />

The donut chart for Sales by Product Type shows that skincare products account for 45 % of total sales, followed by haircare (29.5 %) and cosmetics (25.5 %).
At first glance this suggests skincare drives the company’s top-line revenue, but looking deeper at revenue per SKU reveals a more nuanced story. Cosmetics, despite representing the smallest share of SKUs, generate the highest revenue per SKU (~£6.2 k).
So what? Skincare fuels volume, while cosmetics deliver efficiency. Both categories are vital, but for different reasons.
Business implication: protect cosmetics from stockouts through higher safety stock, while maintaining skincare as the brand’s growth engine.

Insight 2: Inventory Health — Stock Fluctuations Reveal Poor Replenishment Discipline

The Stock Levels Distribution histogram shows an erratic pattern with peaks at both 10–20 units and 80–100 units, meaning several products are either perpetually short or heavily overstocked.
The Stock Levels by SKU line chart mirrors this chaos, jumping wildly across the SKU range with no consistent level of coverage.
So what? The company isn’t following a structured replenishment rule; some items sit idle, locking up working capital, while others repeatedly hit zero stock.
Business implication: introduce dynamic reorder points based on real-time demand and turnover. A simple ABC inventory classification could trim total stock by ~15 % without hurting availability.

Insight 3: Demand vs. Inventory — High Sales Occur Even at Low Stock Levels

The scatter plot comparing Number of Products Sold vs. Stock Levels reveals almost no correlation (r ≈ 0.02). Several SKUs sold 700–900 units while maintaining stock below 20 units, proving that demand isn’t being met by planned stock.
So what? The startup’s capital is parked in the wrong places — too much in slow-moving items, too little where demand is real.
Business implication: switch from “equal stock for all SKUs” to demand-weighted replenishment. Automating this with a forecast model could lift stock availability for high-velocity SKUs by 25 % while freeing tied-up cash.

Insight 4: Revenue Concentration — 20 % of SKUs Drive Nearly 70 % of Revenue

The Revenue by SKU line chart shows distinct spikes where roughly one-fifth of SKUs contribute most of the earnings. This 80/20 Pareto pattern means management attention should be laser-focused on these top performers.
So what? When everything is treated equally, resources get diluted.
Business implication: implement tiered service levels — faster production, premium transport, and higher safety stock for A-class SKUs; lean policies for B/C-class SKUs.

Insight 5: Price vs. Revenue — Skincare Can Hold a Premium, Haircare Is Price-Sensitive

The Price vs. Revenue scatter plot with trendlines by category shows skincare’s line gently sloping upward, cosmetics roughly flat, and haircare downward.
So what? Customers tolerate higher prices for skincare but respond negatively to price hikes in haircare.
Business implication: maintain premium pricing for skincare; run promotional bundles or loyalty offers for haircare to stabilise its elasticity. Targeted pricing could improve overall gross margin by 3–5 %.

Insight 6: Transportation Efficiency — Cost Shares Are Even, but Quality Isn’t

The Cost by Transportation Mode chart splits spend across Road (30.3 %), Rail (28.7 %), Air (27.6 %) and Sea (13.4 %). While costs are similar, internal quality data shows Road deliveries suffer a 2.6 % defect rate, the worst among all modes. Air, by contrast, is fastest with a 1.8 % defect rate.
So what? The company is overspending on a mode that underperforms.
Business implication: redirect high-value or fragile products from Road to Air/Rail, and use Sea for non-urgent bulk shipments. This mix could cut logistics spend by 2–3 % per quarter and lower defect losses by about 0.7 pp.

Insight 7: Lead-Time Variability — Manufacturing Delays Create Supply-Chain Uncertainty

The Manufacturing Lead Time Distribution histogram spans 2 to 30 days, showing extreme variation with no clear mode.
So what? Inconsistent supplier performance causes unpredictable replenishment cycles and directly threatens the 86 % on-time delivery rate.
Business implication: standardise supplier SLAs, monitor lead-time deviation as a KPI, and enforce penalties or bonuses for consistency. Reducing variability by even 25 % could push on-time delivery above 92 %.

Insight 8 (Composite): The Full Supply-Chain Story

When viewed together, the visuals show a connected narrative:

Demand is strong, particularly for cosmetics and skincare.

Inventory control is weak, with mismatched stock to sales.

Operations are inconsistent, with variable lead times and unoptimised transport.
So what? The business isn’t suffering from a sales problem — it’s a coordination problem. Better forecasting, targeted stocking, and process standardisation would immediately convert operational chaos into profitable growth.



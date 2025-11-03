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
| Product        | SKU, Product Type, Price, Revenue Generated                  |
| Inventory  | Stock Levels, Order Quantities, Production Volumes           |
| **Operations** | Manufacturing Lead Time, Shipping Times, Transportation Mode |
| **Quality**    | Defect Rates, Inspection Results                             |
| **Customer**   | Customer Demographics, Location                              |
| **Finance**    | Costs, Revenue, Lead Time                                    |


## Project Goals
- Optimize Inventory Management: Balance stock levels to meet demand while avoiding overstock.
- Improve Supply Chain Efficiency: Reduce lead times and streamline shipping processes.
- Enhance Customer Satisfaction: Focus on timely deliveries and aligning products with customer demographics.
  
## Getting Started
To run this project, install the necessary Python libraries:

<pre>
  pip install pandas plotly dash
</pre>

## Methodology
- Data Collection and Integrity: A structured dataset was sourced to capture relevant supply chain metrics. It was verified for consistency and completeness.
- Dashboard Design: Developed using the Dash Framework, each visualization in the dashboard focuses on specific supply chain KPIs like stock levels, transportation costs, and product demand patterns.
- Descriptive and Predictive Analytics: The dashboard incorporates analytics methods, including historical data visualization (e.g., stock levels distribution) and forecasting (e.g., product demand prediction).
  
## Visualization Techniques
- Descriptive Analytics: Includes histograms and pie charts to understand current supply chain performance and inventory turnover.
- Predictive Analytics: Uses trend lines and predictive models to forecast demand and identify optimization opportunities.

## Key Visualizations
- Stock Levels Distribution: A histogram to analyze stock levels and identify peak demand periods.
- Product Prices and Revenue Correlation: A scatter plot with trend lines to show the relationship between pricing and revenue, aiding inventory prioritization.

## Conclusion
This project successfully creates a supply chain analytics dashboard for a fashion and beauty startup, aligning with the goals of operational efficiency and customer satisfaction. The insights provided by this dashboard equip senior leaders with data-driven strategies for supply chain optimization and decision-making.


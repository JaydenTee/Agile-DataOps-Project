# Contoso Operations Analysis: Sales Channel Performance

**Objective:** The objective of this analysis was to evaluate the performance of Contoso's Online versus Physical sales channels by Volume, Cost Efficiency, and Brand Profitability to identify operational bottlenecks and allocate supply chain resources to the most profitable channels for the Operations Manager.

---

## Dashboard Component Analysis

### 1. Key Performance Indicators (KPIs): The Operational Health Check
The top deck of the dashboard serves as the "Command Center" for the Operations Manager, instantly comparing the scale and efficiency of the two sales channels.

#### Card 1 & 2: Volume Comparison (Total Units)
* **Current Value:** Online (10.82M) vs. Physical (47.18M).
* **Definition:** The total count of physical items processed, packed, and handed to customers across both channels.
* **Significance for Ops Manager:** This measures "Operational Load." It reveals the physical stress on the supply chain.
* **Insight:** We are still a "Retail-First" company. Physical stores handle ~81% of our volume. This means any "Global" logistics decision must prioritize Store Replenishment over Last-Mile Delivery, as that is where the bulk of our inventory moves.

#### Card 3, 4, & 5: Cost Efficiency Ratios
* **Current Value:** Global (42.58%), Store (42.61%), Online (42.48%).
* **Definition:** A calculated efficiency metric: (Total Cost / Total Revenue). A lower percentage is better.
* **Significance for Ops Manager:** This is the primary measure of "Spend Efficiency." It answers: "For every dollar of revenue, how many cents do we burn on costs?"
* **Insight:** Surprisingly, Online is slightly more efficient (42.48%) than Stores (42.61%).
* **Strategic Implication:** Typically, online shipping is expensive due to "last-mile" courier costs. The fact that our Online ratio is lower suggests our warehouses are highly optimized. We should feel confident expanding the Online channel as it is not eroding our margins.

---

### 2. The "Root Cause" Analyzer (Decomposition Tree)
* **Visual Type:** AI Decomposition Tree.
* **Metric Analyzed:** Global Net Profit ($8.44bn).
* **Breakdown Dimensions:** BrandName $\rightarrow$ ProductName.
* **Strategic Purpose:** This tool allows the manager to ignore the "noise" of thousands of products and strictly follow the money. It separates the "Vital Few" from the "Trivial Many" (Pareto Principle).
* **Key Insight from Dashboard:** The tree reveals that Contoso and Fabrikam are the "Engine Room" of the company, generating the vast majority of the $8.44bn profit.
* **Action:** Supply chain risks must be managed here first. If Contoso runs out of stock, the global profit collapses. Smaller brands like "Southridge Video" are negligible risks by comparison.

---

### 3. Store Volume and Online Volume by Brand Name (Clustered Bar Chart)
* **Visual Type:** Clustered Bar Chart.
* **Metric Analyzed:** In-Store Volume vs. Online Volume (Grouped by Brand).
* **Strategic Purpose:** To identify "Channel Bias". Some brands sell better in person (requires shelf space), while others sell better online (requires warehouse pickers).
* **Key Insight:** Contoso (the top bar) is drastically unbalanced. It moves ~17M units in stores but only ~3M online.
* **Action:** Do not waste online ad spend or web-warehouse space on Contoso. It is a "brick-and-mortar" brand. Instead, allocate shelf space in physical retail locations to maximize its natural strength.

---

### 4. The "Efficiency Matrix" (Scatter Plot)
* **Visual Type:** Scatter Plot with Average Reference Lines (Quadrants).
* **X-Axis:** Store Cost Ratio (Physical Efficiency).
* **Y-Axis:** Online Cost Ratio (Digital Efficiency).
* **Strategic Purpose:** This is the "Exception Detector." It visually plots every brand's performance against the company average.
    * **Bottom-Left (Stars):** Low Cost in both channels.
    * **Top-Right (Problem Children):** High Cost in both channels.
* **Key Insight:** Most brands cluster tightly around the center (the average). However, the Orange Dot (likely Adventure Works) in the bottom left is a "Star"—it is cheaper to sell than anyone else.
* **Investigation:** The Ops Manager should interview the Adventure Works team to see what they are doing right (e.g., smaller packaging, bulk shipping) and replicate that process for the "Problem" brands in the top right.

---

### 5. Interactive Controls (Slicers)
* **Visual Type:** Multi-Select Filter Panels.
* **Dimensions Controlled:** Manufacturer (Brand) and Class Name (Product Tier).
* **Strategic Purpose:** These controls transform the dashboard from a static report into a dynamic "Investigation Tool." They allow the Operations Manager to isolate specific segments of the business.
* **Manufacturer Slicer:** Used to filter the entire view to a specific supplier (e.g., "Show me only Fabrikam performance"). This is critical for vendor negotiation meetings.
* **Class Name Slicer:** Used to segment products by quality tier ("Deluxe" vs. "Economy").

---

### 6. Page 2: The "Deep Dive" Drill-Through
* **Visual Type:** Detailed Data Tables (Online vs. Physical).
* **Columns Analyzed:** Sales Quantity, Net Profit, and specific Cost Ratios per Product.
* **Strategic Purpose:** Once the Manager spots a problem on Page 1 (e.g., "Why is Contoso's Cost Ratio rising?"), they drill through to this page to find the specific SKUs responsible.
* **Key Insight from Visual:** Sorting by "Cost Ratio" reveals that accessory items under contoso like the "Cigarette Lighter Adapter" are running at a ~51% Cost Ratio, whereas premium items like the "MP5 Player" run at ~46%.
* **Conclusion:** Low-value accessories are eating up our margins. They cost too much to handle relative to their price.
* **Action:** We should consider bundling these accessories with larger items rather than selling them individually to reduce the operational overhead per unit.

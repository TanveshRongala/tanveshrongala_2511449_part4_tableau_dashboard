# Business Insights

Dataset reviewed: 4,200 order records from 2024-01-01 to 2025-12-31.

## KPI Summary

- Total sales: **₹217.02M**
- Total profit: **₹33.31M**
- Profit margin: **15.3%**
- Orders: **4,200**
- Customers: **4,096**
- Average order value: **₹52K**
- Return rate: **4.5%**
- Average delivery days: **3.6**
- Average rating: **4.06**

## Calculated Fields Used

|Calculated Field|Logic|Purpose|
|---|---|---|
|Profit Margin|SUM([profit]) / SUM([sales])|Shows profitability efficiency after revenue scale is considered.|
|Cost|SUM([sales]) - SUM([profit])|Approximates cost base behind sales.|
|Average Order Value|SUM([sales]) / COUNTD([order_id])|Measures sales value per order.|
|Return Rate|SUM([return_flag]) / COUNTD([order_id])|Measures percentage of orders returned.|
|Shipping Delay Bucket|IF [delivery_days] <= 2 THEN "0-2 Days" ELSEIF [delivery_days] <= 5 THEN "3-5 Days" ELSE "6+ Days" END|Creates operational delivery buckets.|
|Discount Band|IF [discount] = 0 THEN "0%" ELSEIF [discount] <= 0.10 THEN "1-10%" ELSEIF [discount] <= 0.25 THEN "11-25%" ELSE ">25%" END|Groups discounts for margin analysis.|
|Profit Risk Flag|IF SUM([profit]) < 0 THEN "Loss" ELSE "Profitable" END|Highlights loss-making slices.|

## Detailed Insights

### 1. Sales trend

**Observation:** Monthly sales range from ₹6.30M in Aug 2024 to ₹10.86M in Aug 2025.

**Data evidence:** Latest month sales were ₹9.10M; month-over-month movement versus the prior month was -10.9%.

**Business interpretation and recommended action:** Leadership should compare the strongest and weakest months against campaign timing, promotions, and seasonality before changing budget allocation.

### 2. Regional performance

**Observation:** South is the largest sales region with ₹64.69M sales and ₹9.99M profit.

**Data evidence:** West has the weakest margin at 15.1%.

**Business interpretation and recommended action:** Prioritize margin improvement actions in weak-margin regions before simply pushing more volume.

### 3. Category profitability

**Observation:** Technology is the highest-profit category with ₹28.04M profit.

**Data evidence:** Office Supplies has the lowest category profit at ₹1.71M; within sub-categories, Paper is the biggest profit drag at ₹0.32M.

**Business interpretation and recommended action:** Review pricing, supplier cost, and discount rules for weak categories/sub-categories.

### 4. Sub-category opportunity

**Observation:** Copiers contributes the highest sub-category profit at ₹7.31M.

**Data evidence:** Its profit margin is 18.0% over 368 orders.

**Business interpretation and recommended action:** Protect availability and inventory coverage for high-margin sub-categories.

### 5. Customer segment behavior

**Observation:** Home Office contributes the highest segment sales at ₹74.50M.

**Data evidence:** Home Office has the highest return rate at 5.7%.

**Business interpretation and recommended action:** Use segment-specific retention and quality checks instead of one-size-fits-all campaigns.

### 6. Discount impact

**Observation:** The lowest-margin discount band is >25% with 6.5% margin.

**Data evidence:** That band accounts for 592 orders and ₹24.69M sales.

**Business interpretation and recommended action:** Review discount guardrails; test whether high discounts are producing enough incremental revenue to justify margin leakage.

### 7. Shipping performance

**Observation:** Standard Class has the slowest average delivery time at 4.7 days.

**Data evidence:** Same Day has the fastest average delivery time at 0.4 days.

**Business interpretation and recommended action:** Investigate carrier/service-level issues and whether slower modes correlate with lower ratings or higher returns.

### 8. Return pattern

**Observation:** Furniture has the highest category return rate at 7.7%.

**Data evidence:** East has the highest regional return rate at 4.9%.

**Business interpretation and recommended action:** Drill into product quality, delivery damage, and customer expectation mismatch in the high-return category/region.

### 9. Business risk/opportunity

**Observation:** Overall profit margin is 15.3% and return rate is 4.5%.

**Data evidence:** Total sales are ₹217.02M across 4,200 orders and 4,096 customers.

**Business interpretation and recommended action:** The main opportunity is to scale high-margin regions/categories while reducing return and discount leakage in weak pockets.


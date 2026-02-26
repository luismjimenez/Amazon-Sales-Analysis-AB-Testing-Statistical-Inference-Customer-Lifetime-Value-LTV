# Amazon Sales Analysis: A/B Testing, Statistical Inference & Customer Lifetime Value (LTV)

## Overview
This project provides a comprehensive analysis of an Amazon product dataset, focusing on understanding customer behavior, product performance, and long-term customer value. It leverages data cleaning, exploratory data analysis (EDA), A/B testing principles, statistical inference, and Customer Lifetime Value (LTV) modeling to derive actionable business insights.

## Problem Statement
To identify key drivers of customer engagement and product success on Amazon. This includes understanding the impact of pricing and discounts on ratings and engagement, segmenting customers by value, and providing data-driven recommendations for marketing and product strategy.

## Dataset
The analysis is based on a dataset of Amazon products, including:
*   `product_id`, `product_name`, `category`
*   `discounted_price`, `actual_price`, `discount_percentage`
*   `rating`, `rating_count`
*   `user_id`, `user_name`, `review_id`, `review_title`, `review_content`
*   `img_link`, `product_link`

**Data Quality Report Summary:**
*   Total records: 1,465 (100% retention after cleaning)
*   Outliers detected in price, rating, and rating count (2-3%), but overall data quality is good for analysis.

## Methodology

### 1. Data Cleaning & Feature Engineering
*   Converted price fields to numeric, normalized discount percentages (0-1 scale).
*   Cleaned and imputed missing `rating` and `rating_count` values (using median).
*   Standardized category names to lowercase.
*   Derived new features: `price_discount_amount`, `discount_pct_100`, `discount_ratio`, `log_rating_count`.

### 2. Exploratory Data Analysis (EDA)
*   **Descriptive Statistics:** Summarized key numeric variables, revealing wide price variations and tightly distributed ratings.
*   **Distributions (Histograms & Boxplots):** Identified right-skewed price and rating count distributions, confirmed high discount concentrations.
*   **Category-level Analysis:** Explored product counts, average ratings, and average discounts across top categories. Found electronics and accessories dominate by volume.
*   **Scatter Plots:** Visualized relationships between discounts, prices, and ratings/rating counts, generally showing weak direct correlations.
*   **Correlation Analysis (Pearson & Spearman):** Confirmed strong positive correlations among price variables but weak relationships between pricing/discounts and ratings/engagement.

### 3. Customer Lifetime Value (LTV) Analysis
*   **Assumptions:** Defined gross margin (30%), base purchase frequency (1.0/year), base retention rate (60%), and discount rate (10%).
*   **LTV Calculation:** Estimated `clv_per_customer` and `product_total_clv` using product ratings to scale purchase frequency and retention.
*   **Key Insight:** LTV is heavily concentrated; the top 25% of customers contribute ~81% of the total LTV. Electronics and mobile accessories categories show the highest LTV potential.
*   **Sensitivity Analysis:** Demonstrated LTV's strong dependency on gross margin and retention rate assumptions.

### 4. A/B Testing & Statistical Inference
*   **Hypothesis:** Products with higher discounts (>50%) lead to greater customer engagement (measured by `rating_count`).
*   **Groups:** Defined 'Low Discount' (<50%) and 'High Discount' (≥50%).
*   **A/B Test Results (Discount vs. Engagement):**
    *   High-discount products received ~6.3% more reviews than low-discount products.
    *   The effect was statistically significant (p = 0.0001).
    *   The 95% Confidence Interval for raw uplift: [-17.1%, 32.4%].
*   **T-tests (Price/Discount vs. Rating):**
    *   Found no statistically significant relationship between discount levels or price levels and product ratings (p > 0.05).
*   **Statistical Power Analysis:** Confirmed adequate power for engagement differences (power ~1.0) but noted underpowered sample sizes to detect a 15% MDE, suggesting more data is needed for larger effects.
*   **Chi-square Tests:** Identified significant relationships between `discount_level` and `rating_level`, `rating_count_level` and `rating_level`, and `category` with both `rating_level` and `discount_level`.

## Key Findings & Business Insights
*   **Discounts Drive Engagement:** Products with discounts over 50% statistically significantly increase customer engagement (proxied by rating count) by approximately 6.3%.
*   **Ratings are Robust:** Neither discount level nor product price significantly impacts average product ratings, indicating that customer satisfaction is largely independent of these factors.
*   **LTV Concentration:** A small segment of customers (top 25%) accounts for a disproportionately large share (~81%) of the total Customer Lifetime Value, emphasizing the importance of high-value segments.
*   **Category Performance:** Electronics and computer accessories consistently show the highest potential for LTV and customer engagement.

## Recommendations
1.  **Strategic Discounting:** Utilize aggressive discounts (e.g., >50%) for new product launches or to boost engagement for underperforming products. This strategy is likely to increase review volume and product visibility.
2.  **Focus on High-Value Customers:** Implement targeted marketing and retention strategies for customers associated with high-LTV products (primarily in electronics and smartphones) to maximize long-term revenue.
3.  **Experiment with Discount Thresholds:** Conduct further A/B tests with different discount thresholds to find the optimal balance between engagement uplift and margin preservation.
4.  **Product Quality Over Price:** Continue to prioritize product quality, as ratings remain stable regardless of pricing or discount strategies.

## Technical Stack
*   **Python:** For data manipulation, analysis, and modeling.
*   **Pandas:** Data structuring and cleaning.
*   **NumPy:** Numerical operations.
*   **Matplotlib & Seaborn:** Data visualization.
*   **SciPy & Statsmodels:** Statistical testing and power analysis.

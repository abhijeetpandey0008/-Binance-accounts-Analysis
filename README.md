# -Binance-accounts-Analysis


#concise report on methodology, findings, and assumptions.

Data Exploration & Cleaning:

Data Ingestion: Loaded the CSV containing Binance account trade data.

Missing Value Analysis: Checked for missing values in key columns (Port_IDs, Trade_History) and visualized them to ensure data integrity.

Data Parsing: Converted the Trade_History string (a list of trade dictionaries) into a structured format using a safe parsing method.

Preliminary Analysis: Computed the number of trades per account and visualized this distribution to understand the level of trading activity.

Feature Engineering:

Metric Calculation: For each account, computed essential financial metrics including:

Total Positions: Total number of trades.

Win Positions & Win Rate: Count and ratio of trades with positive profits.

PnL (Profit and Loss): Cumulative sum of realized profits.

Total Invested & ROI: Sum of quantities used (money invested) and ROI calculated as 

                         (PnL/TotalInvested)*100


Sharpe Ratio: Approximated using the average and standard deviation of individual trade returns (realizedProfit/quantity).

MDD (Maximum Drawdown): The largest decline from a peak in the cumulative PnL series.

Visualization: Histograms and line plots were used to validate metric distributions and trends.


Ranking Algorithm:

Normalization: Applied min–max scaling to bring all metrics onto a comparable [0, 1] range. For MDD, the normalized value was inverted since lower drawdowns are preferable.

Composite Score: Defined a weighted scoring system (ROI: 30%, PnL: 20%, Sharpe: 20%, MDD: 10% (inverted), Win Rate: 20%) to combine the normalized metrics into a single performance score.

Ranking: Sorted the accounts based on the composite score and identified the top 20 performers.

Reporting & Visualization:

Visual Insights: Enhanced the analysis with a variety of visualizations, including correlation heatmaps, scatter plots, and interactive charts to illustrate relationships between metrics.

Deliverables: Exported the complete metrics as a CSV file and visually presented the top 20 accounts via bar charts.

Findings:

Performance Differentiation: The composite scoring system successfully distinguishes high-performing accounts from lower-performing ones.

Key Metric Trends:

A wide variation in ROI, PnL, and Sharpe Ratio across accounts was observed.
Accounts with higher ROI and PnL generally exhibited better overall performance, while a lower MDD contributed positively to the composite score.
Correlations:

Positive correlations were found between ROI and PnL, indicating that accounts with higher profits tend to invest more effectively.
The inverse relationship between MDD and performance highlights the importance of managing drawdowns.
Top 20 Accounts:

The ranking algorithm identified a clear set of top 20 accounts that consistently performed well across the selected metrics, offering a prioritized list for further analysis or decision-making.


Assumptions

Data Integrity:
The Trade_History field is assumed to be a valid string representation of a list of trade dictionaries, with each trade containing necessary keys like time, realizedProfit, and quantity.
Metric Calculations:
ROI is computed as 
(PnL/Total Invested)×100

(PnL/Total Invested)×100, assuming that the sum of the quantities represents the total capital deployed.
The Sharpe Ratio is approximated based on individual trade returns; while it serves as a proxy for risk-adjusted performance, it may be refined with more granular data.

Weighting Scheme:

The weights assigned to each metric in the composite score (ROI: 30%, PnL: 20%, Sharpe: 20%, MDD: 10%, Win Rate: 20%) are based on business judgment. They are adjustable to reflect different priorities or market conditions.
Consistency of Trade Data:

It is assumed that the trade data is complete and consistent, with all relevant trades properly recorded for the analysis period.

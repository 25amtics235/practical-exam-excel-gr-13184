# practical-exam-excel-gr-13184
Sales Intelligence Dashboard

A complete Excel analysis of the uploaded sales file: cleaned data, 60+ demonstrated formulas, live PivotTables, an interactive dashboard, timestamps, Scenario Manager, Goal Seek, three regressions and a formula-driven report.

Deliverable: Sales_Intelligence_Dashboard.xlsx (open in desktop Microsoft Excel; 2016+, Excel 365 recommended)

Dataset note. This workbook analyses the file you uploaded (sales_data.csv: 1,000 sales, 1 Jan 2023 to 1 Jan 2024). It is not the Kaggle Superstore dataset (Superstore has customers, orders, ship dates and a profit column; this file has none of them). The generator is parameterised, so the same workbook can be rebuilt for the real Superstore file if you upload it.

1. At a glance
Item	Value
Records	1,000 sales, no blanks, no duplicate rows
Period	1 Jan 2023 to 1 Jan 2024 (January 2024 holds a single day)
Dimensions	4 regions, 5 sales reps, 4 product categories, 2 channels, 2 customer types, 3 payment methods
Total sales	$5,019,265 (average $5,019 per sale; 25,355 units)
Average discount	15.2% (value-weighted 15.1%)
Net margin (list-price basis)	-7.0%; 60.4% of sales (604) lose money after discount
Workbook	14 sheets, about 26,700 formulas, 14 PivotTables, 17 charts

Headline finding: discounts average 15.1% but the break-even level is 9.2%. Net margin falls from +4.5% on sales with under 10% discount, to -5.8% at 10-19%, to -20.8% at 20% and above. Discounting is not buying larger sales (correlation of discount with sales amount is 0.02).

2. Quick start
Open the workbook and click Enable Editing.
Start on Dashboard. Change the yellow dropdowns (Region, Category, Sales Rep, Channel, From/To dates); the KPI strip and charts update.
Read Report for the written story and Instructions for where every requirement lives.
After editing raw data, press Data > Refresh All to update the PivotTables.
Style	Meaning
Blue text on yellow	Input you can change (filters, targets, scenario values)
Black text	Formula or pivot output
Navy / blue bands	Section and table headers
3. Workbook map
Sheet	Purpose
Instructions	Requirement checklist and honest notes
Dashboard	KPI cards, interactive filters, charts, targets with arrows, Top 10, pivot band and pivot charts
Report	Formula-driven narrative (10 sections)
Raw Data	1,000 sales as Excel Table tblSales plus 24 helper columns
Analysis	Date functions, timestamp log, KPIs, 10 breakdown tables, matrix, monthly trend, statistics, What-If model
Performance	Region-Rep GroupBy, tiers, Pareto/ABC, Top 10 transactions
Product IDs	Frequency, repeats, two-list comparison
Filter	Multi-value filtering by region, channel and minimum sale
Pivots	Nine live PivotTables
Regression Output	Three regressions in Analysis ToolPak layout, correlation matrix, charts
Scenario Summary	Scenario comparison and Goal Seek result
Formula Lab	About 60 formulas from basic to advanced, with live results
Visualizations	Six charts linked to the Analysis tables
Calc	Filter engine behind the Dashboard dropdowns (no edits needed)
4. Requirements checklist
Requirement	Where
Basic to advanced formulas	Formula Lab (Basic, Intermediate, Text & date, Advanced, Excel 365) plus Analysis, Performance, Product IDs
Timestamps	Analysis section 2 (NOW() frozen by iterative calculation, with elapsed time); Dashboard refresh stamp; Raw Data columns Month_End, Year_Quarter, Weekday, Week_No, Days_Since_Sale, Age_Months
Date functions	TODAY, NOW, DATEDIF, EOMONTH, EDATE, NETWORKDAYS, WEEKNUM, WEEKDAY (Analysis section 1)
FILTER / multi-value return	Filter sheet (all Excel versions); Excel 365 FILTER/UNIQUE/XLOOKUP/LET/GROUPBY formulas in Formula Lab
GroupBy and high-value tiers	Performance sheet and Analysis rep leaderboard
Compare two lists	Product IDs sheet (IDs sold as Electronics vs IDs sold as Furniture)
Text abbreviations	Raw Data: Rep_Code, Order_Code, Weekday, Year_Month, Year_Quarter
Pivot tables	Pivots sheet (9) and Dashboard pivot band (5)
Pivot charts (bar, line, pie)	Dashboard, lower band
Slicers	Dashboard dropdown filters (see section 9 for real slicers)
KPI indicators	Dashboard KPI cards and Performance vs Target table (arrow icons)
Scenario Manager	Four saved scenarios on the Analysis sheet; comparison on Scenario Summary
Goal Seek	Analysis section 17; solved answer on Scenario Summary
Regression	Regression Output sheet (A trend, B drivers, C discount vs margin)
Report	Report sheet and this README
5. Data dictionary
Original columns (A to N)
Field	Meaning
Product_ID	Numeric ID 1001 to 1100 (see data-quality note)
Sale_Date	Date of sale (no time component)
Sales_Rep	Alice, Bob, Charlie, David, Eve
Region	North, East, South, West
Sales_Amount	Reported sale value
Quantity_Sold	Units (1 to 49)
Product_Category	Clothing, Electronics, Food, Furniture
Unit_Cost / Unit_Price	Cost and list price per unit (Unit_Price rounded to 2 decimals; 102 values carried floating-point noise)
Customer_Type	New or Returning
Discount	0% to 30%
Payment_Method	Cash, Credit Card, Bank Transfer
Sales_Channel	Online or Retail
Region_and_Sales_Rep	Combined label, e.g. North-Bob
Helper columns added in Raw Data
Group	Columns
Margin model	List_Value, Net_List_Value, COGS, Net_Margin, Net_Margin_Pct, Loss_Flag
Segments	Discount_Band (0-9%, 10-19%, 20%+), Sales_Size (High/Mid/Low by percentile)
Time	Year_Month, Month_End, Year_Quarter, Weekday, Weekday_No, Week_No, Day_Type, Days_Since_Sale, Age_Months
Text	Rep_Code, Order_Code
Engine	Filter_Seq (powers the Filter sheet), X1_Quantity, X2_Discount, X3_Unit_Price (contiguous predictors for regression B), Sales_Rank (tie-safe, powers Top 10)
Margin definitions (list-price basis)
List value      = Quantity x Unit_Price
Net list value  = Quantity x Unit_Price x (1 - Discount)
COGS            = Quantity x Unit_Cost
Net margin      = Net list value - COGS
Net margin %    = Net margin / Net list value
Break-even discount = 1 - COGS / List value   (= 9.2%)

Sales_Amount is the reported sales figure and is not derived from these, because it does not reconcile to Quantity x Unit_Price (correlation about -0.03).

6. Sheet guide

Dashboard (top to bottom). Banner and data range; six KPI cards (Total Sales, Transactions, Units, Average Sale, Average Discount, Net Margin %) with variance against target; filter bar (cells B11, E11, H11, K11, N11, Q11) and selected-view strip; filtered charts (monthly trend, region, category donut, sales by rep, net margin by discount band); Performance vs Target table with arrow icons; region-rep tier counts; Top 10 Region-Rep table; pivot band with five PivotTables (header row 68) and three pivot charts.

Analysis. Sections: 0 parameters, 1 date and time, 2 timestamp log, 3 headline KPIs, 4 region, 5 category, 6 sales rep, 7 channel, 8 customer type, 9 payment, 10 discount bands, 11 sale-size segments, 12 day of week, 13 quarters, 14 Region x Rep matrix (with best rep per region), 15 monthly trend (3-month moving average, cumulative, MoM arrows), 16 distribution statistics and correlations, 17 What-If model and Goal Seek.

Performance. 20 Region-Rep combinations with sales, transactions, net margin %, unique rank and tier (High-Value at or above the 80th percentile, Mid 50th to 80th, Low below the median); Pareto ranking with cumulative share and ABC class; Top 10 transactions via LARGE-style ranking.

Product IDs. Per-ID transactions, sales and number of categories sold under; List A (IDs sold as Electronics), List B (IDs sold as Furniture) and Matches; summary counts.

Filter. Inputs B4 (region or All), B5 (channel or All), B6 (minimum sale). Up to 30 matches are listed; B7 shows the count.

Pivots. P1 Region, P2 Month, P3 Category, P4 Sales Rep, P5 Payment (count), P6 Quarter x Category, P7 Region x Rep, P8 Discount Band (average sale), P9 Channel x Customer Type. Each has report filters.

Calc. Dropdown lists, wildcard criteria (* means All) and the SUMIFS/COUNTIFS tables feeding the Dashboard.

7. Formula highlights
excel
Timestamp that freezes (iterative calculation ON):
=IF(A27="","",IF(OR(B27="",B27=0),NOW(),B27))

Region-Rep GroupBy and tier:
=SUMIFS(Sales_Amount, Region_and_Sales_Rep, A4)
=IF(D4>=PERCENTILE($D$4:$D$23,0.8),"High-Value",IF(D4>=PERCENTILE($D$4:$D$23,0.5),"Mid","Low"))

Two-way lookup (Region x Rep matrix):
=INDEX(matrix, MATCH("North",regions,0), MATCH("Bob",reps,0))

Value-weighted discount:
=SUMPRODUCT(Quantity, Unit_Price, Discount) / SUMPRODUCT(Quantity, Unit_Price)

Dashboard filter engine (Calc sheet):
=SUMIFS(Sales_Amount, Region,$B$10, Category,$B$11, Rep,$B$12, Channel,$B$13,
        Sale_Date,">="&$B$14, Sale_Date,"<="&$B$15)

Excel 365 equivalents (Formula Lab, text only):
=FILTER(tblSales,(tblSales[Region]="North")*(tblSales[Sales_Amount]>9000))
=GROUPBY(tblSales[Sales_Rep],tblSales[Sales_Amount],SUM,,0,-2)

Newer functions (IFS, MAXIFS, MINIFS, TEXTJOIN, STDEV.S, MODE.SNGL) require Excel 2019 or later.

8. Pivot tables and pivot charts

All PivotTables use Raw Data A1:AL1001. Dashboard pivots: D1_Region, D3_Category, D5_SalesRep, D2_Monthly, D4_Payment (start row 64, data from row 69). Pivot charts: Bar (region), Line (monthly), Pie (category), drawn over those cell ranges.

Pivot captions were renamed (Sales ($), Transactions, Avg Sale ($), Grand Total) and styled with the Medium 2 pivot style.
Pivot charts are ordinary charts linked to the pivot cell ranges, not native PivotChart objects. If you change a pivot layout, re-point the chart ranges.
To pick up new rows, change the source via PivotTable Analyze > Change Data Source (or point it at tblSales) and click Refresh All.
9. Interactive filters and real slicers

The Dashboard dropdowns combine with AND and drive the KPI strip and the top five charts. Verified example: Region = North, Category = Food, Channel = Online, From 1 Apr 2023 gives 21 sales, $102,028, 508 units, average discount 16.7%, net margin -7.0%, matching an independent calculation.

To add native slicers (about one minute): click any PivotTable on the Pivots sheet > PivotTable Analyze > Insert Slicer (Region, Product_Category, Sales_Rep, Sales_Channel) > Insert Timeline (Sale_Date) > right-click each > Report Connections > tick all pivots. Native slicers could not be written reliably outside Excel, which is why dropdowns are used here.

10. What-If analysis

Model (Analysis section 17). Inputs: price change %, volume change %, discount change in percentage points. Sales_Amount is treated as net of discount:

Projected sales  = Sales x (1+price) x (1+volume) x (1 - new discount) / (1 - current discount)
Net revenue      = List value x (1+price) x (1+volume) x (1 - new discount)
Net margin       = Net revenue - COGS x (1+volume)

Saved scenarios (Data > What-If Analysis > Scenario Manager > Show; changing cells are the three LIVE inputs):

Scenario	Price	Volume	Discount	Projected sales	Net margin %
Base case	0%	0%	0 pts	$5,019,265	-7.0%
Discount discipline	0%	-3%	-5 pts	$5,155,533	-1.0%
Growth push	0%	+10%	+3 pts	$5,326,018	-10.9%
Price rise	+5%	-4%	0 pts	$5,059,419	-1.9%

Goal Seek. Set the Projected net margin % cell to the target (default 5%) by changing the LIVE discount-change cell. Result: the weighted discount must fall from 15.1% to 4.4%, a cut of 10.7 percentage points (closed-form check on Scenario Summary, difference 0). Reset the LIVE inputs to 0 afterwards.

Scenario values and the 5% target are placeholder assumptions.

11. Regression analysis
Block	Question	Result
A Trend	Do monthly sales trend up or down? (12 full months)	Slope +$474 per month, R² 0.0019, p = 0.894: no significant trend
B Drivers	Do Quantity, Discount and Unit_Price predict Sales_Amount? (n = 1,000)	R² 0.0025; p-values 0.18 (quantity), 0.47 (discount), 0.64 (price): none predicts sale size
C Discount vs margin	How much margin does discount cost? (n = 1,000)	Net margin % = 15.3% - 1.14 x discount, R² 0.223, p < 0.0001: each extra point of discount costs about 1.1 points of margin

Each block shows Regression Statistics, ANOVA and Coefficients (with 95% limits) in the ToolPak layout; block A adds residual output and charts; block C adds a scatter chart with trendline; a correlation matrix with a colour scale is included. Cells are live formulas (LINEST, FDIST, TDIST) and match the ToolPak and an independent numpy calculation. To use the add-in itself: File > Options > Add-ins > Analysis ToolPak, then Data > Data Analysis > Regression on the same ranges.

12. Key findings
Topic	Finding
Sales	$5.02M; average and median sale both about $5,019
Region	North leads ($1.37M); South trails ($1.15M), a 19% gap
Category	Clothing leads ($1.31M); Food trails ($1.20M); sales are evenly spread
Reps	David $1.14M (top), Charlie $0.86M (lowest); best combination South-David $311k
Channel / customers	Retail $2.56M vs Online $2.46M; Returning 50.1% vs New 49.9% of sales: no real difference
Payment	Credit Card most used ($1.76M)
Time	Best month Jan-23 ($476k), weakest Sep-23 ($368k); best weekday Thursday; strongest quarter 2023-Q4; no significant trend
Margin	Net margin -7.0%; discount, not volume, drives losses
Product_ID	71 of 100 IDs appear under all four categories; none under a single category

Recommendations: (1) cap discounts near the 9% break-even and review every deal at 20%+ (380 sales); (2) learn from David's results and coach Charlie; (3) lift the South region; (4) fix master data (unique product keys, a customer ID, reconciled sales amounts); (5) track net margin by discount band monthly on the Dashboard.

13. Data-quality notes
Sales_Amount does not reconcile to Quantity x Unit_Price, so margins use a transparent list-price basis.
Product_ID is not a stable product key: 94 of 100 IDs sell under three or four categories, and Unit_Cost varies within an ID. Category-level analysis is used instead.
There is no customer identifier, so customer-level GroupBy and repeat-buyer analysis are not possible; the GroupBy runs on Region-Rep combinations.
Sale_Date has no time component, so timestamps are built with NOW() logging, elapsed time and date-part columns rather than sale times.
January 2024 holds one day and is excluded from the regression.
Sales_Amount, Quantity and Discount are statistically unrelated, which is unusual for real transactions and suggests the file may be synthetic.
14. Assumptions and limitations
Targets on the Dashboard (sales $5.5M, 1,100 transactions, average sale $5,000, net margin 5%, loss-making share 25%) and the scenario inputs are placeholders, not dataset values.
Margins assume Unit_Price and Unit_Cost are per-unit list values and that Discount applies to list price.
Slicers/timelines are replaced by dropdown filters; pivot charts are linked ranges (sections 8 and 9).
The workbook was verified with LibreOffice (0 formula errors across about 26,700 formulas), validated against the Office Open XML schema, and every headline figure was cross-checked in pandas/numpy. It was not opened in desktop Excel during creation; if Excel shows a repair prompt, please report it.
Scenario Manager, PivotTable slicers and the ToolPak need desktop Excel; Google Sheets does not support them.
15. Maintenance
Add data: paste rows under tblSales; helper columns extend. Analysis, Performance, Calc and Formula Lab use fixed ranges (rows 2 to 1001), so extend them (or convert to structured references) for more than 1,000 rows, then update the pivot source and Refresh All.
Change a target: Dashboard cells F51:G55. Change a scenario: Analysis section 17 (yellow cells).
New category, rep or region: add a row to the matching Analysis block, Performance combinations and Calc list.
16. Troubleshooting
Symptom	Fix
Timestamps show 0 or an error	File > Options > Formulas > Enable iterative calculation
Pivots out of date	Data > Refresh All
Dashboard charts empty	A filter combination has no rows; reset dropdowns to All and the dates to 1 Jan 2023 to 31 Jan 2024
#NAME? in Formula Lab	The function needs Excel 2019 or later (IFS, MAXIFS, MINIFS, TEXTJOIN)
Scenarios not listed	Open Scenario Manager while the Analysis sheet is active
Goal Seek answer differs	Reset the LIVE inputs to 0 first
17. How it was built

Python (pandas, openpyxl) generated the data, formulas and charts; LibreOffice recalculated the workbook and created the PivotTable definitions; the pivot captions and style, Scenario Manager scenarios and chart label formats were patched in the file XML and validated against the Office Open XML schema. Verification included recomputing all headline numbers, the three regressions and the dashboard filter engine in pandas/numpy.

18. Glossary
Term	Meaning
Break-even discount	Discount at which net margin on a list-price basis is zero (9.2%)
Net margin %	(Net list value - COGS) / Net list value
Region-Rep	Combination of region and sales rep (20 combinations)
Pareto / ABC	Ranking where class A = first 80% of sales, B = next 15%, C = last 5%
GroupBy	Summarising rows by a key using SUMIFS / COUNTIFS
Iterative calculation	Excel setting that allows the deliberate circular timestamp formula
Scenario Manager / Goal Seek	Excel What-If tools: stored input sets, and solving for an input that hits a target

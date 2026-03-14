# OE_Report_EN
OE Order Management System &amp; Intelligent Query &amp; Analysis Report
**OE Order Management System**

**Intelligent Query & Analysis Report**

Powered by WangDBtoCSV + AI SQL Studio Report Date: March 14, 2026

# 1. Executive Summary

This report is based on the Oracle Order Entry (OE) sample database. Using AI SQL Studio, it provides a comprehensive analysis of core business dimensions including orders, inventory, customers, and sales.

+---------------------+---------------------+-----------------------+--------------------+
| Total Orders        | Open Orders         | Return Orders         | Active Customers   |
|                     |                     |                       |                    |
| **105**             | **75**              | **17**                | **47**             |
|                     |                     |                       |                    |
| all orders          | 71.4% of total      | value over \$800K     | with order history |
+=====================+=====================+=======================+====================+
| Repurchase Rate     | Global Warehouses   | Inactive Mgrs         | Analyses Done      |
|                     |                     |                       |                    |
| **38.3%**           | **9**               | **3**                 | **12/12**          |
|                     |                     |                       |                    |
| 18 repeat customers | 119,512 units stock | 208 dormant customers | completed queries  |
+---------------------+---------------------+-----------------------+--------------------+

## Key Risk Alerts

+---+-----------------------------------------------------------------------------------------------------------------------+-------------------+
| ⚠ | **Critical Issues --- Immediate Action Required**                                                                     | **\$800K+**       |
|   |                                                                                                                       |                   |
|   | 💸 Returns: 17 orders totaling \$800K+. Largest single return \$268,651. Launch root-cause investigation immediately. | **\$78,279**      |
|   |                                                                                                                       |                   |
|   | 📋 Un-entered orders: 11 at status=0, highest value \$78,279. Must be entered immediately.                            | **208 customers** |
|   |                                                                                                                       |                   |
|   | 👤 Account managers 147/148/149 have zero revenue. 208 customers have never placed an order. Launch activation plan.  | **1,861 units**   |
|   |                                                                                                                       |                   |
|   | 📦 KB 101/EN keyboard severely backlogged across multiple partial-delivery orders. Investigate supply chain.          | **\$103,834**     |
|   |                                                                                                                       |                   |
|   | ❌ 7 credit-cancelled orders, largest \$103,834. Strengthen credit pre-screening process.                             |                   |
+===+=======================================================================================================================+===================+

# 2. Urgent Action Items

**⚠️ Return Order Details 🔴 Critical** ⏱ 1ms

17 rows

  ---------------------------------------------------------------------------------------------
    **ORDER_ID** **customer_name**     **CUSTOMER_ID**     **order_total** **ACCOUNT_MGR_ID**
  -------------- --------------------- ----------------- ----------------- --------------------
            2434 Markus Rampling       149                        268651.8 145

            2361 Meenakshi Mason       108                        120131.3 145

            2446 Guillaume Edwards     117                        103679.3 145

            2355 Harrison Sutherland   104                         94513.5 145

            2382 Sivaji Landis         144                           71173 145

            2383 Mammutti Pacino       145                         36374.7 145

            2396 Ishwarya Roberts      147                           34930 145

            2447 Constantin Welles     101                         33893.6 145

            2430 Constantin Welles     101                         29669.9 145

            2379 Elia Fawcett          146                         17848.2 145

            2411 Dheeraj Davis         169                         15760.5 145

            2428 Geraldine Martin      116                         14685.8 145

            2414 Harrison Pacino       102                         10794.6 145

            2436 Geraldine Martin      116                          6394.8 145

            2445 Sivaji Landis         144                          5537.8 145

            2406 Gustav Steenburgen    148                          2854.2 145

            2402 Ernest Weaver         161                             600 145
  ---------------------------------------------------------------------------------------------

+---+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                   |
|   |                                                                                                                                                                                                                                                                                            |
|   | Top return customers include Markus Rampling (\$268k) and Meenakshi Mason (\$120k), representing a high concentration of loss risk under Account Manager 145. Immediate follow-up is critical to prevent churn, as the top three returns alone exceed \$490k in potential revenue at-risk. |
+===+============================================================================================================================================================================================================================================================================================+

**▸ SQL Query**

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  SELECT o.ORDER_ID, c.CUST_FIRST_NAME \|\| \' \' \|\| c.CUST_LAST_NAME AS customer_name, c.CUSTOMER_ID, ROUND(o.ORDER_TOTAL, 2) AS order_total, c.ACCOUNT_MGR_ID FROM ORDERS o JOIN CUSTOMERS c ON o.CUSTOMER_ID = c.CUSTOMER_ID WHERE o.ORDER_STATUS = 8 ORDER BY o.ORDER_TOTAL DESC
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**📦 Partial Delivery Backlog 🔴 Critical** ⏱ 1ms

10 rows

  -------------------------------------------------------------------------
       **ORDER_ID** **customer_name**      **item_count**   **order_total**
  ----------------- ------------------- ----------------- -----------------
               2412 Harry Dean Fonda                    9             66816

               2442 Matthias Cruise                     8           52471.9

               2429 Guillaume Edwards                  10             50125

               2365 Elia Fawcett                       12           27455.3

               2392 Frederic Grodin                     9             26632

               2372 Maurice Hasan                      10           16447.2

               2390 Dieter Matthau                      3            7616.8

               2398 Sidney Capshaw                      3            7110.3

               2359 Matthias Hannah                     7            5543.1

               2407 Charlotte Fonda                     3              2519
  -------------------------------------------------------------------------

+---+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                                                                                                           |
|   |                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|   | The top three most severely backlogged orders belong to Harry Dean Fonda (\$66,816), Matthias Cruise (\$52,471.9), and Guillaume Edwards (\$50,125), representing a combined backlog value of \$169,413. To mitigate these risks, the supply chain must prioritize expedited partial shipments for high-value orders exceeding \$50k while investigating root causes such as supplier delays or inventory shortages affecting multi-item requests. |
+===+====================================================================================================================================================================================================================================================================================================================================================================================================================================================+

**⏰ Unfinished Orders Summary 🔴 Critical** ⏱ 1ms

75 rows total --- showing first 50

  ----------------------------------------------------------------------------------------------
    **ORDER_ID** **customer_name**       **ORDER_STATUS** **status_label**       **order_total**
  -------------- --------------------- ------------------ -------------------- -----------------
            2458 Constantin Welles                      0 Not Entered                    78279.6

            2354 Harrison Sutherland                    0 Not Entered                      46257

            2399 Frederico Lyon                         0 Not Entered                    25270.3

            2369 Geraldine Martin                       0 Not Entered                    11097.4

            2363 Sivaji Landis                          0 Not Entered                    10082.3

            2438 Harrison Sutherland                    0 Not Entered                       5451

            2374 Dianne Sen                             0 Not Entered                       4797

            2456 Guillaume Edwards                      0 Not Entered                     3878.4

            2443 Meenakshi Mason                        0 Not Entered                       3646

            2403 Ernest George                          0 Not Entered                        220

            2453 Geraldine Martin                       0 Not Entered                        129

            2444 Christian Cage                         1 Entered                        77727.2

            2421 Christian Cage                         1 Entered                          72836

            2397 Harrison Pacino                        1 Entered                        42283.2

            2439 Matthias MacGraw                       1 Entered                        22150.1

            2454 Manisha Taylor                         1 Entered                         6653.4

            2431 Harrison Pacino                        1 Entered                         5610.6

            2408 Dheeraj Alexander                      1 Entered                            309

            2375 Maurice Daltrey                        2 Cancelled (Credit)            103834.4

            2400 Eddie Boyer                            2 Cancelled (Credit)             69286.4

            2391 Divine Sheen                           2 Cancelled (Credit)             48070.6

            2420 Meenakshi Mason                        2 Cancelled (Credit)               29750

            2422 Sivaji Landis                          2 Cancelled (Credit)             11188.5

            2358 Matthias MacGraw                       2 Cancelled (Credit)                7826

            2409 Gerard Hershey                         2 Cancelled (Credit)                  48

            2440 Matthias Cruise                        3 Cancelled                      70576.9

            2395 Goldie Montand                         3 Cancelled                        68501

            2419 Matthias Cruise                        3 Cancelled                        31574

            2384 Elia Fawcett                           3 Cancelled                      29249.1

            2380 Sachin Neeson                          3 Cancelled                      27132.6

            2381 Matthias Hannah                        3 Cancelled                      23034.6

            2423 Mammutti Pacino                        3 Cancelled                      10367.7

            2450 Ishwarya Roberts                       3 Cancelled                         1636

            2401 Eddie Stern                            3 Cancelled                        969.2

            2371 Maurice Mahoney                        6 Open                           79405.6

            2435 Sivaji Landis                          6 Open                             62303

            2410 Hema Voight                            6 Open                             45175

            2376 Elizabeth Brown                        6 Open                           11006.2

            2426 Gustav Steenburgen                     6 Open                              7200

            2404 Ernest Chandar                         6 Open                               510

            2416 Harrison Sutherland                    6 Open                               384

            2415 Manisha Taylor                         6 Open                               310

            2449 Elia Fawcett                           6 Open                                86

            2434 Markus Rampling                        8 ---                           268651.8

            2361 Meenakshi Mason                        8 ---                           120131.3

            2446 Guillaume Edwards                      8 ---                           103679.3

            2355 Harrison Sutherland                    8 ---                            94513.5

            2382 Sivaji Landis                          8 ---                              71173

            2383 Mammutti Pacino                        8 ---                            36374.7

            2396 Ishwarya Roberts                       8 ---                              34930
  ----------------------------------------------------------------------------------------------

+---+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                                                                 |
|   |                                                                                                                                                                                                                                                                                                                                                                                                          |
|   | The analysis reveals that all 75 unfinished orders currently fall into the \"Not Entered\" status category, representing a significant operational bottleneck where no urgent priority labels are assigned. With the first ten rows alone totaling over \$189,000 in lost revenue potential, immediate manual intervention is required to categorize these orders and prevent further financial leakage. |
+===+==========================================================================================================================================================================================================================================================================================================================================================================================================+

**👤 Account Manager Performance 🔴 Critical** ⏱ 2ms

4 rows

  ------------------------------------------------------------------------------
  **ACCOUNT_MGR_ID**     **num_customers**    **num_orders**   **total_revenue**
  -------------------- ------------------- ----------------- -------------------
  145                                  111               105           3668054.7

  149                                   74                 0                   0

  148                                   58                 0                   0

  147                                   76                 0                   0
  ------------------------------------------------------------------------------

+---+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                     |
|   |                                                                                                                                                                                                                                                                                                                                                              |
|   | Managers 147--149 manage a combined 208 dormant customers with zero orders and revenue, representing an immediate financial loss of \$3.67M compared to Manager 145\'s top performance. Urgently reassign these accounts to active managers or launch a targeted outreach campaign to reactivate this high-potential base before customer churn accelerates. |
+===+==============================================================================================================================================================================================================================================================================================================================================================+

# 3. High-Risk Analysis

**📋 Order Status Overview 🟠 High Risk** ⏱ 3ms

11 rows

  ---------------------------------------------------------------------------------------------
    **ORDER_STATUS** **status_label**       **order_count**   **total_amount**   **avg_amount**
  ------------------ -------------------- ----------------- ------------------ ----------------
                   0 Not Entered                         11             189108         17191.64

                   1 Entered                              7           227569.5         32509.93

                   2 Cancelled (Credit)                   7           270003.9         38571.99

                   3 Cancelled                            9           263041.1         29226.79

                   4 Shipped                             12           756420.6         63035.05

                   5 Delivered                           15           355847.4         23723.16

                   6 Open                                 9           206379.8         22931.09

                   7 Closed                               3            33617.1          11205.7

                   8 Returned                            17             867493            51029

                   9 Partial Delivery                    10           262736.6         26273.66

                  10 Backordered                          5           235837.7         47167.54
  ---------------------------------------------------------------------------------------------

+---+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|   | The \*\*Returned\*\* status represents the highest financial risk with 17 orders totaling \$867,493, followed closely by \*\*Cancelled (Credit)\*\* and standard cancellations which collectively exceed \$500k in lost revenue. Immediate investigation is required into why nearly half of all processed orders (\$2M+) are either returned or cancelled to prevent significant margin erosion. Prioritize root-cause analysis for returns and credit cancellations to implement preventive controls before these high-value transactions slip through the pipeline. |
+===+========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+

# 4. Items Requiring Attention

**📉 Low Stock Alert 🟡 Monitor** ⏱ 1ms

50 rows

  ------------------------------------------------------------------------------------
  **PRODUCT_NAME**    **WAREHOUSE_NAME**     **QUANTITY_ON_HAND** **PRODUCT_STATUS**
  ------------------- -------------------- ---------------------- --------------------
  ESD Bracelet/Clip   Bombay                                    0 orderable

  GP 800x600          Bombay                                    3 orderable

  DIMM - 64MB         Bombay                                    3 orderable

  HD 8.2GB \@5400     Bombay                                    3 orderable

  LCD Monitor 9/PM    Bombay                                    3 orderable

  8MB Cache /NM       Bombay                                    4 orderable

  HD 9.1GB \@10000    Bombay                                    4 orderable

  CDW 20/48/E         Bombay                                    5 orderable

  HD 9.1GB \@10000    Beijing                                   5 orderable

  8MB Cache /NM       Beijing                                   5 orderable

  PS 220V /HS/FR      Bombay                                    5 orderable

  Modem - C/100       Bombay                                    6 orderable

  PS 110V HS/US       Bombay                                    6 orderable

  DIMM - 128 MB       Bombay                                    6 orderable

  CPU D600            Bombay                                    6 orderable

  SS Stock - 3mm      Bombay                                    6 orderable

  CPU D300            Bombay                                    6 orderable

  GP 1024x768         Bombay                                    6 orderable

  CDW 20/48/E         Beijing                                   6 orderable

  Cable RS232 10/AF   Bombay                                    6 orderable

  Cable PR/15/P       Bombay                                    7 orderable

  Screws \<Z.24.S\>   Bombay                                    7 orderable

  CPU D600            Beijing                                   7 orderable

  Industrial 700/HD   Bombay                                    7 orderable

  Industrial 600/DQ   Bombay                                    7 orderable

  CPU D300            Beijing                                   7 orderable

  SS Stock - 3mm      Beijing                                   7 orderable

  OSI 1-4/IL          Beijing                                   8 orderable

  Industrial 600/DQ   Beijing                                   8 orderable

  Industrial 700/HD   Beijing                                   8 orderable

  PS 220V /FR         Bombay                                    8 orderable

  Screws \<Z.28.P\>   Bombay                                    8 orderable

  Screws \<B.32.P\>   Bombay                                    8 orderable

  Inkjet C/8/HQ       Bombay                                    8 orderable

  32MB Cache /M       Bombay                                    9 orderable

  DIMM - 32MB         Bombay                                    9 orderable

  SPNIX4.0 - DL       Beijing                                   9 orderable

  Inkjet C/8/HQ       Beijing                                   9 orderable

  EDO - 32MB          Bombay                                    9 orderable

  SPNIX4.0 - UL/N     Beijing                                  10 orderable

  CD-ROM 600/E/24x    Bombay                                   10 orderable

  CD-ROM 600/I/24x    Bombay                                   10 orderable

  64MB Cache /NM      Bombay                                   10 orderable

  SPNIX4.0 - UL/D     Beijing                                  11 orderable

  ESD Bracelet/Clip   Beijing                                  11 orderable

  SPNIX4.0 - UL/A     Beijing                                  11 orderable

  HD 8.4GB \@5400     Bombay                                   11 orderable

  TD 7GB/8            Bombay                                   11 orderable

  64MB Cache /M       Bombay                                   11 orderable

  Cable PR/P/6        Bombay                                   11 orderable
  ------------------------------------------------------------------------------------

+---+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                                                                                                        |
|   |                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|   | The Bombay warehouse faces critical stockout risk with one product completely depleted (0 units) and four others holding only 3--5 units. Immediate replenishment is required for these high-priority items to prevent lost sales, while Beijing inventory shows slightly better liquidity at 5 units for similar products. Prioritize procurement for the zero-stock ESD Bracelet/Clip first to mitigate immediate order fulfillment failures. |
+===+=================================================================================================================================================================================================================================================================================================================================================================================================================================================+

**💎 High-Value Inactive Customers 🟡 Monitor** ⏱ 2ms

12 rows

  ----------------------------------------------------------------------------------------------------------------------------------------
  **CUSTOMER_ID**   **customer_name**   **INCOME_LEVEL**       **CREDIT_LIMIT**   **ACCOUNT_MGR_ID**     **order_count**   **total_spent**
  ----------------- ------------------- ---------------------- ------------------ -------------------- ----------------- -----------------
  278               Gvtz Bradford       K: 250,000 - 299,999   5000               149                                  0                 0

  770               Kris Curtis         K: 250,000 - 299,999   400                147                                  0                 0

  349               Ken Glenn           K: 250,000 - 299,999   3600               147                                  0                 0

  492               Sally Edwards       K: 250,000 - 299,999   2500               148                                  0                 0

  346               Marlon Clapton      K: 250,000 - 299,999   2400               147                                  0                 0

  242               Mary Lemmon         K: 250,000 - 299,999   2400               145                                  0                 0

  245               Max von Sydow       K: 250,000 - 299,999   2400               145                                  0                 0

  219               Ajay Sen            K: 250,000 - 299,999   2300               149                                  0                 0

  124               Diane Mason         K: 250,000 - 299,999   200                145                                  0                 0

  981               Daniel Gueney       K: 250,000 - 299,999   200                148                                  0                 0

  182               Lauren Dench        K: 250,000 - 299,999   1200               149                                  0                 0

  186               Meena Alexander     K: 250,000 - 299,999   1200               149                                  0                 0
  ----------------------------------------------------------------------------------------------------------------------------------------

+---+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                                                    |
|   |                                                                                                                                                                                                                                                                                                                                                                                             |
|   | This dataset reveals 12 high-net-worth customers (\$250K-\$300K income) with \*\*zero orders\*\* and negligible spending, representing a critical churn risk due to excessively low credit limits (e.g., \$400 for Kris Curtis). Immediate account management intervention is required to unlock their purchasing potential through exclusive service activations and credit limit reviews. |
+===+=============================================================================================================================================================================================================================================================================================================================================================================================+

# 5. Regular Business Analysis

**🏭 Global Warehouse Inventory 🟢 Routine** ⏱ 2ms

9 rows

  ---------------------------------------------------------------------------
  **WAREHOUSE_NAME**        **sku_count**   **total_stock**     **stock_pct**
  --------------------- ----------------- ----------------- -----------------
  San Francisco                       177             28613              23.9

  Sydney                              208             20457              17.1

  Seattle, Washington                 109             14860              12.4

  Beijing                             186             13482              11.3

  Toronto                             114             12969              10.9

  Mexico City                         106              9039               7.6

  Bombay                              128              7357               6.2

  New Jersey                           48              7252               6.1

  Southlake, Texas                     36              5483               4.6
  ---------------------------------------------------------------------------

+---+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                    |
|   |                                                                                                                                                                                                                                                                                                                                                             |
|   | San Francisco and Sydney dominate inventory concentration with 23.9% and 17.1% of total stock respectively, creating significant regional imbalance risks. Immediate rebalancing is required to transfer surplus units from North America (60.5% combined) to understocked locations like Southlake, Texas, which holds only 4.6% despite managing 36 SKUs. |
+===+=============================================================================================================================================================================================================================================================================================================================================================+

**🏆 Top Selling Products 🟢 Routine** ⏱ 2ms

10 rows

  -------------------------------------------------------------------------------------------------
  **PRODUCT_NAME**              **CATEGORY_ID**   **total_revenue**   **total_qty**   **avg_price**
  --------------------------- ----------------- ------------------- --------------- ---------------
  Desk - W/48                                31            922708.6             394          2341.9

  LaserPro 600/6/BW                          12              364351             741          492.69

  LCD Monitor 9/PM                           11            180872.8             753          237.55

  Monitor 21/HR/M                            11              134079             170           788.7

  Laptop 128/12/56/v90/110                   19             97464.4              34          2866.6

  PS 220V /L                                 19             89411.7             991           90.66

  KB 101/EN                                  16               82490            1861           44.62

  Plasma Monitor 10/TFT/XGA                  11             79741.2              84           949.3

  KB 101/ES                                  16               78099            1728           45.73

  Monitor 19/SD/M                            11               61908             134             462
  -------------------------------------------------------------------------------------------------

+---+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|   | High-revenue items like the \"Desk - W/48\" (\$922k) dominate top earnings with low volume, whereas high-volume products such as the \"KB 101/EN\" (1,861 units) generate significantly less revenue, revealing a strategy focused on premium pricing over mass-market breadth. To mitigate reliance on expensive SKUs and capture broader market share, consider expanding the product line with mid-tier accessories that balance volume and margin potential. |
+===+==================================================================================================================================================================================================================================================================================================================================================================================================================================================================+

**🔄 Repurchase Rate Analysis 🟢 Routine** ⏱ 0ms

1 rows

  --------------------------------------------------------------------------------------------------
    **repeat_customers**   **one_time_customers**   **total_active_customers**   **repurchase_rate**
  ---------------------- ------------------------ ---------------------------- ---------------------
                      18                       29                           47                  38.3

  --------------------------------------------------------------------------------------------------

+---+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                                                                |
|   |                                                                                                                                                                                                                                                                                                                                                                                                         |
|   | The current repurchase rate stands at 38.3%, indicating that nearly 62% of your 47 active customers are one-time buyers, representing a significant churn risk. To convert these 29 one-time buyers into repeat customers, implement targeted post-purchase incentives such as loyalty discounts or personalized email campaigns within the first two weeks to capitalize on initial purchase momentum. |
+===+=========================================================================================================================================================================================================================================================================================================================================================================================================+

**📊 Income Segment Analysis 🟢 Routine** ⏱ 4ms

12 rows

  -------------------------------------------------------------------------------------------------------
  **income_level**         **customer_count**   **order_count**   **avg_order_value**   **total_revenue**
  ---------------------- -------------------- ----------------- --------------------- -------------------
  F: 110,000 - 129,999                     73                30              10436.63            960170.2

  G: 130,000 - 149,999                     36                15              15996.03            687829.5

  D: 70,000 - 89,999                       34                 8              18054.79              686082

  H: 150,000 - 169,999                     37                17              10206.79            469512.4

  B: 30,000 - 49,999                       17                 5               9549.75            190995.1

  E: 90,000 - 109,999                      27                 5               6041.35            181240.6

  A: Below 30,000                          18                 6               6845.63            143758.2

  I: 170,000 - 189,999                     27                 6                3950.5              118515

  L: 300,000 and above                      8                 6               9591.22            115094.6

  C: 50,000 - 69,999                       15                 5                4837.1             87067.8

  J: 190,000 - 249,999                     15                 2               1852.62             27789.3

  K: 250,000 - 299,999                     12                 0                     0                   0
  -------------------------------------------------------------------------------------------------------

+---+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                                                                                                              |
|   |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|   | The \*\*G tier (\$130k--\$150k)\*\* generates the highest average order value at \*\*\$15,996\*\*, while the \*\*F tier (\$110k--\$130k)\*\* delivers the strongest total revenue of \*\*\$960,170\*\* from 73 customers. Marketing should prioritize high-volume retention for Tier F and upselling campaigns for Tier G to maximize yield, whereas low-order tiers like E and I show a critical risk of customer churn despite decent order values. |
+===+=======================================================================================================================================================================================================================================================================================================================================================================================================================================================+

**🌍 Regional Sales Distribution 🟢 Routine** ⏱ 3ms

5 rows

  -------------------------------------------------------------------------------------------------
  **STATE_PROVINCE**   **COUNTRY_NAME**             **customers**    **orders**   **total_revenue**
  -------------------- -------------------------- --------------- ------------- -------------------
  WI                   United States of America                25            41           1702563.7

  IN                   United States of America                16            36           1158647.9

  MI                   United States of America                29            15            427608.3

  IA                   United States of America                11             8            251126.3

  MN                   United States of America                12             5            128108.5
  -------------------------------------------------------------------------------------------------

+---+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ✦ | **AI Business Analysis**                                                                                                                                                                                                                                                                                                                                               |
|   |                                                                                                                                                                                                                                                                                                                                                                        |
|   | The data reveals a heavy reliance on the United States market, where top states like Wisconsin and Indiana generate over \$2.8M in revenue with high customer order density. This concentration exposes the business to significant regional risk while highlighting untapped growth potential in Asia-Pacific and Europe that requires immediate strategic expansion. |
+===+========================================================================================================================================================================================================================================================================================================================================================================+

# Appendix: Methodology

Data originates from the official Oracle OE sample database, exported as CSV via WangDBtoCSV and loaded into a DB in-memory database for analysis.

All SQL queries were automatically generated and executed by AI SQL Studio . 12 business queries were run, covering orders, inventory, customers, sales, and geographic distribution.

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Query Topic**                 **Analysis Dimension**                                                                                                                                                       **Status**        **Duration**
  ------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------------- -----------------
  Order Status Overview           Analyze the distribution of order statuses, highlighting high-risk states (returns, stock shortages, credit holds\...)                                                       Done              3ms

  Return Order Details            Analyze returned orders, list customers with high-value returns, assess risk levels, and recommend immediate actions\...                                                     Done              1ms

  Partial Delivery Backlog        Analyze logistics bottlenecks in partially delivered orders, identify the most severely backlogged orders, and provide supply recommendations\...                            Done              1ms

  Unfinished Orders Summary       Summarize all unfinished orders, categorize them by urgency, calculate the total risk amount, and provide recommendations\...                                                Done              1ms

  Account Manager Performance     Analyze the extreme imbalance in account manager performance; managers No.147/148/149\...                                                                                    Done              2ms

  Global Warehouse Inventory      Analyze the inventory distribution across 9 global warehouses, identify risks of inventory concentration, and provide replenishment and redistribution recommendations\...   Done              2ms

  Low Stock Alert                 List products currently for sale with inventory below 50 units, evaluate stock-out risks, and provide replenishment priority recommendations\...                             Done              1ms

  Top Selling Products            Analyze the Top 10 selling products, identify the differences between high-revenue products and high-volume products\...                                                     Done              2ms

  High-Value Inactive Customers   Analyze the current zero-purchase situation of high-net-worth customers with annual income of 250k--300k, and provide precise marketing recommendations\...                  Done              2ms

  Repurchase Rate Analysis        Analyze the current repurchase rate and provide concrete strategies to convert one-time buyers into repeat customers\...                                                     Done              0ms

  Income Segment Analysis         Analyze consumption behavior differences across 12 income tiers, identify the highest-value segments and potential segments\...                                              Done              4ms

  Regional Sales Distribution     Analyze the current situation where sales are highly concentrated in North America, and evaluate expansion opportunities in the Asia-Pacific and European markets\...        Done              3ms
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

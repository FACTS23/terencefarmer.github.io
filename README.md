# Portfolio

<details  open>
<summary>Show credentials:</summary>
 
![MS Computer Science](<assets/img/MS_Computer_Science.png>)
![MS Industrial Engineering](<assets/img/MSIE.png>)
![MS Applied Mathematics](<./assets/img/MSAppliedMathematics2000.png>)
<img src="./assets/img/BachelorofScienceDegree.png" alt="A photo">

</details>


<!--
![BS Mathematics](<./assets/img/BachelorofScienceDegree.png>)

### Education

|   |   |   |   |   |
|--|--|--|--|--|
|**M.S.**|**Computer Science**|Florida Atlantic University|*2019-2020*|![MS Computer Science](<assets/img/MS_Computer_Science.png>)
|**M.S.**|**Industrial Engineering**|University of Missouri|*2009-2009*<sup>*</sup>|![MS Industrial Engineering](<assets/img/MSIE.png>)
|**M.S.**|**Applied Mathematics** |University of Missouri|*1997-2000*|![MS Applied Mathematics](<assets/img/MSAppliedMathematics2000.png>)
|**B.S.**|**Mathematics** |Alabama State University|*1993-1997*|![BS Mathematics](<assets/img/BachelorofScienceDegree.png>)
|   |   |   |   |
|\*Ph.D. Candidate|Industrial Engineering|University of Missouri|*2000-2008*|*No Degree, All But Dissertation (ABD)*





### Experience
 **Senior Director of Risk Data Science** | DigniFi, Inc. | Fort Lauderdale, FL | January 2022 – February 2026
 
Data Science

<details>
<summary>see examples</summary>

![Python Decision Tree](<https://github.com/FACTS23/terencefarmer.github.io/blob/main/assets/img/Decision%20Tree%20for%20Take%20Rate%201%20Python.png>)

![Logistic Regression Analysis](<./assets/img/Logistic%20Regression%20Model%20Validation%20p2%20automation%20Tableau.jpg>)

![Logistic Regression Analysis](<./assets/img/Logistic%20Regression%20Model%20Validation%20p3%20automation%20Tableau.jpg>)

</details>


Visualizations

<details>
<summary>see examples</summary>

![Credit Strategy Analysis Analysis](<./assets/img/Credit%20Strategy%20analysis%20automation%20Tableau.jpg>)

</details>


Reporting

<details>
<summary>see examples:</summary>

![Tableau gallery](<./assets/img/Tableau%20gallery.jpg>)

![WasIs](<./assets/img/Deliquencies%20and%20Loss%20WasIs%20automated%20Tableau.jpg>)

</details>


Automations
<details>
<summary>see examples:</summary>

![Credit Policy Monitoring with Tableau Dashboard](<./assets/img/Credit%20Policy%20Monitoring%20p1%20automation%20Tableau.jpg>)

![Credit Policy Monitoring with Tableau Dashboard](<./assets/img/Credit%20Policy%20Monitoring%20p2%20automation%20Tableau.jpg>)
</details>


Advanced SQL Skills

1. <ins>Window Functions (Analytical Processing)</ins>

Used extensively to perform calculations across a set of table rows that are related to the current row.

Partitioning and Ordering: Functions like ROW_NUMBER() OVER (PARTITION BY ... ORDER BY ...) are used for ranking, deduplication, and selecting the most recent or first record for a group. Example from Spanish NLS Comments.sql  

```sql
QUALIFY ROW_NUMBER() OVER (PARTITION BY LOAN_NUMBER ORDER BY CREATED_DATE DESC) = 1
```

Lag/Lead and Value Retrieval: LAST_VALUE() OVER (...), FIRST_VALUE() OVER (...), and LAG() OVER (...) are used to look up values from previous or subsequent rows, often for calculating time-series metrics. Example from DPD Ever.sql  

```sql
FIRST_VALUE(CAST(dtb31.TRIAL_BALANCE_DATE AS DATE)) OVER (PARTITION BY dtb31.ACCTREFNO ORDER BY dtb31.TRIAL_BALANCE_DATE) AS "first 31 delinquency date"
```

Ratios and Percentiles: RATIO_TO_REPORT() and NTILE(10) are used for comparative analysis and decile/bucket assignments. Example from PSI by Month.sql  

```sql
ratio_to_report("Application") over (partition by s.SUBMIT_MONTH) as "% Application Validation"
```

2. <ins>Common Table Expressions (CTEs)</ins>

   For complex queries, I utilize multiple, named sub-queries (CTEs) which significantly improves query readability, modularity, and maintainability by breaking down logic into manageable steps.
    
- Example structure from Application Funnel.sql:

```sql
WITH DATE AS (
/* logic for date dimension and flags */
)
, CREDIT AS (
/* logic for credit population  */
)
-- ... other CTEs (DPA, RAM)
SELECT ... FROM DATE
INNER JOIN CREDIT ...
/* The main query combines the named steps  */
```

3. <ins>Conditional Logic and Data Transformation</ins>

Conditional expressions utilized for classifying data, applying business rules, and managing data quality. Specifically, complex CASE and IFF Statements are used to categorize loans, flag time periods, and translate coded values into meaningful descriptions.

-   Example from WasIs.sql (for DPD Status):

```sql
case when c.days_past_due = 0 then '1.CURRENT'
when c.days_past_due > 0 and c.days_past_due <= 30 then '2.1-30 DPD'
...
end as Was_DPD_Status
```

-   Example from Compliance 07 2023 Bank Testing - BSA OFAC & CIP.sql (for Decoding):\

```sql
DECODE (ofac_messageNumber,
'1200', 'NAME MATCHES OFAC/PLC/FSE LIST',
'1201', 'OFAC LIST TEMPORARILY UNAVAILABLE',
'1202', 'OFAC NO RECORD FOUND ') AS ofac_messageText
```

4. <ins>Advanced String and JSON Parsing</ins>

Extensive use of regular expressions (regexp_substr) and JSON path functions (json_extract_path_text) to extract specific data elements embedded within complex text or JSON/Variant columns, such as from audit logs or credit bureau API requests and responses. This is crucial for pulling specific attributes like credit scores or decline reasons from raw log data.

- Example from Adverse_Action_Top_Factors.sql:

```sql
CAST(LTRIM(regexp_substr(EA_RAM.REQUEST,'\"bankruptcy_count_24_month\":\\\\W+(\\\\\w+)',1,1,'e',1)) AS FLOAT) AS bankruptcy_count_24_month
```

- Example from Credit Policy Applications.sql:

```sql
CAST(json_extract_path_text(REQUEST,'\"experian\".\"income_insight\"') AS NUMBER(38,0)) AS INCOME_INSIGHT_CODE
```

5. <ins>Date/Time and Variable Management</ins>

The queries demonstrate sophisticated handling of dynamic timeframes, which is common in financial and analytical reporting.
Date Arithmetic and Configuration: Queries use variables ($START_DATE, $CURDATE, $AS_OF_DATE) and complex date functions (DATEADD, DATE_TRUNC, LAST_DAY) to define and calculate rolling analysis windows (e.g., last 2 months, year-over-year, last 13 months).

- Example from Application Funnel.sql (for a 2-month flag):

```sql
WHEN date >= DATEADD(MONTH, -1, DATE_TRUNC(MONTH, today + 1)) AND date <= DATE_TRUNC(MONTH, today + 1) - 1
THEN 1
```

- Example from WasIs.sql (for setting a query variable):

```sql
set CURDATE = to_date('2023-01-01');
```
-->

<!-- 
**Innovation Unit Supervisor** | Broward County Government | Fort Lauderdale, FL | March 2020 – January 2022
- Visualizations\
![Covid PowerBI Dashboard](<assets/img/Broward Covid dashboard 1 PowerBI.png>)
![Animal Shelter ArcGIS Dashboard](<assets/img/Broward Animal Care Dashboard 2 ArcGIS.png>)
![Animal Shelter ArcGIS Newsletter](<assets/img/Broward Animal Care Newsletter 2 ArcGIS.png>)

**Senior Risk Analyst** | Southeast Toyota Finance | Fort Lauderdale, FL | January 2018 – March 2020

**Manager, Tool & Analytics** | Citrix Systems | Fort Lauderdale, FL | January 2017 – October 2017

**Experience Insights Analytics Manager** | The Walt Disney Company | Orlando, FL | January 2014 – January 2017

**Senior Revenue Analyst** | The Walt Disney Company | Orlando, FL | November 2011 – December 2013

**Senior Industrial Engineer** | The Walt Disney Company | Orlando, FL | November 2008 – November 2011
![SAS Dashboard - Proc Ganno](<assets/img/Disney New York Times article training 1 SAS.jpg>)
![As seen in NY Times](<assets/img/Disney New York Times article SAS dashboard.png>)

**Marketing Reporting & Analytics Manager** | The Walt Disney Company | Orlando, FL | July 2007 – November 2008

**Senior Credit Policy Data Manager** | CitiMortgage (Citigroup) | St. Louis, MO | August 2005 – June 2007

### Certifications
- **Revenue Management Certificate** | Cornell University | 2012
- **Tableau Desktop Qualified Associate**| Tableau | 2017
- **SAS Certified Base Programmer**| SAS | 2005
- **IBM Certified Database Associate**| IBM | 2005
- **Microsoft Excel Expert Certification**| Microsoft | 2004 \
![SAS Badge](<assets/img/SAS badge.bmp>){: .portfolio-badge} ![IBM badge](<assets/img/IBM badge.bmp>){: .portfolio-badge}

<details>

<summary>Show credentials:</summary>

![SAS](<assets/img/SAS Certified Base Programmer.jpg>){: .portfolio-image}
![Excel](<assets/img/Microsoft Excel 2000.jpg>){: .portfolio-image}
![MS Office](<assets/img/Microsoft Office Specialist Master 2000.jpg>){: .portfolio-image}
![IBM](<assets/img/CERTIFICATE_DB2_F1483398_19.bmp>){: .portfolio-image}

</details>

### Continuing Education Units
- Using ChatGPT and Generative AI in FinTech | NASBA | 2026
- Generative Al Fundamentals | Databricks Academy | 2026
- Project Management Foundations | PMI Institute | 2026
- Python Data Analysis| LinkedIn Learning | 2026
- The Data Science of Economics, Banking, and Finance| LinkedIn Learning | 2026
- Microsoft Azure Fundamentals| Microsoft | 2020
- Power BI Dashboarding| Microsoft | 2020
- Credit Scorecard Development and Implementation | SAS | 2020
- Building and Solving Optimization Models | SAS | 2018
- Survival Data Mining | SAS | 2018

<details>

<summary>Show credentials:</summary>

![ESRI Learning ArcGIS 9](<assets/img/ESRI Learning ArcGIS 9.jpg>)
![Web Authoring Fundamentals](<assets/img/Web Authoring Fundamentals.bmp>)
![Advanced Wiring and NEC Code](<assets/img/Advanced Wiring and NEC Code.bmp>)
![CPR](<assets/img/CPR_front.bmp>)
![Introduction to Urban and Regional Planning Concepts](<assets/img/Introduction to Urban and Regional Planning Concepts.bmp>)

</details>

<details>

<summary>Awards:</summary>

![NSF](<assets/img/National Science Foundation.jpg>){: .portfolio-image}

</details>

-->

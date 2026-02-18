# Portfolio

## Education

|   |   |   |   |   |
|--|--|--|--|-----|
|**M.S.**|**Computer Science**|Florida Atlantic University|*2019-2020*|![MS Computer Science](<assets/img/MS_Computer_Science.png>)
|**M.S.**|**Industrial Engineering**|University of Missouri|*2009-2009*<sup>*</sup>|![MS Industrial Engineering](<assets/img/MSIE.png>)
|\*Ph.D. Candidate|Industrial Engineering|University of Missouri|*2000-2008*|*No Degree*, *All But Dissertation (ABD)* ![IMSE dissertation](<assets/img/IMSE_dissertation.png>)
|**M.S.**|**Applied Mathematics** |University of Missouri|*1997-2000*|![MS Applied Mathematics](<assets/img/MSAppliedMathematics2000.png>)
|**B.S.**|**Mathematics** |Alabama State University|*1993-1997*|![BS Mathematics](<assets/img/BachelorofScienceDegree.png>)

<hr>

## Experience
### **Senior Director of Risk Data Science** | DigniFi, Inc. | Fort Lauderdale, FL | January 2022 – February 2026
 
- #### Data Science
  <details  closed>
  <summary>see examples</summary>

  <blockquote>Using Python, I created Decision Trees to identify the strength of model predictor varaibles</blockquote>
  <img src="./assets/img/Decision%20Tree%20for%20Take%20Rate%201%20Python.png" alt="Python Decision Tree">
  
  <blockquote>Using Snowflake advanced SQL and Tableau, I created a fully automated report of key model statistics (KS, AUC, PSI)</blockquote>
  <img src="./assets/img/Logistic%20Regression%20Model%20Validation%20p2%20automation%20Tableau.jpg" alt="Logistic Regression Analysis">
  <img src="./assets/img/Logistic%20Regression%20Model%20Validation%20p3%20automation%20Tableau.jpg" alt="Logistic Regression Analysis">
  </details>

- #### Visualizations
  <details>
  <summary>see examples</summary>

  <blockquote> using Snowflake advanced SQL, Tableau and geo mapping, I created and published a Dashboard to analyze strategy</blockquote>
  <img src="./assets/img/Credit%20Strategy%20analysis%20automation%20Tableau.jpg" alt="Credit Strategy Analysis Analysis">
  </details>

- #### Reporting
  <details  closed>
  <summary>see examples:</summary>

  <blockquote> I managed more than 30 reports using efficient coding and dashboarding</blockquote>
  <img src="./assets/img/Tableau%20gallery.jpg" alt="Tableau gallery">
  
   > This automated and interactive report provided executives, peers, and auditors with real-time information
  <img src="./assets/img/Deliquencies%20and%20Loss%20WasIs%20automated%20Tableau.jpg" alt="WasIs">
  </details>

- #### Automations
  <details  closed>
  <summary>see examples:</summary>

  <blockquote> using Snowflake advanced SQL, Tableau and Adobe, I created a live PDF process that automatically identifies issues and areas of investigation</blockquote>
  <img src="./assets/img/Credit%20Policy%20Monitoring%20p1%20automation%20Tableau.jpg" alt="Credit Policy Monitoring with Tableau Dashboard">
  <img src="./assets/img/Credit%20Policy%20Monitoring%20p2%20automation%20Tableau.jpg" alt="Credit Policy Monitoring with Tableau Dashboard">
  </details>

- #### Advanced SQL Skills
  <details  closed>
  <summary>see examples:</summary>
  
  1. <ins>Window Functions (Analytical Processing)</ins>
  <blockquote> Used extensively to perform calculations across a set of table rows that are related to the current row</blockquote>
  
  Partitioning and Ordering: Functions like ROW_NUMBER() OVER (PARTITION BY ... ORDER BY ...) are used for ranking, deduplication, and selecting the most recent or first record for a group. Example from Spanish NLS Comments.sql

  <pre><code class="language-sql">
  QUALIFY ROW_NUMBER() OVER (PARTITION BY LOAN_NUMBER ORDER BY CREATED_DATE DESC) = 1
  </code></pre>

  Lag/Lead and Value Retrieval: LAST_VALUE() OVER (...), FIRST_VALUE() OVER (...), and LAG() OVER (...) are used to look up values from previous or subsequent rows, often for calculating time-series metrics. Example from DPD Ever.sql  

  <pre><code class="language-sql">
  FIRST_VALUE(CAST(dtb31.TRIAL_BALANCE_DATE AS DATE)) OVER (PARTITION BY dtb31.ACCTREFNO ORDER BY dtb31.TRIAL_BALANCE_DATE) AS "first 31 delinquency date"
  </code></pre>

  Ratios and Percentiles: RATIO_TO_REPORT() and NTILE(10) are used for comparative analysis and decile/bucket assignments. Example from PSI by Month.sql  

  <pre><code class="language-sql">
  ratio_to_report("Application") over (partition by s.SUBMIT_MONTH) as "% Application Validation"
  </code></pre>

  2. <ins>Common Table Expressions (CTEs)</ins>
  <blockquote> For complex queries, I utilize multiple, named sub-queries (CTEs) which significantly improves query readability, modularity, and maintainability by breaking down logic into manageable steps</blockquote>
      
  - Example structure from Application Funnel.sql:
  
  <pre><code class="language-sql">
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
  </code></pre>
  
  3. <ins>Conditional Logic and Data Transformation</ins>
  <blockquote> Conditional expressions utilized for classifying data, applying business rules, and managing data quality. Specifically, complex CASE and IFF Statements are used to categorize loans, flag time periods, and translate coded values into meaningful descriptions.</blockquote>
  
  -   Example from WasIs.sql (for DPD Status):
  
  <pre><code class="language-sql">
  case when c.days_past_due = 0 then '1.CURRENT'
  when c.days_past_due > 0 and c.days_past_due <= 30 then '2.1-30 DPD'
  ...
  end as Was_DPD_Status
  </code></pre>
  
  -   Example from Compliance 07 2023 Bank Testing - BSA OFAC & CIP.sql (for Decoding):\
  
  <pre><code class="language-sql">
  DECODE (ofac_messageNumber,
  '1200', 'NAME MATCHES OFAC/PLC/FSE LIST',
  '1201', 'OFAC LIST TEMPORARILY UNAVAILABLE',
  '1202', 'OFAC NO RECORD FOUND ') AS ofac_messageText
  </code></pre>
  
  4. <ins>Advanced String and JSON Parsing</ins>
  <blockquote> Extensive use of regular expressions (regexp_substr) and JSON path functions (json_extract_path_text) to extract specific data elements embedded within complex text or JSON/Variant columns, such as from audit logs or credit bureau API requests and responses. This is crucial for pulling specific attributes like credit scores or decline reasons from raw log data.</blockquote>
  
  - Example from Adverse_Action_Top_Factors.sql:
  
  <pre><code class="language-sql">
  CAST(LTRIM(regexp_substr(EA_RAM.REQUEST,'\"bankruptcy_count_24_month\":\\\\W+(\\\\\w+)',1,1,'e',1)) AS FLOAT) AS bankruptcy_count_24_month
  </code></pre>
  
  - Example from Credit Policy Applications.sql:
  
  <pre><code class="language-sql">
  CAST(json_extract_path_text(REQUEST,'\"experian\".\"income_insight\"') AS NUMBER(38,0)) AS INCOME_INSIGHT_CODE
  </code></pre>
  
  5. <ins>Date/Time and Variable Management</ins>
  <blockquote> The queries demonstrate sophisticated handling of dynamic timeframes, which is common in financial and analytical reporting.</blockquote>
  
  Date Arithmetic and Configuration: Queries use variables ($START_DATE, $CURDATE, $AS_OF_DATE) and complex date functions (DATEADD, DATE_TRUNC, LAST_DAY) to define and calculate rolling analysis windows (e.g., last 2 months, year-over-year, last 13 months).
  
  - Example from Application Funnel.sql (for a 2-month flag):
  
  <pre><code class="language-sql">
  WHEN date >= DATEADD(MONTH, -1, DATE_TRUNC(MONTH, today + 1)) AND date <= DATE_TRUNC(MONTH, today + 1) - 1
  THEN 1
  </code></pre>
  
  - Example from WasIs.sql (for setting a query variable):
  
  <pre><code class="language-sql">
  set CURDATE = to_date('2023-01-01');
  </code></pre>
  </details>

### **Principal Consultant** | Farmer Analytical Consulting Technology Services LLC  | Fort Lauderdale, FL | August 2023 – Present
- #### Projects
  <details  closed>
  <summary>see examples:</summary>

  <blockquote>I supported a private equity fund with idenfying acquisition opportunities by creating custom models, heat maps, and market reports utilizing ESRI ArcGIS, Python, Excel, and Tableau.</blockquote>
  <img src="./assets/img/FACTS_Heat_Map_1.png" alt="FACTS Heat Map">
  <img src="./assets/img/FACTS_Heat_Map_2.png" alt="FACTS Heat Map">
  <img src="./assets/img/FACTS_SiteRankings1.png" alt="FACTS Site Rankings">
  <img src="./assets/img/FACTS_WhatsInMyCommunity.png" alt="FACTS Whats In My Community">
  <img src="./assets/img/FACTS_TapestryReport.png" alt="FACTS Tapestry Report">
  <img src="./assets/img/FACTS_ModelVariables.png" alt="FACTS Model Variables">
  </details>
 
### **Innovation Unit Supervisor** | Broward County Government | Fort Lauderdale, FL | March 2020 – January 2022
- #### Visualizations
  <details  closed>
  <summary>see examples:</summary>

  <blockquote> I used PowerBI and ArcGIS to create public-facing dashbaords and newsletters. I received recognition for supporting the community during the COVID pandemic.</blockquote>
  <img src="./assets/img/Broward%20Covid%20dashboard%201%20PowerBI.png" alt="Covid PowerBI Dashboard">
  <img src="./assets/img/Broward%20Animal%20Care%20Dashboard%20ArcGIS.png" alt="Animal Shelter ArcGIS Dashboard">
  <img src="./assets/img/Broward%20Animal%20Care%20Dashboard%202%20ArcGIS.png" alt="Animal Shelter ArcGIS Dashboard">
  <img src="./assets/img/Broward%20Animal%20Care%20Newsletter%20ArcGIS.png" alt="Animal Shelter ArcGIS Newsletter">
  </details>


### **Senior Risk Analyst** | Southeast Toyota Finance | Fort Lauderdale, FL | January 2018 – March 2020

### **Manager, Tool & Analytics** | Citrix Systems | Fort Lauderdale, FL | January 2017 – October 2017

### **Experience Insights Analytics Manager** | The Walt Disney Company | Orlando, FL | January 2014 – January 2017

### **Senior Revenue Analyst** | The Walt Disney Company | Orlando, FL | November 2011 – December 2013

### **Senior Industrial Engineer** | The Walt Disney Company | Orlando, FL | November 2008 – November 2011
- #### Visualizations
  <details  closed>
  <summary>see examples:</summary>

  <blockquote> I used Advanced SAS Programming and multiple database connections (MySQL,Oracle,IBM) to create real-time operations monitoring. These efforts were spotlighted in the New York Times.</blockquote>
  <img src="./assets/img/Disney%20New%20York%20Times%20article%20training%201%20SAS.jpg" alt="SAS Dashboard - Proc Ganno"><br>
  <br> 
  <br> <img src="./assets/img/Disney%20New%20York%20Times%20article%20SAS%20dashboard.png" alt="As seen in NY Times">
  <img src="./assets/img/Disney%20New%20York%20Times%20article%20SAS%202%20dashboard.png" alt="As seen in NY Times">
  <img src="./assets/img/Disney%20New%20York%20Times%20article%20SAS%203%20dashboard.png" alt="As seen in NY Times">
  </details>

- #### Personalizations
  <details  closed>
  <summary>see examples:</summary>

  <blockquote> I used SAS and Tableau to create personalized itineraries. I shared these methods across the company and was recognized by Disney with a technology grant.</blockquote>
  <img src="./assets/img/Disney%20itinerary%20recommendation%20Tableau.png" alt="Disney Custom Itinerary">
  <img src="./assets/img/Disney%20itinerary%20recommendation%20Guide%20Setup.png" alt="Disney Custom Itinerary design">
  <img src="./assets/img/Disney%20personalization%20strategy%20training%20PPT.jpg" alt="Disney Training Session">
  </details>

### **Marketing Reporting & Analytics Manager** | The Walt Disney Company | Orlando, FL | July 2007 – November 2008

### **Senior Credit Policy Data Manager** | CitiMortgage (Citigroup) | St. Louis, MO | August 2005 – June 2007

<hr>

## Certifications

![Tableau Badge](<assets/img/TableauBadge.png>)  ![SAS Badge](<assets/img/SAS badge.bmp>)  ![IBM badge](<assets/img/IBM badge.bmp>)

|   |   |   |   |
|--|--|--|--|
|**Revenue Management Certificate**|Cornell University|*2012*|![Cornell](<assets/img/Cornell_Revenue_Management_certificate.png>)
|**Tableau Desktop Qualified Associate**|Tableau|*2017*|![Tableau](<assets/img/Tableau_certification.png>)
|**SAS Certified Base Programmer**|SAS|*2005*|![SAS](<assets/img/SAS%20Certified%20Base%20Programmer.jpg>)
|**IBM Certified Database Associate**|IBM|*2005*|![IBM](<assets/img/IBM.png>)
|**Microsoft Excel Expert Certification**|Microsoft|*2004*|![Excel](<assets/img/Microsoft%20Excel%202000.jpg>)
|**Microsoft Office Master Certification**|Microsoft|*2004*|![Excel](<assets/img/Microsoft%20Office%20Specialist%20Master%202000.jpg>)

<!--
<details  open>
<summary>Show credentials:</summary>

<img src="./assets/img/Tableau_certification.png" alt="Tableau">
<img src="./assets/img/SAS%20Certified%20Base%20Programmer.jpg" alt="SAS">
<img src="./assets/img/Microsoft%20Excel%202000.jpg" alt="Excel">
<img src="./assets/img/Microsoft%20Office%20Specialist%20Master%202000.jpg" alt="MS Office">
<img src="./assets/img/IBM.png" alt="IBM">
</details>
-->

<hr>

## Continuing Education Units

|   |   |   |   |
|--|--|--|--|
|**Using ChatGPT and Generative AI in FinTech**|NASBA|*2026*|![Using ChatGPT and Generative AI in FinTech](<assets/img/UsingChatGPTand GenerativeAIinFinTech.png>)
|**Generative Al Fundamentals**| Databricks Academy |*2026*|![Generative Al Fundamentals](<assets/img/GenerativeAIFundamentals.png>)
|**Project Management Foundations**| PMI Institute |*2026*|![Project Management Foundations](<assets/img/ProjectMagementFoundations.png>)
|**Python Data Analysis**| LinkedIn Learning |*2026*| ![Python Data Analysis](<assets/img/PythonDataAnalysis.png>)
|**The Data Science of Economics, Banking, and Finance**|LinkedIn Learning|*2026*|![The Data Science of Economics Banking and Finance](<assets/img/DataScienceofEconomicsBankingFinance.png>)
|**Databricks Fundamentals**|Databricks Academy|*2026*|![Databricks Fundamentals](<assets/img/DatabricksFundamentals.png>)
|**Microsoft Azure Fundamentals**|Microsoft|*2020*|
|**Power BI Dashboarding**|Microsoft|*2020*|
|**Credit Scorecard Development and Implementation**|SAS|*2020*|
|**Building and Solving Optimization Models**|SAS|*2018*| ![SAS Optimization Models](<assets/img/SASOptimizationModels.png>)
|**Survival Data Mining**|SAS| *2018*|![SAS Data Mining](<assets/img/SASDataMining.png>)
|**Using SAS Programs to Execute Pig and HiveQL in Hadoop**|SAS|*2018*|![SAS Hadoop](<assets/img/SASHadoop.png>)
|**Advanced SAS Programming Library**|SAS|*2008*|![Advanced SAS Programming Library](<assets/img/AdvancedSASProgrammingLibrary.png>)
|**Performing Advanced Queries Using PROC SQL**|SAS|*2008*|![Performing Advanced Queries Using PROC SQL](<assets/img/PerformingAdvancedQueriesUsingPROCSQL.png>)


<!--
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
-->

<details  closed>
<summary>more credentials:</summary>

<img src="./assets/img/ESRI%20Learning%20ArcGIS%209.jpg" alt="ESRI Learning ArcGIS 9">
<img src="./assets/img/Web%20Authoring%20Fundamentals.png" alt="Web Authoring Fundamentals">
<img src="./assets/img/Advanced%20Wiring%20and%20NEC%20Code.png" alt="Advanced Wiring and NEC Code">
<img src="./assets/img/Introduction%20to%20Urban%20and%20Regional%20Planning%20Concepts.png" alt="Introduction to Urban and Regional Planning Concepts">
<img src="./assets/img/CPR_front.bmp" alt="CPR">
</details>

<hr>

## Awards & Recognitions

<details  closed>
<summary></summary>

<img src="./assets/img/National%20Science%20Foundation.jpg" alt="NSF">
</details>

## Public Speaking

<details  closed>
<summary></summary>

<blockquote>Panelist discussing the importance of Diversity within Data & Analytics</blockquote>
<img src="./assets/img/TableauTalk.jpg" alt="Tableau Talk">

<blockquote>Panelist sharing my career journey at the intersection of Data Science, AI and Smart Cities</blockquote>
<img src="./assets/img/BEYA_talk.png" alt="BEYA">
</details>

1. Document Purpose
The purpose of this document is to establish a centralized repository and functional specification for all Data Analysis Expressions (DAX) measures implemented within the analytical data model. It provides clear definitions, underlying calculation logic, and business context to ensure data consistency, maintainability, and accurate reporting across power BI reports.
This documentation encapsulates DAX measures categorized into four core business domains:
•	Financial Measures: KPI calculations covering revenue metrics, billing, payment performance, and profitability indicators.
•	Lead and Sales Measures: Operational metrics tracking lead acquisition volume, conversion rates, sales pipeline progression, and response time efficiency.
•	Marketing Measures: Performance analytics evaluating campaign reach, acquisition costs (CAC), channel efficiency, and return on marketing investment.
•	Student and Courses Measures: Academic metrics analyzing student enrollment rates, course completion progress, retention rates, and churn dynamics.
2. Here is the comprehensive English documentation for all metrics across our four core categories, formatted for technical specifications and data model documentation.
1. Lead and Sales Funnel Measures
Metrics tracking lead acquisition volume, conversion efficiency, pipeline velocity, and sales performance.
Measure Name	Category	Description & Business Definition
Total Leads	Lead & Sales Funnel	Calculates the total count of all captured lead records within the selected timeframe, including duplicates or multi-channel entries.
Unique Leads	Lead & Sales Funnel	Calculates the distinct count of individual prospective students based on a unique identifier (e.g., LeadID, email, or phone number).
Converted Leads	Lead & Sales Funnel	Counts the number of unique leads who successfully transitioned from a prospect state to a confirmed paying customer/enrollment.
Total Enrollments	Lead & Sales Funnel	Counts the total number of course enrollments generated across all students within the reporting period.
Lead-to-Enrollment Conversion Rate	Lead & Sales Funnel	Measures the percentage of unique leads that converted into active enrollments $\left(\frac{\text{Converted Leads}}{\text{Unique Leads}} \times 100\right)$.
Average Days to Enrollment	Lead & Sales Funnel	Calculates the average elapsed time (in days) between the initial lead creation date and the final enrollment date.
Average First Response Time	Lead & Sales Funnel	Measures the average duration (in minutes or hours) between the moment a lead is created and the first registered sales contact.
Lead Conversion vs Previous Period	Lead & Sales Funnel	Evaluates the percentage change or basis point variance in the conversion rate compared to the prior equivalent timeframe (MoM/QoQ).
2. Financial Measures
KPI calculations covering revenue streams, transaction adjustments, sales productivity, and financial performance trends.
Measure Name	Category	Description & Business Definition
Gross Revenue	Financial	Computes the total monetary value of all processed customer orders and invoices before deducting refunds, discounts, or processing fees.
Net Revenue	Financial	Represents the actual recognized revenue after deducting total refund amounts, discounts, and chargebacks from Gross Revenue.
Total Refund Amount	Financial	Sums the total monetary value of transactions refunded or credited back to students during the reporting period.
Refund Rate	Financial	Calculates the proportion of revenue or total orders returned to customers $\left(\frac{\text{Total Refund Amount}}{\text{Gross Revenue}} \times 100\right)$.
Average Order Value (AOV)	Financial	Measures the average revenue generated per completed transaction or enrollment $\left(\frac{\text{Gross Revenue}}{\text{Total Enrollments}}\right)$.
Revenue per Course	Financial	Aggregates gross or net revenue broken down by specific course titles, categories, or academic programs.
Revenue per Manager	Financial	Aggregates recognized sales revenue attributed to individual sales representatives or managers for performance tracking.
Revenue MoM / YoY Growth	Financial	Calculates the percentage growth in net or gross revenue compared to the previous month (Month-over-Month) or previous year (Year-over-Year).
3. Marketing Measures
Performance analytics evaluating advertising campaign efficiency, traffic generation, acquisition costs, and marketing ROI.
Measure Name	Category	Description & Business Definition
Marketing Spend	Marketing	Sums total advertising expenditure across all paid acquisition channels (e.g., Meta Ads, Google Ads, influencers) within a given timeframe.
Impressions	Marketing	Counts the total number of times ad creatives were rendered and displayed to prospective users across marketing channels.
Clicks	Marketing	Counts the total number of user interactions/clicks registered on promotional links, ad banners, or marketing campaigns.
Click-Through Rate (CTR)	Marketing	Evaluates ad creative engagement by measuring the percentage of impressions that resulted in a click $\left(\frac{\text{Clicks}}{\text{Impressions}} \times 100\right)$.
Cost per Click (CPC)	Marketing	Calculates the average marketing cost incurred for each user click delivered to landing pages $\left(\frac{\text{Marketing Spend}}{\text{Clicks}}\right)$.
Cost per Lead (CPL)	Marketing	Measures the efficiency of paid user acquisition by calculating the average cost spent to acquire a single lead $\left(\frac{\text{Marketing Spend}}{\text{Total Leads}}\right)$.
Customer Acquisition Cost (CAC)	Marketing	Computes the average marketing expenditure required to acquire a single paying enrolled student $\left(\frac{\text{Marketing Spend}}{\text{Converted Leads}}\right)$.
Return on Ad Spend (ROAS)	Marketing	Measures direct revenue generated per currency unit spent on advertising campaigns $\left(\frac{\text{Gross Revenue from Marketing}}{\text{Marketing Spend}}\right)$.
Marketing ROI	Marketing	Evaluates overall marketing profitability after accounting for ad spend $\left(\frac{\text{Net Revenue} - \text{Marketing Spend}}{\text{Marketing Spend}} \times 100\right)$.
4. Student and Course Measures
Academic metrics analyzing student activity levels, program progression, retention dynamics, and learning engagement.
Measure Name	Category	Description & Business Definition
Active Students	Student & Course	Counts the distinct number of enrolled students who logged in, submitted homework, or accessed learning material within a specified active window (e.g., past 30 days).
Completion Rate	Student & Course	Measures the percentage of enrolled students who successfully finished all mandatory modules and received a course completion certificate $\left(\frac{\text{Completed Students}}{\text{Total Enrollments}} \times 100\right)$.
Returning Student Rate	Student & Course	Calculates the percentage of total students who have enrolled in more than one course or program over their lifetime $\left(\frac{\text{Repeat Students}}{\text{Total Unique Students}} \times 100\right)$.
Dropout or Cancellation Rate	Student & Course	Tracks student churn by measuring the proportion of enrolled students who formally canceled their subscription or abandoned the program before completion.
Average Student Engagement	Student & Course	Quantifies student learning activity by averaging key behavior metrics (e.g., average hours spent on platform, video view rates, or assignment submission frequency).
3. Main DAX Measure Definitions
This section provides the technical specifications, DAX formulas, business rules, and formatting standards for all core measures implemented in the data model.
3.1 Lead and Sales Funnel Measures
Total Leads
DAX
Total_Leads = COUNT(Fact_Leads[LeadID])


Unique Leads
DAX
Unique_Leads = DISTINCTCOUNT(Fact_Leads[LeadID])



Converted_Leads
DAX
Converted_Leads = CALCULATE(
    [Total_Leads],
    NOT ISBLANK(Fact_Leads[ConvertedAt])
)


Total Enrollments
DAX
Total Enrollments = 
COUNT(FactEnrollments[EnrollmentID])


Lead-to-Enrollment Conversion Rate
DAX
Lead-to-Enrollment Conversion Rate = 
DIVIDE(
    [Total Enrollments], 
    [Total_Leads], 
    0)





Average Days to Enrollment
DAX
Average Days to Enrollment = 
AVERAGEX(
    FactEnrollments,
    VAR LeadDate = CALCULATE( SELECTEDVALUE( Fact_Leads[CreatedAt] ) )
    VAR EnrollDate = FactEnrollments[EnrollmentDate]
    RETURN
        IF(
            NOT ISBLANK( LeadDate ) && NOT ISBLANK( EnrollDate ),
            DATEDIFF( LeadDate, EnrollDate, DAY )
        )
)



Average First Response Time (Hours)
DAX
Average First Response Time (Hours) = 
AVERAGEX(
    FILTER(
        Fact_Leads,
        Fact_Leads[FirstContactAt] >= Fact_Leads[CreatedAt]
    ),
    DATEDIFF(
        Fact_Leads[CreatedAt],
        Fact_Leads[FirstContactAt],
        MINUTE
    )
) / 60




Lead Conversion vs Previous Period
DAX
Lead Conversion vs Previous Period = 
CALCULATE(
    [Lead-to-Enrollment Conversion Rate],
    SAMEPERIODLASTYEAR('DateTable'[Date])
)


3.2 Financial Measures

Gross Revenue
DAX
Gross Revenue = SUM(FactPayments[GrossAmountBase])




Net Revenue
DAX
Net Revenue = SUM(FactPayments[NetAmountBase])



Total Refund Amount
DAX
Total Refund Amount = SUM(FactPayments[RefundAmount])



Refund Rate
DAX
Refund Rate = 
DIVIDE(
    [Total Refund Amount],
    [Gross Revenue],
    0
)


Average Order Value
DAX
Average Order Value = AVERAGE(FactPayments[GrossAmountBase])




Revenue per Course
DAX
Revenue per Course = 
SUMX(
    VALUES(FactPayments[CourseID]),
    CALCULATE(SUM(FactPayments[GrossAmountBase]))
)




Revenue per Manager
DAX
Revenue per Manager = 
SUMX(
    VALUES(FactPayments[ManagerID]),
    CALCULATE(SUM(FactPayments[GrossAmountBase]))
)




Revenue PM
DAX
Revenue PM = 
CALCULATE(
    [Gross Revenue],
    PREVIOUSMONTH(DateTable[Date])
)




Revenue PY
DAX
Revenue PY = 
CALCULATE(
    [Gross Revenue],
    SAMEPERIODLASTYEAR(DateTable[Date])
)



Revenue YoY Change
DAX
Revenue YoY Change = [Gross Revenue] - [Revenue PY]





Revenue MoM Change
DAX
Revenue MoM Change = [Gross Revenue] - [Revenue PM]


3.3 Marketing Measures
Marketing Spend
DAX
Marketing Spend = SUM(Fact_MarketingSpend[SpendBaseCurrency])




Impressions
DAX
Impressions = SUM(Fact_MarketingSpend[Impressions])



CTR  Click-Through Rate
DAX
CTR = 
DIVIDE(
    SUM(Fact_MarketingSpend[Clicks]),
    SUM(Fact_MarketingSpend[Impressions]),
    0
)



CPC (Cost per Click)

DAX
CPC (Cost per Click) = 
DIVIDE(
    SUM(Fact_MarketingSpend[SpendBaseCurrency]),
    SUM(Fact_MarketingSpend[Clicks]),
    0
)



CPL (Cost per Lead)
DAX
CPL (Cost per Lead) = DIVIDE(
    SUM(Fact_MarketingSpend[SpendBaseCurrency]),
    SUM(Fact_MarketingSpend[LeadsReported]),
    0)
Total Paying Customers
DAX
Total Paying Customers = DISTINCTCOUNT(FactPayments[LeadID])




CAC Customer Acquisition Cost
DAX
CAC Customer Acquisition Cost = 
DIVIDE(
    [Marketing Spend],
    [Total Paying Customers],
    0
)




ROAS (Return on Advertising Spend)

DAX
ROAS Return on Advertising Spend = 
DIVIDE(
    [Gross Revenue],
    [Marketing Spend],
    0
)



MROI Marketing ROI
DAX
MROI Marketing ROI = 
DIVIDE(
    [Gross Revenue] - [Marketing Spend],
    [Marketing Spend],
    0
)



3.4 Student and Course Measures



Active Students
DAX
Active Students = DISTINCTCOUNT(FactStudentActiity[StudentID])





Completed Enrollments
DAX
Completed Enrollments = 
CALCULATE(
    COUNTROWS(FactEnrollments),
    FactEnrollments[EnrollmentStatus] = "Completed" 
)




Completion Rate
DAX
Completion Rate = 
DIVIDE(
    [Completed Enrollments],
    [Total Enrollments],
    0)





Repeat Enrolled Students
DAX
Repeat Enrolled Students = 
COUNTROWS(
    FILTER(
        VALUES(FactEnrollments[StudentID]),
        CALCULATE(COUNTROWS(FactEnrollments)) > 1
    )
)




Returning Student Rate
DAX
Returning Student Rate = 
DIVIDE(
    [Repeat Enrolled Students],
    [Total Enrolled Students],
    0
)




Dropout or Cancellation Enrollments
DAX

Dropout or Cancellation Enrollments = 
CALCULATE(
    COUNTROWS(FactEnrollments),
    FactEnrollments[EnrollmentStatus] IN { "Dropped", "Cancelled" }
)




Dropout or Cancellation Rate
DAX
Dropout or Cancellation Rate = 
DIVIDE(
    [Dropout or Cancellation Enrollments],
    [Total Enrollments],
    0)









Average Student Engagement
DAX
Average Student Engagement = 
DIVIDE(
    SUM(FactStudentActiity[LessonsCompleted]),
    DISTINCTCOUNT(FactStudentActiity[StudentID]),
    0
)






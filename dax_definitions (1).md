**1. Document Purpose**

The purpose of this document is to establish a centralized repository
and functional specification for all Data Analysis Expressions (DAX)
measures implemented within the analytical data model. It provides clear
definitions, underlying calculation logic, and business context to
ensure data consistency, maintainability, and accurate reporting across
power BI reports.

This documentation encapsulates DAX measures categorized into four core
business domains:

-   **Financial Measures:** KPI calculations covering revenue metrics,
    billing, payment performance, and profitability indicators.

-   **Lead and Sales Measures:** Operational metrics tracking lead
    acquisition volume, conversion rates, sales pipeline progression,
    and response time efficiency.

-   **Marketing Measures:** Performance analytics evaluating campaign
    reach, acquisition costs (CAC), channel efficiency, and return on
    marketing investment.

-   **Student and Courses Measures:** Academic metrics analyzing student
    enrollment rates, course completion progress, retention rates, and
    churn dynamics.

2\. Here is the comprehensive English documentation for all metrics
across our four core categories, formatted for technical specifications
and data model documentation.

### 1. Lead and Sales Funnel Measures

Metrics tracking lead acquisition volume, conversion efficiency,
pipeline velocity, and sales performance.

  --------------------------------------------------------------------------------
  **Measure Name**       **Category**   **Description & Business Definition**
  ---------------------- -------------- ------------------------------------------
  **Total Leads**        Lead & Sales   Calculates the total count of all captured
                         Funnel         lead records within the selected
                                        timeframe, not including duplicates or
                                        multi-channel entries.

  **Unique Leads**       Lead & Sales   Calculates the distinct count of
                         Funnel         individual prospective students based on a
                                        unique identifier, not including
                                        duplicates (e.g., LeadID).

  **Converted Leads**    Lead & Sales   Counts the number of valid leads who
                         Funnel         successfully transitioned from a prospect
                                        state to a confirmed paying
                                        customer/enrollment.

  **Total Enrollments**  Lead & Sales   Counts the total number of course
                         Funnel         enrollments generated across all students
                                        within the reporting period.

  **Lead-to-Enrollment   Lead & Sales   metric calculates the percentage of valid
  Conversion Rate %**    Funnel         leads that successfully convert into
                                        student enrollments. It uses the DIVIDE
                                        function.

  **Average Days to      Lead & Sales   Calculates the average elapsed time (in
  Enrollment**           Funnel         days) between the initial lead creation
                                        date and the final enrollment date.

  **Average First        Lead & Sales   Measures the average duration (in hours)
  Response Time**        Funnel         between the moment a lead is created and
                                        the first registered sales contact.

  **Lead Conversion vs   Lead & Sales   Evaluates the percentage change in the
  Previous Period %**    Funnel         conversion rate compared to the prior
                                        equivalent timeframe.

  **First Touch Leads**  Lead & Sales   This metric counts total leads based on
                         Funnel         their **first-touch** marketing channel,
                                        ignoring any filters from the marketing
                                        source table.

  **Last Touch Leads**   Lead & Sales   This metric counts total leads based on
                         Funnel         their **last-touch** marketing channel,
                                        ignoring any filters from the marketing
                                        source table

  **Won Leads**          Lead & Sales   This metric counts the total number of
                         Funnel         successful leads that reached the
                                        **\"Won\"** status in the pipeline.

  **Manager Conversion   Lead & Sales   This metric measures the conversion
  Rate %**               Funnel         efficiency of sales managers by
                                        calculating the percentage of total leads
                                        that successfully reach the **\"Won\"**
                                        status.
  --------------------------------------------------------------------------------

### 2. Financial Measures

KPI calculations covering revenue streams, transaction adjustments,
sales productivity, and financial performance trends.

  ----------------------------------------------------------------------------
  **Measure       **Category**   **Description & Business Definition**
  Name**                         
  --------------- -------------- ---------------------------------------------
  **Gross         Financial      This metric calculates total initial income
  Revenue**                      generated from all processed payments,
                                 including those later refunded or partially
                                 refunded.

  **Net Revenue** Financial      This metric calculates the true revenue by
                                 subtracting total refunds from gross revenue.

  **Total Refund  Financial      Calculates the total monetary value of all
  Amount**                       refunds issued, converted to the base
                                 currency.

  **Refund Rate   Financial      This metric calculates the percentage of
  %**                            gross revenue that was returned to customers
                                 through refunds.

  **Average Order Financial      Calculates the average revenue generated per
  Value (AOV)**                  enrollment by dividing gross revenue by total
                                 enrollments.

  **Revenue per   Financial      Calculates gross revenue evaluated per
  Course**                       individual course using an iterator function
                                 over course IDs.

  **Revenue per   Financial      Calculates gross revenue attributed to each
  Manager**                      sales manager using an iterator function over
                                 manager IDs.

  **Revenue PM    Financial      Calculates gross revenue for the equivalent
  (Previous                      period in the previous month using time
  Month)**                       intelligence functions.

  **Revenue PY    Financial      Calculates gross revenue for the same period
  (Previous                      in the previous year using time intelligence
  Year)**                        functions.

  **Revenue YoY   Financial      Measures the absolute change in gross revenue
  Change**                       compared to the same period in the previous
                                 year.

  **Revenue MoM   Financial      Measures the absolute change in gross revenue
  Change**                       compared to the previous month.

  **Sales         Financial      Calculates the total sales target for active
  target**                       sales managers over the selected period,
                                 adjusting dynamically for hire and
                                 termination dates while preventing display
                                 when filtered by individual courses.

  **Target        Financial      Measures the percentage of the sales target
  Completion %**                 achieved by dividing gross revenue by the
                                 sales target

  **Target        Financial      Calculates the absolute difference between
  Variance**                     gross revenue and the sales target to show
                                 whether sales are over or underperforming.
  ----------------------------------------------------------------------------

### **3. Marketing Measures**

Performance analytics evaluating advertising campaign efficiency,
traffic generation, acquisition costs, and marketing ROI.

  ----------------------------------------------------------------------------
  **Measure Name**  **Category**   **Description & Business Definition**
  ----------------- -------------- -------------------------------------------
  **Marketing       Marketing      Sums total advertising expenditure across
  Spend**                          all paid acquisition channels (e.g., Meta
                                   Ads, Google Ads, influencers) within a
                                   given timeframe.

  **Impressions**   Marketing      Counts the total number of times ad
                                   creatives were rendered and displayed to
                                   prospective users across marketing
                                   channels.

  **Clicks**        Marketing      Counts the total number of user
                                   interactions/clicks registered on
                                   promotional links, ad banners, or marketing
                                   campaigns.

  **Click-Through   Marketing      Measures the percentage of ad impressions
  Rate (CTR) %**                   that resulted in a click

  **Cost per Click  Marketing      Calculates the average cost paid for each
  (CPC)**                          ad click by dividing total marketing spend
                                   by total clicks

  **Cost per Lead   Marketing      Calculates the average acquisition cost for
  (CPL)**                          each lead by dividing total marketing spend
                                   by total valid leads

  **Customer        Marketing      Measures the average cost required to
  Acquisition Cost                 acquire a paying customer by dividing total
  (CAC)**                          marketing spend by total paying customers

  **Return on Ad    Marketing      Evaluates campaign revenue generation
  Spend (ROAS)**                   efficiency by dividing gross revenue by
                                   total marketing spend.

  **Marketing ROI   Marketing      Calculates the net return on marketing
  %**                              investment by dividing gross profit (gross
                                   revenue minus marketing spend) by total
                                   marketing spend.
  ----------------------------------------------------------------------------

### 4. Student and Course Measures

Academic metrics analyzing student activity levels, program progression,
retention dynamics, and learning engagement.

  ---------------------------------------------------------------------------
  **Measure Name**   **Category**   **Description & Business Definition**
  ------------------ -------------- -----------------------------------------
  **Active           Student &      Counts the distinct number of unique
  Students**         Course         students who currently hold an \"Active\"
                                    enrollment status.

  **Completion Rate  Student &      Measures the percentage of total
  %**                Course         enrollments that were successfully
                                    completed

  **Completed        Student &      Counts the total number of course
  Enrollments**      Course         enrollments that have successfully
                                    reached the \"Completed\" status.

  **Repeat Enrolled  Student &      Counts the number of unique students who
  Students**         Course         have enrolled in more than one course or
                                    session.

  **Returning        Student &      Calculates the percentage of repeat
  Student Rate %**   Course         students relative to the total number of
                                    enrolled students.

  **Dropout or       Student &      Counts the total number of course
  Cancellation       Course         enrollments that ended in a drop or
  Enrollments**                     cancellation.

  **Dropout or       Student &      Measures the percentage of total
  Cancellation Rate  Course         enrollments that resulted in a dropout or
  %**                               cancellation.

  **Average Student  Student &      Calculates the average number of
  Engagement**       Course         completed lessons per student by dividing
                                    total completed lessons by the distinct
                                    count of active students.
  ---------------------------------------------------------------------------

## 3. Main DAX Measure Definitions

This section provides the technical specifications, DAX formulas,
business rules, and formatting standards for all core measures
implemented in the data model.

**3.1 Lead and Sales Funnel Measures**

### **Total Leads**

**DAX**

Total_Leads = CALCULATE(

    COUNTROWS(Fact_Leads),

    Fact_Leads\[IsDuplicateCandidate\] = FALSE()

)

**Unique Leads**

**DAX**

Unique Leads =

CALCULATE(

    DISTINCTCOUNT(Fact_Leads\[LeadID\]),

    Fact_Leads\[IsDuplicateCandidate\] = FALSE()

)

**Converted_Leads**

**DAX**

Converted_Leads = CALCULATE(

    \[Total_Leads\],

    NOT ISBLANK(Fact_Leads\[ConvertedAt\])

)

**Total Enrollments**

**DAX**

Total Enrollments =

COUNT(FactEnrollments\[EnrollmentID\])

**Lead-to-Enrollment Conversion Rate**

**DAX**

Lead-to-Enrollment Conversion Rate =

DIVIDE(

    \[Total Enrollments\],

    \[Total_Leads\],

    0)

**Average Days to Enrollment**

**DAX**

Average Days to Enrollment =

AVERAGEX(

    FactEnrollments,

    VAR LeadCreatedAt =

        LOOKUPVALUE(

            Fact_Leads\[CreatedAtFinal\],

            Fact_Leads\[LeadID\],

            FactEnrollments\[LeadID\]

        )

    RETURN

        IF(

            NOT ISBLANK(LeadCreatedAt),

            INT(FactEnrollments\[EnrollmentDate\] - LeadCreatedAt)

        )

)

**Average First Response Time (Hours)**

**DAX**

Average First Response Time (Hours) =

AVERAGEX(

    FILTER(

        Fact_Leads,

        Fact_Leads\[FirstContactAt\] \>= Fact_Leads\[CreatedAt\]

    ),

    DATEDIFF(

        Fact_Leads\[CreatedAt\],

        Fact_Leads\[FirstContactAt\],

        MINUTE

    )

) / 60

**Lead Conversion vs Previous Period**

**DAX**

Lead Conversion vs Previous Period =

CALCULATE(

    \[Lead-to-Enrollment Conversion Rate\],

    SAMEPERIODLASTYEAR(\'DateTable\'\[Date\])

)

**First Touch Leads**

**DAX**

First Touch Leads =

VAR SelectedSources =

    VALUES(DimMarketingSource\[Source\])

RETURN

    CALCULATE(

        \[Total_Leads\],

        REMOVEFILTERS(DimMarketingSource),

        TREATAS(

            SelectedSources,

            Fact_Leads\[FirstTouchSource\]

        )

    )

**Last Touch Leads**

**DAX**

Last Touch Leads =

VAR SelectedSources =

    VALUES(DimMarketingSource\[Source\])

RETURN

    CALCULATE(

        \[Total_Leads\],

        REMOVEFILTERS(DimMarketingSource),

        TREATAS(

            SelectedSources,

            Fact_Leads\[LastTouchSource\]

        )

    )

**Won Leads**

**DAX**

Won Leads =

CALCULATE(

    \[Total_Leads\],

    Fact_Leads\[LeadStatus\] = \"Won\"

)

**Manager Conversion Rate**

**DAX**

Manager Conversion Rate =

DIVIDE(

    \[Won Leads\],

    \[Total_Leads\]

)

**Total Paying Customers**

**DAX**

Total Paying Customers = DISTINCTCOUNT(FactPayments\[LeadID\])

**3.2 Financial Measures**

**Gross Revenue**

**DAX**

Gross Revenue =

CALCULATE(

    SUM(FactPayments\[GrossAmountBase\]),

    FactPayments\[PaymentStatus\] IN { \"Completed\", \"Refunded\",
\"Partially Refunded\" }

)

**Net Revenue**

**DAX**

Net Revenue =

CALCULATE(

    SUM(FactPayments\[NetAmountBase\]),

    FactPayments\[PaymentStatus\] IN { \"Completed\", \"Partially
Refunded\" }

)

**Total Refund Amount Base**

**DAX**

Total Refund Amount Base =

CALCULATE(

    SUMX(

        FactPayments,

        FactPayments\[RefundAmount\] \*
FactPayments\[ExchangeRateToBase\]

    ),

    FactPayments\[PaymentStatus\] IN { \"Completed\", \"Refunded\",
\"Partially Refunded\" }

)

**Refund Rate**

**DAX**

Refund Rate =

DIVIDE(

    \[Total Refund Amount Base\],

    \[Gross Revenue\],

    0

)

**Average Order Value**

**DAX**

Average Order Value =

DIVIDE(

    \[Gross Revenue\],

    \[Total Enrollments\])

**Revenue per Course**

**DAX**

Revenue per Course =

SUMX(

    VALUES(FactPayments\[CourseID\]),

    CALCULATE (\[Gross Revenue\])

)

**Revenue per Manager**

**DAX**

Revenue per Manager =

SUMX(

    VALUES(FactPayments\[ManagerID\]),

    CALCULATE (\[Gross Revenue\])

)

**Revenue PM**

**DAX**

Revenue PM =

CALCULATE(

    \[Gross Revenue\],

    PREVIOUSMONTH(DateTable\[Date\])

)

**Revenue PY**

**DAX**

Revenue PY =

CALCULATE(

    \[Gross Revenue\],

    SAMEPERIODLASTYEAR(DateTable\[Date\])

)

**Revenue YoY Change**

**DAX**

Revenue YoY Change = \[Gross Revenue\] - \[Revenue PY\]

**Revenue MoM Change**

**DAX**

Revenue MoM Change = \[Gross Revenue\] - \[Revenue PM\]

**Sales Target**

**DAX**

Sales Target =

IF(

    ISFILTERED(Dim_Course\[CourseName\]),

    BLANK(),

    SUMX(

        VALUES(Dim_Manager\[ManagerID\]),

       

        VAR Target = CALCULATE(MAX(Dim_Manager\[MonthlySalesTarget\]))

        VAR Hire = CALCULATE(MIN(Dim_Manager\[HireDate\]))

        VAR Term = CALCULATE(MAX(Dim_Manager\[TerminationDate\]))

       

        VAR ActiveMonths =

            CALCULATE(

                COUNTROWS(

                    SUMMARIZE(DateTable, DateTable\[Year\],
DateTable\[MonthNumber\])

                ),

                DateTable\[Date\] \>= Hire,

                ISBLANK(Term) \|\| DateTable\[Date\] \<= Term

            )

           

        RETURN

            Target \* ActiveMonths

    ))

**Target Completion**

**DAX**

Target Completion % =

DIVIDE(

    \[Gross Revenue\],

    \[Sales Target\],

    0

)

**Target Variance**

**DAX**

Target Variance =

\[Gross Revenue\] - \[Sales Target\]

**3.3 Marketing Measures**

**Marketing Spend**

**DAX**

Marketing Spend = SUM(Fact_MarketingSpend\[SpendBaseCurrency\])

**Impressions**

**DAX**

Impressions = SUM(Fact_MarketingSpend\[Impressions\])

**CTR Click-Through Rate**

**DAX**

CTR =

DIVIDE(

    \[Clicks\],

\[Impressions\],

)

**CPC (Cost per Click)**

**DAX**

CPC (Cost per Click) =

DIVIDE(

   \[MarketingSpend\],

   \[Clicks\],

    0

)

**CPL (Cost per Lead)**

**DAX**

CPL (Cost per Lead) = DIVIDE(

    \[Marketing Spend\],

    \[Total_Leads\],

    0

)

Total Paying Customers

**DAX**

Total Paying Customers = DISTINCTCOUNT(FactPayments\[LeadID\])

**CAC Customer Acquisition Cost**

**DAX**

CAC Customer Acquisition Cost =

DIVIDE(

    \[Marketing Spend\],

    \[Total Paying Customers\],

    0

)

**ROAS (Return on Advertising Spend)**

**DAX**

ROAS Return on Advertising Spend =

DIVIDE(

    \[Gross Revenue\],

    \[Marketing Spend\],

    0

)

**MROI Marketing ROI**

**DAX**

MROI Marketing ROI =

DIVIDE(

    \[Gross Revenue\] - \[Marketing Spend\],

    \[Marketing Spend\],

    0

)

**3.4 Student and Course Measures**

**Active Students**

**DAX**

Active Students =

CALCULATE(

    DISTINCTCOUNT(FactEnrollments\[StudentID\]),

    FactEnrollments\[EnrollmentStatus\] = \"Active\"

)

**Completed Enrollments**

**DAX**

Completed Enrollments =

CALCULATE(

    COUNTROWS(FactEnrollments),

    FactEnrollments\[EnrollmentStatus\] = \"Completed\"

)

**Completion Rate**

**DAX**

Completion Rate =

DIVIDE(

    \[Completed Enrollments\],

    \[Total Enrollments\],

    0)

**Repeat Enrolled Students**

**DAX**

Repeat Enrolled Students =

COUNTROWS(

    FILTER(

        VALUES(FactEnrollments\[StudentID\]),

        CALCULATE(COUNTROWS(FactEnrollments)) \> 1

    )

)

**Returning Student Rate**

**DAX**

Returning Student Rate =

DIVIDE(

    \[Repeat Enrolled Students\],

    \[Total Enrolled Students\],

    0

)

**Dropout or Cancellation Enrollments**

**DAX**

Dropout or Cancellation Enrollments =

CALCULATE(

    COUNTROWS(FactEnrollments),

    FactEnrollments\[EnrollmentStatus\] IN { \"Dropped\", \"Cancelled\"
}

)

**Dropout or Cancellation Rate**

**DAX**

Dropout or Cancellation Rate =

DIVIDE(

    \[Dropout or Cancellation Enrollments\],

    \[Total Enrollments\],

    0)

**Average Student Engagement**

**DAX**

Average Student Engagement =

DIVIDE(

    SUM(FactStudentActiity\[LessonsCompleted\]),

    DISTINCTCOUNT(FactStudentActiity\[StudentID\]),

    0

)

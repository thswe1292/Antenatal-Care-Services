# Antenatal-Care-Services
The Antenatal Care Dashboard is a data-driven project developed using SQL and Power BI to provide comprehensive insights into maternal health care. 
This dashboard focuses on tracking key maternal care metrics and trends to enhance the quality of antenatal services. 

Features
Comprehensive Maternal Care Tracking: Monitor vital metrics such as antenatal care visits, number of pregnant women receiving deworming medicine, tetanus, clean delivery kit, newborn care kit and so on.
SQL-Based Data Management: Use SQL queries to extract, clean, and transform large datasets for analysis.
Power BI Visualizations: Utilize Power BI's robust visualization tools to create dynamic and interactive dashboards.
Real-Time Data Updates: Ensure data accuracy with automated updates and refreshes.
Custom Metrics and KPIs: Develop custom metrics using Power BI formulas to measure the effectiveness of antenatal care services.

Example functions: 

AgeGroup = SWITCH(
        TRUE(),
            ANCTbl[Age] < 20 , "Under 20",
            ANCTbl[Age] >= 20 && ANCTbl[Age]<30, "20-30",
            ANCTbl[Age] >= 30 && ANCTbl[Age] < 50 && ANCTbl[AgeUnit]="Year", "31-49",
            ANCTbl[Age]>= 50, "50+", 
            "Unknown"
        )

4Visits_WHO = Calculate( 
    DISTINCTCOUNT(ANCTbl[RegistrationNumber]),
    FILTER(
        SUMMARIZE(
            ANCTbl,
            ANCTbl[RegistrationNumber],
            ANCTbl[FirstTrimesterVisits],
            ANCTbl[SecondTrimesterVisits],
            ANCTbl[ThirdTrimesterVisits]
           
        ),
        ANCTbl[FirstTrimesterVisits]>=1 && ANCTbl[SecondTrimesterVisits]>=1 && ANCTbl[ThirdTrimesterVisits]>=2 &&
        (ANCTbl[FirstTrimesterVisits]+ANCTbl[SecondTrimesterVisits] + ANCTbl[ThirdTrimesterVisits])>=4
))



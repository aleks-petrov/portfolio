---
description: "Transaction-Level Dashboard for Variance from Budget Analysis"
featured_image: "/images/dashboard1.png"
tags: 
title: "2. Variance & Transactions Dashboard"
---

Summary: Dashboard that incorporates transaction-level data to assist in month-end variance from budget analysis. Utilized ERP Cloud (SAP HANA) in order to pull the relevant transaction data, the EPM (Hyperion) to pull budget data, and a SQL query to pull relevant invoice information. Then transformed and prepared the data with PowerQuery in PowerBI. Afterwards used DAX and PowerPivot in PowerBI to create a model. Finally used PowerBI to visualize the data and create a dashboard. Goal was to have an automated report for routine analysis at each month end for the reporting analyst, operations, and the FP&A group.  

---

## Background

For one of my previous internships at an upstream oil & gas company, I had the opportunity to build a dashboard that incorporated transaction-level data in order to aid the reporting analyst with month-end variance analysis and operations with transaction analysis. This information was later compiled and present to several different parties like the CEO and the FP&A group. I've recreated that dashboard here for demonstrative purposes with randomly generated data. 

{{< figure src="/images/dashboard1.png">}}

## Extract

For the transaction-level data, I began by narrowing down the relevant expenses from the ERP via several filters in order for the totals to tie to the PnL. I then used a SQL query in the enterprise data flows in PowerBI to pull the relevant transaction-level data. For the budget data, I pulled the relevant data for that asset area and time period. And lastly, I also pulled the invoice information from via a SQL pull. 

---

## Transform

Utilizing PowerQuery in PowerBI after the initial SQL pull, I was able to clean and prepare all of the tables for analysis later on. This included a combination of manipulating data types, making dates and other data formattable, removing duplicates, among other things. 

---

## Model

The initial model building stage I utilized PowerPivot in PowerBI to link all tables in order to enable cross filtering. This included ensuring one-to-many relationships and proper cross filtering directions. I then used DAX measures in order to create a more dynamic model. DAX measures were most useful in summing costs, budget data and computing variance calculations. 

{{< figure src="/images/dashboard2.png">}}

---

## Sharing

In order to enable reusability and sharability, the report was posted to the corporation's PowerBI website where permissions could be set for the relevant individuals who needed the report as well as a scheduled Outlook delivery based on their needs.

{{< figure src="/images/dashboard3.png">}}

[Link to GitHub Repository](https://github.com/aleks-petrov/variance_dashboard)
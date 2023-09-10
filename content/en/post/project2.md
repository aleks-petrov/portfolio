---
description: "Personal Finances Dashboard"
featured_image: "/images/pfdashboard1.png"
tags: 
title: "3. Personal Finances Dashboard"
---

Summary: Excel model that incorporates personal financial information like expenses and budget data. Utilizing PowerQuery to extract and transform the data, PowerPivot to create a model with logic, and finally Excel to display the data in a dashboard for analysis. This model is an example of what I use to track my personal finances except it uses randomized data. Goal was to have an automatable report for easy analysis of personal financial data. 

---

## Extract & Transform

The Excel workbook is set up with sheets for each month. You would have to populate each month's expenses with a bank account data pull and label it with the correct expense category and expense type. Ultimately, the table for each month would look like this: 

{{< figure src="/images/expense_table_example.png">}}

Afterwards, all the monthly data across the entire workbook would be aggregated in PowerQuery using the following m-code:    
<br>  
<br>
``Source = Excel.Workbook(File.Contents("C:\git\budget&expenses\model_showcase\mock_personal_financial_model.xlsx"))``    
<br>  
<br>
The function of this is to convert the file contents of the file into an Excel workbook; afterwards, the table data would be aggregated by expanding the table column.  
<br>  
<br>
The ultimate product in PowerQuery would look like this: 

{{< figure src="/images/pf_pq_ex1.png">}}

## Load & Model

In order to load and model the data, it would only be loaded as a connection into the Excel workbook and into the PowerPivot model.  
<br>  
<br>
An example of some calculated measures used in the model include:  
<br>  
Monthly Average:  
<br>
``AvgCosts:=AVERAGEX( VALUES('Date'[Index]), [Costs])``   
<br>  
Variance from Budget:  
<br>
``BudgetVarDollars:=[Costs] - [BudgetAmount]``  
<br>  
These DAX measures help with modelling the data which will be displayed later in the dashboard.  
<br>  
<br>
Ultimately, the model in PowerPivot came out like this: 

{{< figure src="/images/pf_pp_ex1.png">}}

The consequence of this model is that expense and budget data can both be filtered by expense category and month. 

## Product

The final product was a dashboard with a table displaying average by category, costs by category (monthly), variance from budget, and a chart displaying variance from budget. This dashboard would be efficacious in examining your personal expenses and determining what has caused variance from your budget. 

{{< figure src="/images/pfdashboard1.png">}}

[Link to GitHub Repository](https://github.com/aleks-petrov/personal-finances-dashboard)
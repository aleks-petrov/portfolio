---
description: "Well Production & Project Economics Dashboard"
featured_image: "/images/well_dashboard_screenshot.png"
tags: 
title: "1. Well Production & Project Economics Dashboard"
---

Summary: PowerBI dashboard that incorporates well production data and oil prices over time. This is a stylized version of a dashboard that was built for use by the FP&A group of an upstream oil & gas company I previous interned with. The dashboard visualizes and reports well production and revenue over time, as well as the project economics of the individual wells going forward. The dashboard includes net present value measures in order to determine profitability of the producing wells as well as scenario analysis in forecasting revenue. The goal of this dashboard is to test out forward looking analytical features in an oil & gas context. 

---

## Extract 

The first part of this project involved downloading the Volve field dataset from Kaggle: https://www.kaggle.com/datasets/lamyalbert/volve-production-data. This dataset is an open source dataset provided by Equinor from their North Sea oil field. This public data set most closely resembles the data I was able to work with in the firm and present a unique opportunity to look at the dynamics of a North sea field. The other dataset used is monthly oil price data retrieved from Macrotrends: https://www.macrotrends.net/1369/crude-oil-price-history-chart. Together, these two data sets will be used to create a model. 

---

## Transform

The next step of the process was to import the data into PowerQuery and to clean the data. As these are both publically available datasets, they were relatively ready for use. The only particular that might affect analysis was the fact that the production data duplicated dates in order to show production for each well. As you'll see later, this was sidestepped in the modelling phase using Dax while a conventional tabular calculated column approach would've been less efficient to deploy. 

## Load & Model

Once the datasets were loaded, this is what they looked like in the PowerQuery editor:  
<br>  
Production Data: 
{{< figure src="/images/production_dataset.png">}}  
<br>
Price Data: 
{{< figure src="/images/price_data.png">}}  
<br>
The next step of the process was to create a model by linking up the tables. Ultimately, this was the result: 
{{< figure src="/images/production_model.png">}} 
This model will enables us to create a DAX calculated measure for revenue:  
<br>
``Revenue = [BOE (Total)] * sum('Crude Oil Prices'[U.S. Crude Oil First Purchase Price Dollars per Barrel])``  
<br>  
For NPV:  
``NPV = XNPV('Monthly Production Data',[Revenue],'Monthly Production Data'[Period (Prod.)],.05)``  
<br>  
Other measures include "Barrels of Oil", "Gas BOE", "BOE Total", "Avg. BOE" and Pessimistic/Neutral/Pessimistic measures for NPV and Revenue; these latter six will be helpful in the forecasting of revenue. 

---

## Visualization

The Dashboard: 
{{< figure src="/images/well_dashboard_screenshot.png">}} 
The end result was a dashboard with a number of visuals that will aid in reporting and forecasting purposes.  
<br>   
The first is an oil & gas production over time area chart with a multi-row scorecard: 
{{< figure src="/images/production_visual1.png">}} 
This visual showcases oil and gas production seperately over time. This would be useful in visualizing specific periods of production, ratio of production, as well as the overall declining production of the field. The multi-row scorecard next to it displays more granular detail regarding production. The functionality of this and all other charts is the ability to cross filter across dimensions like individual wells, time, and production.  
<br>  
The next visual is a production and revenue over time line and clustered column chart: 
{{< figure src="/images/production_visual2.png">}} 
This visual showcases the same line visual for production as the above chart, though overall, and additionally displays revenue in a column chart visual along a secondary axis. This aids in showing when oil prices might have picked up the slack in driving revenue when production might've been low. This is due to prices being the only driving force in this model of why revenue doesn't follow production exactly. The revenue measure is calculated using historical prices and oil & gas production.  
<br>  
The following visual is a series of donut charts that show well and production ratios: 
{{< figure src="/images/production_visual3.png">}} 
These visuals would be useful in determining production mix and other more granular data regarding the individual wells. These visuals can be cross filtered by time using the other visuals or the data slicer in order to show you the production mix at different periods.  
<br>  
The final visual is a forecast visual with a NPV and scenario-analysis feature: 
{{< figure src="/images/production_visual4.png">}} 
This visual would be most useful in testing different scenarios and the sensitivities of inputs like oil price, discount rate, and production in determining revenue. The scenario selection would be applied across both the NPV computation as well as the revenue forecast. The forecast is created employing time-series econometric methods and a seasonality factor which is appropriate for the commodities market which is known to display seasonality. Ultimately, this visual would be most efficacious in forward looking analytical decisions, in conjunctions with all the others. 

[Link to GitHub Repository](https://github.com/aleks-petrov/production_dashboard)
# Data requirements for forecasting<a name="data-requirements-for-forecasting"></a>

Amazon Connect generates forecasts using a machine\-learning model tailored for contact center operations\. It requires a sufficient amount of recent contact data to ensure the model is trained with relevant data and is able to generate high\-quality forecasts\.

## Important things to know<a name="important-things-to-know-data-requirements"></a>
+ Amazon Connect generates forecasts using historical data for all queues included in all forecast groups\.
+ Amazon Connect performs a *data sufficiency* check \(is there enough data\) based on the aggregation of all queues included in all forecast groups\.
  + At least 2,000 monthly contacts in the past six months are required to successfully generate a forecast\.
    + Amazon Connect does not require 2,000 monthly contacts for every queue\. All queues in all forecast groups must total to more than 2,000 monthly contacts\.
  + While Amazon Connect can generate forecasts with six months of data, we recommend 12 months of recent contact data to ensure contact patterns \(for example, seasonality\) are properly captured\.
+ Amazon Connect performs a *data recency* check \(is the data recent enough\) based on the aggregation of all queues included in all forecast groups\.
  + At least one data point in the past four weeks is required to successfully generate a forecast\.

## Do I have a sufficient amount of recent contact data?<a name="provide-sufficient-data-for-forecasting"></a>
+ If you have been using Amazon Connect for more than 12 months, you do not need to provide any additional data\.
+ If you have been using Amazon Connect for more than six months but less than 12, we recommend providing additional historical data\. You can import historical data from a source that is external to Amazon Connect\. For instructions, see [Import historical data](import-data-for-forecasting.md)\. 
+ If you have been using Amazon Connect for less than six months, make sure it has at least six months of data\. Otherwise, forecasting will fail\. 

For instructions about how to import more data, see [Import historical data](import-data-for-forecasting.md)\.
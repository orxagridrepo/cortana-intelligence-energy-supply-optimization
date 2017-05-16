# Resource Optimization- A Cortana Intelligence Solution How-To Guide

Accurately forecasting spikes in demand for products and services can give a company a competitive advantage. The better the forecasting, the more they can scale as demand increases, and the less they risk holding onto unneeded inventory. Use cases include predicting demand for a product in a retail/online store, forecasting hospital visits, and anticipating power consumption.

This solution focuses on Supply Optimization within the energy sector. Storing energy is not cost-effective, so utilities and power generators need to forecast future power consumption so that they can efficiently balance the supply with the demand. During peak hours, short supply can result in power outages. Conversely, too much supply can result in waste of resources. Advanced demand forecasting techniques detail hourly demand and peak hours for a particular day, allowing an energy provider to optimize the power generation process. This solution using Cortana Intelligence enables energy companies to quickly introduce powerful forecasting technology into their business.

The process described above is operationalized and deployed in the Cortana Intelligence Suite. This solution will enable companies to ingest historical energy data, predict future demand, and obtain optimal pricing recommendations on a regular basis. As a result, the solution drives opportunities for improved profitability and reductions in time and effort allocated to pricing tasks.

For a discussion of the analytical approach used in this solution, see the [Solution Description](https://github.com/Azure/cortana-intelligence-price-optimization/blob/master/Manual%20Deployment%20Guide/Solution%20Description.md) in the Manual Deployment Guide.

## Solution Architecture
In this session, we provide more details about how the above analytical approach is operationalized in Cortana Intelligence. The following chart describes the solution architecture.

![Architecture Diagram](Manual Deployment Guide/Figures/resourceOptArchitecture.png)
### What’s Under the Hood
Raw simulated transactional data are pushed into Azure Data Lake Storage, whence the Spark Jobs run on HDInsight Cluster will take the raw data as inputs and:

1. Turn the unstructured raw data into structured data and aggregate the individual transactions into weekly sales data.
2. Train demand forecasting model on the aggregated sales data.
3. Run the optimization algorithm and return the optimal prices for all products in all competing groups.

The final results are visualized in Power BI Dashboard. The whole process is scheduled weekly, with data movement and scheduling managed by Azure Data Factory.

### About Implementation on Spark
A parallel version of the price optimization algorithm is implemented on Spark. Utilizing `RDD.map()`, the independent price optimization problems for products in different competing group can be solved in parallel, reducing runtime.

## Solution Dashboard
The snapshot below shows the Power BI dashboard that visualizes the results of demand forecasting and price optimization solution. 

![Dashboard](https://github.com/Azure/cortana-intelligence-price-optimization/blob/master/Manual%20Deployment%20Guide/Figures/PriceOptDashboard.png)

The dashboard contains four parts:
1. **Price Elasticity**: shows the relationship between sales and price, and using the filters on the right, you can select to view the results for a specific store, department or product.
2. **Demand Forecasting**: shows the results and performance of the demand forecasting model.
3. **Price Optimization** shows the profit gain realized by using the recommended optimal price, as well as corresponding changes in sales volume and price that resulted in the profit gain.
4. **Execution Time** shows the time decomposition of different computational stages, allowing the user to monitor the runtime.

## Getting Started

This solution template contains materials to help both technical and business audiences understand our demand forecasting and price optimization solution built on [Cortana Intelligence](https://www.microsoft.com/en-us/server-cloud/cortana-intelligence-suite/Overview.aspx).

## Business Audiences

In this repository you will find a folder labeled **[Solution Overview for Business Audiences](https://github.com/Azure/cortana-intelligence-price-optimization/tree/master/Solution%20Overview%20for%20Business%20Audiences)**. This folder contains:
- Walking Deck: In-depth exploration of the solution for business audiences

For more information on how to tailor Cortana Intelligence to your needs, [connect with one of our partners](http://aka.ms/CISFindPartner).

## Technical Audiences

See the **[Manual Deployment Guide](https://github.com/Azure/cortana-intelligence-price-optimization/blob/master/Manual%20Deployment%20Guide)** folder for a full set of instructions on how to deploy the end-to-end pipeline, including a step-by-step walkthrough and files containing all the scripts that you’ll need to deploy resources. **For technical problems or questions about deploying this solution, please post in the issues tab of the repository.**





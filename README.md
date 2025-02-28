# Cryptocurrency Data Pipeline Architecture Using Azure & Databricks
This project implements a real-time streaming data pipeline to process cryptocurrency data. The data is sourced from CoinMarketCap and streamed through Azure Event Hub. The raw data is ingested into Azure Data Lake Storage (ADLS) in its original format JSON into Bronze Container, and further processed and transformed into a more refined Delta format into Silver & Gold Container using Delta Lake and Azure Databricks.



![image](https://github.com/user-attachments/assets/1d060dee-5ba5-4987-a0af-9de75853582d)

Architecture Overview
Data Sourcing:
 * CoinMarketCap API is used to fetch live cryptocurrency data.
 * The data is streamed into Azure Event Hub for real-time ingestion.
Stream Analytics:
 * Azure Stream Analytics processes the raw streaming data from Event Hub.
Data Storage:
 Raw Data is stored in Azure Data Lake Storage (ADLS) in a Bronze layer.
 Transformed Data is stored in Delta Lake format in Silver layer.
Delta Lake Processing:
 Data from the Bronze layer is read using Azure Databricks, transformed, and written back in the Silver layer in Delta format.
# Project Workflow
1. CoinMarketCap Streaming Data to Event Hub
   
     Event Hub acts as a message broker where real-time cryptocurrency data from CoinMarketCap API is ingested.
  
     The data from CoinMarketCap includes:
  
     Cryptocurrency name (Name)
  
     Symbol (Symbol)
  
     USD Price (Price)
  
     Percent changes in 1 hour, 24 hours, 7 days, 30 days, etc.
  
     Market Cap, Volume, Circulating Supply, etc.
  
 3. Stream Data to Azure Data Lake Storage
   
    Azure Stream Analytics listens to the Event Hub, processes the incoming data, and writes it to Azure Data Lake Storage in JSON format into Bronze container. 
    Data is written without any transformation in this stage; it is stored in its raw format for later processing.
    
4. Writing Raw Data to Delta Format
   
    The raw data is stored in Azure Data Lake Storage (ADLS) Silver container. This data is not transformed at this stage but it is cleaned.
    Delta Lake is used to organize and manage the data in Delta format.
   
5. Delta Lake Silver Layer Transformation
   
   Data from the Silver layer is read using Azure Databricks. Transformations are applied on data (e.g., rounding values, handling missing data, or performing aggregations). Once transformed, the data is stored in Delta Tables in the Silver layer. Delta Lake ensures data consistency, schema evolution, and versioning. The transformed data is written back into Delta format into the Gold layer.

Azure Components Used:

Azure Event Hub: Handles real-time data ingestion from CoinMarketCap API.

Azure Stream Analytics: Processes incoming streams from Event Hub and stores them in ADLS.

Azure Data Lake Storage (ADLS): Stores both raw and transformed data in Bronze and Silver layers.

Azure Databricks: Reads data from ADLS, performs transformations, and stores it back as Delta tables.

Delta Lake: Provides ACID transactions, schema enforcement, and versioning for the data stored in ADLS.

Project Steps:

Step 1: Setup Event Hub and Stream Data

Register and configure an Azure Event Hub instance to receive streaming data.

Use CoinMarketCap API to stream cryptocurrency data into Event Hub.

Step 2: Process Data with Azure Stream Analytics

Create a Stream Analytics Job to process incoming data from Event Hub and output it to Azure Data Lake Storage (ADLS) in raw format.

Step 3: Store Raw Data in Data Lake (Bronze Layer)

Store the raw streaming data in ADLS without transformation, ensuring it is easily accessible for further processing.

Step 4: Read Raw Data from Data Lake

Use Azure Databricks to read raw data from ADLS (Bronze layer).

Step 5: Apply Transformations and Store in Silver Layer

Perform necessary transformations (such as rounding numerical values, handling missing data, or aggregating data) within Azure Databricks. Write the transformed data back into ADLS in Delta format, under the Gold  layer.

Step 6: Query and Analyze Data

Use Delta Lake for efficient querying, analytics, and reporting. Leverage the benefits of ACID transactions and schema evolution to handle future changes in data structure.


# Conclusion

This project demonstrates the full lifecycle of real-time streaming data ingestion, storage, and transformation. Using Azure Event Hub, Stream Analytics, Azure Data Lake Storage, and Azure Databricks, you can 
easily store and process large amounts of data for advanced analytics and machine learning.

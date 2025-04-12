# Building an End-to-End Data Analytics Pipeline on Microsoft Azure

## Steps:

#### step1: Ingest the raw sales data into ADLS storage using ADF
#### step2: Transformed the data in Azure Databricks by cleaning it and computing new fields.
#### step3: Stores the transformed data back in ADLS.
#### step4: Loads the transformed data into an Azure SQL Database for further analysis.

## Resource-creation:

#### 1. Created an ADLS Storage account -- while creation enable Hirerchical Namespace
#### 2. Created 2 container one for Raw data another for Processed data
#### 3. Create ADF and Azure Databricks workspace
#### 4. Create an Azure SQL database resource

## Step-1:

#### 1. Loaded the sales data into Raw container
#### 2. Created a Linked service for ADLS storage to connect from ADF
#### 3. Created 2 dataset, one for Raw container and another for Processed container, which are acting as source and sink respectively
#### 4. Craetd an ADF pipeline with Copy Activity
#### 5. In copy activity, used dataset linked to Raw container in Source and dataset linked to Processed container in Sink
#### 6. Run it and load the data

## Step-2:

#### 1. Imported Libraries
#### 2. To access ADLS storage from Azure Databricks:
  &nbsp;&nbsp;&nbsp;&nbsp; 2.1 Set up the service principal 
  &nbsp;&nbsp;&nbsp;&nbsp; 2.2 To ensure accessing ADLS using Service Principal, we need to assign role to Service Principal as Storage Blob Data Contributor, to allow read, write on ADLS
  &nbsp;&nbsp;&nbsp;&nbsp; 2.3 Created an Azure Key Vault and assign role as Key Vault Administrator
  &nbsp;&nbsp;&nbsp;&nbsp; 2.4 Create secrets using Service Principal client ID and password
  &nbsp;&nbsp;&nbsp;&nbsp; 2.5 Create an Azure Key Vault backed Scope to fetch secret from Azure Key Vault
  &nbsp;&nbsp;&nbsp;&nbsp; 2.6 Now we are ready to configure the connection
#### 3. Configure Databricks + Azure Data Lake Gen 2 account connection
#### 4. Create mount point for accessing ADLS Gen 2 storage as a local storage
#### 5. Read the file from ADLS Raw container using spark readed API and read it using Mount-Point
#### 6. Clean and transform the data as per business requirement

## Step-3:

#### 1. To store transformed data into ADLS writing the dataframe into ADLS in Parquet file format

## Step-4:

#### 1. Created a Linked service for Azure SQL Database to connect from ADF
#### 2. Created a SQL table called SalesData
#### 3. Created 2 dataset, one for Processed container pointing to Parquet file and another for SQL table(SalesData), which are acting as source and sink respectively
#### 4. Craetd an ADF pipeline with Copy Activity
#### 5. In copy activity, used dataset linked to Processed container in Source and dataset linked to SQL table in Sink
#### 5. Run it and load the data

## Now, we can use the table data for further analysis


#### Storage-Account link: https://portal.azure.com/#@oindrilamoonmete1999gmail.onmicrosoft.com/resource/subscriptions/44da3401-226e-4354-b234-1f7857fac629/resourceGroups/TestEnvironment/providers/Microsoft.Storage/storageAccounts/storageadlsdemooin/containersList

#### Raw container file link: https://storageadlsdemooin.blob.core.windows.net/herovired-raw/sales_data_proj_2.csv

#### Processed container file(loaded by ADF) link: https://storageadlsdemooin.blob.core.windows.net/herovired-processed/sales_data_proj_2.csv

#### Processed container file(loaded as parquet after databricks transformation) link: https://storageadlsdemooin.blob.core.windows.net/herovired-processed/sales_data_transformed/part-00000-tid-3492786193996661090-d6fd3986-9077-4a60-8815-1b5c28ce21f1-19-1.c000.snappy.parquet

#### SQL table: SalesData

#### Databricks Notebook link: https://adb-1901518579341212.12.azuredatabricks.net/editor/notebooks/3618207380252548?o=1901518579341212#command/7297826428019200

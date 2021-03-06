# BlockchainBatchETL

Analyze the blocks and quantify anomalies. Data Source : ICON Blockchain

## Table of Contents
1. [Motivation](#Motivation)
2. [Project Setup](#Project-Setup)
3. [Usage](#Usage)
    - [Project Infrastructure](#Project-Infrastructure)
    - [SQL Analysis](#SQL-Analysis)
        - [Schemas](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/schemas.md#sql-schemas)
        - [Materialized Views](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#materialized-views)
    - [Charts and Dashboard](#Charts-and-Dashboard)

## Motivation
Blockchain data is like Big Data. But unlike Big Data, querying blockchain data is expensive. This is due to the fact that Blockchain Data lives in a decentralized network of nodes that are constantly replicating records among themselves. This project will allow you to deploy a powerful infrastructure for blockchain ETL, creating an environment for data transfer and to perform analytics on the queried data. The data pipeline is develoved using airflow, allowing multiple tasks to schedule that might have dependencies on one another. This project also uses AWS and terraform for easy deployment. 

## Projet Setup
There are Three main components of this project: 
1. Project Infrastructure
2. SQL Analysis  
3. Charts and Dashboard

## Usage 

### Project Infrastructure
The Infrastructure needed for this project can be found at: [terragrunt-icon-analytics](https://github.com/kevinpatelco/terragrunt-icon-analytics). Some postgres scripts were added to allow analysis on data and create charts in Apache Superset. 

Prerequisites:
* Terraform v0.12.29
* Terragrunt v0.23.40
* Ansible


The Infrastructure components are dependent on previous components. Clone the directory. 
 
 ``` git clone https://github.com/kevinpatelco/terragrunt-icon-analytics```.
 
Navigate to ```icon-analytics/aws```. You will find all the needed infrastructure components here. Use the following order to deploy the infrastructure by running ```terragrunt apply``` after navigating to the respective folder: 

  1. network
  2. rds
  3. postgres
  4. airflow
  5. superset

### SQL Analysis  

- [Schemas](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/schemas.md#sql-schemas)
  - [Blocks](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/schemas.md#blocks)
  - [Transactions](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/schemas.md#transactions)
  - [Logs](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/schemas.md#logs)
  - [Receipts](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/schemas.md#Receipts)
  
- [Materialized Views](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#materialized-views) 
  - [Transactions Count Distribution](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#transactions-count-distribution)
  - [Addresses with most transactions received](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#addresses-with-most-transactions-received)
  - [Transactions cluster to and from](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#transactions-cluster-to_and-from)
  - [Score addresses with most transactions](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#score-addresses-with-most-transactions)
  - [Distinct data types(transactions)](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#distinct-transaction-data-types(transactions))
  - [Transactions destination distinct count distribution](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#transactions-destination-distinct-count-distribution)
  - [No Address transaction data type](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#no_address-transaction-data-type)
  - [No address transaction by value](https://github.com/kevinpatelco/BlockchainBatchETL/blob/main/mv.md#no-address-transaction-by-value)

### Charts and Dashboard 




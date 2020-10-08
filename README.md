# BlockchainBatchETL

Analyze the blocks and quantify anomalies. Data Source : ICON Blockchain

## Motivation
Blockchain data is like Big Data. But unlike Big Data, querying blockchain data is expensive. This is due to the fact that Blockchain Data lives in a decentralized network of nodes that are constantly replicating records among themselves. This project will allow you to deploy a powerful infrastructure for blockchain ETL, creating an environment for data transfer and to perform analytics on the queried data. The data pipeline is develoved using airflow, allowing multiple tasks to schedule that might have dependencies on one another. This project also uses AWS and terraform for easy deployment. 

## Projet Setup
There are Three main components of this project: 
1. Project Infrastructure
2. SQL Analysis  
3. Charts and Dashboards

## Usage 

### Project Infrastructure
The Infrastructure needed for this project can be found at: [terragrunt-icon-analytics](https://github.com/kevinpatelco/terragrunt-icon-analytics). Some postgres scripts were added to allow analysis on data and create charts in Apache Superset. 

Prerequisites:
* Terraform v0.12.29
* Terragrunt v0.23.40
* Ansible

1. The Infrastructure components are dependent on previous components. Clone the directory. 

  ``` git clone https://github.com/kevinpatelco/terragrunt-icon-analytics```.
  
2. Navigate to ```icon-analytics/aws```. You will find all the needed infrastructure components here. Use the following order to deploy the infrastructure by running ```terragrunt apply``` after navigating to the respective folder: 
  1. network
  2. rds
  3. postgres
  4. airflow
  5. superset




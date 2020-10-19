 # SQL Schemas 
  - [Blocks](#blocks)
  - [Transactions](#transactions)
  - [Logs](#logs)
  - [Receipts](#receipts)
  
  Further information about the data used in the schemas is available in the [ICON JSON RPC documentation.](https://www.icondev.io/docs/icon-json-rpc-v3)

Primary keys for each table are **indicated in bold**.

## Blocks

| Field            	| Type   	|
|------------------	|--------	|
| number           	| bigint 	|
| hash             	| string 	|
| parent_hash      	| string 	|
| merkle_root_hash 	| string 	|
| timestamp        	| bigint 	|
| version          	| string 	|
| peer_id          	| string 	|
| signature        	| string 	|
| next_leader      	| string 	|

## Transactions

| Field             	| Type           	|
|-------------------	|----------------	|
| version           	| string         	|
| from_address      	| string         	|
| to_address        	| string         	|
| value             	| numeric(38,0)  	|
| step_limit        	| numeric(38,0)  	|
| timestamp         	| bigint         	|
| nid               	| int            	|
| nonce             	| numeric(100,0) 	|
| **hash**          	| **string**     	|
| transaction_index 	| bigint         	|
| block_hash        	| string         	|
| block_number      	| bigint         	|
| fee               	| numeric(38,0)  	|
| signature         	| string         	|
| data_type         	| string         	|
| data              	| string         	|

## Logs

| Field                 	| Type       	|
|-----------------------	|------------	|
| **log_index**         	| **int**    	|
| **transaction_hash**  	| **string** 	|
| **transaction_index** 	| **int**    	|
| block_hash            	| string     	|
| block_number          	| int        	|
| address               	| string     	|
| data                  	| string     	|
| indexed               	| string     	|

## Receipts

| Field                 	| Type          	|
|-----------------------	|---------------	|
| **transaction_hash**  	| **string**    	|
| **transaction_index** 	| **int**       	|
| block_hash            	| string        	|
| block_number          	| int           	|
| cumulative_step_used  	| numeric(38,0) 	|
| step_used             	| numeric(38,0) 	|
| step_price            	| numeric(38,0) 	|
| score_address         	| string        	|
| status                	| string        	|

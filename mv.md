# Materialized Views
  - [Transactions Count Distribution](#transactions-count-distribution)
  - [Addresses with most transactions received](#addresses-with-most-transactions-received)
  - [Transactions cluster to and from](#transactions-cluster-to_and-from)
  - [Score addresses with most transactions](#score-addresses-with-most-transactions)
  - [Distinct data types(transactions)](#distinct-transaction-data-types(transactions))
  - [Transactions destination distinct count distribution](#transactions-destination-distinct-count-distribution)
  - [No Address transaction data type](#no_address-transaction-data-type)
  - [No address transaction by value](#no-address-transaction-by-value)

## Transactions Count Distribution
```
create materialized view transactions_count_distribution as
select transactions_count.ct, transactions_count.ct_title
FROM(
    (SELECT count(*) as ct, 'total_transactions' as ct_title
    FROM transactions)
    UNION
    (SELECT count(*) as ct, 'Smart_Contract_transactions' as ct_title
    FROM transactions
    WHERE LEFT(to_address, 2) = 'cx')
    UNION
    (SELECT count(*) as ct, 'Node_to_Node_transactions' as ct_title
    FROM transactions
    WHERE LEFT(to_address, 2) = 'hx')
    union
    (SELECT count(*) as ct, 'No_Address_transactions' as ct_title
    FROM transactions
    WHERE LEFT(to_address, 2) = '')
) transactions_count;
```

## Addresses with most transactions received
```
create materialized view addresses_with_most_transactions_received as
select temp_table.ct, temp_table.to_address
FROM(
    (SELECT count(*) as ct, to_address
    FROM transactions group by to_address)
) temp_table;

```

## Transactions cluster to and from
```
create materialized view transactions_cluster_to_and_from as
select temp_table.ct, temp_table.to_address, temp_table.from_address
FROM(
    (SELECT count(*) as ct, to_address, from_address
    FROM transactions group by to_address, from_address)
) temp_table;
```

## Score addresses with most transactions
```
create materialized view score_addresses_with_most_transactions as
select temp_table.address, temp_table.name, temp_table.ct
from(
    SELECT s.address, s.name, count(*) as ct from
    score_addresses as s
    join
    reduced_trans as r
    ON s.address = r.to_address
    GROUP BY s.address, s.name
) temp_table;
```

## Distinct data types(transactions)
```
create materialized view distinct_data_types as
select temp_table.ct, temp_table.data_type
FROM(
    (select data_type, count(*) as ct from reduced_trans group by data_type)
) temp_table;
```

## Transactions destination distinct count distribution
```
create materialized view transactions_destination_distinct_count_distribution as
select temp_table.ct, temp_table.ct_title
FROM(
    (SELECT count(*) as ct, 'EOA_Address_Receiver' as ct_title
    	FROM (select distinct to_address from addresses_with_most_transactions_received where left(to_address, 2) = 'hx') x)
    UNION
    (SELECT count(*) as ct, 'SCORE_Address_Receiver' as ct_title
    	FROM (select distinct to_address from addresses_with_most_transactions_received where left(to_address, 2) = 'cx') x)
    UNION
    (SELECT count(*) as ct, 'No_Address_Receiver' as ct_title
    	FROM (select distinct to_address from addresses_with_most_transactions_received where left(to_address, 2) = '') x)
) temp_table;
```

## No Address transaction data type
```
create materialized view no_address_transaction_data_type as
select temp_table.data_type, temp_table.ct
from (
select data_type, count(*) as ct from reduced_trans where to_address = '' group by data_type
) temp_table;
```

## No Address transaction by value
```
create materialized view no_address_transaction_by_value as
select temp_table.value, temp_table.ct
from (
select value, count(*) as ct from reduced_trans where to_address = '' group by value
) temp_table;
```

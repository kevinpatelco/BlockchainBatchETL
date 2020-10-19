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

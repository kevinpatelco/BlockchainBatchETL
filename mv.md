# Materialized Views

- [Transactions Count Distribution](#transactions_count_distribution)

##Transactions Count Distribution
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

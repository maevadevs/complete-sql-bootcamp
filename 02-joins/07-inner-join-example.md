# `INNER JOIN`

- Returns ONLY the set of records that match in both right table and left table
- Most common join type used
- But not always the most efficient in some cases
- Default `JOIN` is the same as `INNER JOIN`

## Code Steps

1. Specify the columns from both tables (specify table names to avoid ambiguity): If it is obvious and there is no ambiguity, the table names can be dropped
1. Specify the Main table (`table_A`) Alias can be used
1. Specify the table that joins the Main table (`table_B`) Alias can be used
1. Add a join condition `ON`

```sql
SELECT tA.pk, tA.colA1, tB.pk, tB.colB1
FROM table_A as tA INNER JOIN table_B as tB
ON table_A.pk = table_B.fk;
```

## Pseudo-Code Interpretation of INNER JOIN

```python
def inner_join(table_A, table_B, on_condition='row_A.pk == row_B.fk'):
  result_set = ()
  for row_A in table_A:
    for row_B in table_B:
      isMatch = search_match(row_A, row_B, on_condition)
      if isMatch:
        result_set.append(row_A.columns) + result_set.append(row_B.columns)
  return result_set
```

## Example of Advanced Use

```sql
SELECT
  cst.customer_id AS "Customer ID - CST",
  pmt.customer_id AS "Customer ID - PMT", /* We can select from both tables */
  cst.email AS "Email Address",
  sum(pmt.amount) AS "Total Amount"
FROM customer AS cst INNER JOIN payment as pmt
ON cst.customer_id = pmt.customer_id
GROUP BY "Customer ID - CST", pmt.customer_id /* Aliases can be used here */
ORDER BY "Total Amount" DESC
LIMIT 10;
```

## Inner Join Example

```visual
table_a             table_b

id  name            id  name
**  ****            **  ****
1   Pirate          1   Rutabaga
2   Monkey          2   Pirate
3   Ninja           3   Darth Vader
4   Spaghetti       4   Ninja
```

### Query

```sql
SELECT *
FROM table_a JOIN table_b
ON table_a.name = table_b.name;
```

### Result

```visual
a.id  a.name  b.id  b.name
****  ******  ****  ******
1     Pirate  2     Pirate
3     Ninja   4     Ninja
```

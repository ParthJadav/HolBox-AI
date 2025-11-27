# HolBox-AI - Expense Query

## API Documentation

### Generate SQL Endpoint

**URL**: `http://98.92.74.96:8000/api/v1/generate`  
**Method**: `POST`  
**Content-Type**: `application/json`

#### Example Request

```bash
curl -X 'POST' \
  'http://98.92.74.96:8000/api/v1/generate' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "execute": true,
  "query": "list all the expenses of parth jadav which is unpaid"
}'
```

#### Example Response

```json
{
  "success": true,
  "query": "list all the expenses of parth jadav which is unpaid",
  "sql": "SELECT lm.leave_id, lm.leave_type_id, lm.leave_reason, lm.leave_start_date, lm.leave_end_date, lm.leave_total_days, lm.leave_day_type, lm.leave_status, lm.leave_created_date FROM leave_master lm JOIN users_master um ON lm.user_id = um.user_id WHERE um.user_full_name LIKE '%parth jadav%' AND lm.paid_unpaid = 1",
  "validated_sql": "SELECT lm.leave_id, lm.leave_type_id, lm.leave_reason, lm.leave_start_date, lm.leave_end_date, lm.leave_total_days, lm.leave_day_type, lm.leave_status, lm.leave_created_date FROM leave_master lm JOIN users_master um ON lm.user_id = um.user_id WHERE um.user_full_name LIKE '%parth jadav%' AND lm.paid_unpaid = 1",
  "validation_errors": null,
  "execution_results": {
    "rows": [],
    "row_count": 0,
    "columns": [
      "leave_id",
      "leave_type_id",
      "leave_reason",
      "leave_start_date",
      "leave_end_date",
      "leave_total_days",
      "leave_day_type",
      "leave_status",
      "leave_created_date"
    ],
    "execution_time": 0.0015571117401123047
  },
  "error": null
}
```

### SQL Query Example

The following SQL is generated for the query: *"list all the expenses of parth jadav which is unpaid"*

```sql
SELECT
    lm.leave_id,
    lm.leave_type_id,
    lm.leave_reason,
    lm.leave_start_date,
    lm.leave_end_date,
    lm.leave_total_days,
    lm.leave_day_type,
    lm.leave_status,
    lm.leave_created_date
FROM
    leave_master lm
JOIN users_master um ON
    lm.user_id = um.user_id
WHERE
    um.user_full_name LIKE '%parth jadav%'
    AND lm.paid_unpaid = 1;
```

---

### Generate SQL Endpoint - Error Case (Table Not Found)

**URL**: `http://98.92.74.96:8000/api/v1/generate`  
**Method**: `POST`  
**Content-Type**: `application/json`

#### Example Request

```bash
curl -X 'POST' \
  'http://98.92.74.96:8000/api/v1/generate' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "execute": true,
  "query": "list all the expense entries of parth jadav which is unpaid or pending"
}'
```

#### Example Response

```json
{
  "success": false,
  "query": "list all the expense entries of parth jadav which is unpaid or pending",
  "sql": "SELECT e.expense_id, e.expense_amount, e.expense_date, e.expense_status, u.user_full_name, u.user_email FROM expense_master e JOIN users_master u ON e.user_id = u.user_id WHERE u.user_full_name LIKE '%parth jadav%' AND (e.expense_status = 'Unpaid' OR e.expense_status = 'Pending')",
  "validated_sql": null,
  "validation_errors": [
    "Table 'expense_master' not found in schema"
  ],
  "execution_results": null,
  "error": "Validation failed: Table 'expense_master' not found in schema"
}
```

### SQL Query Example (Failed Validation)

The following SQL was generated but failed validation:

```sql
SELECT
    e.expense_id,
    e.expense_amount,
    e.expense_date,
    e.expense_status,
    u.user_full_name,
    u.user_email
FROM
    expense_master e
JOIN users_master u ON
    e.user_id = u.user_id
WHERE
    u.user_full_name LIKE '%parth jadav%'
    AND(
        e.expense_status = 'Unpaid'
        OR e.expense_status = 'Pending'
    );
```

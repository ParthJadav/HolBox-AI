# HolBox-AI - Holiday Query

## API Documentation

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
  "query": "give me the list of holidays in August month of 2025"
}'
```

#### Example Response

```json
{
  "success": false,
  "query": "give me the list of holidays in August month of 2025",
  "sql": "SELECT h.holiday_date, h.holiday_name, h.holiday_type FROM holiday_master h JOIN society_master s ON h.society_id = s.society_id WHERE YEAR(h.holiday_date) = 2025 AND MONTH(h.holiday_date) = 8 ORDER BY h.holiday_date;",
  "validated_sql": null,
  "validation_errors": [
    "Table 'holiday_master' not found in schema"
  ],
  "execution_results": null,
  "error": "Validation failed: Table 'holiday_master' not found in schema"
}
```

### SQL Query Example (Failed Validation)

The following SQL was generated but failed validation:

```sql
SELECT
    h.holiday_date,
    h.holiday_name,
    h.holiday_type
FROM
    holiday_master h
JOIN society_master s ON
    h.society_id = s.society_id
WHERE
    YEAR(h.holiday_date) = 2025
    AND MONTH(h.holiday_date) = 8
ORDER BY
    h.holiday_date;
```

# HolBox-AI - Work Report Query

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
  "query": "get the work reports of parth jadav only template work report for November 2025"
}'
```

#### Example Response

```json
{
  "success": true,
  "query": "get the work reports of parth jadav only template work report for November 2025",
  "sql": "SELECT am.attendance_date_start, am.work_report_title, am.work_report FROM attendance_master am JOIN users_master um ON am.user_id = um.user_id WHERE um.user_full_name LIKE '%parth jadav%' AND am.work_report_title LIKE '%template%' AND YEAR(am.attendance_date_start) = 2025 AND MONTH(am.attendance_date_start) = 11 ORDER BY am.attendance_date_start",
  "validated_sql": "SELECT am.attendance_date_start, am.work_report_title, am.work_report FROM attendance_master am JOIN users_master um ON am.user_id = um.user_id WHERE um.user_full_name LIKE '%parth jadav%' AND am.work_report_title LIKE '%template%' AND YEAR(am.attendance_date_start) = 2025 AND MONTH(am.attendance_date_start) = 11 ORDER BY am.attendance_date_start",
  "validation_errors": null,
  "execution_results": {
    "rows": [],
    "row_count": 0,
    "columns": [
      "attendance_date_start",
      "work_report_title",
      "work_report"
    ],
    "execution_time": 0.0017857551574707031
  },
  "error": null
}
```

### SQL Query Example

The following SQL is generated for the query: *"get the work reports of parth jadav only template work report for November 2025"*

```sql
SELECT
    am.attendance_date_start,
    am.work_report_title,
    am.work_report
FROM
    attendance_master am
JOIN users_master um ON
    am.user_id = um.user_id
WHERE
    um.user_full_name LIKE '%parth jadav%'
    AND am.work_report_title LIKE '%template%'
    AND YEAR(am.attendance_date_start) = 2025
    AND MONTH(am.attendance_date_start) = 11
ORDER BY
    am.attendance_date_start;
```

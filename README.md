# HolBox-AI

HolBox-AI is an intelligent service designed to translate natural language queries into executable SQL commands.

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
  "query": "Show attendance for the last 7 days for the employee name parth jadav"
}'
```

#### Example Response

```json
{
  "success": false,
  "query": "Show attendance for the last 7 days for the employee name parth jadav",
  "sql": "SELECT am.attendance_date_start, am.punch_in_time, am.punch_out_time, am.total_working_hours, am.attendance_status, bm.block_name, fm.floor_name, stm.shift_name FROM attendance_master am JOIN users_master um ON am.user_id = um.user_id LEFT JOIN block_master bm ON am.society_id = bm.society_id LEFT JOIN floors_master fm ON am.society_id = fm.society_id LEFT JOIN shift_timing_master stm ON am.shift_time_id = stm.shift_time_id WHERE um.user_full_name LIKE '%parth jadav%' AND am.attendance_date_start >= DATE_SUB(CURDATE(), INTERVAL 7 DAY) ORDER BY am.attendance_date_start DESC",
  "validated_sql": "SELECT am.attendance_date_start, am.punch_in_time, am.punch_out_time, am.total_working_hours, am.attendance_status, bm.block_name, fm.floor_name, stm.shift_name FROM attendance_master am JOIN users_master um ON am.user_id = um.user_id LEFT JOIN block_master bm ON am.society_id = bm.society_id LEFT JOIN floors_master fm ON am.society_id = fm.society_id LEFT JOIN shift_timing_master stm ON am.shift_time_id = stm.shift_time_id WHERE um.user_full_name LIKE '%parth jadav%' AND am.attendance_date_start >= DATE_SUB(CURDATE(), INTERVAL 7 DAY) ORDER BY am.attendance_date_start DESC",
  "validation_errors": null,
  "execution_results": null,
  "error": "Execution failed: Database not connected"
}
```

### SQL Query Example

The following SQL is generated for the query: *"Show attendance for the last 7 days for the employee name parth jadav"*

```sql
SELECT
    am.attendance_date_start,
    am.punch_in_time,
    am.punch_out_time,
    am.total_working_hours,
    am.attendance_status,
    bm.block_name,
    fm.floor_name,
    stm.shift_name
FROM
    attendance_master am
JOIN users_master um ON
    am.user_id = um.user_id
LEFT JOIN block_master bm ON
    um.block_id = bm.block_id
LEFT JOIN floors_master fm ON
    um.floor_id = fm.floor_id
LEFT JOIN shift_timing_master stm ON
    am.shift_time_id = stm.shift_time_id
WHERE
    um.user_full_name LIKE '%parth jadav%' 
    AND am.attendance_date_start >= DATE_SUB(CURDATE(), INTERVAL 7 DAY)
ORDER BY
    am.attendance_date_start DESC;
```
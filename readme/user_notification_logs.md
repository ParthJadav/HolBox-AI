# HolBox-AI - Notification Logs Query

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
  "query": "give me all the notification logs of parth jadav"
}'
```

#### Example Response

```json
{
  "success": false,
  "query": "give me all the notification logs of parth jadav",
  "sql": "SELECT n.notification_id, n.notification_title, n.notification_message, n.notification_type, n.notification_date, u.user_full_name, u.user_email FROM notification_master n JOIN users_master u ON n.user_id = u.user_id WHERE u.user_full_name LIKE '%parth jadav%' ORDER BY n.notification_date DESC",
  "validated_sql": null,
  "validation_errors": [
    "Table 'notification_master' not found in schema"
  ],
  "execution_results": null,
  "error": "Validation failed: Table 'notification_master' not found in schema"
}
```

### SQL Query Example (Failed Validation)

The following SQL was generated but failed validation:

```sql
SELECT
    n.notification_id,
    n.notification_title,
    n.notification_message,
    n.notification_type,
    n.notification_date,
    u.user_full_name,
    u.user_email
FROM
    notification_master n
JOIN users_master u ON
    n.user_id = u.user_id
WHERE
    u.user_full_name LIKE '%parth jadav%'
ORDER BY
    n.notification_date DESC;
```

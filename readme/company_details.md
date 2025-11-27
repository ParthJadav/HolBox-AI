# HolBox-AI - Company Details Query

## API Documentation

### Generate SQL Endpoint - Execution Error (Unknown Column)

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
  "query": "give my company details"
}'
```

#### Example Response

```json
{
  "success": false,
  "query": "give my company details",
  "sql": "SELECT sm.society_name, sm.society_address, sm.society_contact_number, sm.society_email, sm.society_website FROM society_master sm LIMIT 1",
  "validated_sql": "SELECT sm.society_name, sm.society_address, sm.society_contact_number, sm.society_email, sm.society_website FROM society_master sm LIMIT 1",
  "validation_errors": null,
  "execution_results": null,
  "error": "Execution failed: 1054 (42S22): Unknown column 'sm.society_contact_number' in 'field list'"
}
```

### SQL Query Example (Execution Failed)

The following SQL was generated and validated, but failed during execution:

```sql
SELECT
    sm.society_name,
    sm.society_address,
    sm.society_contact_number,
    sm.society_email,
    sm.society_website
FROM
    society_master sm
LIMIT 1;
```

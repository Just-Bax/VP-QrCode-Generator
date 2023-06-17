# Rule Packages
This procedure handles a callback from a HTTP request made to generate a QR code. It takes the following parameters:
- `p_http_status:` The HTTP status code of the response.
- `p_response:` The response message received from the HTTP request.
- `p_tid:` The unique identifier associated with the request.
- `p_http_call_log_id:` The ID of the HTTP call log.
- `p_id2:` Another identifier. Inside the procedure, the following steps are performed:

##### Inside the procedure, the following steps are performed:
- Retrieve the `xitor_type_id` corresponding to the `p_tid` parameter by calling the `get_ttid` function and assign it to the `ttid` variable.
- Perform a SELECT query on the config_field table to retrieve the `config_field_id` into the qrid variable. The query filters the rows based on the `xitor_type_id` and `data_type` values, and the field names containing "QRCODE" or "QR_CODE".
- Insert a new record into the `blob_data` table, providing the values for `blob_data`, `thumbnail`, `config_field_id`, `filename`, and `key_value`. The inserted `blob_data_id` is returned into the `blob_id` variable.
- Commit the transaction.
- Call the `util.setvalnumbyid` procedure with the `p_tid`, `qrid`, and `blob_id` values to perform additional processing.

# Usage
- Set your onevizion system url (`https://cloud-erp.onevizion.com/`)
- Enhance the `Id Numbers` data by including the trackers that possess a field with either `QRCODE` or `QR_CODE` in their field names.

#### Please let me know if you need any further assistance!
# SPL Queries

## Internal ERROR Logs
index=_internal sourcetype="splunkd" log_level="ERROR"

## INFO Logs from Host
index="_internal" host="Mac" log_level="INFO"

## Event Count by Host
index=_internal | stats count by host | sort -eventCount

##  BUSCAR QUERY EXTRAÑOS

```sql
SELECT 
	wait_event_type,
	wait_event,
	datname,
	usename,
    pid,
    query,
    state,
    query_start,
    applicwrite_uidation_name,
    backend_start
FROM pg_stat_activity
WHERE 
wait_event_type like 'Lock'
or wait_event_type like 'IPC'
```

##  BLOQUEOS EN LA BASE

```sql

SELECT 
    blocking.pid AS blocking_pid,
    blocking.query AS blocking_query,
    blocked.pid AS blocked_pid,
    blocked.query AS blocked_query,
    blocked.state AS blocked_state,
    blocked.wait_event_type,
    blocked.wait_event,
    blocked.query_start AS blocked_query_start,
    blocked.application_name AS blocked_application_name,
    blocked.backend_start AS blocked_backend_start
FROM pg_stat_activity blocked
JOIN pg_locks blocked_locks ON blocked.pid = blocked_locks.pid
JOIN pg_locks blocking_locks 
    ON blocked_locks.transactionid = blocking_locks.transactionid
JOIN pg_stat_activity blocking 
    ON blocking_locks.pid = blocking.pid
WHERE 
    blocked_locks.granted = false
    AND blocked.wait_event_type IN ('Lock', 'IPC')
ORDER BY blocked.query_start;
```


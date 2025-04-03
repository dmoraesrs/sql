-- Ver processos ativos e comandos em execução
SELECT
    r.session_id,
    r.status,
    r.command,
    r.cpu_time,
    r.total_elapsed_time,
    r.reads,
    r.writes,
    r.logical_reads,
    r.blocking_session_id,
    t.text AS sql_text
FROM sys.dm_exec_requests r
CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) t
WHERE r.session_id <> @@SPID;





SELECT 
    r.session_id,
    r.status,
    r.wait_type,
    r.wait_time,
    r.wait_resource,
    t.text
FROM sys.dm_exec_requests r
CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) t
WHERE r.session_id IN (56, 60, 87, 91, 98, 102);  -- ou todas listadas



SELECT 
    r.session_id,
    r.status,
    r.wait_type,
    r.wait_time,
    r.wait_resource,
    t.text
FROM sys.dm_exec_requests r
CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) t
WHERE r.session_id IN (56, 87, 102, 106);





SELECT 
    migs.user_seeks,
    mid.statement AS tabela,
    mid.equality_columns,
    mid.inequality_columns,
    mid.included_columns
FROM sys.dm_db_missing_index_groups mig
JOIN sys.dm_db_missing_index_group_stats migs ON mig.index_group_handle = migs.group_handle
JOIN sys.dm_db_missing_index_details mid ON mig.index_handle = mid.index_handle
ORDER BY migs.user_seeks DESC;


# Mysql

## profiling log 옵션 

- set global slow_query_log = 'ON';
- set global log_queries_not_using_indexes = 'ON'
- set global long_query_time = '20';

- 로그 세팅 적용
 -> flush logs;
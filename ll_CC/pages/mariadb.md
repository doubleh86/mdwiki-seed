# Mysql

## profiling log 옵션 

- set global slow_query_log = 'ON';
- set global log_queries_not_using_indexes = 'ON'
- set global long_query_time = '20';

- 로그 세팅 적용
 -> flush logs;

## 권한 주기
```
grant all privileges on *.* to '계정명'@'%' identified by '비밀번호';
```

## Mysql (Maria) 기본 세팅

```
 [client]
port                           = 10012

[mysqld_safe]
socket                         = /var/lib/mysql/mysql.sock

[mysqld]
user                           = mysql
pid-file                       = /var/run/mysqld/mysql.pid
socket                         = /var/lib/mysql/mysql.sock
port                           = 10012
datadir                        = /var/lib/mysql
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
max_connections = 1000
wait_timeout = 50
query_cache_type = 1
query_cache_size = 64M

max_allowed_packet=16M
thread_cache_size=500

innodb_flush_log_at_trx_commit = 2
innodb_log_buffer_size = 8M
innodb_log_file_size = 256M
innodb_buffer_pool_size=1G
innodb_flush_method=O_DIRECT
innodb_io_capacity=1000
innodb_old_blocks_time=1000
innodb_open_files=5000

slow-query-log=1
log-queries-not-using-indexes
long_query_time=1
log-slow-queries=/var/log/mysql/log-slow-queries.log

[mysql]
!includedir /etc/mysql/conf.d
```
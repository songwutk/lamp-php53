# lamp-php53
Apache mysql  php5.3  - for MA old source code 

Directory Structure 

build - script for build container (apache, php 5.3) 

conf - apache config 

db - mysql data 

logs - apache log 

www - web data 

docker-compose.yml



Instruction : docker-compose up -d 

Why choose mariadb ?

You can trace sql log by query .. 

SET GLOBAL general_log=OFF;
TRUNCATE table mysql.general_log;
SET GLOBAL log_output = 'TABLE';
SET GLOBAL general_log=ON;

Open table mysql->general_log to view sql log.

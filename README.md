### 安装mysql、redis并设置密码

| DB    | version |
| ----- | ------- |
| MySQL | \>= 5.7 |
| Redis | \>= 5.0 |

```javascript
git clone https://github.com/luo964973791/jumpserver.git
cd jumpserver && yum install ./redis-7.0.0-1.el7.remi.x86_64.rpm -y
mysql> create database jumpserver charset='utf8';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'jumpserver'@'%' IDENTIFIED BY 'Test@123' WITH GRANT OPTION;
#授权jumpserver用户jumpserver数据库的所有权限.
cat /etc/redis.conf
bind 172.27.0.5
requirepass Test@123
```

### 下载.
```javascript
curl -sSL https://github.com/jumpserver/jumpserver/releases/download/v2.21.1/quick_start.sh | bash

cd /opt/jumpserver-installer-v2.21.1
vi config-example.txt
##  MySQL 配置, USE_EXTERNAL_MYSQL=1 表示使用外置 MySQL, 请输入正确的 MySQL 信息
USE_EXTERNAL_MYSQL=1
DB_HOST=172.27.0.8
DB_PORT=3306
DB_USER=root
DB_PASSWORD=Test@123
DB_NAME=jumpserver

##  Redis 配置, USE_EXTERNAL_REDIS=1 表示使用外置 Redis, 请输入正确的 Redis 信息
USE_EXTERNAL_REDIS=1
REDIS_HOST=172.27.0.8
REDIS_PORT=6379
REDIS_PASSWORD=Test@123


vi .env
##  MySQL 配置, USE_EXTERNAL_MYSQL=1 表示使用外置 MySQL, 请输入正确的 MySQL 信息
USE_EXTERNAL_MYSQL=0
DB_HOST=mysql
DB_PORT=3306
DB_USER=root
DB_PASSWORD=NzlhZTRkNTYtMThjMS1iNDUxLW
DB_NAME=jumpserver

##  Redis 配置, USE_EXTERNAL_REDIS=1 表示使用外置 Redis, 请输入正确的 Redis 信息
USE_EXTERNAL_REDIS=0
REDIS_HOST=redis
REDIS_PORT=6379
REDIS_PASSWORD=NzlhZTRkNTYtMThjMS1iNDUxLW
```

### 启动

```javascript
cd /opt/jumpserver-installer-v2.21.1 &&  ./jmsctl.sh uninstall
cd /opt/jumpserver-installer-v2.21.1 && ./jmsctl.sh install
```


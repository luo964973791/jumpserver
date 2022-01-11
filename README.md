### 安装mysql、redis并设置密码
```javascript
mysql> create database jumpserver charset='utf8';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'jumpserver'@'%' IDENTIFIED BY 'Test@123' WITH GRANT OPTION;
#授权jumpserver用户jumpserver数据库的所有权限.
cat /etc/redis.conf
bind 172.27.0.5
requirepass Test@123
```

### 启动
```javascript
#!/bin/bash
if [ "$SECRET_KEY" = "" ]; then SECRET_KEY=`cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 50`; echo "SECRET_KEY=$SECRET_KEY" >> ~/.bashrc; echo $SECRET_KEY; else echo $SECRET_KEY; fi

if [ "$BOOTSTRAP_TOKEN" = "" ]; then BOOTSTRAP_TOKEN=`cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 16`; echo "BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN" >> ~/.bashrc; echo $BOOTSTRAP_TOKEN; else echo $BOOTSTRAP_TOKEN; fi
docker run -d --name jumpserver -h jumpserver --restart=always  \
    -v /data/jumpserver:/opt/jumpserver/data/media \
    -p 31080:80 \
    -p 2222:2222 \
    -e SECRET_KEY=$SECRET_KEY \
    -e BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN \
    -e DB_HOST=172.27.0.5 \
    -e DB_PORT=3306 \
    -e DB_USER=jumpserver \
    -e DB_PASSWORD="Test@123" \
    -e DB_NAME=jumpserver \
    -e REDIS_HOST=172.27.0.5 \
    -e REDIS_PORT=6379 \
    -e REDIS_PASSWORD="Test@123" \
jumpserver/jms_all:latest

#登录密码默认admin
```

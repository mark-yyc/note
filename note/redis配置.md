#### redis 环境配置（默认6379）

+ apt-get update
+ apt-get install redis-server
+ redis-cli 检查是否安装成功
+ vi /etc/redis/redis.conf
  + requirepass <password>
  + 注释bind 127.0.0.1

+ /etc/init.d/redis-server restart 重启
+ /etc/init.d/redis-server start 启动服务
+ /etc/init.d/redis-server stop 停止服务
进阶实战

编写一个自己的应用，编写一个 hello world 应用

安装一个 redis：

~~~bash
docker pull redis

redis.conf -> /data/redis/redis.conf
/data -> /data/redis/data # 希望有一个挂载

docker run redis # 启动容器，所有设置都设置好，为：

docker run -v /data/redis/redis.conf:/etc/redis/redis.conf \
-v /data/redis/data:/data \
-d --name myredis \
-p 6379:6379 \
redis redis-server /etc/redis/redis.conf


~~~


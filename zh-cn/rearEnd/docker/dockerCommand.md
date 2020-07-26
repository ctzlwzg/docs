## docker

### 命令

> yum install docker

- 安装 docker 而后输入 y

> systemctl start docker

- 启动 docker

> docker -v

- 检查 docker 版本

> systemctl enable docker

- 开机启动 docker

> systemctl stop docker

- 关闭 docker

> docker search 关键字（如 MySQL

- 检索镜像

> docker pull mysql:5.7.28

- 拉取 MySQL 镜像

> docker images

- 搜索所有的镜像

> docker rmi images-id

- 删除指定的本地镜像

> docker run -p 3306:3306 --name mysql -v /docker_volumes_data/mysql/config:/etc/mysql/conf.d -v /docker_volumes_data/mysql/logs:/logs -v /docker_volumes_data/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7.28

- 运行容器 -p 端口映射把服务器端口映射到容器的端口 -d 后台运行-e 设置环境变量，或者覆盖已存在的环境变量 -v 主机目录：容器目录

> docker ps

- 查看哪些容器在运行(可以查看到 id，下面的 id 厚实从这里查看获取)

> docker stop id

- 停止运行中的容器

> docker start id

- 启动容器

> docker rm id

- 删除容器

> docker ps -a

- 查看所有的容器

> docker logs id

- 查看容器日志

> docker exec -it mysql bash

- 连接测试，其中 mysql 是运行镜像的名字 ,名字为安装时取的名称

> docker run -d --name redis -p 6379:6379 redis --requirepass "123456"

- redis 安装 最新 运行容器，并设置密码

> docker run -d --name redis -p 6379:6379 -v /docker_volumes_data/redis/data:/data -v /docker_volumes_data/redis/conf/redis.conf:/usr/local/etc/redis/redis.conf redis redis-server /usr/local/etc/redis/redis.conf --requirepass "123456" --appendonly yes

#### 注意

- 先去https://github.com/microsoftarchive/redis/blob/3.0/redis.conf 下载配置文件

- 根目录先创建 docker_volumes_data 文件夹，里面在创建 redis 文件中，再 redis 文件夹中创建 config data 两个文件夹，一个用于存配置文件，一个用于存储持久化的数据

- 在/docker_volumes_data/redis/conf/redis.conf 目录下创建 redis.conf 文件，修改 appendonly 为 yes

- 注释掉 bind 127.0.0.1 ,设置密码 requirepass 123456

- 这样关闭 redis 数据也持久化到硬盘中了.

> 远程连接，不要忘记在服务器中开放对应的端口

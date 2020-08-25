## 拉取镜像

```
docker pull rabbitmq:3.7.7-management
```



## 创建数据挂载目录

```
mkdir -p /data/rabbitmq/data
```



## 使用镜像运行容器

```dockerfile
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 -v /data/rabbitmq/data:/var/lib/rabbitmq --hostname rabbit-node1 -e RABBITMQ_DEFAULT_VHOST=rabbit_node1_vhost -e RABBITMQ_DEFAULT_USER=root -e RABBITMQ_DEFAULT_PASS=root rabbitmq:3.7.7-management
命令解析：
    -d 后台运行容器；
	--name 指定容器名；
	-p 指定服务运行的端口（5672：应用访问端口；15672：控制台Web端口号）；
	-v 映射目录或文件；
	--hostname  主机名（RabbitMQ的一个重要注意事项是它根据所谓的 “节点名称” 存储数据，默认为主机名）；
	-e 指定环境变量；（RABBITMQ_DEFAULT_VHOST：默认虚拟机名；RABBITMQ_DEFAULT_USER：默认的用户名；RABBITMQ_DEFAULT_PASS：默认用户名的密码）

5、使用命令：docker ps 查看正在运行容器

#当15672端口管理页面无法显示的时

docker exec -it [name|id] bash #进入容器

rabbitmq-plugins enable rabbitmq_management #开启web管理界面插件
```
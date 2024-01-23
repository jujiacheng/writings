# Docker使用

## 常用命令

- 查看所有容器：`docker ps -a`
- 删除所有停止的容器：`docker container prune`
- 停止容器：`docker stop <id或name>`
- 启动容器：`docker start <id或name>`
- 杀死容器：`docker kill <id或name>`
- 重启容器：`docker restart <id或name>`
- 查看所有images：`docker images`
- 删除images：`docker rmi <image id>`
- docker-compose启动：docker-compose up -d
- docker-compose关闭：docker-compose stop

## docker-compose配置

```JavaScript
version: '3'
services:                                      # 集合
  jenkins:
    user: root                                 # 为了避免一些权限问题 在这我使用了root
    restart: always                            # 重启方式
    image: jenkins/jenkins:lts                 # 指定服务所使用的镜像 在这里我选择了 LTS (长期支持)
    container_name: jenkins                    # 容器名称
    ports:                                     # 对外暴露的端口定义
      - 8080:8080
      - 50000:50000
    volumes:                                   # 卷挂载路径
      - /home/mydocker/jenkins/jenkins_home/:/var/jenkins_home  # 这是我们一开始创建的目录挂载到容器内的jenkins_home目录
      - /var/run/docker.sock:/var/run/docker.sock
      - /usr/bin/docker:/usr/bin/docker                # 这是为了我们可以在容器内使用docker命令
      - /usr/local/bin/docker-compose:/usr/local/bin/docker-compose
  my-nginx:
    restart: always
    image: nginx
    container_name: my-nginx
    ports:
      - 8090:80
      - 8091:443
    volumes:
      - /home/mydocker/nginx/conf.d/nginx.conf:/etc/nginx/nginx.conf
      - /home/mydocker/myfrontend/static/dist:/usr/share/nginx/html
  mysqlserver:
     restart: always
    # 这里指定我们的镜像文件，mysql版本是8.0.28，这里要使用docker命令拉取镜像，这里先写着，后面我教大家怎么拉取镜像
     image: mysql:8.0.28
    # 配置我们容器的名字
     container_name: mysqlserver
    # 通过我们的宿主机的3306端口映射到容器里的3306端口，因为容器内的网络与我们外界是不互通的，只有宿主机能够去访问我们的容器，这样我们就能通过宿主机的3306端口去访问容器的mysql了
     ports:
       - 3306:3306
    # 配置环境，主要是配置我们的mysql的登陆密码，mysql容器创建出来默认可以用不同的ip地址访问，所以这里不用进行配置
     environment:
       - MYSQL_ROOT_PASSWORD=jjc@970615
    # 配置挂载的文件夹，在当前文件夹下面创建mysql文件夹，里面有conf，logs，data，分别挂载到容器mysql中的conf.d，logs，mysql中，这样当我们的容器如果没了，但是我们的数据还是在的
     volumes:
       - /home/mydocker/mysql/conf:/etc/mysql/conf.d
       - /home/mydocker/mysql/logs:/logs
       - /home/mydocker/mysql/data:/var/lib/mysql
  mongodb:
     image: mongo:4
     restart: always
     container_name: mongodb
     environment:
       MONGO_INITDB_ROOT_USERNAME: root
       MONGO_INITDB_ROOT_PASSWORD: jjc@970615
     ports:
       - 27017:27017
"docker-compose.yml" 53L, 2717C                                                                                                                                                           43,3         顶端
version: '3'
services:                                      # 集合
  jenkins:
    user: root                                 # 为了避免一些权限问题 在这我使用了root
    restart: always                            # 重启方式
    image: jenkins/jenkins:lts                 # 指定服务所使用的镜像 在这里我选择了 LTS (长期支持)
    container_name: jenkins                    # 容器名称
    ports:                                     # 对外暴露的端口定义
      - 8080:8080
      - 50000:50000
    volumes:                                   # 卷挂载路径
      - /home/mydocker/jenkins/jenkins_home/:/var/jenkins_home  # 这是我们一开始创建的目录挂载到容器内的jenkins_home目录
      - /var/run/docker.sock:/var/run/docker.sock
      - /usr/bin/docker:/usr/bin/docker                # 这是为了我们可以在容器内使用docker命令
      - /usr/local/bin/docker-compose:/usr/local/bin/docker-compose
  my-nginx:
    restart: always
    image: nginx
    container_name: my-nginx
    ports:
      - 8090:80
      - 8091:443
    volumes:
      - /home/mydocker/nginx/conf.d/nginx.conf:/etc/nginx/nginx.conf
      - /home/mydocker/myfrontend/static/dist:/usr/share/nginx/html
  mysqlserver:
     restart: always
    # 这里指定我们的镜像文件，mysql版本是5.7，这里要使用docker命令拉取镜像，这里先写着，后面我教大家怎么拉取镜像
     image: mysql:8.0.28
    # 配置我们容器的名字
     container_name: mysqlserver
    # 通过我们的宿主机的3306端口映射到容器里的3306端口，因为容器内的网络与我们外界是不互通的，只有宿主机能够去访问我们的容器，这样我们就能通过宿主机的3306端口去访问容器的mysql了
     ports:
       - 3306:3306
    # 配置环境，主要是配置我们的mysql的登陆密码，mysql容器创建出来默认可以用不同的ip地址访问，所以这里不用进行配置
     environment:
       - MYSQL_ROOT_PASSWORD=jjc@970615
    # 配置挂载的文件夹，在当前文件夹下面创建mysql文件夹，里面有conf，logs，data，分别挂载到容器mysql中的conf.d，logs，mysql中，这样当我们的容器如果没了，但是我们的数据还是在的
     volumes:
       - /home/mydocker/mysql/conf:/etc/mysql/conf.d
       - /home/mydocker/mysql/logs:/logs
       - /home/mydocker/mysql/data:/var/lib/mysql
  mongodb:
     image: mongo:4
     restart: always
     container_name: mongodb
     environment:
       MONGO_INITDB_ROOT_USERNAME: root
       MONGO_INITDB_ROOT_PASSWORD: jjc@970615
     ports:
       - 27017:27017
     volumes:
       - /home/mydocker/mongo:/data/db
  redisserver:
    image: redis
    restart: always
    container_name: redisserver
    ports:
      - 6379:6379
    volumes:
      - /home/mydocker/redisserver:/data
    command: ["redis-server","--requirepass","123456"]
```
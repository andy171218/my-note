## **1. 镜像（Image）管理**

| 命令          | 作用                     | 示例                                |
| ------------- | ------------------------ | ----------------------------------- |
| docker pull   | 拉取镜像                 | docker pull nginx:alpine            |
| docker images | 列出本地镜像             | docker images                       |
| docker rmi    | 删除镜像                 | docker rmi ubuntu:latest            |
| docker tag    | 给镜像打标签             | docker tag my_app:1.0 my_app:latest |
| docker build  | 通过 Dockerfile 构建镜像 | docker build -t my_app:1.0 .        |



## **2. 容器（Container）管理**

| 命令         | 作用             | 示例                                           |
| ------------ | ---------------- | ---------------------------------------------- |
| docker run   | 创建并启动容器   | docker run -d -p 8080:80 --name my_nginx nginx |
| docker ps    | 查看运行中的容器 | docker ps -a（显示所有容器）                   |
| docker exec  | 进入运行中的容器 | docker exec -it my_nginx /bin/bash             |
| docker stop  | 停止容器         | docker stop my_nginx                           |
| docker start | 启动已停止的容器 | docker start my_nginx                          |
| docker rm    | 删除容器         | docker rm -f my_nginx（强制删除）              |
| docker logs  | 查看容器日志     | docker logs -f my_nginx（实时跟踪）            |



## **3. 数据持久化**

| 命令                  | 作用           | 示例                                          |
| --------------------- | -------------- | --------------------------------------------- |
| -v（Bind Mount）      | 挂载主机目录   | docker run -v C:\data:/app/data nginx         |
| docker volume create  | 创建数据卷     | docker volume create mysql_data               |
| -v（Volume）          | 挂载数据卷     | docker run -v mysql_data:/var/lib/mysql mysql |
| docker volume ls      | 列出所有数据卷 | docker volume ls                              |
| docker volume inspect | 查看卷详情     | docker volume inspect mysql_data              |



## **4. 镜像更新与保存**

| 命令          | 作用                     | 示例                                   |
| ------------- | ------------------------ | -------------------------------------- |
| docker commit | 将容器保存为新镜像       | docker commit my_container my_nginx:v2 |
| docker build  | 通过 Dockerfile 更新镜像 | docker build -t my_app:v2 .            |
| docker push   | 推送镜像到仓库           | docker push my_registry/my_app:v2      |
| docker tag    | 重命名镜像               | docker tag my_app:1.0 my_app:latest    |



## **5. 网络与端口**

| 命令                  | 作用           | 示例                         |
| --------------------- | -------------- | ---------------------------- |
| -p                    | 端口映射       | docker run -p 8080:80 nginx  |
| docker network ls     | 查看网络列表   | docker network ls            |
| docker network create | 创建自定义网络 | docker network create my_net |



## **6. 系统维护**

| 命令                | 作用             | 示例                               |
| ------------------- | ---------------- | ---------------------------------- |
| docker stats        | 查看容器资源占用 | docker stats                       |
| docker system prune | 清理无用数据     | docker system prune -a（清理所有） |
| docker image prune  | 清理悬空镜像     | docker image prune                 |



## **7. Dockerfile 核心指令**

```
FROM ubuntu:22.04          # 基础镜像
WORKDIR /app               # 设置工作目录
COPY . .                   # 复制文件
RUN apt update && apt install -y curl  # 安装依赖
EXPOSE 80                  # 声明端口
CMD ["nginx", "-g", "daemon off;"]  # 启动命令
```





## **8. 完整工作流示例**

1. **构建镜像** docker build -t my_app:1.0 . 
2. **运行容器（带数据卷）** docker run -d -p 8080:80 -v app_data:/data --name my_app my_app:1.0 
3. **更新并保存镜像** docker exec -it my_app bash  # 进入容器修改 exit docker commit my_app my_app:1.1 
4. **推送到 Docker Hub** docker tag my_app:1.1 username/my_app:1.1 docker push username/my_app:1.1 



### **总结表格**

| 场景       | 核心命令                          |
| ---------- | --------------------------------- |
| 镜像管理   | pull, images, rmi, build          |
| 容器管理   | run, ps, exec, stop, rm           |
| 数据持久化 | -v, volume create, volume inspect |
| 镜像更新   | commit, tag, push                 |
| 网络/端口  | -p, network ls, network create    |
| 系统维护   | stats, prune, logs                |
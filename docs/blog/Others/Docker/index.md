# Docker 简介

## Docker 是什么

Docker 是一个用于打包、分发和运行应用的容器化平台。它把应用程序、运行时、系统库、环境变量和启动命令一起封装成镜像，然后用容器的形式运行。

可以把 Docker 理解成一种更轻量的“应用运行环境快照”。它不需要像虚拟机一样启动完整操作系统，而是复用宿主机内核，通过命名空间和控制组隔离进程、网络、文件系统和资源。

## 为什么需要 Docker

在没有容器之前，一个常见问题是：本地能跑，服务器不能跑。原因通常来自系统版本、依赖库、配置文件、启动脚本或环境变量差异。

Docker 解决的是应用交付的一致性问题：

- 开发环境、测试环境和生产环境尽量保持一致
- 依赖随应用一起发布，减少手动配置
- 应用可以快速启动、停止、迁移和回滚
- 多个服务可以在同一台机器上相互隔离地运行

## 核心概念

### 镜像 Image

镜像是只读模板，里面包含应用运行需要的文件系统、依赖和默认启动命令。镜像通常由 `Dockerfile` 构建出来。

常见操作：

```shell
docker pull nginx
docker images
docker build -t my-app .
```

### 容器 Container

容器是镜像运行后的实例。一个镜像可以启动多个容器，每个容器都有自己的进程、网络和文件系统视图。

常见操作：

```shell
docker run -d --name web -p 8080:80 nginx
docker ps
docker stop web
docker rm web
```

### Dockerfile

`Dockerfile` 是构建镜像的说明书。它描述基础镜像、依赖安装、文件复制、工作目录和启动命令。

一个简单示例：

```dockerfile
FROM nginx:alpine
COPY ./dist /usr/share/nginx/html
EXPOSE 80
```

### Registry

Registry 是镜像仓库，用于保存和分发镜像。常见的公共仓库是 Docker Hub，企业内部也经常搭建私有镜像仓库。

```shell
docker pull redis:7
docker tag my-app registry.example.com/my-app:v1
docker push registry.example.com/my-app:v1
```

### Volume

容器默认文件系统会随着容器删除而丢失。Volume 用于持久化数据，例如数据库文件、上传文件和配置文件。

```shell
docker run -d \
  --name mysql \
  -e MYSQL_ROOT_PASSWORD=123456 \
  -v mysql-data:/var/lib/mysql \
  mysql:8
```

### Network

Docker 网络让容器之间可以相互通信。使用 `docker compose` 时，同一个 Compose 项目里的服务默认会进入同一个网络，并且可以通过服务名访问。

## Docker Compose

Docker Compose 用于管理多容器应用。它把多个服务、端口、环境变量、数据卷和网络写在一个 `compose.yml` 文件里。

例如一个 Web 服务和 Redis：

```yaml
services:
  web:
    image: my-app:latest
    ports:
      - "8080:8080"
    depends_on:
      - redis

  redis:
    image: redis:7
```

启动：

```shell
docker compose up -d
docker compose logs -f
docker compose down
```

## 常见使用场景

- 本地快速启动 MySQL、Redis、Nginx 等中间件
- 为后端服务提供一致的运行环境
- 在 CI/CD 中构建、测试和发布镜像
- 把单机上的多个服务用 Compose 编排起来
- 作为 Kubernetes 部署前的镜像打包工具

## Docker 的边界

Docker 负责把应用打包成镜像并运行容器，但它不负责大规模集群调度。单机或少量服务可以用 Docker Compose；如果需要自动扩缩容、滚动更新、服务发现、故障自愈和多节点调度，通常会使用 Kubernetes。

## 常用命令速查

```shell
# 查看版本
docker version

# 查看正在运行的容器
docker ps

# 查看所有容器
docker ps -a

# 查看镜像
docker images

# 进入容器
docker exec -it <container> sh

# 查看日志
docker logs -f <container>

# 删除无用资源
docker system prune
```

## 学习路线

1. 先掌握 `image`、`container`、`volume`、`network` 的关系。
2. 学会写简单的 `Dockerfile`，把自己的应用构建成镜像。
3. 用 Docker Compose 启动一个包含数据库和后端服务的小项目。
4. 理解镜像分层、端口映射、环境变量和数据持久化。
5. 再继续学习 Kubernetes 如何管理大量容器。

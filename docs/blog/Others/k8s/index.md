# Kubernetes 简介

## Kubernetes 是什么

Kubernetes 通常简称为 K8s，是一个用于管理容器化应用的集群编排系统。它不负责构建镜像，而是负责在多台机器上运行容器、调度资源、维持副本数量、暴露服务、滚动更新和故障恢复。

如果说 Docker 更关注“如何把应用打包并运行成一个容器”，那么 Kubernetes 更关注“如何在一组机器上稳定地运行很多容器”。

## 为什么需要 Kubernetes

当服务数量变多之后，单纯用 Docker 手动管理会遇到很多问题：

- 某个容器挂了，需要自动拉起
- 某台机器资源不足，需要把服务调度到别的机器
- 服务需要多个副本来承载流量
- 发布新版本时，需要滚动更新并支持回滚
- 服务 IP 会变化，需要稳定的服务发现方式
- 配置、密钥、存储和网络都需要统一管理

Kubernetes 通过声明式配置解决这些问题。使用者描述“我希望系统是什么状态”，Kubernetes 负责不断把实际状态调整到期望状态。

## 集群结构

一个 Kubernetes 集群通常由控制平面和工作节点组成。

### Control Plane

控制平面负责管理整个集群状态，核心组件包括：

- `kube-apiserver`：集群统一入口，所有操作都通过 API Server
- `etcd`：保存集群状态的分布式键值数据库
- `kube-scheduler`：决定 Pod 应该调度到哪个节点
- `kube-controller-manager`：负责副本控制、节点状态、任务控制等控制循环

### Node

工作节点负责真正运行容器，核心组件包括：

- `kubelet`：节点代理，负责和控制平面通信并管理本机 Pod
- `container runtime`：容器运行时，例如 containerd
- `kube-proxy`：负责服务转发和部分网络规则

## 核心对象

### Pod

Pod 是 Kubernetes 中最小的调度单位。一个 Pod 可以包含一个或多个容器，这些容器共享网络命名空间和部分存储卷。

最常见的情况是一个 Pod 运行一个主业务容器。

### Deployment

Deployment 用于管理无状态应用。它声明应用镜像、副本数量、更新策略和 Pod 模板。

一个简单示例：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.27
          ports:
            - containerPort: 80
```

### Service

Pod 会被创建和销毁，IP 不稳定。Service 为一组 Pod 提供稳定访问入口，并通过标签选择后端 Pod。

常见类型：

- `ClusterIP`：集群内部访问，默认类型
- `NodePort`：通过节点端口暴露服务
- `LoadBalancer`：在云厂商环境中创建负载均衡器

### Ingress

Ingress 用于管理 HTTP/HTTPS 入口流量，通常配合 Ingress Controller 使用。它可以根据域名和路径把请求转发到不同 Service。

### ConfigMap 和 Secret

`ConfigMap` 用于保存普通配置，例如配置文件、环境变量和命令参数。

`Secret` 用于保存敏感信息，例如密码、Token 和证书。实际生产环境中还需要结合权限控制和外部密钥系统使用。

### Volume

容器本身是临时的，Volume 用于持久化数据或挂载配置。数据库、消息队列这类有状态服务通常需要配合 PersistentVolume 和 PersistentVolumeClaim 使用。

## Kubernetes 的工作方式

Kubernetes 的核心思想是声明式 API 和控制循环。

例如你声明一个 Deployment 需要 `replicas: 3`，Kubernetes 会持续观察当前实际 Pod 数量。如果只有 2 个，它会创建新的 Pod；如果有 4 个，它会删除多余的 Pod。

这种模式让集群具备一定的自愈能力。

## 常用命令

```shell
# 查看集群信息
kubectl cluster-info

# 查看节点
kubectl get nodes

# 查看 Pod
kubectl get pods

# 查看服务
kubectl get svc

# 应用配置
kubectl apply -f deployment.yml

# 查看资源详情
kubectl describe pod <pod-name>

# 查看日志
kubectl logs -f <pod-name>

# 进入容器
kubectl exec -it <pod-name> -- sh
```

## Docker 和 Kubernetes 的关系

Docker 常用于构建镜像和本地运行容器。Kubernetes 使用容器运行时在集群中运行容器，现在常见运行时是 containerd。

典型流程是：

1. 写应用代码。
2. 用 `Dockerfile` 构建镜像。
3. 推送镜像到镜像仓库。
4. 编写 Kubernetes YAML。
5. 用 `kubectl apply` 部署到集群。

## 适合 Kubernetes 的场景

- 微服务数量较多，需要统一部署和治理
- 需要滚动更新、回滚、弹性伸缩和故障自愈
- 多团队共用一套资源池
- 应用需要跨多台机器运行
- 有成熟的监控、日志、发布和权限管理需求

## 不一定需要 Kubernetes 的场景

Kubernetes 的学习和运维成本不低。如果只是个人项目、单机服务、小型内部工具，Docker Compose、普通进程管理器或云厂商的托管应用平台可能更简单。

## 学习路线

1. 先理解 Docker 镜像和容器。
2. 学会 `Pod`、`Deployment`、`Service` 三个核心对象。
3. 用 `kubectl apply` 部署一个 Nginx 或后端 Demo。
4. 学习配置管理、日志查看、滚动更新和回滚。
5. 再继续学习 Ingress、存储、权限控制和 Helm。

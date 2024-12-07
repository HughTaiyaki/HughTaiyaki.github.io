# Internet for kids
> 以下是一些常用的网络基础知识

## IPv4 & IPv6
??? info "IPv4 & IPv6"
    IPv4

    - 由 4 个段组成，每个段 8 位，表示 32 位整数的方式 IPv4 地址

    IPv6 

    - [测一测你的 IPv6](https://test-ipv6.com/)
    - 由 8 个段组成，每个段 16 位，表示 128 位整数的方式 IPv6 地址
    - 连续全 0 段可以省略
    - 也有 IPv4-mapped IPv6 地址，用于兼容 IPv4 地址 `::ffff:10.78.18.216`
    - Linux 由 `ping6` 命令
## 从输入 URL 到页面展示展示发生了什么？
??? info "执行过程"
    - 浏览器先做 `URL 解析`，分为协议，域名，路径，端口号（默认http就是80）
    - 做 `DNS 解析`，浏览器先会查dns缓存有没有，没有问操作系统缓存，再没有就问本地的dns服务器，然后递归查询，返回给浏览器。
    - 浏览器获得ip地址后，`三次握手` 建立tcp连接。
    - 发送请求：浏览器通过 HTTP 或 HTTPS 协议，向目标网站的服务器发送 `http/https请求报文` ，询问它是否能提供所需的网页。
    - 网站的服务器接收到请求后，会处理并`返回网页内容`（HTML 文件、图片、样式等）。
    - 浏览器接收到网页内容后，会产生 DOM 树 和 CSSOM 树，结合产生 `渲染树` 进行解析和渲染，再执行 js
## TCP/IP 模型和 OSI 模型

## HTTP 协议概述
请求报文和响应报文

请求方式

GET 和 POST 的区别

请求常见状态码

强缓存和协商缓存

1.0 和 1.1 区别

2.0 和 1.1 区别

HTTPS 和 HTTP

HTTPS 加密过程

## TCP 和 UPD 协议概述
TCP 连接确保可靠性

UDP 实现可靠传输

三次握手，四次挥手

TCP 的 Keep-Alive 和 HTTP 的 Keep-Alive

## 域名系统与 DNS
DNS 查询过程

CDN 是什么

Cookie 和 Session 是什么



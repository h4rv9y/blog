---
title: Nginx 安装
date: 2020-03-18 23:09:37
categories: [Ops, Nginx]
tags:
    - Linux
    - Nginx
    - 安装教程

---
### Nginx 安装

1. 去 [Nginx 官网](http://nginx.org) 下载对应的 Nginx 包，推荐使用稳定（stable）版本

2. 上传至目标服务器，或直接在云端服务器使用 `wget` 命令下载

3. 安装所需依赖

   1. 安装 gcc 环境

      ```bash
      yum install gcc-c++
      ```

   2. 安装 PCRE 库，用于解析正则表达式

      ```bash
      yum install -y pcre pcre-devel
      ```

   3. 安装 zlib 压缩和解压缩依赖

      ```bash
      yum install -y zlib zlib-devel
      ```

   4. 安装 SSL 安全的加密套接字协议层，用于 HTTP 安全传输（HTTPS）

      ```bash
      yum install -y openssl openssl-devel
      ```

4. 解压下载的压缩包，得到源码

   ```bash
   tar -zxvf -y nginx-1.16.1.tar.gz
   ```

5. 编译前建立 Nginx 临时目录，若不创建，有可能在启动过程中报错

   ```bash
   mkdir /var/temp/nginx -p
   ```

6. 在解压的源码目录中，通过如下命令进行配置

   ```bash
   ./configure \
   --prefix=/usr/local/nginx \
   --pid-path=/var/run/nginx/nginx.pid \
   --lock-path=/var/lock/nginx.lock \
   --error-log-path=/var/log/nginx/error.log \
   --http-log-path=/var/log/nginx/access.log \
   --with-http_gzip_static_module \
   --http-client-body-temp-path=/var/temp/nginx/client \
   --http-proxy-temp-path=/var/temp/nginx/proxy \
   --http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
   --http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
   --http-scgi-temp-path=/var/temp/nginx/scgi
   
   ```

   > 注：`\` 代表在命令行中换行，用于提高可读性
   >
   > | 命令                           | 解释                                   |
   > | ------------------------------ | -------------------------------------- |
   > | --prefix                       | 指定 Nginx 的安装目录                  |
   > | --pid-path                     | 指向 Nginx 的 pid                      |
   > | --lock-path                    | 锁定安装文件，防止恶意篡改或误操作     |
   > | --error-log                    | 错误日志存放位置                       |
   > | --http-log-path                | HTTP 日志存放位置                      |
   > | --with-http_gzip_static_module | 启用 gzip 模块，在线实时压缩输出数据流 |
   > | --http-client-body-temp-path   | 设定客户端请求的临时目录               |
   > | --http-proxy-temp-path         | 设定 http 代理临时目录                 |
   > | --http-fastcgi-temp-path       | 设定 fastcgi 临时目录                  |
   > | --http-uwsgi-temp-path         | 设定 uwsgi 临时目录                    |
   > | --http-scgi-temp-path          | 设定 scgi 临时目录                     |

7. 编译

   ```bash
   make
   ```

8. 安装

   ```bash
   make install
   ```

9. 进入 sbin 目录启动 Nginx

   ```bash
   ./nginx
   ```

10. 打开浏览器访问，即可打开 Nginx 默认页面

> 本教程使用的系统发行版为 CentOS 7.3
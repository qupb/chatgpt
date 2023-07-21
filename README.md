## 概述

一键启动前后端，数据库密码一定要设置复杂点。

## 修改配置

修改 `server\config\index.js` 中的邮箱配置，还要修改的是mysql的账户密码。

修改`docker-compose` 文件中的数据库配置信息，主要是下面3行，这里要和上文的mysql账户密码一致。

```bash
- MYSQL_DATABASE=chatgpt
- MYSQL_USER=chatgpt
- MYSQL_PASSWORD=chatgpt
```

## 运行

克隆项目

```bash
git clone https://github.com/qupb/chatgpt.git
cd chatgpt
```

运行

```bash
# 编译
docker compose build
# 后台运行
docker compose up -d
# 删除容器
docker compose down
```

## 启动成功

```bash
docker logs mapp
#显示如下即为运行成功
#MySQL database connection succeeded.
```

## 导入数据库

ip:8001打开phpmyadmin，输入配置的用户名和密码

```bash
ip:8001
```

## 使用

```bash
ip
```

打开ip，注册账号使用即可。

## 自行打包前端

使用client目录下的源码，指定 `.env.production` 如下即可。

```bash
# 请求地址
VITE_APP_REQUEST_HOST=pro
```

## 反代配置

```bash
server {
    listen 80;
    listen 443 ssl;
    server_name a.xxx.com;
    ssl_certificate /etc/nginx/xxx.com/cert.pem;
    ssl_certificate_key /etc/nginx/xxx.com/key.pem;
    location /auth {
        root /var/www/faka;
        index index.html;
    }
    if ($scheme != "https") {
        return 301 https://$server_name$request_uri;
    }
    location / {
        proxy_pass http://localhost:8002/;
    	proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_set_header Host $host;
        proxy_buffering off;
    }
}
```

### Star History

[![Star History Chart](https://api.star-history.com/svg?repos=rita-iot/chatgpt&type=Date)](https://star-history.com/#rita-iot/chatgpt&Date)

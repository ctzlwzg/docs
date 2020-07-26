## nginx

### 安装教程

> 直接按照菜鸟教程中的步骤安装即可，这里不再赘述

```
https://www.runoob.com/linux/nginx-install-setup.html
```

#### 相关命令

> 输入命令需校验自己的文件位置是否与我之相同

```linux
1. /usr/local/webserver/nginx/sbin/nginx   启动nginx
2. /usr/local/webserver/nginx/sbin/nginx -s reload   重新载入配置文件
3. /usr/local/webserver/nginx/sbin/nginx -s reopen  重启nginx
4. /usr/local/webserver/nginx/sbin/nginx -s stop  停止nginx
5. /usr/local/webserver/nginx/sbin/nginx -t 检查配置文件

```

### 相关配置单独一个文件

- 在 nginx.conf 文件中添加导入文件的代码

  - 如 include /usr/local/webserver/nginx/conf/customize_conf/blog.conf;注意文件的位置

- 在 同级目录下创建 customize_conf 文件夹，把 blog.conf 配置文件放在这个文件夹中即可，如需后续扩展，只需在 nginx.conf 文件中导入配置文件即可

### 注意点

> 修改配置文件以后需要重新载入配置文件，在此之前也可以先检查一下配置文件

> 如果觉得配置没有问题，请清除浏览器缓存，该办法已经解决了我两次遇到的问题了

### 静态资源服务配置

```nginx

server {
	listen 80;
    server_name pdd.wuzhenggang.com;
    location / {
           proxy_pass http://127.0.0.1:8084;
		   index   index.html index.htm;
        }
}
server {
  listen 8084;
  server_name localhost;
	index index.html index.htm index.php;
  root /usr/local/webserver/nginx/html/pdd;#站点目录

	location / {
  		try_files $uri $uri/ /index.html;
	}

	location ~ .*\.(php|php5)?$
    {
      #fastcgi_pass unix:/tmp/php-cgi.sock;
      fastcgi_pass 127.0.0.1:9000;
      fastcgi_index index.php;
      include fastcgi.conf;
    }

    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf|ico)$
    {
      expires 30d;
	# access_log off;
    }
    location ~ .*\.(js|css)?$
    {
      expires 15d;
	# access_log off;
    }
    access_log off;
}

```

### vue History 模式配置

```nginx
location / {
  try_files $uri $uri/ /index.html;
}
```

> 原文地址： https://router.vuejs.org/zh/guide/essentials/history-mode.html#%E5%90%8E%E7%AB%AF%E9%85%8D%E7%BD%AE%E4%BE%8B%E5%AD%90

### https 相关配置

```nginx

server {
	listen 80;
	server_name www.wuzhenggang.com;
	rewrite ^(.*)$ https://$host$1 permanent;
}
server {
	listen 443 ssl;
	server_name www.wuzhenggang.com;
    #证书放置地址
	ssl_certificate "/home/www/ssl/blog/1_www.wuzhenggang.com_bundle.crt";
	ssl_certificate_key "/home/www/ssl/blog/2_www.wuzhenggang.com.key";

	location / {
				proxy_pass http://127.0.0.1:8081;
				proxy_set_header X-Real-IP $remote_addr;
				proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
				proxy_set_header Host $http_host;
				proxy_set_header X-NginX-Proxy true;
				proxy_redirect default;
		}
}

server{
	listen 8081;#监听端口
	server_name localhost;#域名
	index index.html index.htm index.php;
	root /usr/local/webserver/nginx/html/blogweb;#站点目录

	location / {
		try_files $uri $uri/ /index.html;
	}

	  location ~ .*\.(php|php5)?$
	{
	  #fastcgi_pass unix:/tmp/php-cgi.sock;
	  fastcgi_pass 127.0.0.1:9000;
	  fastcgi_index index.php;
	  include fastcgi.conf;
	}

	location ~ .*\.(gif|jpg|jpeg|png|bmp|swf|ico)$
	{
	  expires 30d;
	# access_log off;
	}
	location ~ .*\.(js|css)?$
	{
	  expires 15d;
	# access_log off;
	}
	access_log off;
}

```

#### 注意

> 配置是域名，监听端口，证书位置，入口文件的位置需要再三确认是否正确

> 服务器中域名解析需要加上

### https 证书免费申请

- 腾讯云地址 https://cloud.tencent.com/

- 登录控制台

- 搜索 SSL 证书

- 购买证书，选择域名型免费版

#### 注意

> 如需二级域名也需要 htts，证书需要单独再次申请

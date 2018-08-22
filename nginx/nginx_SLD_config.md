* 首先进入到[nginx](https://github.com/Sokkam/server_config/blob/master/nginx/nginx_config.md)安装目录下，进入conf文件夹
```
cd conf
ls
```
* 继续看到```nginx.conf```那个文件
```
vi nginx.conf
```
* 然后开始修改文件，比如当前我有几个端口，8080、8090、8091，我想让他们都被80端口监听然后并且配置二级域名就要这样
```
server {
    listen 80;
    server_name a.domainname.com;
    location / {
       proxy_pass http://localhost:8080;
    }
}
server {
    listen 80;
    server_name b.domainname.com;
    location / {
       proxy_pass http://localhost:8090;
    }
}
server {
    listen       80;
    server_name  c.domainname.com;

    server_name_in_redirect off;
    proxy_set_header Host $host:$server_port;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header REMOTE-HOST $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

    location / {
        root   html;
        index  index.html index.htm;
        proxy_pass http://localhost:8091;
    }
}
```
* 配置好后重启```nginx```
* 接下来就是去我们的云服务器上进行二级子域名的配置，小弟这里用的是腾讯云，域名也是已经经过备案了的；点击解析
![image](https://github.com/Sokkam/server_config/blob/master/nginx/nginx_slc_1.png)
* 进去后是这个样子的
![image](https://github.com/Sokkam/server_config/blob/master/nginx/nginx_slc_2.png)
* 然后就到了自己动手配置的时候了，主机记录填写的就是域名前缀，比如刚刚我们在```nginx.conf```中配置的三个url：a.domainname.com、b.domainname.com和c.domainname.com
1. 主机记录填写a或者b或者c
2. 记录值填写你项目部署所在的服务器，没错也正是你nginx配置的那个服务器的公网ip
![image](https://github.com/Sokkam/server_config/blob/master/nginx/nginx_slc_3.png)
* 然后再根据nginx上配置的server_name来进行访问

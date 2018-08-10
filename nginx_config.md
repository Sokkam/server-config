* 准备好 ```nginx.tar.gz``` 的包
```
tar -zxvf nginx-1.15.2.tar.gz
```
```
cd nginx-1.15.2
```
```
yum install gcc-c++
yum install -y pcre pcre-devel
yum install -y zlib zlib-devel
```
* 自定义配置
```
./configure
```
* 安装
```
make install
```
* 查找安装在什么地方
```
whereis nginx
```
* 去到指定目录下
```
cd /sbin
```
* 执行 ```nginx``` 服务测试，测试完通过先关闭
```
# 执行完访问服务器，通过显示nginx页面算成功
./nginx
./nginx -s stop
```
* 然后进入到 ```conf``` 目录
```
cd ../conf
vi ./nginx.conf
```
* 添加配置，假设我有个服务端口是 ```8090```
```
server {
    listen       80;
    server_name  localhost;
    #charset koi8-r;

    #access_log  logs/host.access.log  main;

    # 以下五行一定要配，不然可能出现无法将80端口转发到8090端口的现象
    server_name_in_redirect off;
    proxy_set_header Host $host:$server_port;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header REMOTE-HOST $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        location / {
            root   html;
            index  index.html index.htm;
            proxy_pass http://localhost:8090;
        }
```
* 退出回到刚刚的 ```sbin``` 目录，执行 ```nginx```
```
./nginx
```
* 再去通过你的ip地址，不用配端口号，加上服务名称，就可以访问到项目了

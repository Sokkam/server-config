> 小弟这里使用的是腾讯云，所以以腾讯云来进行演示。
1. 首先你要有一个域名
2. 登录，点击去到```SSL证书管理```，点击申请证书
* 通用名称可写一二级域名，通过Nginx配置以及腾讯云```域名管理云解析```即可
* 申请邮箱你懂得
3. 申请好后，有个审核时间，审核成功后，就可以去对证书进行一个下载的操作，我们这里需要用到的是Nginx的，所以只列出Nginx的证书文件
```
.
├── Tomcat
├── Nginx
|   ├── 2_a.domain.com.key
|   └── 1_a.domain.com_bundle.crt
├── IIS
├── Apache
```
4. 然后进入到自己配置了Nginx的服务器中，把这两个证书文件，放入到服务器中，这里演示是放置在```/usr/local/nginx/conf/ssl/```目录下
5. 然后在conf目录下执行命令```vi nginx.conf```
```
server {
    listen 80;
    server_name a.domain.com;
    rewrite ^(.*) https://$server_name$1 permanent;
}

server {
    listen       443 ssl;
    server_name  a.domain.com;

    # ssl on;
    ssl_certificate /usr/local/nginx/conf/ssl/1_a.domain.com_bundle.crt;
    ssl_certificate_key /usr/local/nginx/conf/ssl/2_a.domain.com.key;
    ssl_session_timeout 5m;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2; #按照这个协议配置
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;#按照这个套件配置
    ssl_prefer_server_ciphers on;

    server_name_in_redirect off;
    server_name_in_redirect off;
    proxy_set_header Host $host:$server_port;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header REMOTE-HOST $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        
    location / {
        root   html;
        index  index.html index.htm;
        proxy_pass http://localhost:8015;
     }
}
```

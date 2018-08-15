> [Redis](http://www.redis.cn/download.html)
* 刚刚已经安装好了 ```gcc``` 环境了
* 准备好redis的压缩包
```
tar -xvf redis-4.0.1.tar.gz -C /usr/local

cd /usr/local/redis-4.0.1
```
* 编译
```
make
```
* 还是该目录下执行指定目录安装
```
make PREFIX=/usr/local/redis install

cd /usr/local/redis/bin
```
* 然后可以启动一下 ```redis-server``` 来测试一下
* 然后引入配置文件
```
cd ../../redis-4.0.1/

cp -r redis.conf ../redis/bin

cd ../redis/bin

vi redis.conf
```
* 找到几个参数修改一下，在linux里面太多代码要快速查找，就按住 ```shift + :(反正就这个冒号键)```，然后打一个 ```/(这里跟你要查的代码，忽略括号)，回车就能找到了
```
# 改为yes（后端模式启动）
daemonize no

# 开放远程连接（或者把这个bind注释掉也行，然后如果架设在云服务器上是要去安全组那里设置的，端口号6379啦，然后地址就是0.0.0.0/0）
bind 0.0.0.0

# 连接密码
requirepass yourpassword

# 开启aof持久化
appendonly yes

# 选择aof持久化策略
appendfsync everysec

# 设置缓存文件生成和读取的目录
dir /找一个你自己想要的路径
```
* 一定要先启动服务才行！！
```
./redis-server redis-conf
```
* 设置了密码后启动redis就需要添加密码才能启动
```
./redis-cli -a yourpassword
```

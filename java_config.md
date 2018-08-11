> [JDK下载地址](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* 准备好JDK放在服务器目录下，我这里用的是JDK8
```
tar -zxvf /root/package/jdk/jdk-8u181-linux-x64.tar.gz
```
* 更改名字
```
mv jdk1.8.0_181/ jdk8
```
* 配置Java环境
```
vim /etc/profile
```
* 末尾添加
```
export JAVA_HOME=/root/package/jdk/jdk8
export CLASSPATH=.:${JAVA_HOME}/lib/tools.jar:${JAVA_HOME}/jre/lib/dt.jar
export PATH=${JAVA_HOME}/bin:${JAVA_HOME}/jre/bin:$PATH
```
* 退出vim命令，并使 ```/etc/profile``` 生效
```
source /etc/profile
```
* 输入以下命令，如查看到Java版本代表成功
```
java -version
```

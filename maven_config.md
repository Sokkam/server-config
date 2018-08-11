> [Maven Download](https://maven.apache.org/download.cgi)
* 解压下载好的 ```maven```
```
tar -zxvf apache-maven-3.5.4-bin.tar.gz
```
* 配置环境
```
vim /etc/profile
```
* 先配置Maven主路径，再追加到PATH中
```
export MAVEN_HOME=/root/package/maven/apache-maven-3.5.4
export JAVA_HOME=/usr/lib/jdk8
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib/tools.jar:${JRE_HOME}/lib/dt.jar
export PATH=${JAVA_HOME}/bin:${JAVA_HOME}/jre/bin:$PATH:${MAVEN_HOME}/bin
```
* 配置好后退出来，使环境配置生效
```
source /etc/profile
```
* 输入命令，查看到版本号代表配置成功
```
mvn -v
```

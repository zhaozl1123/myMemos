# 部署JDK

````bash
# 下载对应版本jdk
https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html
# user:545362989@qq.com
# pwd:WObugaosuni1123
# 例如：Linux x64 Compressed Archive	137.06 MB	jdk-8u281-linux-x64.tar.gz
# 解压
tar -zxvf jdk-8u211-linux-x64.tar.gz 
mv jdk1.8.0_211/ /opt/jdk
# 设置java 环境变量,配置profile**
vi /etc/profile
# 末尾增加
JAVA_HOME=/opt/jdk/
JAVA_BIN=/opt/jdk/bin
JRE_HOME=/opt/jdk/jre
CLASSPATH=/opt/jdk/jre/lib:/opt/jdk/lib:/opt/jdk/jre/lib/charsets.jar
export  JAVA_HOME  JAVA_BIN JRE_HOME  PATH  CLASSPATH
# 配置立马有效
source /etc/profile
# 配置 bashrc
vi ~/.bashrc
# 末尾增加
export JAVA_HOME=/opt/jdk
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
# 生效
source ~/.bashrc
# 查看部署结果
java -version
`````


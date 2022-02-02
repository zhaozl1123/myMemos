# Nodejs安装

```bash
# 从官网下下载最新的nodejs，https://nodejs.org/en/download/
# 历史版本可从https://nodejs.org/dist/下载
tar -xvf node-v10.16.0-linux-x64.tar.xz
# 移动并改名文件夹
cd /usr/local/
mv /var/ftp/pub/node-v10.16.0-linux-64 . //后面的.表示移动到当前目录
mv node-v10.16.0.0-linux-64/ nodejs
# 让npm和node命令全局生效
vim /ect/profile
export PATH=$PATH:/usr/local/nodejs/bin
# 使配置文件生效
source /etc/profile
# 软链接方式
ln -s /usr/local/nodejs/bin/npm /usr/local/bin/
ln -s /usr/local/nodejs/bin/node /usr/local/bin/
# 查看nodejs是否安装成功
node -v
npm -v
# 安装cnpm
npm set registry https://registry.npm.taobao.org
npm set disturl https://npm.taobao.org/dist
npm cache clean --force
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm -v
# 设置用户变量
D:\node.js\node_global\
# 安装vue-cli
npm set registry https://registry.npm.taobao.org
npm set disturl https://npm.taobao.org/dist
npm cache clean --force
cnpm install @vue/cli --registry=http://registry.npm.taobao.org
```


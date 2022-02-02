### 一、安装node环境(https://www.cnblogs.com/yanxulan/p/8978732.html)

1、下载地址为：https://nodejs.org/en/

2、检查是否安装成功：如果输出版本号，说明我们安装node环境成功

　　![img](https://images2018.cnblogs.com/blog/1389839/201805/1389839-20180502095431754-1395324051.png)

3、为了提高我们的效率，可以使用淘宝的镜像：http://npm.taobao.org/

　　输入：npm install -g cnpm –registry=https://registry.npm.taobao.org，即可安装npm镜像，以后再用到npm的地方直接用cnpm来代替就好了。

　　![img](https://images2018.cnblogs.com/blog/1389839/201805/1389839-20180502101905053-1587213309.png)

　　检查是否安装成功：

　　![img](https://images2018.cnblogs.com/blog/1389839/201805/1389839-20180502102033938-355932808.png)

### 二、搭建vue项目环境

1、全局安装@vue/cli

　　npm install --global @vue/cli

![image-20210716120329006](C:/Users/54536/AppData/Roaming/Typora/typora-user-images/image-20210716120329006.png)

2、创建基于 webpack 模板的新项目: vue create newproject000

　　![image-20210716120648139](C:/Users/54536/AppData/Roaming/Typora/typora-user-images/image-20210716120648139.png)

3、进入项目：cd newproject000，安装依赖

npm install --global @vue/cli-service

npm install --global @vue/compiler-sfc

4、启动项目npm run serve

### 三、Vue项目打包(build)后index.html空白页修正

- 在项目root目录新建文件vue.config.js,并添加如下代码

```
module.exports = {
  publicPath: './',
  outputDir: 'dist',
  configureWebpack: {
    externals: {
    }
  }
}

```

### 四、Vue项目dist发布至github

1. git中新建repo
2. 将dist目录及其内容添加至git并push
3. 在repo > setting > Pages中选择Source
4. 正确访问地址为:https://zhaozl1123.github.io/repoName/dist/index.html


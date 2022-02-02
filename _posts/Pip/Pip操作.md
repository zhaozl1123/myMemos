# 在本地创建pip镜像源

## 国内镜像源
````text
阿里云 http://mirrors.aliyun.com/pypi/simple/
豆瓣http://pypi.douban.com/simple/
清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/
中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/
华中科技大学http://pypi.hustunique.com/
````

## 创建requirements.txt
```text
setuptools==41.0.0
docker==4.3.1
Flask==1.1.2
flask-nav==0.6
gevent==20.9.0
gunicorn==20.0.4
joblib==0.16.0
Keras==2.3.1
matlab==0.1
matplotlib==3.3.0
numpy==1.18.5
pandas==1.1.0
PyMySQL==0.10.0
requests==2.24.0
scikit-learn==0.23.2
scipy==1.4.1
sklearn==0.0
statsmodels==0.11.1
tensorflow==2.0.0a0
My-Toolbox-zhaozl
MysqlOperater-zhaozl
```

## 下载资源
```bash
pip download -d /python-packages -r requirements.txt -i http://mirrors.aliyun.com/pypi/simple --trusted-host mirrors.aliyun.com
```

## 安装pypiserver
```bash
pip install pypiserver -i http://mirrors.aliyun.com/pypi/simple --trusted-host mirrors.aliyun.com
# 为了让在系统启动的时候同时启动pypiserver，修改/etc/rc.local
cat /etc/rc.local |egrep -v "^#|^$"
pypi-server /python-packages &>/var/log/pypi-server.log &
exit 0
```

## 启动pypiserver
```bash
# 查找pypi-server位置
find / -name pypi-server  # /usr/local/python3/bin/pypi-server
# 添加环境变量
export PATH=$PATH:/usr/local/python3/bin/
source /etc/profile
# 启动服务
pypi-server -p 9090 /python-packages
# 访问服务
pip install pypiserver -i http://127.0.0.1:9090 --trusted-host 127.0.0.1
```

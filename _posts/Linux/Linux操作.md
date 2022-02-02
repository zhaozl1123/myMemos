# Linux操作

## 1. 查看内核
```bash
uname -r  # 3.10.0-327.el7.x86_64
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
yum --enablerepo=elrepo-kernel install kernel-ml
```

## 2. 开机自启动
````bash
cd /etc/init.d
touch docker_autostart.sh
chmod a+x docker_autostart.sh
vim docker_autostart.sh
# 编辑内容
chkconfig  --add lnmp_autostart.sh
# 编辑内容
!/bin/sh
# 开机自动启动的配置
add for chkconfig
chkconfig:2345 60 20
processname:docker_autostart
description: ......
````

## 3. 无Console后台运行
```bash
nohup ./xxx.sh &
```

## 4.蓝屏后的处理

- 进入单用户模式：
  在开机界面选择希望进入的系统时，按e，在“Linux……UTF-8”后部加入“init=/bin/sh”，后按ctrl+x执行

  参考：https://www.cnblogs.com/junjind/p/8993420.html

- 进入路径/etc/rc.d/，修改权限：chmod a-x rc.local

  如果修改权限时出现：chmod: changing permissions of ‘…’: Read-only file system

  输入：mount -rw -o remount /

  参考：https://blog.csdn.net/zhangpeterx/article/details/83928344

- 重启

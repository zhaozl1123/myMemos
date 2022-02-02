# Git

## 仓库初始化
> 在GitHub上创建Repository<kbd>Test</kbd>

````bash
# 本地创建SSH-KEY
ssh-keygen -t rsa -C "mail@mail.com"
# RSA默认建立在本地的USER下
# 在GitHub的Account中，定义SSH-key，key内容位于上一步生成的RSA的.pub文件中
# 在git bash中定义本地Git的环境变量
git config --global user.name "name"
git config --global user.email "mail@mail.com"
# cd至需要创建仓库的文件夹中，执行初始化
cd /e/Test
git init
# 此时应当可以看见.git隐藏文件
`````

## 主要操作

### 文件上载
```bash
git add ./readme.md
```

### 文件提交
```bash
git commit -m "comment ......"
```

### 差异性检查
```bash
git diff <file> <originFile>
```

### 历史记录
```bash
git log --stat  # 可以显示有关文件的历次改版
git log --pretty=oneline  # 简要记录
git log --name-only  # 查看移交项目所含文件名
```

### 状态查询
```bash
# 检查版本是否一致
git status
```

### 版本调用/回滚
```bash
git reset --hard xxxx  # xxxx是版本Hash值的截断,lenth(xxxx)>=4
```

### 版本更新记录
```bash
git reflog
```

### Push
```bash
### github新建repository名称为Project01
cd ~/Project01
git init
git add ./readme.md
git commit -m "......"
git remote add origin git@github.com:username/Project01.git  # 链接到远程的网络项目
git push -u origin master  # 后续使用git push即可
```

### Pull
```bash
git pull
git pull origin master
git pull origin master --allow-unrelated-histories
```

### Clone
```bash
cd /e
mkdir Project02
cd ~/Project02
git clone git@github.com:zhaozl1123/Project01.git newName  # 以newName作为新项目名称从网络克隆项目
```

### 仓库状态查询
```bash
git log --stat
git reflog --stat
```

### 仓库状态修改
```bash
# 修改commit message
git log  # 查询过去的版本信息（初始信息不能修改）
git rebase -i HEAD~5  # 显示最近5次版本修改
# 将相应版本的pick修改为edit
git commit --amend  # 开始修改commit message
git rebase --continue  # 提交
```

### 编辑Tag
```bash
# 定义、查找、修改
git tag  # 查看仓库设计的tag
git tag -a <Version> <SerieNumber> -m "<Message>"
git tag -d <Version>  # 删除某一版本号
git tag -l "*<...>"  # 查看具有通配符和字符串<...>的版本号
```
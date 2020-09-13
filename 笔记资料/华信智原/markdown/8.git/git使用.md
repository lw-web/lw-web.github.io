# `git`使用

## 新增相关文件

### 新增`.gitignore`文件

- 添加忽略信息：
  - `node_modules`
  - `.idea`
  - `.vscode`
  - `.git`

### 新增`README.md`文件

- 描述项目

### 添加项目开源协议`LICENSE`

## 创建本地仓储

- `git init`初始化

- `git status`查看文件状态

- `git add .`将项目放入暂存区

- `git commit -m 'init my project'`提交到本地仓储

## 创建远程仓储

- 码云：`gitee.com`

- 查找自己的公钥：`c——用户——asus——.ssh——id_rsa.pub`

- 复制公钥到码云

- 在码云新建空白空仓储

## 连接远程仓储，推送送项目

- 在命令行运行：

```shell
git config --global user.name "李伟"
git config --global user.email "872993425@qq.com"
```

- 连接远程仓库，提交项目到远程仓库：

```shell
git remote add origin https://gitee.com/lw6989661/vue2019.git
git push -u origin master
```

## 我的码云

用户名：`lw6989661`

密码：`lw6989661`


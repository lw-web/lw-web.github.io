# git学习

## 安装git

- [安装git](https://git-scm.com/downloads)

## git初始设置

- 设置用户名

```shell
git config --global user.name "Firstname Lastname"
```

- 设置邮箱

```shell
git config --global user.email "your_email@example.com"
```

- 设置提高可读性

```shell
git config --global color.ui auto
```

- 查看git配置信息

```shell
git config --list
```

## 创建GitHub账户

- [注册](https://github.com/join)
- [我的GitHub](https://github.com/weblw/study)
  - 用户名：weblw
  - 密码：lw6989661
- 设置SSH Key并添加公开密钥[参考文档](https://www.cnblogs.com/yehui-mmd/p/5962254.html)
  - 输入`ssh-keygen -t rsa -C 872993425@qq.com`
  - 打开你的id_rsa.pub文件，复制下里面的内容，然后登录进去你的github
  - `C:\Users\asus\.ssh\id_rsa.pub`
  - 点击settings进去，找到左侧的SSH Keys
  - 点击Add SSH Key，在title处填入任意的标识，在Key部分里面添加刚才复制的id_rsa.pub文件里的内容
  - 输入：`ssh -T git@github.com`，这时会问是否继续连接，我们输入 yes

- clone已有仓库
  - `git clone git@github.com:weblw/study.git`
  - 加入文件到暂存盘`git add hello_world.php`
  - 提交`git commit -m "Add hello world script by php"`
  - 更新仓库`git push`

## 初始化仓库

- 创建目录`mkdir test`
- 切换目录`cd test`
- 初始化`git init`

## 查看仓库状态

- `git status`
- `touch README.md`

## 向暂存区添加文件

- `git add README.md`

## 保存仓库的历史记录

- `git commit -m "First commit"`
- -m 参数后的`First commit`称作提交信息，是对这个提交的
  概述。
- 如果想要记述得更加详细，请不加 -m，直接执行 git commit命令
  - 在编辑器中记述提交信息的格式如下
    - 第一行：用一行文字简述提交的更改内容
    - 第二行：空行
    - 第三行以后：记述更改的原因和详细内容
- 终止提交：关闭git就会终止

## 查看提交后的相关信息

- 查看提交后的状态
  - `git status`
- 查看提交日志
  - `git log`
  - 如果只想让程序显示第一行简述信息，可以在 git log命令后加
    上 `--pretty=short`
    - `git log --pretty=short`
  - 只要在 git log命令后加上目录名，便会只显示该目录下的日志
    - `git log README.md`
- 显示文件的改动
  - `git log -p`
  - 只查看 README.md 文件的提交日志以及提交前后的差别
    - `git log -p README.md`
- 查看更改前后的差别
  - `git diff`命令可以查看工作树、暂存区、最新提交之间的差别
  - “+”号标出的是新添加的行，被删除的行则用“-”号标出。
- 查看最新提交的差别
  - `git diff HEAD`

## 使用GitHub生成个人主页

- `https://weblw.github.io/`


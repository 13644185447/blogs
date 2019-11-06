#Git
##初始配置

配置文件为 ~/.gitconfig ，执行任何Git配置命令后文件将自动创建。

第一个要配置的是你个人的用户名称和电子邮件地址。这两条配置很重要，每次 Git 提交时都会引用这两条信息，说明是谁提交了更新，所以会随更新内容一起被永久纳入历史记录：

```
git config --global user.email "16344185447@163.com"
git config --global user.name "16344185447@163.com"
```
##常用命令

* 1.初始化新仓库 `git init`
* 2.克隆旧仓库 `git clone https://github.com/13644185447/blogs.git`
* 3.查看状态 `git status`
* 4.提交单个文件 `git add index.php`
* 5.提交所有文件 `git add .`
* 6.使用通配符提交 `git add *.js`
* 7.提交到仓库中 `git commit -m '提示信息'`
* 8.提交已经跟踪过的文件，不需要执行`add git commit -a -m '提交信息'`
* 9.删除版本库与项目目录中的文件 `git rm index.php`
* 10.只删除版本库中文件但保存项目目录中文件 `git rm --cached index.php`
* 11.修改最后一次提交 `git commit --amend`

##清理
* 1.放弃没有提交的修改 `git checkout .`
* 2.删除没有add 的文件和目录 `git clean -fd`
* 3.显示将要删除的文件或目录 `git clean -n`
##日志查看
* 1.查看日志 `git log`
* 2.查看最近2次提交日志并显示文件差异 `git log -p -2`
* 3.显示已修改的文件清单 `git log --name-only`
* 4.显示新增、修改、删除的文件清单 `git log --name-status`
* 5.一行显示并只显示SHA-1的前几个字符 `git log --oneline`
##定义别名
通过创建命令别名可以减少命令输入量。
```
git config --global alias.c commit
```
可以在配置文件中查看或直接编辑,打开文件命令
```
git config --global -e
```
下面是一个Git命令Alias配置
```
[alias]
	a = add .
	c = commit
	s = status
	l = log
	b = branch
```
现在可以使用 git a 实现 git add . 一样的效果了。
##.gitignore
.gitignore用于定义忽略提交的文件
* 所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。
* 匹配模式最后跟反斜杠（/）说明要忽略的是目录。
* 可以使用标准的 glob 模式匹配。
```
.idea
/vendor
.env
/node_modules
/public/storage
*.txt
```
##Branch
分支用于为项目增加新功能或修复Bug时使用。
* 1.创建分支,名字为dev `git branch dev`
* 2.查看分支列表 `git branch`
* 3.切换到dev分支 `git checkout dev`
* 4.创建并切换分支 `git checkout -b dev`
* 5.合并dev分支到master
```
git checkout master  //先切换到master
git merge dev  //合并dev分支
```
* 6.删除分支 `git branch -d dev`
* 7.强制删除未合并的分支 `git branch -D dev`
* 8.查看未合并分支 `git branch --no-merged`
* 9.查看已合并分支 `git branch --merged`

##Stashing
当你正在进行项目中某一部分的工作，里面的东西处于一个比较杂乱的状态，而你想转到其他分支上进行一些工作。问题是，你不想提交进行了一半的工作，否则以后你无法回到这个工作点。

"暂存" 可以获取你工作目录的中间状态——也就是你修改过的被追踪的文件和暂存的变更——并将它保存到一个未完结变更的堆栈中，随时可以重新应用

注意：add添加后，才可以用stash暂存


* 1.暂存工作 `git stash`
* 2.查看暂存列表 `git stash list`
* 3.恢复到上一个暂存 `git stash apply`
* 4.恢复到指定暂存 `git stash apply stash@{0}` (`stash@{0}`为版本号，在`git stash list` 列表中显示)
* 5.删除指定暂存 `git stash drop stash@{0}`
* 6.恢复并删除暂存 `git stash pop`

##Tag
Git 也可以对某一时间点上的版本打上标签 ，用于发布软件版本如 v1.0.1

* 添加标签 `git tag v1.0.1`
* 列出标签 `git tag`
* 推送标签 `git push --tags`
* 删除标签 `git tag -d v1.0.1`
* 删除远程标签 `git push origin :v1.0.1`
##打包发布
对mster分支代码生成压缩包供使用者下载使用，`--prefix` 指定目录名
```
git archive master --prefix='blogs/' --format=zip > blogs.zip
```
###SSH
##生成秘钥
使用ssh连接Github发送指令更加安全可靠，也可以免掉每次输入密码的困扰
在命令行中输入以下代码（windows用户使用 Git Bash）
```
ssh-keygen -t rsa
```
一直按回车键直到结束。系统会在`~/.ssh` 目录(windows会在`C:\Users\Administrator\.ssh`)中生成 `id_rsa`和`id_rsa.pub`，即密钥`id_rsa`和公钥`id_rsa.pub`。

向GitHub添加秘钥

![muhua](https://qqadapt.qpic.cn/txdocpic/0/94152d5d684863bebba0537138a85917/1600?_type=png)
点击 `New SSH key` 按钮，添加上面生成的 `id_rsa.pub` 公钥内容

##pull
拉取远程主机某个分支的更新，再与本地的指定分支合并。

1.拉取origin主机的ask分支与本地的master分支合并 `git pull origin ask:ask`

2.拉取origin主机的ask分支与当前分支合并 `git pull origin ask`

3.如果远程分支与当前本地分支同名直接执行 `git pull`
##PUSH
`git push`命令用于将本地分支的更新，推送到远程主机。它的格式与`git pull`命令相似。
1.将当前分支推送到origin主机的对应分支(如果当前分支只有一个追踪分支 ，可省略主机名)
```
git push origin
```
2.使用-u选项指定一个默认主机 ,这样以后就可以不加任何参数直播使用git push。
```
git push -u origin master
```
3.删除远程ask分支  `git push origin --delete ask`

4.本地ask分支关联远程分支并推送 `git push --set-upstream origin ask`
##自动部署
GitHub设置 `WebHook`
![muhua](https://qqadapt.qpic.cn/txdocpic/0/de7721392447f243e222eaab5bf1efe6/1600?_type=png)

#同步脚本
项目中添加处理 webhook 的webhook.php文件内容如下，并提交到版本库
```
<?php
// GitHub Webhook Secret.
// GitHub项目 Settings/Webhooks 中的 Secret
$secret = "huangjianning";

// Path to your respostory on your server.
// e.g. "/var/www/respostory"
// 项目地址
$path = "/www/wwwroot/hjn.com";

// Headers deliveried from GitHub
$signature = $_SERVER['HTTP_X_HUB_SIGNATURE'];

if ($signature) {
  $hash = "sha1=".hash_hmac('sha1', file_get_contents("php://input"), $secret);
  if (strcmp($signature, $hash) == 0) {
    echo shell_exec("cd {$path} && /usr/bin/git reset --hard origin/master && /usr/bin/git clean -f && /usr/bin/git pull 2>&1");
    exit();
  }
}

http_response_code(404);
?>
```
#其他配置※※
* 1.函数

执行 `git pull` 指令需要使用 `shell_exec` 函数，确保php没有禁用`shell_exec`函数

* 2.修改权限

```
chown -R www .
chmod -R g+s .
sudo -u www git pull
```
现在向GitHub 推送代码后，服务器将自动执行代码拉取，自动部署功能设置完成了。

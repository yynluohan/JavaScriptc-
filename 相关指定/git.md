# git 相关命令


## git 常用命令

```
git init                    // 初始化
git init --bare  <name>.git   // 初始化一个项目     
git clone 地址              // 将远程地址代码clone到本地
git clone -b 分支名 地址     // 将分支的代码clone到本地
git status                  // 查看当前状态
git add 文件名              // 将某个文件存入暂存区
git add b c                //把b和c存入暂存区
git add .                  // 将所有文件提交到暂存区
git add -p 文件名          // 一个文件分多次提交
git commit -m "备注信息"   // 提交到仓库
git log                   // 日志信息

```


## git 创建/删除/查看分支

- `创建分支`： git branch <name>

  例如：创建aaa分支   git branch aaa

- `创建+切换分支`： git checkout -b <name>

- `查看分支`：git branch

- `切换分支`： git checkout <name>

- `合并某分支到当前分支`： git merge <name>

- `删除分支`： git branch -d <name>


## 版本回退问题

-  `git log` 查看日志，找到需要回退的版本号

-  `git reset --hard 版本号`  本地进行回退

-  `git push --force origin master`  强制推送到主分支

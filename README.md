# Git使用方法

> 你现在想把电脑上的一个项目上传到 GitHub。

# 目录
- [Git使用方法](#git使用方法)
- [目录](#目录)
  - [代理网络问题解决方案](#代理网络问题解决方案)
  - [在 GitHub 上建立仓库 (Create Repository)](#在-github-上建立仓库-create-repository)
  - [初次将本地代码推送到远程](#初次将本地代码推送到远程)
    - [情况 A：是一个全新的空文件夹](#情况-a是一个全新的空文件夹)
    - [情况 B：已经有代码了(更常用，本地写完README.md后上传)](#情况-b已经有代码了更常用本地写完readmemd后上传)
  - [后续修改](#后续修改)
  - [分支 (Branch) 的使用](#分支-branch-的使用)
    - [创建并切换到新分支](#创建并切换到新分支)
    - [切回主分支](#切回主分支)
    - [合并代码 (Pull Request / PR)](#合并代码-pull-request--pr)
  - [.gitignore](#gitignore)
  - [误删文件处理](#误删文件处理)

## 代理网络问题解决方案
配置代理（如果你开了“梯子”/加速器）

如果正在使用 VPN、加速器或代理软件来访问 GitHub，Git 它是不会自动使用你的代理的，你需要手动告诉它端口号。

查看你的代理端口：

打开你的代理软件设置，找到 “本地监听端口” 或 “HTTP/S 代理端口”。

假设端口号是 7890（Clash 常见端口）或者 10809（v2ray 常见端口）。

设置 Git 代理（把 7890 换成你实际的端口号）：


```
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```

再次尝试 `git push`。

## 在 GitHub 上建立仓库 (Create Repository)
   
1. 登录 GitHub，点击右上角的 + 号，选择 New repository。

2. Repository name: 输入项目名字（例如 my-first-project）。

3. Description: 选填，写一段项目简介。

4. Public/Private: 选择公开或私有。

5. 点击 Create repository。
   
## 初次将本地代码推送到远程
   
创建完成后，GitHub 会给出一串指令。回到你的电脑，在你的项目文件夹内右键打开 Git Bash (或终端)，依次执行：

### 情况 A：是一个全新的空文件夹

```
echo "# my-first-project" >> README.md   # 创建一个说明文件
git init                                 # 初始化 Git 仓库（建立时光机）
git add .                                # 把所有文件放入“暂存区”
git commit -m "first commit"             # 提交！并附带备注信息
git branch -M main                       # 将主分支重命名为 main
git remote add origin <你的仓库地址URL>   # 关联远程仓库（URL在GitHub页面复制，不用加<>）
git push -u origin main                  # 推送到远程 GitHub
```

### 情况 B：已经有代码了(更常用，本地写完README.md后上传)

```
git init
git branch -M main
git remote add origin <你的仓库地址URL>
git add .
git commit -m "初始化项目"
git push -u origin main
```

## 后续修改

```
git add .  # 添加所有修改过的文件
git commit -m "修复了登录页面的bug"  # 引号内写清楚你干了什么
git push
```

进阶与协作 (Branch & Pull Request)
如果你要和别人合作，或者想开发新功能但不影响主程序，绝对不要直接在 main 分支上改代码。

## 分支 (Branch) 的使用

### 创建并切换到新分支
```
git checkout -b feature-login  # 创建一个叫 feature-login 的分支
```
在这个分支上随意修改、提交 (add, commit)，这完全不会影响 main 分支的代码。

### 切回主分支
```
git checkout main
```

### 合并代码 (Pull Request / PR)
这是 GitHub 最核心的社交/协作功能。

1. 在 feature-login 分支开发完并 git push 后。

2. GitHub 页面会提示你 "Compare & pull request"。

3. 点击它，填写描述，创建一个 Pull Request。

4. 你的队友（或者你自己）在网页上审查代码，没问题后点击 Merge pull request。

5. 代码就被合并进 main 分支了。

## .gitignore
这是一个黑名单文件。

写在这里面的文件名，Git 会自动忽略，绝对不会上传到仓库。

示例：
```gitignore
# LaTeX 中间文件
*.aux
*.log
*.out
*.toc
*.synctex.gz
*.fls
*.fdb_latexmk
*.bbl
*.blg
```

## 误删文件处理
> 只要库还在，不管在本地还是云端删除文件都可以通过如下方式恢复

方法一：GitHub 网页版“时光倒流” (最简单，无需命令)
如果你不熟悉命令行，直接在网页上操作最快。

1. 打开 GitHub 仓库首页。

2. 点击代码列表右上方的 Commits（通常是一个时钟图标，旁边写着数字，比如 `25 commits`）。

3. 寻找历史： 在列表中找到你删除文件之前的那次提交（也就是文件还存在的那个版本）。

4. 浏览旧文件： 点击该次提交记录右侧的 <> 按钮（提示文字是 Browse the repository at this point）。

5. 找回文件：

- 此时页面会显示旧版本的文件列表。 

- 找到你误删的文件，点进去。

- 点击右上角的 `Copy raw file (复制内容)` 或者 `Download (下载)`。

6. 恢复： 在你本地电脑新建一个同名文件，把内容粘贴进去，保存。完事！

**方法二：命令行精准恢复单个文件 (最专业,更常用)**
如果你想用命令行只把那一个文件“拉”回到现在的目录里：

1. 查看历史，找到文件还存在时的 Commit ID：
```git log```
- 按 `Enter` 向下翻，找到删除操作之前的那次提交。

- 复制那次提交的哈希值（例如 `a1b2c3d`）。

- 按 q 退出查看。

2. 把那个文件“传送”回来： 命令格式：`git checkout [旧版本ID] -- [文件路径]`
```
git checkout a1b2c3d -- 学习笔记_latex版/note_main.tex
```
(如果不记得具体路径，可以先打一部分然后按 Tab 键尝试补全，或者直接去文件夹里看)

3. 检查并提交： 此时文件已经回到你的文件夹了。
```
git status  # 你会看到文件被列为 "new file"
git commit -m "找回误删的文件"
git push
```
方法三：撤销“删除”这一整个操作 (最干净)
如果你那次提交里只做了删除文件这一件事，你可以直接“撤销”那次提交。

1. 找到“执行删除”的那次 Commit ID： 假设 ID 是 `e5f6g7h`。

2. 执行撤销命令：```git revert e5f6g7h```
- Git 会自动生成一个新的提交，内容正好和“删除”相反（也就是把文件加回来）。

3. 推送：`git push`

核心知识点
永远记住：在 Git 里，只要你曾经提交过（Commit），就几乎不可能彻底弄丢文件。 所谓的“删除”，只是在最新的版本里把它隐藏了，旧版本里它永远都在。

下一步建议： 如果你在执行 `git checkout` 时不知道文件的准确路径（比如是在子文件夹里），可以在终端输入 `git ls-tree -r [旧版本ID] --name-only` 来列出那个版本下的所有文件路径。

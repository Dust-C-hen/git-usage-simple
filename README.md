# Git使用方法

假设你现在想把电脑上的一个项目上传到 GitHub。

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

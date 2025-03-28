GitHub代码推送教程
前提条件
安装好Git
已有GitHub账户
要推送的代码文件夹
GitHub个人访问令牌(PAT)
详细步骤
1. 初始化Git仓库
如果你的项目还没有初始化为Git仓库，先执行：

# 进入项目文件夹
cd 你的项目路径
# 例如：cd D:\Users\Administrator\Desktop\gemni-image-generation

# 初始化Git仓库
git init
2. 配置Git用户信息
# 设置用户名
git config user.name "你的GitHub用户名"
# 例如：git config user.name ""

# 设置邮箱
git config user.email "你的邮箱"
# 例如：git config user.email ""
你可以添加--global参数使配置全局生效：

git config --global user.name "你的GitHub用户名"
git config --global user.email "你的邮箱"
3. 添加远程仓库
# 添加远程仓库地址
git remote add origin https://github.com/你的用户名/你的仓库名.git

如果提示remote origin already exists，使用以下命令修改：

git remote set-url origin https://github.com/你的用户名/你的仓库名.git
可以通过以下命令验证远程仓库是否添加成功：

git remote -v
4. 添加并提交文件
# 查看当前变更状态
git status

# 添加所有文件到暂存区
git add .

# 或者只添加特定文件
git add 文件名

# 提交更改
git commit -m "Initial commit"
5. 设置代理（如果需要）
如果你在中国或其他需要代理才能访问GitHub的地区：

# 设置HTTP代理
git config --global http.proxy http://127.0.0.1:你的代理端口
# 例如：git config --global http.proxy http://127.0.0.1:7890

# 设置HTTPS代理
git config --global https.proxy http://127.0.0.1:你的代理端口
# 例如：git config --global https.proxy http://127.0.0.1:7890
如果需要取消代理设置：

git config --global --unset http.proxy
git config --global --unset https.proxy
6. 推送代码（使用PAT）
方法一：使用环境变量（推荐，更安全）

# PowerShell中设置环境变量并推送
$env:GIT_PAT="你的个人访问令牌"; git push -u origin master
# 例如：$env:GIT_PAT=""; git push -u origin master

# CMD中设置环境变量
set GIT_PAT=你的个人访问令牌
git push -u origin master
方法二：在URL中包含PAT

# 设置带凭据的远程URL
git remote set-url origin https://你的用户名:你的个人访问令牌@github.com/你的用户名/你的仓库名.git
# 例如：git remote set-url origin https://bitezhang330:github_pat_xxx@github.com/bitezhang330/gemni-image-generation.git

# 然后推送
git push -u origin master
注意：使用-u参数会将本地分支与远程分支关联，以后可以直接使用git push命令。

7. 验证推送结果
# 检查状态
git status
如果显示Your branch is up to date with 'origin/master'.，说明推送成功了。

也可以在GitHub网站上查看你的仓库是否已更新。

常见问题解决
1. 403权限错误
如果遇到error: 403错误，通常是认证问题，确保：

PAT没有过期
PAT有正确的权限（至少需要repo权限）
用户名拼写正确
仓库名称正确
2. 网络问题
如果遇到连接超时或SSL错误：

检查代理设置
尝试关闭SSL验证（不推荐用于生产环境）：
git config --global http.sslVerify false
尝试使用SSH而不是HTTPS连接
3. 冲突问题
如果远程仓库已有内容且与本地冲突：

先拉取并合并：
git pull origin master
解决冲突后再推送
4. 分支问题
如果要推送到非主分支：

git push -u origin 你的分支名
# 例如: git push -u origin develop
获取GitHub个人访问令牌(PAT)
登录GitHub
点击右上角头像 -> Settings
左侧菜单点击Developer settings
点击Personal access tokens -> Tokens (classic)
点击Generate new token
输入令牌描述，选择过期时间
勾选repo权限
点击Generate token
复制并保存生成的令牌（仅显示一次）
注意事项
个人访问令牌(PAT)需要妥善保管，不要分享给他人
推送前先检查是否有敏感信息被误添加
大型文件应该考虑使用Git LFS或其他解决方案
对于团队项目，建议使用分支开发模式，不要直接在master分支上工作
定期备份本地代码库
常用Git命令
# 克隆远程仓库
git clone https://github.com/用户名/仓库名.git

# 拉取最新变更
git pull

# 查看提交历史
git log

# 创建并切换到新分支
git checkout -b 分支名

# 切换分支
git checkout 分支名

# 合并分支
git merge 分支名

# 查看分支
git branch
希望本教程对你有帮助！下次手动推送代码时，按照这些步骤操作即可。

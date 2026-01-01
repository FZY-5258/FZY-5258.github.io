# Git Bash推送VS项目到GitHub的操作流程
## 一、前期准备
1. 确保已安装Git for Windows，并在GitHub上新建空白仓库（不勾选 README.md / .gitignore ）
2. 打开VS 2022项目的根文件夹，在空白处右键选择Git Bash Here，打开Git Bash终端
## 二、Git Bash核心操作步骤
1. 初始化本地仓库
*bash*
*git init  # 将当前文件夹初始化为Git仓库*
2. 添加文件到暂存区
*bash*
*git add .  # "."表示添加所有文件，也可指定文件如"git add main.c"*
3. 提交暂存区文件到本地仓库
*bash*
*git commit -m "初始化VS 2022项目，包含C语言矩形面积计算代码"  # 引号内为提交说明，需清晰*
4. 关联GitHub远程仓库
*bash*
*git remote add origin https://github.com/你的GitHub用户名/仓库名.git  # 替换为自己的仓库地址*
5. 推送本地代码到GitHub
*bash*
*git push -u origin main  # "main"为分支名，若默认是master则替换为master*
## 后续常规操作
- 拉取远程仓库更新： git pull origin main 
- 查看仓库状态： git status 
- 查看提交记录： git log 




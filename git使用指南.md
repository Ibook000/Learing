<h1 id="M19QY">怎么使用git</h1>
<h2 id="MJ4SF">git 的安装</h2>
<h4 id="zzkFq">[git下载地址](https://git-scm.com/downloads) </h4>
<h2 id="YEgYL">基本的git 流程</h2>
![画板](https://cdn.nlark.com/yuque/0/2024/jpeg/48755742/1731473320472-6174e76e-645c-4787-8947-a508a5b6e916.jpeg)

本地 有3个区 **工作区 暂存区 本地仓库** 

+ 工作区：本地能看得见的目录 **可以理解成 工厂** - 暂存区：一个临时存储区域，它包含了即将被提交到版本库中的文件快照，在提交之前，你可以选择性地将工作区中的修改添加到暂存区**可以理解成从工厂到仓库的运输车** - 本地仓库：包含了项目的所有版本历史记录。每次提交都会创建一个新的快照，这些快照是不可变的，确保了项目的完整历史记录**可以理解成仓库**



远程有  **远程仓库**通过命令add将本地文件添加到暂存区：`git add`   
通过命令commit将修改提交到本地仓库：	`git commit`  
通过命令push将本地仓库代码提交到远程仓库：`git push`  
通过命令pull拉取远程仓库的代码到本地工作区：`git pull`

<h2 id="y5fGn">git 初始化</h2>
<h3 id="VrvSC">进行 config配置</h3>
```plain
git config --list 显示当前配置
git config --globa user.name 进行用户名配置
git config --globa user.email 进行用户邮箱配置
```

<h3 id="EfBsy">创建本地仓库</h3>
有2种方法初始化仓库

<h4 id="XCDGt">本地初始化`git init`</h4>
目录下就会生成一个.git的**隐藏目录**

**从远端克隆仓库**：`git clone`



<h2 id="QO9JV">文件状态</h2>
![画板](https://cdn.nlark.com/yuque/0/2024/jpeg/48755742/1731472957804-1f904618-593d-45c2-9a9b-95dbf2731b24.jpeg)

未跟踪：新创建未被git管理的文件  
未修改：已经被git管理的文件  
已修改：已经修改但是未被添加到暂存区的文件  
已暂存：修改后并添加的文件  
**[未跟踪]>**`git add`**>[未修改]>**_**修改文件**_**>[已修改]> **`git add`** >[已暂存]**  
**[未跟踪]>**`git add`**>[已暂存]**

<h2 id="J1PaV">添加和提交文件</h2>
<h3 id="p7CK9">使用git add 添加文件到暂存区(告诉git我要把文件添加到仓库)</h3>
+ 批量添加 `git add <file1.txt> <file2.txt> <file3.txt>`
+ 添加目录下所有文件 `git add .`
+ 添加目录下所有txt `git *.txt`

<h3 id="a5AnJ">使用git commit 提交到仓库(告诉git把文件提交到仓库)</h3>
+ 可以修改好之后一起提交
+ 只会提交暂存区的文件不会提交工作区的文件
+ 提交之后git会告诉你我呢见的改动和改动的内容

<h3 id="gZLJE">可以使用git status 查看文件的变化</h3>
**git命令必须再git仓库目录内执行 不然会报错**

<h2 id="egf0T">版本回退 git reset</h2>
回退到某个版本 **会保存工作区和暂存区的内容**：`git reset --soft `  
回退到某个版本 **会丢弃工作区和暂存区的内容**：`git reset --hard`  
回退到某个版本 **会保留工作区和丢弃暂存区的内容**：`git reset --mixed`

<h2 id="PIzPX">查看差异 git diff</h2>
+ 默认查看**工作区**和**暂存区**的差异：`git diff`
+ 比较**工作区**和**本地仓库**的差异：`git diff HEAD`
+ 比较**暂存区**和**本地仓库**的差异：`git diff --cache`
+ 比较**2个提交**的差异：  `git diff <commitID1> <commitID2>`  
  `git diff <commitID1> HEAD HEAD是最新的提交`  
  `git diff HEAD~ HEAD ~是上一个提交和最新的差异`  
  `git diff HEAD~2 HEAD 上2个提交和最新的差异`  
  `git diff HEAD~3 HEAD 上3个提交和最新的差异`

<h2 id="gEGFT">删除文件 git rm</h2>
**从工作区和暂存区中删除：**`git rm <file.txt>`

> 记得提交不然本地仓库中还是存在的
>

<h2 id="EczEA">忽略文件 .gitignore</h2>
在我们本地仓库的目录下有一个.gitignore文件  
忽略的文件使用 git add 不会添加到暂存区  
匹配规则是从上到下匹配的  
可以使用Blob模式匹配

```plain
build/ 忽略任何目录下的build文件夹
doc/*.txt 忽略doc/目录下的所有txt
!main.py 忽略除了main.py的其他文件
*.txt 忽略所有txt文件
```

[.gitignore的使用文档](https://git-scm.com/docs/gitignore)



<h2 id="D7NES">远程仓库</h2>
 可以连接远程仓库  
 有2种方式  
 http 和 ssh  
 **但是github已经不支持http了我们需要使用ssh连接远程仓库**

```plain
  ssh-keygen -t rsa -b 4096 -C "your_email@example.com" 申请密钥
```

会生成一个公钥一个私钥  
复制公钥  
到github上配置ssh密钥

```plain
ssh -T git@github.com 测试ssh链接有没有正常
```

**你可以添加远程仓库**

**添加远程仓库：**`git remote add <origin> <url> `  
**可以查看远程仓库的别名和地址：**`git remote -v` 

<h2 id="UD0Dh">推送新的内容 git push</h2>
**把分支推送到远程仓库：** `git push <remote> <branch> `  
**关联本地仓库的分支和远程仓库的分支：** `git push -u <remote> <temote_branch>:<loca_branch>`

<h2 id="D6yud">拉取最新内容</h2>
**差别是 git pull 会拉取下来和本地仓库合并然而git ferch只会拉取**

**拉取最新内容到本地仓库：**`git pull <remote> <temote_branch>:<loca_branch>`

<h2 id="TUwSk">分支操作</h2>
```plain
git branch 查看分支
git branch <branch> 可以创建一个新分支
git checkout <branch> 切换分支
git switch <branch> 切换分支
git merge <>branch> 合并分支 合并会进行一次提交
git merge --abort 如果发生冲突可以终止合并
git branch -d <branch> 删除分支(合并之后才能使用)
git branch -D <branch> 删除分支
```

如果2个分支修改发生冲突  
我们需要手动解决

<h2 id="zia0f">githubflow</h2>
![画板](https://cdn.nlark.com/yuque/0/2024/jpeg/48755742/1731473617847-cefa9816-37c2-4c69-a29c-61623afb3e4c.jpeg)

对于小型企业和开源团队使用githubflow是比较好的选择  
一般都是基于一个**main**分支进行开发

1. 当其他成员要开发功能时从**main分支创建一个新的分支进行开发**
2. 需要注意新分支的命名规范以便其他成员理解
3. 修改完成后进行push注意需要有描述性的信息帮助理解
4. 分支上传后github上可以发起**PR**(pull request)进行讨论评审代码
5. 然后管理员进行合并代码旧分支旧可以删除了

<h3 id="Os5ZS">命名规范</h3>
1. **功能分支**：
    - **命名格式**：`feature/<description>`
    - **示例**：`feature/add-user-login`、`feature/improve-dashboard-ui`
    - **说明**：用于开发新功能或增强现有功能的分支。
2. **修复分支**：
    - **命名格式**：`fix/<description>`
    - **示例**：`fix/login-bug`、`fix/broken-link`
    - **说明**：用于修复bug或问题的分支。
3. **热修复分支**：
    - **命名格式**：`hotfix/<description>`
    - **示例**：`hotfix/critical-login-issue`
    - **说明**：用于紧急修复生产环境中的问题。
4. **发布分支**：
    - **命名格式**：`release/<version>`
    - **示例**：`release/1.0.0`
    - **说明**：用于准备新版本的发布，可能包括最后的测试和文档更新。
5. **版本分支**：
    - **命名格式**：`<version>`
    - **示例**：`1.0.0`
    - **说明**：用于标记特定版本的分支，通常从`master`分支创建。
6. **文档分支**：
    - **命名格式**：`docs/<description>`
    - **示例**：`docs/update-user-guide`
    - **说明**：用于更新文档的分支。
7. **实验分支**：
    - **命名格式**：`experiment/<description>`
    - **示例**：`experiment/new-architecture`
    - **说明**：用于实验性或探索性工作的分支。
8. **重构分支**：
    - **命名格式**：`refactor/<description>`
    - **示例**：`refactor/code-cleanup`
    - **说明**：用于代码重构的分支，不增加新功能，不修复bug，只改进代码结构。
9. **依赖更新分支**：
    - **命名格式**：`deps/<description>`
    - **示例**：`deps/update-npm-packages`
    - **说明**：用于更新项目依赖的分支。


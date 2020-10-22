# Git Flow开发规范

## 一、Git Flow成熟方案

![成熟方案](https://img-blog.csdn.net/20161227161342176?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3M5NTg5MDM5ODA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

 环境及对应分支：

- 本地开发环境：本地仓库分支工作环境
- 线上测试环境：远程develop分支
- 线上生产环境：远程master分支
- 

Git Flow流程图（代码提交流程）：

![git flow](https://img-blog.csdn.net/20161227161427129?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3M5NTg5MDM5ODA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)



**分支职责**

- master: 最为稳定、功能最为完整、随时可以发布的代码
- develop: 永远是功能最新最全的分支
- hotfix：修复线上代码bug
- feature: 某个功能点正在开发

> 确切的说 master、develop 分支大部分情况下都会保持一致，只有在上线前的测试阶段 develop 比 master 的代码要多，一旦测试没问题，准备发布了，这时候会将 develop 合并到 master 上.
>
> 但是我们发布之后又会进行下一版本的功能开发，开发中间可能又会遇到需要紧急修复 bug ，一个功能开发完成之后突然需求变动了等情况，所以 Git Flow 除了以上 master 和 develop 两个主要分支以外，还提出了以下三个辅助分支：

- feature：开发新功能的分支，基于develop， 完成后merge回develop
- hotfix: 修复master上的问题，等不及release版本就必须马上上线，基于master，完成后merge 回master和develop



## 流程

### 下载项目

首先安装 SSH keys : [详细教程](https://code.aliyun.com/help/ssh/README)

项目管理员会首选在远程仓库创建仓库，并建立develop分支.

作为开发人员，在本地：

```javascript
git clone git@code.aliyun.com:your_org/your_project.git
git branch -a -v
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

### 建立 develop 分支

```javascript
git checkout -b develop master
## add & commit .....
git push –set-upstream origin master
git branch -a -v
```



## 开发流程

### 情况一 （分支开发）

以开发功能分支 feature/search-recommend 为例，工程师需要做以下步骤：

1. 建立 develop 的分支 feature/search-recommend
2. 在该分支上进行开发，完成后进行本地提交
3. 切换到 develop 分支，pull拉取远程仓库最新版本
4. 此时本地 develop 分支是最新版本，然后 merge 分支 feature/search-recommend
5. 如果此时有冲突，清除后commit
6. 把本地合并后的分支 develop push 到远程 develop
7. 在 develop 分支环境下进行测试
8. 一切ok，删除该功能分支
9. 切到 master 分支，pull 然后 merge develop，收工

### 遵循原则&事项

1. 每次 merge 前先 pull 远程分支在进行合并
2. 每完成一个功能就提交一次，不要累计代码

```bash
git checkout -b feature/search-recommend develop ##创建并切换到分支
git add somefile
git commit -m 'msg'
git checkout develop
git pull
git merge feature/search-recommend
git push
git checkout master
git merge devlop
git push
```

### 情况二 （紧急修复bug）

工程师们开开心心的在自己分支上进行开发，此时线上突然出现一bug，需要立即修复，那么：

1. 在 master 分支上拉一个 hotfix 分支 hotfix/0.0.1
2. 修复后 merge 回 master 分支
3. 再 merge 回 develop 分支
4. 删除该分支
5. 应始终保证 master 和 develop 上都修复了该bug



## 命名规范

### 分支命名

除了主要分支的名字是固定的之外，派生分支是需要自己命名的，采用如下形式：

- **feature :** 按照功能点（而不是需求）命名 **feature/** ；如 *feature/weixin_recharge
- **hotfix :** 通过平台生成的问题编号来命名；如 *hotfix/#1*
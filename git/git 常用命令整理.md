## git 常用命令 



### 远程仓库相关

```java
 //将本地仓库和远程仓库做关联
git remote add origin url

//将远程仓库clone到本地
git clone url

//获取本地仓库关联的url
git remote get-url origin 

//设置本地仓库关联远程仓库的url
git remote set-url origin url
```
### git 常用命令

```java
//初始化一个git仓库
git init

//从远程分支下载代码
git pull origin 远程分支

//查看工作区的修改
git status

//将工作区的修改放到暂存区 (.指的是将工作区的全部文件放到暂存区，如果要指定文件，可以将. 替换为指定的文件名)
git add .

//将暂存区修改提交到代码仓库
git commit -m "msg" 

//将本地代码推送到远程仓库
git push origin 远程分支名称

```

### git 分支管理

  ```java
//查看本地所有的分支 (当前分支会用“*”标记)
git branch

//查看本地和远端所有的分支名称 (远程分支会用特殊颜色标记，且前边会加 remote/)
git  branch -a  

//删除分支
git branch -d 

//删除远程分支
git push --origin -delete branch

//本地新建分支
git branch  "分支名称"

//分支切换
git checkout "分支名称"

//创建并切换分支
git checkout -b "分支名称"
  ```

### git 提交日志

```java
//查看已提交的所有版本信息，不包括reset commit
git  log

//查看所有的版本信息，包含了reset commit
git  reflog

//使用可视化界面查看提交信息
gitk

```

![image-20201210103950642](assets/image-20201210103950642.png)

##### git log 和 reflog 的区别

​            比如 使用 git reset --hard HEAD~1，退回到上一个版本，用git log则是看不出来被删除的commitid，用git reflog则可以看到被删除的commitid，我们就可以使用被删除的commitid 恢复到被删除的那个版本。



### git revert

#### 使用场景

​        假设主分支为master分支，先分别将test1 分支 和test2分支代码合并到master分支，因为某些原因test2分支的代码不能够上线，需要在主分支中删除test2分支的代码，可以使用git revert 命令 来重做test2分支。

##### 使用方法：

     //切换到dev分支
    git checkout dev
    
    //合并test1分支代码到master
    git merge test1
    
    //合并test2分支代码到master
    git merge test2
    
    //使用git log 查看commitid
    git log
    
    //撤销通过test2分支合并进来的代码
    git revert test2commitid
    
​         git revert是用一次新的commit来回滚之前的commit。 比如主分支为master分支，有两个开发分支依次为test1,test2。依次把test1,test2开发分支合并到master分支，

 此时git提交记录为:![image-20201206151742735](assets/image-20201206151742735.png)

​     后来 发现从test2 分支合并过来的代码有问题，需要把test2分支合并的代码删除掉。可通过git revert 回滚test2分支的代码

  执行完  git revert 6bd9ddbe56  后git的提交记录变为:

![image-20201206151906152](assets/image-20201206151906152.png)

  对应的工作区从test2合并到的代码也没有了。

  从提交记录可以看到  revert 命令是用一个新的commit 覆盖了原有test2的代码。

### git 版本回退（reset）

##### 工作区修改，未执行add 操作，需要丢弃当前工作区修改

**git checkout .**

![image-20201206152622822](assets/image-20201206152622822.png)



##### 2. 执行了git add 操作后，需要丢弃暂存区的修改

**git reset head**![image-20201206152956857](assets/image-20201206152956857.png)



##### 3. 执行了git commit 后，需要丢弃修改

**git reset --hard commitid**

![image-20201206153235435](assets/image-20201206153235435.png)



### git rebase

 ##### 使用场景：

​         主分支为master，从master切出test1分支做开发工作，期间test1分支commit了多次，可以通过rebase合并多次commit 为一次，也可以通过rebase命令，将test1分支代码合并到master。

##### 使用方法:

```java
//切换到主分支
git checkout master
//拉取主分支最新代码
git pull
//切换到开发分支
git checkout test1;
//多次commit
git add/commit
git add/commit
//合并多次commit
git rebase -i HEAD~2  //合并提交 --- 2表示合并两个
git rebase master---->解决冲突--->git rebase --continue
git checkout master
git merge dev
git push
```

​     git rebase 和git merge 都可以用来合并一个分支到另外一个分支，不同点是，通过rebase 合并后的分支比较干净，是一条直线。通过merge 合并的分支会有很多支线分支

##### git rebase 合并分支图：

 ![image-20201206155120104](assets/image-20201206155120104.png)  

#####  通过git merge 合并的分支图 比较乱：

![image-20201206155202283](assets/image-20201206155202283.png)      

### git stash

git stash 作用的将工作区的修改暂存起来，不add 也不commit。

##### 使用场景：

​        从master 分支 切出一个分支 test1 ，并在test1上开发任务。 此时需要在master分支做一些改动，比如bugfix。 但是test1分支的功能还没开发完成，如果commit的话，相当于是commit了一个非完整功能。可以使用git stash，将test1分支的代码暂存。然后checkout 到master,在master 分支修改。

##### 使用方法：

```java
//在test1分支开发
git checkout test1

//暂存更改的内容
git stash save "msg"

//切换到master 
git checkout master
  
//在master修改
git add commit push;

//切换到test1分支
git checkout test1
  
//将暂存区的内容恢复到工作区
git stash pop;
```



##### 常用命令

```java
 //将工作区的修改暂存
git stash save "save message"  :

//查看当前所有的暂存
git stash list 

// 将暂存的内容恢复到工作去，并删除对应的stash，默认弹出第一个git stash pop stash@{$num}
git stash pop 

//丢弃stash@{$num}存储，从列表中删除这个存储
git stash drop stash@{$num} ：丢弃stash@{$num}存储，从列表中删除这个存储

//清空暂存区
git stash clear 
```



 

### 日常工作流程

假定 主分支 master 开发分支 test

 ```java
//将远程仓库代码clone到本地
git clone remoteurl

//创建功能开发分支
git checkout -b dev

//提交分支代码
git add .
git commit -m "msg"

//切换到master分支
git checkout master
//拉取远程分支代码
git pull origin master

//切换到test分支
git checkout dev;

//将master最新的改动合并到test，有冲突解决冲突
git merge master

//切换到master分支
git checkout master

//合并test分支代码
git merge test

//推送到远程
git push origin master
 ```




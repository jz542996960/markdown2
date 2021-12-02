### git 拉取指定文件目录

> 在实际开发过程中，如果存在一个git仓库里存放多个项目情况，如果全量拉取，则会把所有项目都拉取到本地，本地如果有修改，也会看到所有项目的修改，可以配置git拉取指定的项目



```java
//初始化git仓库
git init；
//设置允许克隆子目录
git config core.sparsecheckout true;
//添加远程仓库
git  remote add origin url.git
//设置指定的目录
echo '目录/' >> .git/info/sparse-checkout
//开始拉取（只会拉取设置的目录下的文件）
git pull origin master 
```




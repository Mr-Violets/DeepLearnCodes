#  24.07.18

新建该仓库为了保存我自己和学习别人的有关深度学习的程序

我发现我在CodesManage文件夹中初始化git仓库以后，尝试把github仓库中的DeepLearnCodes仓库与CodesManage进行关联，但结果是将DeepLearnCodes仓库拉到了CodesManage仓库中

也就是说，CodesManage文件夹作为本地仓库可以管理多个远程仓库

<img src="C:\Users\CLee2\AppData\Roaming\Typora\typora-user-images\image-20240718012559518.png" alt="image-20240718012559518" style="zoom:80%;" />

解决问题的过程

参考：[为什么Git分支开始从“master”变为“main”了？ (carm.cc)](https://pages.carm.cc/doc/branch-main.html)

参考：[关于Github默认分支main和master以及如何在git init时指定默认分支_git init main-CSDN博客](https://blog.csdn.net/mo_sss/article/details/137927136)

初始化本地仓库，本地仓库的默认仓库变为master

在github的远程仓库中，默认分支又为main

可以修改本地仓库名称master->main

```python
git remote add origin git@github.com:Mr-xxxx/xxxxx.git # 建立本地仓库与远程仓库联系
git remote -v # 查看当前我们仓库所对应的远程仓库的别名和地址
git branch -M main # 指定分支的名称为main，默认名称为main则可以省略
```

直接进行推送存在以下问题

<img src="C:\Users\CLee2\AppData\Roaming\Typora\typora-user-images\image-20240718014655521.png" alt="image-20240718014655521" style="zoom:80%;" />

直接推送不成功，使用git remote -v查看当前我们仓库所对应的远程仓库的别名和地址

<img src="C:\Users\CLee2\AppData\Roaming\Typora\typora-user-images\image-20240718015513050.png" alt="image-20240718015513050" style="zoom:80%;" />

发现存在错误，这是怎么回事？通过ChatGPT可以知道这是由于**本地分支和远程分支之间存在冲突**，因为**远程仓库已经包含了本地没有的更改**。在推送之前，你需要**先将远程仓库的更改拉取到本地**。

```python
git pull origin main --rebase
```

将会把远程 `main` 分支的更改拉取到本地，并且使用 `--rebase` 选项可以**让本地更改应用在最新的远程更改之后**。

<img src="C:\Users\CLee2\AppData\Roaming\Typora\typora-user-images\image-20240718015843305.png" alt="image-20240718015843305" style="zoom:80%;" />

再次推送，就可以将本地仓库与远程仓库分支一体化

```python
git push -u origin main
```

正常情况下，输入git remote -v都会存在以下输出，但无法使用push或pull命令时，这是远程仓库与本地仓库存在冲突

<img src="C:\Users\CLee2\AppData\Roaming\Typora\typora-user-images\image-20240718020256786.png" alt="image-20240718020256786" style="zoom:80%;" />

##  解决远程与本地仓库冲突指令

```python
git pull origin main --rebase
```








## Git 是什么？

阅读：https://liaoxuefeng.com/books/git/what-is-git/index.html

## 为什么要用Git？

主要功能就2个：版本管理、多人协作。

一版来说，一个大型项目的开发肯定需要多个版本的迭代（想象一下你写论文要改好多版），有时候还需要回滚，那么之前的版本怎么保存呢？每次开一个新版本都把整个代码库复制一遍肯定不优雅，而且你也不知道这两个版本之间的区别是什么。

用Git就可以实现比较好的版本管理，并且可以直观地对比两个版本间的不同之处（diff功能）

而多人协作也是如此，比如说我要在这个程序上新增功能A，同学甲要在程序上新增功能B，那我们都做完了，要怎么合并这个程序使其同时具有A和B呢？这就可以用Git的来融合了！（Branch-分支功能，和Merge-融合分支功能）。

而且我们通常需要在线协作，代码的传输是通过在线代码库来做，也就是Github。所以同学们尽快注册一个自己的Github账号。

## 详细学习

### 本地Git教程

阅读：https://liaoxuefeng.com/books/git/create-repo/index.html 3～8章

### 在线代码库：Github教程

阅读：https://docs.github.com/zh/get-started/start-your-journey/hello-world

学会如何推送代码和分支到远程仓库，以及拉取远程仓库的代码。

### Git工具

有一些工具可以用于辅助Git管理，例如Fork：https://git-fork.com/
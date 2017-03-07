
## git 工作命令

### diff

+ git diff 显示 目前文件 与上次提交的区别 (git add 之前的文件与已提交文件的差别)
>merge 之后 git diff 即显示存在冲突的地方

+ git diff --staged 显示 暂存区与上次提交的区别 （git add 之后）
+ git diff HEAD 显示 当前工作树与上次提交的区别 （add 之前之后文件的和，HEAD是最近一次提交的别名）
+ git diff --color-words 或者 --word-diff  把一行内的改动显示出来
+ git diff --stat 简要显示区别 （只显示被改动的文件名）
+ git diff 分支名 分支名 显示2个分支之间的区别

> 提示
  + 各个参数可以组合使用 比如 git diff 分支名 分支名  --stat ，快速判断两个分支之间的不同的文件。
  + 分清楚暂存区和commit的区别

### log
+ git log 显示提交历史
+ git log --oneline 把每次提交压缩成一行显示
+ git log --stat   显示每次提交的改动了那些文件 （用于快速查看提交改动了那些文件，而不关心具体如何改动）
+ git log --patch  显示每次提交之间的改动（也就是每次提交和上次提交相比的改动）
+ git log graph --all --decorate --oneline  表示提交结构的样子

### reset
+ git reset --soft或者--hard 摘要（git log 查看每次commit 后面的hash码，不必全复制，代表区别即可）
>把当前分支重置为摘要所代表的commit的状态
> 自动merge失败后，可以add ,commit ,git log 查到想回到哪个分支 ，重置。
> soft会留下目标commit之后的所有commit，hard会把目标之后的commit删除。

+ git reset --hard HEAD       回到合并前的状态，HEAD是当前分支的头的简写。
+ git reset --hard ORIG_HEAD       撤销已经提交的合并后的代码。(merge 之后解决冲突又add，commit 了)
>但是命令比较危险，如果把已经被别的分支合并的分支删掉，以后和它合并时会出错。

+ git reset --hard origin/master 把当前分支放弃，强行和远程master同步

### checkout
+ git checkout 分支名|commit摘要    跳转到某个分支或某次commit
+ git checkout -b 分支名         基于当前分支创建一个新的分支（分支名），并跳转过去


### branch
+ git branch -d 分支名        删除某个分支

### merge
+ git  merge 分支A           把分支A合并到当前分支

### push
+ git push origin 分支名     把当前分支推到origin远端的分支
+ git push -u origin 分支名  若分支不存在，在远端创建一个
+ git push -f origin 分支名   强行把当前分支推到远端，若不存在创建一个，若存在，覆盖掉。

### remote
+ git remote add origin git@github.com:meifans/meifans-patterns.git（例子） 添加一个远端到本地，用origin表示

## git 身份验证命令

+ 启动agent : eval $(ssh-agent -s)
+ 添加key :   ssh-add 私钥名字（不带.pub）

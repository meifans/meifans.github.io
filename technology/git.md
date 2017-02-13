

### diff
+ git diff 显示 目前文件 与上次提交的区别 (git add 之前的文件与已提交文件的差别)
+ git diff --staged 显示 暂存区与上次提交的区别 （git add 之后）
+ git diff HEAD 显示 当前工作树与上次提交的区别 （add 之前之后文件的和，HEAD是最近一次提交的别名）
+ git diff --color-words 或者 --word-diff  把一行内的改动显示出来
+ git diff --stat 简要显示区别 （只显示被改动的文件名）

### log
+ git log 显示提交历史
+ git log --oneline 把每次提交压缩成一行显示
+ git log --stat   显示每次提交的改动了那些文件
+ git log --patch  显示每次提交之间的改动（也就是每次提交和上次提交相比的改动）
+ git log graph --all --decorate --oneline  表示提交结构的样子

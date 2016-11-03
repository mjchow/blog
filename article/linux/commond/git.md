## git命令
> 1.git checkout -t newBranch targetBranch [从target分支检出到新的分支newBranch中]
> 2.git checkout -b newBranch [从当前分支检出一个新的分支到newBranch]
> 3.git revert commitId       [以一次新的commit来撤销commitId这次的提交]



## win下git客户端配置
> 1. 可查看git分支详细操作信息[用图的形式来展现]，需要在git安装目录下/etc/bash.bashrc文件中增加一个别名 **alias gitlog='git log --all --graph --pretty=format:"%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset" --abbrev-commit --date=relative'**
> 
> 2. grep 查询高亮 /etc/bash.bashrc 新增别名 **alias grep='grep --color=auto'
export GREP_COLOR='4;32'**


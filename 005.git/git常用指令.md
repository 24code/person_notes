# git常用指令
## branch
1. git remote update origin --prune #更新远端分支
2. git checkout -b dltOnboarding remotes/origin/dltOnboarding #检出远端分支
3. git branch --set-upstream-to=origin/master master #设置跟踪远程分支
4. git push --set-upstream origin hotfix1009_lineup #直接设置跟踪分支
## remote
1. git remote set-url origin https://github.com/USERNAME/REPOSITORY.git # 修改url
## push
1. git push --force #强制推送本地分支
## 统计代码行数
git log --since=2020-02-07 --until=2020-03-06 --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }'

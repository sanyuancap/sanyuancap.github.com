# git学习

 - sourcetree

 - svn
 
 1.必须联网
 2.window和二进制支持较好
 3.每个分支都是单独副本

 - git
 1.大多数不需要联网
 2.对mac和linux支持较好，二进制较差
 3.针对文件变化记录版本，分支只是一个指针

 - 区别
 集中式 vs 分布式

 - head
    头指针，指向最后一次提交结果

 - 状态
 未修改、已修改、已暂存、已提交、已推送

## git基本操作

        git init 
        git remote add url
        git remote -v
        git remote show origin
        git branch feature
        git branch -a
        git branch -d feature
        git checkout -b feature

        git status -s
        git checkout .
        git reset --hard
        git reset --hard HEAD^
        git reflog
        git push -f

        git merge test
        git merge --abort
        git merge --continue
        git pull
        git fetch

        git diff filepath
        git diff HEAD filepath

        git tag V2.1 -m 'version 2.1'
        git show V2.1
        git push origin V2.1
        git push origin --tags

        git --help
        
        git rm -r --cached

        git stash // 暂存
        git stash list
        git stash apply 0
        git stash pop

        git cherry-pick // 遴选
        git cherry-pick --continue
        git cherry-pick --abort

        git blame

## git权限控制

        owner master developer reporter guest

## 提交规范

 1.可维护
 2.方便排查与回退
 3.过滤关键字，迅速定位
 4.生成changelog，自动生成版本迭代报告、更新列表等

    [type]([scope]): [subject]

 - type

feat fix docs stype refactore test chore

 - 影响范围

 view model serving config

## git基本存储原理

    cd .git
    cat HEAD
    tree -L 2
    git cat-file -t/-p


    tree 967ebd8985353dfad068b235e04e96dfc937d14b
    parent 50b185ccb3634b3f20c5b4583ff612f2d010c9cb
    parent fc262c0689c5e8d762d3a8e062cbe78ece5de564
    author 邱南南 <qiunannan@baijiahulian.com> 1553583669 +0800
    committer 邱南南 <qiunannan@baijiahulian.com> 1553583669 +0800
    Merge branch 'feature-spring19-qn' into 'dev-spring19'
    【开发】【g1_l13】

文件结构：blob tree commit 
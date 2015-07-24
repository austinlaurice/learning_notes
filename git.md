#Git  
**把branch接回upstream最後的點**

    git checkout -b [newbranch]
    git reset --hard [the commit that I want to return to ]
    git fetch upstream
    git pull --rebase upstream [remote-branch]

在找個東西add、 commit、 push就好囉！！

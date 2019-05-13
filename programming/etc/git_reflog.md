# Git reflog

git reflog는 HEAD가 변경되는 이력을 보여주는 명령어입니다. 레퍼런스 로그(줄여서 reflog)는 로컬 리포짓토리에서 브랜치에 변화가 생긴 내용을 기록하고 있습니다. git log은 현재 브랜치의 히스토리를 보여주면서 단순히 이전 커밋을 순서대로 보여줍니다. 하지만 레퍼런스 로그를 이해하면 소스가 한번 커밋이 되고 나면 절대 데이터를 잃어버릴 일이 없다는 것을 알게 됩니다.

```shell
$ git reflog
22ee309 (HEAD -> master) HEAD@{0}: cherry-pick: review: Add delete function
d3c00c9 HEAD@{1}: cherry-pick: review: Add update function
5dc0734 (origin/master, origin/HEAD) HEAD@{2}: reset: moving to 5dc0734
e16690d HEAD@{3}: commit: review: Add delete function
4e4af76 HEAD@{4}: commit: review: Add update function
5dc0734 (origin/master, origin/HEAD) HEAD@{5}: rebase finished: returning to refs/heads/master
```

로그의 3번재 줄 내용은 git reset --hard를 한 명령어입니다. 눈에 보이는 소스를 보면 5dc0734에서 두번 커밋을 한 내용이 순간 사라진 것을 알 수 있습니다. 하지만 reflog로 보니 삭제된 것으로 보였던 2개의 커밋 해쉬를 알 수 있습니다. 그래서 git cherry-pick 명령어를 사용해서 사라졌던 내용을 다시 살릴 수 있었습니다. 실제로 깃은 한번 커밋된 정보는 완전히 버리지 않고 보관을 하고 있었던 것이죠. git reflog로 확인하면 커밋 해쉬를 확인할 수 있습니다.

Reference: https://tech.10000lab.xyz/git/git-tips-you-need.html

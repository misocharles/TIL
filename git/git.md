# Git을 익히는데 도움되는 글들

- [Git을 이용한 협업 워크플로우 배우기](http://blog.appkr.kr/learn-n-think/comparing-workflows/)
- [Git Flow](http://blog.appkr.kr/work-n-play/git-flow/)

### diff3 사용하기

git에서 병합 충돌(merge conflicts)이 났을 경우 `diff3` 포맷으로 볼 수 있다.

> $ git config --global merge.conflictstyle diff3

### git merge

remote 파일을 기준으로 덮어씌우기

> $ git checkout --theirs path/file

수정한 commit을 기준으로 덮어씌우기

> $ git checkout --ours path/file

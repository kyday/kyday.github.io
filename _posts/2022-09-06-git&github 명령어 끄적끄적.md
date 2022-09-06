---
title: git & github 명령어 끄적끄적
categories: [dev]
comments: true
---

### git 저장소 만들기

```
git init
```

### git 현재 상태 확인

```
git status
```

### git 작업 디렉토리의 변경 내용을 staging 영역에 추가

```
git add .
```

### 버전을 등록하고, 로컬 저장소로 현재 상태를 저장

```
git commit -m "커밋 메세지"
```

### 브랜치를 원격 저장소로 저장

```
git push origin branch
```

### git commit을 했는데 이전 상태로 돌아가고 싶을 때

```
git reset --hard HEAD

```

### 작업중인 변경 사항들을 잠시동안 저장하고 싶을 때 (git stash apply && git stash drop)

```
git stash
```

### 작업중이었던 파일을 다시 꺼내오고 stash list에서 지우는 명령어

```
git stash pop
```

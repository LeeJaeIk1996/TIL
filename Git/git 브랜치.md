# Git 브랜치
<br>

## 1. branch란?


### - branch?

---

`branch` : 분기, 가지 
<br>

```bash
버전 관리 시스템에서는 branch를 나무가 가지에서 새 줄기를 뻗듯이 
여러 갈래로 퍼지는 데이터 흐름을 가리키는 말로 사용한다
```

### - branch 기능

---

 우선, 깃으로 버전 관리를 시작하면 기본적으로 `master`라는 브랜치가 만들어진다. <br>
사용자가 커밋할 때마다 `master` 브랜치는 최신 커밋을 카리킨다.
<br>
1. `분기(branch)` : master 브랜치에서 뻗어 나오는 새 브랜치를 만드는 것을 '분기(branch)'한다고 한다.
<br>

2. `병합(merge)` : 분기(branch)했던 브랜치를 master 브랜치에 합치는 것을 '병합(merge)'한다고 한다.

<br>

## 2. branch 만들기

### - git branch

---

`git branch` : 깃에서 브랜치를 만들거나 확인하는 방법

![branchmake](https://user-images.githubusercontent.com/84573261/125770701-42964ed0-e73d-481b-97d5-221be3b19043.PNG)

```bash
$ git branch
* master
```

저장소를 만들 때 기본적으로 master 브랜치가 만들어지며, `git branch`를 통해 확인할 수 있다.<br>
여기서 * (별 표시)는 현재 master 브랜치에서 작업하고 있다는 뜻이다.

```bash
sec@DESKTOP-K48FQ26 MINGW64 ~/manual (master)
$ git branch apple

sec@DESKTOP-K48FQ26 MINGW64 ~/manual (master)
$ git branch
  apple
* master
```

`git branch`를 통해 확인할 수 있을 뿐만 아니라, 위와 같이 브랜치를 추가할 수 있다.

```bash
commit f97f2ae68ce81fbd57effa2a55cfbd892e440edd (HEAD -> master, apple)
```

apple 브랜치가 추가되면서 `(HEAD -> master, apple)`로 바뀌었음을 확인할 수 있으며,<br>
`HEAD -> master`이므로 현재 작업 중인 브랜치는 master 브랜치라는 것을 알 수 있다.

### - git checkout

---

`git checkout` : 현재 브랜치에서 다른 브랜치로 이동시켜주는 명령어

![checkout](https://user-images.githubusercontent.com/84573261/125772078-fe26fe8f-d538-440d-8b8d-2be81596b92c.PNG)

```bash
$ git checkout apple
Switched to branch 'apple'
```

이를 통해, 현재 브랜치인 master에서 apple로 브랜치가 이동되었음을 확인할 수 있다.

```bash
$ git log --oneline
f97f2ae (HEAD -> apple, ms, google) work 3
c6a8518 work 2
78a23d9 work 1
```

이를 통해, apple 브랜치가 master 브랜치에서 분기된 이후에 master 브랜치에 추가된 커밋은<br>
apple 브랜치에 영향을 미치지 않았다는 것을 알 수 있다.

<br>

## 3. branch 정보 확인하기

<br>

![info](https://user-images.githubusercontent.com/84573261/125778955-18c2358c-797d-41c5-b097-8956e88c0af3.PNG)

### - git log --oneline

---

`git log --oneline` : oneline 옵션은 한 줄에 한 commit씩 나타내준다.

```bash
3db6d48 (HEAD -> apple) apple content 4
f97f2ae (ms, google) work 3
c6a8518 work 2
78a23d9 work 1
```

현재 브랜치가 apple로 설정되어 있는 것을 볼 수 있다.

### - git log --oneline --branches

---

`git log --oneline --branches' : 각 브랜치의 commit을 함께 볼 수 있다.

```bash
sec@DESKTOP-K48FQ26 MINGW64 ~/manual (apple)
$ git log --oneline --branches
3db6d48 (HEAD -> apple) apple content 4
686f73c (master) master content 4
f97f2ae (ms, google) work 3
c6a8518 work 2
78a23d9 work 1
```

### - git log --oneline --branches --graph

---

`git log --oneline --branches --graph` : 브랜치와 commit의 관계를 좀 더 보기 쉽게 그래프 형태로 표시

```bash
sec@DESKTOP-K48FQ26 MINGW64 ~/manual (apple)
$ git log --oneline --branches --graph
* 3db6d48 (HEAD -> apple) apple content 4
| * 686f73c (master) master content 4
|/
* f97f2ae (ms, google) work 3
* c6a8518 work 2
* 78a23d9 work 1
```

이를 통해 master 브랜치와 apple 브랜치는 'work 3' commit까지는 같고 <br>
그 이후부터 브랜치마다 다른 commit을 만들었다는 사실을 알 수 있다.

### - git log master..apple

---

`git log master..apple` : 브랜치 이름 사이에 마침표 두개를 넣는 명령으로 차이점을 확인할 수 있다.

```bash
commit 3db6d486d4fbf2d21fada4e0520770acb1a25023 (HEAD -> apple)
Author: Jaeik <ly7kdd@naver.com>
Date:   Thu Jul 15 20:00:44 2021 +0900

    apple content 4
```

이를 통해 apple브랜치에만 있는 commit, 즉 'apple content 4' commit을 볼 수 있다.

<br>

## 4. branch 병합

### - 서로 다른 파일 병합하기

---



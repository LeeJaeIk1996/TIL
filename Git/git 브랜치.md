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

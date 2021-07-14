# Git 버전관리
<br>

## 1. 깃 저장소 만들기

### - Git init

---
`git init` : 깃 초기화
<br>
<br>
![init2](https://user-images.githubusercontent.com/84573261/125633918-661f3306-cd93-4607-b6a4-59b759a31066.PNG)

```bash
Initialized empty Git repository in C:/Users/sec/hello-git2/.git/
```
이러한 메시지가 나타난다면 이제 해당 디렉터리에서 깃을 사용할 수 있다.
<br>

```bash
drwxr-xr-x 1 sec 197121 0 Jul 14 22:48 .git/
```


`ls-al`을 입력하면 위와 같이 `.git`이라는 디렉터리가 새로 생긴 것을 확인할 수 있는데,<br>
이 디렉터리가 깃을 사용하면서 버전이 저장될 저장소(repository)이다.

<br>

## 2. 버전 만들기

```bash
1. working tree에서 문서를 수정하고, 
2. 수정한 파일을 stage에 저장한 후,
3. 스테이지에 있던 파일을 repository로 커밋하는 것이 git을 만드는 순서이다.
```

### - working tree

---

`working tree`: 파일 수정, 저장 등의 작업을 하는 디렉터리로, `working directory`라고도 한다.

![vim](https://user-images.githubusercontent.com/84573261/125638561-85465b87-cb32-4777-ba6f-c545eb5d4007.PNG)

위와 같이 디렉터리를 생성하기 위해선 `vim` 명령어와 디렉터리명을 써준다.<br>
그리고 파일에 원하는 문서를 작성한다.<br>
<br>
그 뒤 `git status`명령어를 통해 깃 상태를 확인할 수 있는데, 

```bash
Untracked files:
```

이러한 문장을 볼 수 있다. 이는 아직 한 번도 버전 관리하지 않은 파일을 Untracked files라고 부른다.

### - stage

---

`stage`: 버전으로 만들 파일이 대기하는 곳이며, `staging area`라고 부르기도 한다.

![add](https://user-images.githubusercontent.com/84573261/125640016-1157a1c0-fcbd-4cb7-9998-0944b5865876.PNG)

위와 같이 파일을 스테이징하기 위해선 `git add` 명령어를 사용한다.<br>
그 뒤 `git status`라는 명령어를 통해 깃 상태를 확인하면 

```bash
Changes to be committed:
```

이라는 문구를 볼 수 있는데, 이는 이전에 Untracked files 문구가 Changes to be committed로 바뀌었음을 알 수 있으며, <br>
정상적으로 스테이징 되었음을 알 수 있다.

### - repository

---

`repository`: 스테이지에서 대기하고 있던 파일들을 버전으로 만들어 저장하는 곳이다.

![commit](https://user-images.githubusercontent.com/84573261/125640678-f16df900-6715-4587-a253-f9ca090eec08.PNG)

위와 같이 깃에서 파일을 커밋하기 위해선 `git commit` 명령어를 사용한다. <br>
그리고 `-m` 옵션을 통해 커밋과 함께 저장할 메시지를 적을 수 있다.
<br>
<br>
마지막으로 `git log` 명령어를 통해 저장소에 저장된 버전을 확인할 수 있으며, 위의 사진을 통해

```bash
commit a54e2fcb083bbeea1ee82a77d3a9293213adc31a (HEAD -> master)
Author: Jaeik <ly7kdd@naver.com>
Date:   Wed Jul 14 23:35:18 2021 +0900

    message1
```

 볼 수 있다. 여기서 커밋을 만든 사람, 만든 시간과 커밋 메시지가 함께 나타난다.

<br>

## 3. 커밋 내용 확인하기

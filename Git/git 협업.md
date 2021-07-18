# Git 협업

<br>

## 1. 여러 컴퓨터에서 원격 저장소 함께 사용

### git clone

---

`git clone` : **원격** 저장소 복제 명령어.

**원격(remote) 저장소**를 함께 사용하기 위해선 해당 원격 저장소를 **지역(local) 저장소**로 가져와야 한다.

![clone](https://user-images.githubusercontent.com/84573261/126061430-1d7d690d-c8ff-479a-ac7c-192caa88c87f.PNG)

위 사진에서 **git_home**디렉터리와 **git_office**디렉터리는 서로 다른 두 **지역 저장소**라 가정한다.

위 사진을 보면 `git clone 원격 저장소 git_home`과 `git clone 원격 저장소 git_office`를 볼 수 있다.

![clone2](https://user-images.githubusercontent.com/84573261/126061487-91977987-02b4-4431-a747-f645d0774273.PNG)

`git log`명령을 통해 디렉터리에 제대로 저장되어있는지 확인할 수 있으며, 위 사진은 **3개의 commit**이 저장되어 있음을 알 수 있다.

<br>

### git push & pull

`git push` : **지역**저장소 -> **원격**저장소

`git pull` : **원격**저장소 -> **지역**저장소

![push](https://user-images.githubusercontent.com/84573261/126064129-3ab3476b-0853-4f79-a521-56be6c430f54.PNG)

![push2](https://user-images.githubusercontent.com/84573261/126064155-25aefe10-6a32-4d68-9e83-bc546cc0d360.PNG)


우선 사진과 같이 git_home디렉터리(**하나의 지역 저장소**)에서 **pullpush.txt**를 만들고 **원격 저장소**로 `git push`한다.

![pull](https://user-images.githubusercontent.com/84573261/126064194-8b8046d8-97b0-46a0-b839-24be1c034f01.PNG)

이를 **원격 저장소**에서 git_office디렉터리(**또 다른 지역 저장소**)로 `git_pull`한다.
<br>
이렇게 **원격 저장소**를 통해 집(git_home)에서 회사(git_office)로 파일을 내려받을 수 있다는 것을 알 수 있다.

<br>

## 2. 원격 브랜치 정보 가져오기


### 원격 master 브랜치

---

**원격 저장소도 지역 저장소의 master 브랜치처럼 기본적으로 master 브랜치가 생성된다**

![master1](https://user-images.githubusercontent.com/84573261/126064364-249d3b12-1175-433c-9956-a27e35d82f6d.PNG)

```hash
commit 10477f6a080345c2965dc499d2a7ada8cc819c75 (HEAD -> master, origin/master, origin/HEAD)
```

여기서 **HEAD -> master**는 이 커밋이 지역 저장소의 최종 커밋이라는 뜻이고, <br>
**origin/master**는 원격 저장소의 최종 커밋이라는 뜻이다.

![master2](https://user-images.githubusercontent.com/84573261/126064478-2583e519-7871-4c83-8cec-13fc538e202e.PNG)

```hash
$ git log --oneline
da8ed6d (HEAD -> master) create f3.txt
10477f6 (origin/master, origin/HEAD) add d
```

**f3.txt**를 새로 만들고 `git commit`한 뒤 커밋 로그를 확인해보면 위와 같은 문장이 나온다.

```hash
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

그리고 `git status`를 통해 위와 같은 문장을 볼 수 있는데, 이를 통해 <br>
**현재 master 브랜치가 origin에 있는 원격 master브랜치의 버전보다 하나 앞서 있는**것을 알 수 있다.<br>
또한 `git push` 명령으로 지역 저장소의 commit을 원격 저장소로 올리라고 알려준다.

![master3](https://user-images.githubusercontent.com/84573261/126064554-cd26f8c1-8e77-41ee-ad26-2474e52dd1e8.PNG)

위 사진과 같이 `git push`한 뒤 다시 `git log`를 하면 master와 origin/master 브랜치가 같은 commit을 가리키게 된다.

### git fetch

---

![fetch](https://user-images.githubusercontent.com/84573261/126064578-681598ea-a7ae-485b-8068-a42df6b294b4.PNG)

`git fetch`: 원격 저장소의 정보를 가져오는 명령어.(fetch: 불러오다, 가져오다)

![fetch2](https://user-images.githubusercontent.com/84573261/126064612-22ce80a9-5ce3-4efd-b0f1-1e0f96ba94b4.PNG)

`git fetch` 명령을 입력하면 무언가를 가져오는 듯한 문장이 나오는데, 막상 `ls -al` 명령을 입력하면 이전의 **f3.txt**가 보이지 않는다.

![fetch3](https://user-images.githubusercontent.com/84573261/126064643-8271c6c1-d648-44f0-8215-720c15ef9094.PNG)

```hash
On branch master
Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)
```

이를 `git status`로 확인해보면 **현재 브랜치가 origin/master에 비해 1개의 커밋이 뒤쳐져 있다**고 나온다.

![fetch4](https://user-images.githubusercontent.com/84573261/126064707-4703c426-eb48-48c6-a147-170e93baba85.PNG)

`git checkout FETCH_HEAD`로 패치해서 가져온 최신 커밋을 살펴볼 수 있다. 그러면 f3.txt를 확인할 수 있으며, <br>
`git log`를 통해 FETCH_HEAD에서 최신 커밋에 origin/master와 origin/HEAD가 표시되어 있는 것을 볼 수 있다.


![fetch5](https://user-images.githubusercontent.com/84573261/126064838-382bea8a-b718-4c47-ac0f-660f24450496.PNG)

이를 이전과 같이 `git pull`을 통해 내려받을 수도 있지만, <br>
`git merge FETCH_HEAD`를 통해 **병합하여 받을 수도 있다.**
<br>

즉, `git pull` 명령은 **git fetch 명령 + git merge FETCH_HEAD 명령**과 같다고 볼 수 있다.




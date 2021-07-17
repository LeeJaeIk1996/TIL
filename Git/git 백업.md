# Git 백업

## 1.원격저장소와 깃허브


### 원격 저장소?

---

`local repository` : 자신의 컴퓨터에서 작업한 뒤 그 컴퓨터 안에 커밋을 저장하는 저장소.

`remote repository` : **local repository**가 아닌 컴퓨터나 서버에 만든 저장소. 대표적으로 **Github**가 remote repository이다.

```bash
remote repository는 local repository와 연결되어 있으면서 '백업'과 '협업'이라는 중요한 역할을 한다.
```

<br>

## 2. 지역 저장소를 원격 저장소에 연결하기

### git remote 

---

![remote](https://user-images.githubusercontent.com/84573261/126039085-f3bf8418-cfc6-4c53-9d72-de9ac7728ef4.PNG)

`git remote add origin 원격저장소 주소` : 원격 저장소(`remote`)에 `origin`을 추가(add)하겠다고 git에게 알려주는 명령어.
여기서 `origin`은 **Github** 저장소 주소를 가리킨다.
<br>

`git remote -v` : 원격 저장소(`remote`)에 제대로 연결되었는지 확인하는 명령어.

<br>

## 3. 원격 저장소에 올리기 및 내려받기

### git push

---

`git push` : 지역 저장소의 소스를 원격 저장소로 올리는(**push**) 명령어.

![push2](https://user-images.githubusercontent.com/84573261/126039172-f1132eaa-f1f8-4819-a5fa-15e14a989c09.PNG)
<br>
위 사진에서 '-u' 옵션은 지역 저장소의 브랜치를 원격 저장소의 master 브랜치에 연결하기 위한 것으로<br>
**처음에 한번만 사용하면 된다.**
<br>
명령어 push 뒤에 나오는 origin master는 지역 저장소의 브랜치를 origin, 즉 원격 저장소의 master<br>
브랜치로 push하라는 명령이다.

![push](https://user-images.githubusercontent.com/84573261/126039234-44d8be22-009b-4281-af78-a8d779442d14.PNG)

제대로 **push** 되었으면 위 사진과 같이 원격 저장소로 올라오게 된다.

### git pull

---

`git pull` : 원격 저장소에서 지역 저장소로 내려받는(**pull**) 명령어.

![pull1](https://user-images.githubusercontent.com/84573261/126039313-d87ae807-d487-41c8-99c3-063a6a75f93b.PNG)

위 사진에서 f1.txt는 전에 push 받았던 파일이다. 이번엔 pull하기 위해 github에서 직접 f2.txt를 만들고<br>
파일에 Create f2.txt라는 문장을 작성했다.<br>
<br>
![pull2](https://user-images.githubusercontent.com/84573261/126039365-9550c237-3436-4c9c-9408-24cd7b8db4ea.PNG)

그 뒤 `git pull origin master` 명령을 입력하여 origin(원격 저장소)의 내용을 master 브랜치로 가져오도록 한다.<br>
그리고 git log를 입력하여 로그를 확인해보면 이전에 github에서 만들었던 Create f2.txt라는 커밋이 나타나는 것을 확인할 수 있다.

<br>

## 4. github에 SSH 원격 접속하기

### SSH 원격 접속?

---

`SSH` : **Secure Shell**의 줄임말로, 보안이 강화된 안전한 방법으로 정보를 교환하는 방식. <br>
**SSH**에서는 기본적으로 `Private Key'와 'Public Key`를 한 쌍으로 묶어 컴퓨터를 인증한다.

### SSH 키 생성하기

---

`ssh-keygen` : ssh 키 생성 명령어.

![SSHmake](https://user-images.githubusercontent.com/84573261/126039515-088385e8-ea0f-4945-bbe6-899bacaffaea.PNG)

```hash
Your identification has been saved in /c/Users/sec/.ssh/id_rsa
Your public key has been saved in /c/Users/sec/.ssh/id_rsa.pub
```
여기서 `id_rsa`파일이 **Private Key**, `id_rsa.pub`파일이 **Public Key**이다.

![sshlook](https://user-images.githubusercontent.com/84573261/126039637-52c1797f-3df9-4efb-8bce-b4da2f7b6123.PNG)

위 사진을 통해 .ssh 디렉터리 안에 private key `id_rsa`파일과 public key `id_rsa.pub`파일이 만들어진 것을 확인할 수 있다.

### github에 Public Key 전송하기

---

```hash
SSH 방식의 원리는 
사용자 컴퓨터에 있는 Public Key를 github server로 전송한 다음,
사용자 컴퓨터에서 github repository에 접속하면 사용자 컴퓨터에 있는 Private Key와 
github server에 있는 Public Key를 비교하는 것이다.
```

![sshpub](https://user-images.githubusercontent.com/84573261/126039830-eeecb55f-d79c-49fd-ba15-ccc523b7aee3.PNG)

위 사진과 같이 우선 **Public Key**에 담긴 내용을 확인한다.

![pub](https://user-images.githubusercontent.com/84573261/126039862-ffc13d1c-4ba5-4bb0-94b4-add2749d3934.PNG)

그 뒤 **Public Key**에 담긴 내용을 복사하여 깃허브 서버에 올린다.<br>
이렇게 SSH 방식을 사용하면 로그인 정보를 입력하지 않고도 즉시 해당 저장소에 접속할 수 있다.

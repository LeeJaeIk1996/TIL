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


### git push & pull

`git push` : **지역**저장소 -> **원격**저장소
`git pull` : **원격**저장소 -> **지역**저장소

# 장고 프로젝트 만들기

(+ 장고 프로젝트를 만들 때 파이참과 cmdr을 사용했습니다.)

## 1. 장고의 작동 구조

![structure](https://user-images.githubusercontent.com/84573261/126514209-5142c17e-edef-459f-a40b-b7e8a8a0997d.jpg)

**MTV**패턴이란: Model로 자료의 형태를 정의하고, View로 어떤 자료를 어떤 동작으로 보여줄지 정의하고, Template으로 웹페이지에서 출력할 모습을 정의하는데, 이러한 작동 구조를 줄여서 **MTV**패턴이라고 한다.

---

## 2. 장고 프로젝트 만들기

### - 깃허브 저장소 만들기

![repo](https://user-images.githubusercontent.com/84573261/126515893-e3f96020-99e8-4fad-b7c7-f5be29dc37fe.PNG)

위의 사진처럼 개인 깃허브 저장소를 만든 뒤, 저장소 URL을 복사하여 내 컴퓨터로 깃허브 저장소를 클론한다.

---

### - 파이참으로 가상 환경 만들기

![venv](https://user-images.githubusercontent.com/84573261/126516462-bef8ccb3-e700-44a6-a575-6c0f898932f6.PNG)

파이참으로 가상 환경을 만들 경우 위의 사진과 같이 새로운 가상환경이 **venv**폴더 안에 생성된다.<br>
장고를 비롯해 웹사이트를 만드는데 필요한 외부 라이브러리는 가상 환경에 설치할 예정.<br>
가상환경을 사용하는 이유는 한 컴퓨터 안에 또 다른 프로젝트를 별도로 진행할 경우 웹 사이트 개발 프로젝트를 위해 설치한 외부 모듈이 파이썬 개발환경 전체에 영향을 준다면 관계가 없는 프로젝트에 의도하지 않은 영향을 끼칠 수도 있기 때문이다.

가상환경을 만든 뒤 터미널에서 가상환경을 실행하기 위해선 현재 프로젝트 위치에서 `venv\Scripts\activate.bat`을 입력한다.<br>

![venv2](https://user-images.githubusercontent.com/84573261/126517399-4c5ad8f2-949f-4484-9b4a-63530757ba71.PNG)

`venv\Scripts\activate.bat`를 입력할 경우 다음 사진과 같이 가상환경으로 접속된다. 만약 가상환경을 빠져나오고 싶다면 `deactivate`를 입력하면 된다.

![venvinstallDjango](https://user-images.githubusercontent.com/84573261/126517715-1ba1bd2a-4ab3-4aea-a975-d591c8ba2573.PNG)

그 뒤 장고를 설치하기 위해선 사진과 같이 `pip install django`를 입력한다.

---

### - 장고로 기초 웹 사이트 만들기

1. 우선 장고 프로젝트를 생성해야 된다. 이를 생성하기 위해선 터미널에 `django-admin startproject do_it_django_prj .`을 입력한다.

![djangoadmin](https://user-images.githubusercontent.com/84573261/126518077-c5d5c532-8aaf-4187-994b-4ecf4f6c0f8d.PNG)

++ `django-admin startproject do_it_django_prj .`에서 .은 '이 폴더에 장고 프로젝트를 만들자'라는 의미이다.

사진처럼 `ls`로 확인해보면 **do_it_django_prj/  manage.py** 가 새로 생성되었다는 것을 확인할 수 있다.

2. 새 장고 프로젝트가 잘 생성되었는지 확인하기 위해 `python manage.py runserver`를 입력한다.

![runserver3](https://user-images.githubusercontent.com/84573261/126519737-75f4dae3-599f-4ffd-99d0-b82cfbf459f9.PNG)

++ 사진에서 빨간색의 오류메시지를 확인할 수 있는데, 메시지에 나오는 **마이그레이션(migration)** 이란 **데이터베이스에 적용시켜야 하는 변화에 대한 기록**을 말한다.

출력값 중에서 **http://127.0.0.1:8000** 가 써있는 것을 확인할 수 있는데, 이 서버 IP주소를 확인해보면 아래와 같은 화면을 볼 수 있다.

![127](https://user-images.githubusercontent.com/84573261/126519213-7ef80d7a-f578-45ca-a77d-ac6f4ae74f4d.PNG)

3. 이전의 사진에서 나온 **migration**을 적용하기 위해 `python manage.py migrations`를 입력해야 하지만 **장고가 알아서 만든 migration이 있으므로** <br>
바로 `python manage.py migrate`명령어를 입력한다.

![migrate2](https://user-images.githubusercontent.com/84573261/126521078-0703aee8-8cff-4037-bc18-b08b39c2b9d6.PNG)

그 뒤 `ls`를 입력하면 사진과 같이 **db.sqlite3**이 새로 생성된 것을 볼 수 있다.<br>
++ db.sqlite3의 특징은 파일 하나로 관리하는 데이터베이스라는 점이다. 이는 파일 하나만 관리하면 된다는 장점이 있지만, 파일 기반의 데이터베이스이기 때문에 읽고 쓰기가 빈번하게 일어나는 대형 프로젝트에서는 불리하다는 단점이 있다.

4. 웹 사이트 관리자 계정을 생성하기 위해 `python manage.py createsuperuser`를 입력한다.

![superuser](https://user-images.githubusercontent.com/84573261/126521679-787dcb09-7300-4603-9846-0f0998106428.PNG)

사진과 같이 username, Eamil, Password를 입력하면 된다.

5. 그 뒤 `python manage.py runserver`로 서버를 실행한다.

![runserver4](https://user-images.githubusercontent.com/84573261/126522026-af3f9715-ec34-4e14-be7c-35722bd13c1b.PNG)

그러면 이전과 달리 **migration** 오류 없이 잘 실행된다.<br>
그 뒤 http://127.0.0.1:8000/admin 으로 접속해보면 **사용자명과 비밀번호 입력** 칸이 나오고, 이전에 설정했던 username과 password를 입력하면

![admin](https://user-images.githubusercontent.com/84573261/126522302-382b97f8-cf8a-4b17-b32d-6eb74511c859.PNG)

장고가 기본으로 만들어 주는 관리자 페이지가 나온다.

6. 마지막으로 오늘 해놓은 것들을 commit한다.

![commit](https://user-images.githubusercontent.com/84573261/126522533-c48bc8bb-58a4-4502-9ad6-e34946ca4cae.PNG)

위의 사진과 같이 `git add.`과 `git commit -m "Django 프로젝트 셍성"`,`git push`를 입력하면 

![commit2](https://user-images.githubusercontent.com/84573261/126522710-0c3440f3-2284-4ee4-9272-89e2f4db2f84.PNG)

깃허브에 오늘 했던 것들이 올라온다.

---

**금일 배운 것들 정리**
1. 가상환경에 들어가기 위해선 `venv/Scripts\activate.bat`을 입력한다. 나가기 위해선 `deactivate`를 입력한다.
2. 장고를 설치하기 위해선 `pip install django`를 입력한다. 설치한 장고의 버전을 확인하기 위해선 `pip list`를 입력한다.
3. 장고 프로젝트를 생성하기 위해선 `django-admin startproject 프로젝트 명 . `을 입력한다. 설치한 프로젝트의 폴더를 열어보면 **urls.py**와 **settings.py**가 있는데, **urls.py**는 사용자가 어떤 URL 형식으로 접근했을 때 어떻게 웹 사이트를 작동시킬지를 정리해놓은 파일이고, **settings.py**는 이 장고 프로젝트의 설정을 담고 있는 파일이다.
4. 서버를 실행하기 위해선 `python manage.py runserver`를 입력한다. 서버를 중단하기 위해선 **Ctrl+C**를 입력한다.
5. `python manage.py migrate`를 입력하면 db.sqlite3이 새로 생성되고, 그 안에 마이그레이션을 반영한 데이터베이스가 생성된다.
6. 관리자 계정을 생성하기 위해선 `python manage.py createsuperuser`를 입력한다.
7. 마지막에 `git add . `과 `git commit`, `git push`로 깃허브에 저장하는거 잊지 말자.


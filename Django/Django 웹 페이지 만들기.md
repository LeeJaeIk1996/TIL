# 웹 페이지 만들기

## URL 설정하기

**1. 표지판 역할을 하는 url.py**

`url.py`: 사용자가 어떤 URL 형식으로 접근했을 때, 어떻게 웹사이트를 작동시킬지 정리해놓은 파일.

필요한 페이지와 URL
- 대문 페이지: 도메인/
- 블로그 페이지: 1. 포스트 목록 페이지(도메인/blog/), 2. 포스트 상세 페이지(도메인/blog/포스트 pk)<br>
++ `pk`: 각 레코드에 대한 고유 값.
- 자기소개 페이지: 도메인/about_me/

![url](https://user-images.githubusercontent.com/84573261/126897087-08d08492-a7ed-47fd-abf1-26b3ab7b0e4f.jpg)

**2. 포스트 목록 페이지 만들기**

![pagenotfound](https://user-images.githubusercontent.com/84573261/126897101-1ee00ce0-fbc5-4ec7-86a5-83f917e5e3b0.PNG)
 
위 사진처럼, **http://127.0.0.1:8000/blog/** 를 입력하면 아직 blog/ URL을 설정하지 않아 오류가 나온다.<br>
이를 **프로젝트 폴더**에 있는 `url.py`에 들어가 아래와 같이 수정해준다.

![blogurl](https://user-images.githubusercontent.com/84573261/126897191-fb134875-fa2d-44e1-b4a6-52ebd309f69e.PNG)

그리고 **blog 앱 폴더**에 똑같이 `url.py`를 만들고, 아래와 같이 작성한다.

![blogurl2](https://user-images.githubusercontent.com/84573261/126897231-e1b3fad6-a37f-425a-876a-b1eebe8fd2a3.PNG)

---

## FBV로 페이지 만들기

**url.py에 들어갈 함수나 클래스 등은 view.py에서 정의하는데, view.py를 만들 때 FBV와 CBV라는 2가지 선택지가 있다.**

**FBV**: Function based view. 함수에 기반을 둔 방법으로, 함수를 직접 만들어서 원하는 기능을 직접 구현할 수 있는 장점이 있다.<br>
**CBV**: Class based view. 장고가 제공하는 클래스를 활용해 구현하는 방법으로, 장고는 웹 개발을 할 때 반복적으로 많이 구현하는 것들을 클래스로 미리 만들어서 제공하고 있다.

**1. FBV로 포스트 목록 페이지 만들기**

![FBVurl](https://user-images.githubusercontent.com/84573261/126897320-fdfdb877-7575-4595-8656-4b34cb16926f.PNG)

1. `view.py`에 **index**라는 함수를 만들어서 FBV로 구현할 예정이다.<br>
여기서 **from . import views**는 현재 폴더에 있는 `view.py`를 사용할 수 있게 가져오라는 뜻이다.

![viewpy](https://user-images.githubusercontent.com/84573261/126897436-2fe86044-5cdd-40b3-bcc7-3c0f3ed83fe0.PNG)

2. 아직 **blog 폴더**의 `view.py`에 **index()함수가 정의되지 않았으므로,** 위 사진과 같이 index()함수를 정의한다.<br>
**index()함수**가 하는 역할은 **장고가 기본으로 제공하는 render()함수를 사용해 템플릿 폴더에서 blog 폴더의 index.html파일을 찾아 방문자에게 보내준다.**

![indexhtml](https://user-images.githubusercontent.com/84573261/126897553-54024e15-ebe2-441c-b2b1-f8338392ebbf.PNG)

위 사진처럼 `index.html`을 만들어준다. 

![blogurl3](https://user-images.githubusercontent.com/84573261/126897593-c13b6c66-f8d9-4e7c-9ca5-ad8f9bd234d9.PNG)

3. 블로그 페이지에 포스트 목록을 나열한다. 그러기 위해선 `view.py`를 개선해주면 된다.

![viewpy2](https://user-images.githubusercontent.com/84573261/126898712-be167f03-18a4-4d4c-aee2-3bab499142fb.PNG)

윗 사진처럼 우선 **models.py에 정의되어 있는 Post 모델을 import한다.** 그리고 index() 함수에서 `Post.object.all()`로 모든 Post 레코드를 가져와 posts에 저장한다.<br>
마지막으로 render() 함수 안에 posts를 딕셔너리 형태로 추가한다.<br>
++ `Post.object.all()`과 같은 방식으로 `views.py`에서 데이터베이스에 쿼리를 날려 원하는 레코드를 가져올 수 있다.

![indexhtml3](https://user-images.githubusercontent.com/84573261/126898875-464d180b-103c-4d3c-bbdf-1d5b38178bbc.PNG)

`index.html`도 다음과 같이 수정한다. 웹 브라우저를 새로고침하면 밑의 그림과 같이 각각의 필드값까지 나타난다.

![blogurl4](https://user-images.githubusercontent.com/84573261/126898895-9eba77e8-706b-43fc-8871-acbab9ff4dca.PNG)

4. 최신 포스트부터 보여주기 위해 `order_by`를 사용한다.

![orderby](https://user-images.githubusercontent.com/84573261/126898936-b0a7a20f-98ad-4a68-b77b-5fec6129102c.PNG)

**2. FBV로 포스트 상세 페이지 만들기**












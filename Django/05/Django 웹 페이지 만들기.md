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

1. 포스트 상세 페이지 URL을 정의하기 위해서 아래와 같이 `path('<int:pk>/', views.single_post_page),`코드를 추가한다.

![path](https://user-images.githubusercontent.com/84573261/126899118-fdb518a9-48c9-4d6a-9a55-439489660a5b.PNG)

위 사진에서 `<int:pk>`는 정수 형태의 값을 `pk`라는 변수로 담아 `single_post_page()`함수로 넘기겠다는 의미이다.

2. single_post_page() 함수 정의하기

![single2](https://user-images.githubusercontent.com/84573261/126900409-cdaf3d05-107f-46f4-8d34-d05b4039d7cb.PNG)

```Python
def single_post_page(request, pk):
    post = Post.objects.get(pk=pk)

    return render(
        request,
        'blog/single_post_page.html',
        {
            'post':post,
        }
    )

```

3. 템플릿 파일을 만들기 위해선 **blog/templates/blog**폴더에 `single_post_page.html`을 만든다.

![single4](https://user-images.githubusercontent.com/84573261/126900486-e5517d3c-9cdb-423e-8e40-10ff86f77bf8.PNG)

**3. 포스트 제목에 링크 만들기**

포스트 상세 페이지에서 **Blog 링크를 클릭하면 포스트 목록 페이지로 이동할 수 있는 것처럼**, <br>
포스트 목록 페이지에서 **포스트 제목(title)을 클릭하면 해당 포스트의 상세 페이지로 갈 수 있는 링크를 만든다.** 

1. 우선 `index.html`을 수정한다.

![indexhtml4](https://user-images.githubusercontent.com/84573261/126900583-5d7256c2-26ee-4269-9f4c-da6a80c492bd.PNG)

위 그림과 같이 `<h2><a href="{{ p.get_absolute_url }}">{{ p.title }}</a></h2>`로 수정해준다. 하지만 **이렇게만 해놓으면 상세 페이지로 갈 수 없다.** <br>
왜냐하면 `model.py`에서 **Post 모델에 get_absolute_url() 함수를 정의하지 않았기 때문이다.**

2. 그러므로 아래와 같이 `model.py`를 수정한다.

![modelpy](https://user-images.githubusercontent.com/84573261/126900690-ea09514f-9ccf-44e9-bc5d-0ba27b71c0d9.PNG)

```Python
 def get_absolute_url(self):
        return f'/blog/{self.pk}/'
```

이렇게 한 뒤 관리자 페이지에서 보면 **VIEW ON SITE**버튼이 생긴 것을 확인할 수 있다.

![viewonsite](https://user-images.githubusercontent.com/84573261/126900767-448b510f-3455-49f8-aeb8-286e7b151ce5.PNG)

**4. 대문 페이지와 자기소개 페이지 만들기**

1. 대문 페이지는 **도메인 뒤에 아무 것도 붙이지 않았을 때 나타나는 페이지**이다. 그러므로 도메인 뒤에 아무 것도 붙어 있지 않은 경우에는 <br>
`single_pages`앱에서 처리하도록 **장고 프로젝트 폴더**의 `urls.py`를 수정한다.

![singlepage](https://user-images.githubusercontent.com/84573261/126900935-55c1856e-88e9-40cf-abfc-75ddf33873c4.PNG)

위 사진처럼 `ulrpatterns`에 `path('', include('single_pages.urls')),`를 추가한다.

2. 대문 페이지와 자기소개 페이지의 URL 지정한다. 이 때, `single_pages`앱 폴더에 `urls.py`를 만들고 2가지 URL 패턴에 대한 명령을 추가한다.<br>
먼저 **도메인 뒤 아무것도 없을 때는 view.py에 있는 landing()함수를 실행해 대문 페이지를 보여주고,**<br>
**도메인 뒤 about_me/가 붙어 있을 때는 about_me()함수를 실행해 자기소개 페이지를 보여준다.**

![urlpy](https://user-images.githubusercontent.com/84573261/126901700-2b8683fc-430a-4833-ac6b-2c4272cf0f90.PNG)

3. `single_pages`앱의 `views.py`에 **landing()함수와 about_me()함수를 만들어 FBV 스타일로 페이지를 보여줘야 한다.**<br>
landing()함수에서는 `landing.html`을 보여주고, <br>
about_me()함수에서는 `about_me.html`을 보여주도록 한다.

![singlepageviewpy](https://user-images.githubusercontent.com/84573261/126901796-c1c5dde0-1ee2-4fe1-9755-a0a8c0a68e83.PNG)

4. 2개의 함수에 대한 파일들(landing.html,about_me.html)을 만든다.

![landing](https://user-images.githubusercontent.com/84573261/126901991-f7e4cc48-5ac4-4a17-846d-be3b8bd33c92.PNG)

![aboutme](https://user-images.githubusercontent.com/84573261/126902000-cf488d54-2102-4ee1-a436-acebe52437e7.PNG)

5. 마지막으로 제대로 되었는지 확인해본다. 

![dal](https://user-images.githubusercontent.com/84573261/126902318-81627f68-5e9d-4e3a-94cf-559659b2dd2a.PNG)

![dal2](https://user-images.githubusercontent.com/84573261/126902320-c5b9860d-6dd8-4be9-ba44-4e491c599291.PNG)

---

## CBV로 페이지 만들기

장고는 웹 개발할 때 사람들이 반복해서 사용하는 기능들을 클래스 형태로 제공해 주기 때문에,<br>
CBV(Class based view)를 사용하면 더 간편하게 페이지를 만들 수 있는 경우가 많다.

**1. CBV로 포스트 목록 페이지 만들기**

1. ListView로 포스트 목록 페이지를 만든다. **ListView**클래스는 여러 포스트를 나열 할 때 활용하면 좋다.

![ListView](https://user-images.githubusercontent.com/84573261/126903409-3f925780-c6ba-48bd-b838-0d2c20084964.PNG)

이전에 FBV로 만든 것은 주석처리하고, CBV로 새로 포스트 목록 페이지를 만들었다.

2. urls.py도 수정한다. 이전과 같이 기존에 했던 것은 주석 처리하였다.

![ListView2](https://user-images.githubusercontent.com/84573261/126902569-d9b62ad2-cec5-461a-9491-3913bb3fc0c9.PNG)

3. 다시 127.0.0.1:8000/blog/를 들어가면 아래와 같이 나온다.

![ListView3](https://user-images.githubusercontent.com/84573261/126903424-7964622d-7939-4f37-8063-afb482946b4d.PNG)

이를 해결하기 위해선 두 가지 방법이 있는데, 첫번째로<br>
**PostList클래스에서 template_name을 직접 지정하는 방법**이고, <br>
**또 다른 하나는 post_list.html을 만드는 방법**이다.

4. 이전의 FBV에서 했던 최신포스트부터 보여주기를 CBV 방식에서도 적용한다.

![ordering](https://user-images.githubusercontent.com/84573261/126903620-ff3c8bd7-6b71-4273-aa90-1cb5cd3688fd.PNG)

**2. CBV로 포스트 상세 페이지 만들기**

1. 여러 레코드를 목록 형태로 보여줄 때는 ListView를 이용했다면, **한 레코드를 자세히 보여줄 때는 DetailView를 사용한다.**

![Detail](https://user-images.githubusercontent.com/84573261/126903757-46e6e58d-283d-4420-a3d0-ae93d1509668.PNG)

2. blog/urls.py도 아래의 사진과 같이 수정한다.

![Detail2](https://user-images.githubusercontent.com/84573261/126903834-e1693123-7d45-4b8b-a3ee-c61f481a1698.PNG)

3. 서버를 실행해보면 아래 사진과 같이 나온다. 이를 해결하기 위해 **single_post_page.html 파일명을 post_detail.html로 수정한다.**

![Detail3](https://user-images.githubusercontent.com/84573261/126903900-3aa61067-0082-4fc1-ac09-6d1a072d9c0b.PNG)

4. 파일명을 수정한 뒤 다시 접속하면 제대로 실행되고 있음을 확인할 수 있다.

![Detail4](https://user-images.githubusercontent.com/84573261/126903962-a83d4fa7-05ed-449d-82a4-a16ef06f5040.PNG)



















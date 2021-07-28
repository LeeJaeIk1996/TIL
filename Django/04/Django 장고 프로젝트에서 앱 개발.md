# 장고 프로젝트에서 앱 개발하기

## 1. 블로그 앱, 페이지 앱 만들기

### - blog 앱과 single_pages 앱 만들기

**앱(app)**: 특정한 기능을 수행하는 단위 모듈. 

![startapp1](https://user-images.githubusercontent.com/84573261/126619652-ed936aa0-dd74-4de2-8835-ede597ca6cc1.PNG)

위 사진처럼 `python manage.py startapp`명령을 입력한 뒤 `blog`와 `single_pages`라는 이름을 입력한다.

![startapp2](https://user-images.githubusercontent.com/84573261/126619806-0c12c7fe-3af1-4938-ae2a-d4313f5ce850.PNG)

그 뒤 파이참을 들어가 보면 2개의 폴더(blog,single_pages)가 생성되어 있고, 각 폴더에는 **admin.py, apps.py, models.py, tests.py, views.py**와 같은 파일이 생성되어 있음을 확인할 수 있다. 이처럼 **앱은 각각 독립된 파일들로 구성되어 독립된 기능을 한다.**

![commit1](https://user-images.githubusercontent.com/84573261/126620229-1e73d9ef-3955-45b1-9247-6f9debc43be4.PNG)

완료가 되었으면 깃으로 commit한다. **깨끗한 상태의 migrations 폴더**를 커밋한 이유는 모델이 생성, 수정될 때마다 앱의 migrations 폴더에 자동으로 새로운 마이그레이션 파일이 생성되기 때문이다. 

---

## 2. 데이터베이스 개념 이해하기

### - 데이터베이스에 관한 기본적인 개념

1. 데이터베이스를 사용하는 이유는 여러 가지 정보를 효율적으로 저장하고 관리하기 위해 데이터베이스를 사용한다.

2. 전체를 **테이블**, 가로 방향(행)으로 읽는 데이터를 **레코드**, 세로 방향(열)으로 읽는 데이터를 **필드**라고 한다.

3. 기본키와 외래키

---

## 3. 모델 만들기

### - 블로그의 글을 위한 모델 만들기

1. Post 모델 만들기

![post](https://user-images.githubusercontent.com/84573261/126621118-75e95890-5592-4c36-b924-b59046434783.PNG)

```Python
from django.db import models

# Create your models here.
class Post(models.Model):
    title = models.CharField(max_length=30)
    content = models.TextField()

    created_at = models.DateTimeField()
```

2. 데이터베이스에 Post 모델 반영하기

![makemi](https://user-images.githubusercontent.com/84573261/126621333-ff5f265d-0827-486a-98b2-8fe98b59b617.PNG)

데이터베이스에 반영하기 위해 `python manage.py makemigrations`를 입력하면 **No changes detected**라는 메시지가 나타나는데,<br>
이는 **settings.py 파일에 현재 우리의 'blog' 앱을 등록하지 않았기 때문이다!!**

![set](https://user-images.githubusercontent.com/84573261/126621731-4a9456cc-e71d-4c8e-bb92-47cc467d4803.PNG)
 
이렇게 설정해준 뒤, 다시 `python manage.py makemigrations`를 입력하면 **blog/migrations 폴더에 0001_initial.py 파일이 생성된다.**

![0001](https://user-images.githubusercontent.com/84573261/126621862-94c75e3a-413b-4848-bb1f-33b4815e531c.PNG)

**이 상태는 아직 데이터베이스에 모델이 적용되지 않은 상태이므로**, 실제 데이터베이스 모델에 적용하기 위해선 `python manage.py migrate`명령을 실행해야 한다.

![migration](https://user-images.githubusercontent.com/84573261/126622075-9e3a8292-785c-453c-ba61-b5acbc36df25.PNG)

++ 이전에 생긴 **0001_initial.py** 파일은 **.gintignore**를 이용해 깃 관리 대상에서 제외한다. 왜냐하면 개발할 때 models.py를 수정해야될 일이 많은데,<br>
모델 수정 내역을 일일이 기록하다 보면 로컬 컴퓨터의 데이터베이스와 서버의 데이터베이스가 일치하지 않아 문제가 생길 수 있기 때문이다.

![gitig](https://user-images.githubusercontent.com/84573261/126622453-1b398406-97cf-4c07-a020-ff3f2cc6eeab.PNG)

### - 관리자 페이지에서 첫 포스트 작성하기

1. 우선 **blog/admin.py** 파일을 열고 두 줄만 추가하여 관리자 페이지에 Post 모델을 등록한다.

![admin](https://user-images.githubusercontent.com/84573261/126622723-168caa07-4701-4028-8e95-cdbdaa9c88ff.PNG)

```Python
from .models import Post

admin.site.register(Post)
```

![adminpost](https://user-images.githubusercontent.com/84573261/126622896-9666cfab-f07b-4672-9791-0f7c655676eb.PNG)

위 사진과 같이 관리자 페이지에 Blog 섹션과 Post 메뉴를 확인할 수 있다.

2. 새로운 포스트 생성하기

![firstpost](https://user-images.githubusercontent.com/84573261/126623051-e55d9564-9c1d-4776-8a93-04ccd8173671.PNG)

++ 특정 지역 기준으로 작성 시각을 설정하기 위해선 아래 사진과 같이 **settings.py**에서 <br>
`TIME_ZONE = UTC`를 `TIME_ZONE = Asia/Seoul`로 수정하고 `USE_TZ = True`를 `USE_TZ = False`로 수정해야 한다.

![time](https://user-images.githubusercontent.com/84573261/126623431-43c61e24-7098-47c3-85f8-b3bdf459dd86.PNG)

++ 처음 Post를 만들면 아래 사진과 같이 **Post object(1)** 으로 나온다. 이를 수정하기 위해선 **blog/models.py**파일에 내용을 추가해야 된다.

![object](https://user-images.githubusercontent.com/84573261/126623789-efa3ef97-4881-4be3-9709-7b9213611480.jpg)

![str](https://user-images.githubusercontent.com/84573261/126623909-612ab706-12a1-469e-a930-be66c70b7260.PNG)

```Python
    def __str__(self):
        return f'[{self.pk}] {self.title}'
```

여기서 `pk`는 각 레코드에 대한 고유값이라 보면 된다.

++ 자동으로 작성 시각과 수정 시각을 저장하기 위해선 **blog/models.py**에서 아래와 같이 수정해준다.

![auto](https://user-images.githubusercontent.com/84573261/126624294-80531929-e308-4ca1-a0a6-4d99f87618a9.PNG)

```Python
created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

3. 모델을 수정하였으므로 이를 `makemigrations`로 장고에게 알려주고, `migrate`로 데이터베이스에 반영해야 한다. 그리고 다시 서버를 실행한다.

![fin](https://user-images.githubusercontent.com/84573261/126624621-896df2dc-9d10-4574-8115-7db198a2ceaa.PNG)

![fin2](https://user-images.githubusercontent.com/84573261/126624730-44c8bcde-993f-43e9-b4a5-321e596a6f5e.PNG)

위 사진을 보면 이전에 작성 시각과 수정 시각을 auto로 수정하여 더 이상 입력 란이 보이지 않는 것을 확인할 수 있다.

---

마지막에 `git commit`과 `git push`를 하여 깃허브에 업로드 한다.

![fin3](https://user-images.githubusercontent.com/84573261/126625152-522687c6-03d1-4408-9d48-a82d07d7e782.PNG)

---

금일 배운 것 정리
1. `python manage.py startapp 명` → 앱을 만드는 명령어
2. **admin.py, apps.py, models.py, tests.py, views.py** → 앱을 만든 뒤 생기는 폴더들
3. Post 모델 만들기위한 코드

```Python
from django.db import models

# Create your models here.
class Post(models.Model):
    title = models.CharField(max_length=30)
    content = models.TextField()

    created_at = models.DateTimeField()
```

4. `python manage.py makemigrations`, `python manage.py migrate`
5. **admin.py**에 Post 모델 등록하기 위한 코드

```Python
from .models import Post

admin.site.register(Post)
```

6. **___str()___** 함수로 포스트 제목과 번호 보여주는 코드

```Python
    def __str__(self):
        return f'[{self.pk}] {self.title}'
```

7. 자동으로 작성 시각과 수정 시각 저장해주는 코드

```Python
created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```







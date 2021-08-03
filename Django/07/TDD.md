# ✔ TDD 이해하기

## 1. TDD 란?

📌 **테스트 주도 개발(TDD)** : Test Driven Development. 일종의 개발 방식 또는 개발 패턴.<br>
무언가를 개발할 때 개발부터 하는 것이 아니라 **개발하려는 항목에 대한 점검 사항을 테스트 코드로 만들고** 그 테스트를 통과시키는 방식으로 개발을 진행하는 방법.


![TDD](https://user-images.githubusercontent.com/84573261/128052298-a37cb847-c7b1-4909-be03-3e074a56a945.jpg)

📌 **리팩터링(Refactoring)**: 소프트웨어 공학에서 **결과의 변경 없이 코드의 구조를 재조정함**을 뜻한다. <br>
주로 가독성을 높이고 유지보수를 편하게 한다. 버그를 없애거나 새로운 기능을 추가하는 행위는 아니다.<br>
사용자가 보는 외부 화면은 그대로 두면서 내부 논리나 구조를 바꾸고 개선하는 유지보수 행위이다.

## 2. beautifulsoup 란?

📌 **beautifulsoup**:  HTML정보로부터 원하는 데이터를 가져오기 쉽게, 비슷한 분류의 데이터별로 **나누어주는(parsing)** 파이썬 라이브러리.

- `pip install beautifulsoup4`: **beautifulsoup4 라이브러리 설치 명령어.**

```hash
beautifulsoup는 파이썬에 추가할 수 있는 크롤링을 위한 라이브러리이다.
결국, 웹에 있는 데이터를 가져와서 추출할 경우에 사용하는 외부 라이브러리로
추가 설치가 필요하다.
```

- **크롤링(crawling)**: 웹페이지에서 필요한 데이터를 추출하는 작업을 의미한다.
- **파싱(parsing)**: 간단하게 말하면 정제하기, 해석하기를 의미한다.<br>
파싱이란 어떤 일정한 문법을 토대로 나열된 data들을 그 문법에 맞게 분석하여 새롭게 구성하는 작업을 뜻한다.<br>
어떤 data를 파싱한다는 것은 크게 두 가지를 의미한다.<br>
(1) 파싱하는 data가 특정 문법에 알맞게 정리된 data인지 확인하는 것을 뜻함.<br>
(2) 파싱하는 data를 응용 프로그램이 목적에 맞게 이용하기 쉬운 형태로 구성해주는 것.

---

# ✔ TDD 사용 예시

## 1. test.py 내 from, import

```Python
from django.test import TestCase, Client
from bs4 import BeautifulSoup
from .models import Post

class TestView(TestCase):
    # 크게 4개의 함수로 나누었다.
    # def setUp(self), def navbar_test(self, soup),
    # def test_post_list(self), def test_post_detail(self) 
```

- **TestCase를 이용한 테스트 방식은 실제 데이터베이스는 건드리지 않고 가상의 데이터베이스를 새로 만들어서 테스트한다.**

## 2. setUp( 함수

```Python
def setUp(self):
  self.client = Client()
```

- **TestCase** 내에서 기본적으로 설정되어야 하는 내용이 있으면 `setUp()` 함수에서 정의.
- 현재는 `setUp()` 함수 내에 `Client()`를 사용하겠다는 내용만 담음.
- **Client는 테스트를 위한 가상의 사용자라고 볼 수 있다.**

## 3. navbar_test(self, soup) 함수

```Python
def navbar_test(self, soup):
  
  navbar = soup.nav
  self.assertIn('Blog', navbar.text)
  self.assertIn('About Me', navbar.text)

  logo_btn = navbar.find('a', text='JaeIk Lee')
  self.assertEqual(logo_btn.attrs['href'], '/')

  home_btn = navbar.find('a', text='Home')
  self.assertEqual(home_btn.attrs['href'], '/')

  blog_btn = navbar.find('a', text='Blog')
  self.assertEqual(blog_btn.attrs['href'], '/blog/')

  about_me_btn = navbar.find('a', text='About Me')
  self.assertEqual(about_me_btn.attrs['href'], '/about_me/')
```

- `navbar = soup.nav`: **soup.nav로 soup에 담긴 내용 중 nav 요소만 가져와 navbar에 저장.**
- `self.assertIn('Blog', navbar.text)` : **navbar의 텍스트 중에 Blog가 있는지 확인.**
- `logo_btn = navbar.find('a', text='JaeIk Lee')`: **navbar.find로 네비게이션 바에서 'JaeIk Lee'라는 문구를 가진 a요소를 찾아 logo_btn변수에 담음.** 
- `self.assertEqual(logo_btn.attrs['href'], '/')`: **a 요소에서 href 속성을 찾아 값이 '/'인지 확인한다.**
- ![jaeiklee](https://user-images.githubusercontent.com/84573261/128062723-ad8f980b-14f6-4df2-9298-0bb3df267421.PNG)

## 4. test_post_list(self) 함수

```Python
def test_post_list(self):
  
  # 1.1 포스트 목록 페이지를 가져온다.
  response = self.client.get('/blog/')
  # 1.2 정상적으로 페이지가 로드된다.
  self.assertEqual(response.status_code, 200)
  # 1.3 페이지 타이틀은 'Blog'이다.
  soup = BeautifulSoup(response.content, 'html.parser')
  self.assertEqual(soup.title.text, 'Blog')
  
  # 1.4 네비게이션 바가 있다.
  # navbar = soup.nav
  # 1.5 Blog, About Me라는 문구가 내비게이션 바에 있다.
  # self.assertIn('Blog', navbar.text)
  # self.assertIn('About Me', navbar.text)
  # 1.4와 1.5의 과정은 앞에서 설명한 navbar_test 함수에 정리되어 있으므로 아래와 같이 표현할 수 있다.
  self.navbar_test(soup)
  
  # 2.1 메인 영역에 게시물이 하나도 없다면
  self.assertEqual(Post.objects.count(), 0)
  # 2.2 '아직 게시물이 없습니다.'라는 문구가 보인다.
  main_area = soup.find('div', id='main-area')
  self.assertIn('아직 게시물이 없습니다', main_area.text)

  # 3.1 게시물이 2개 있다면
  post_001 = Post.objects.create(
  title='첫 번째 포스트입니다.',
  content='Hello World. We are the world',
  )
  post_002 = Post.objects.create(
  title='두 번째 포스트입니다.',
  content='1등이 전부는 아니잖아요?',
  )
  self.assertEqual(Post.objects.count(), 2)
  # 3.2 포스트 목록 페이지를 새로고침 했을 때
  response = self.client.get('/blog/')
  soup = BeautifulSoup(response.content, 'html.parser')
  self.assertEqual(response.status_code, 200)
  # 3.3 메인 영역에 포스트 2개의 타이틀이 존재한다.
  main_area = soup.find('div', id='main-area')
  self.assertIn(post_001.title, main_area.text)
  self.assertIn(post_002.title, main_area.text)
  # 3.4 '아직 게시물이 없습니다.'라는 문구는 더 이상 보이지 않는다.
  self.assertNotIn('아직 게시물이 없습니다', main_area.text)
```

- `response = self.client.get('/blog/')`: **(가상의) 사용자가 웹 프라우저에 '127.0.0.1:8000/blog/'를 입력했다고 가정하고 그 때 열리는 웹 페이지 정보를 response에 저장.**
- `self.assertEqual(response.status_code, 200)`: **페이지가 정상적으로 열렸다면 status_code의 값으로 200이 나온다.**<br>
++404: 요청한 페이지를 찾을 수 없을 때 / 200: 요청한 페이지를 성공적으로 돌려줄 때
- `soup = BeautifulSoup(response.content, 'html.parser')`: **HTML 요소에 쉽게 접근하기 위해 먼저 Beautifulsoup으로 읽어들이고, html.parser명령어로 파싱한 결과를 soup에 담음.**
- `post_001 = Post.objects.create( ~ )`: **Post 레코드가 데이터베이스에 존재하는 상황도 테스트하기 위해 포스트를 2개 만든다. 
Post.objects.create()로 새로운 포스트를 만들 수 있다. 매개변수에는 Post 모델의 필드 값을 넣는다.**
- `self.assertNotIn('아직 게시물이 없습니다', main_area.text)`: **포스트가 생성되었으므로 '아직 게시물이 없습니다'라는 문구가 메인 영역에 더이상 나타나지 않아야 한다.**

## 5. test_post_detail(self) 함수

```Python
def test_post_detail(self):

  # 1.1 포스트가 하나 있다.
  post_001 = Post.objects.create(
  title='첫 번째 포스트입니다.',
  content='Hello World. We are the world.',
  )
  # 1.2 그 포스트의 url은 '/blog/1/'이다.
  self.assertEqual(post_001.get_absolute_url(),'/blog/1/')

  # 2 첫 번째 포스트의 상세 페이지 테스트
  # 2.1 첫 번째 포스트의 url로 접근하면 정상적으로 작동한다.(status code: 200).
  response = self.client.get(post_001.get_absolute_url())
  self.assertEqual(response.status_code, 200)
  soup = BeautifulSoup(response.content, 'html.parser')

  # 2.2 포스트 목록 페이지와 똑같은 내비게이션 바가 있다.
  # navbar = soup.nav
  # self.assertIn('Blog', navbar.text)
  # self.assertIn('About Me', navbar.text)
  self.navbar_test(soup)

  # 2.3 첫 번째 포스트의 제목이 웹 브라우저 탭 타이틀에 들어 있다.
  self.assertIn(post_001.title, soup.title.text)

  # 2.4 첫 번째 포스트의 제목이 포스트 영역에 있다.
  main_area = soup.find('div', id='main-area')
  post_area = main_area.find('div', id='post-area')
  self.assertIn(post_001.title,post_area.text)

  # 2.5 첫 번째 포스트의 작성자(author)가 포스트 영역에 있다.(아직 구현할 수 없음)
  # 아직 작성 불가

  # 2.6 첫 번째 포스트의 내용(content)이 포스트 영역에 있다.
  self.assertIn(post_001.content, post_area.text)
```

- `self.assertEqual(post_001.get_absolute_url(),'/blog/1/')`: **post_001.get_absolute_url()은 models.py에서 Post의 get_absolute_url()이다.**

## 6. 개인 정리

- .assertIn()
- .assertNotIn()
- .assertEqual()
- self.client.get()
- .find()
- Post.objects.count()
- Post.objects.create()
- .content 
- .text





# 부트스트랩 적용

![finish](https://user-images.githubusercontent.com/84573261/126341670-1c918d8b-b4a8-4922-b614-1c5dfd99229b.PNG)


## 1. 부트스트랩 알아보기

### - 부트스트랩?

**Bootstrap** : 웹 개발에 있어 보편적으로 널리 쓰이는 구성 요소들을 미리 디자인 해둔 툴킷(toolkit).

---

### - 부트스트랩의 CSS와 JavaScript 적용

![boot](https://user-images.githubusercontent.com/84573261/126338692-e673edd8-870c-4319-87e9-71e7a01fa825.PNG)
 
```hash
1. getbootstrap.com접속 후 download
2. 압축 파일에서 bootstrap.min.css와 bootstrap.min.css.map 파일을 저장한다.
```

![boot2](https://user-images.githubusercontent.com/84573261/126340065-7b0b0044-0e01-4940-b87a-b20d35a5694a.PNG)

```hash
3. <link href="./bootstrap4/css/bootstrap.min.css" rel="stylesheet" type="text/css"> 를 넣는다.
```

![boot3](https://user-images.githubusercontent.com/84573261/126340436-7fe9600b-c9ac-4431-83a3-63f65e1a98c2.PNG)

```hash
4. 위 사진에서 밑에 있는 코드를 copy하여 넣는다.
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.2/dist/umd/popper.min.js" integrity="sha384-IQsoLXl5PILFhosVNubq5LC7Qb9DXgDA9i+tQ8Zj3iwWAwPtgFTxbJ8NT4GN1R8p" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.min.js" integrity="sha384-cVKIPhGWiC2Al4u+LWgxfKTRIcfu0JTxR+EQDz/bgldoEyl4H0zUF0QKbrJ0EcQF" crossorigin="anonymous"></script>
```

++ 여기서 **CDN**이란?<br>
**CDN**: Contents delivery network. 부트스트랩 사이트에서 코드를 바로 가져오는 방식으로, CDN은 사람들이 자주 사용하는 CSS, Js 파일 등을 모아둔 곳을 말한다.

---

### - nav 수정

![nav](https://user-images.githubusercontent.com/84573261/126344201-9a7fb641-b954-4388-9b4c-1fdc2084541b.PNG)

```hash
1. getbootstrap.com에서 Documentation -> Components 접속
2. 그 중 Navbar접속
3. nav 종류 중 dropdown 네비게이션 바 선택하여 copy
```
![nav2](https://user-images.githubusercontent.com/84573261/126344651-391d8f6a-a53c-439b-9132-99b7784e1e5e.PNG)

++ **화면이 줄어들면 네비게이션 바의 목록이 보기 편하도록 세로로 나열되는 것을 확인할 수 있다.**

---

### - container 레이아웃 적용

![conta](https://user-images.githubusercontent.com/84573261/126345415-1a4d7605-aa1f-4369-af8f-037128636a37.PNG)

```hash
<div class="container">
```

부트스트랩의 `container`를 사용하여 페이지 구성을 위한 레이아웃을 간단히 만들 수 있다.

---

### - grid 웹 페이지 구성 관리

`grid`: 웹 페이지를 세로 12칸으로 나누어 관리. **grid**를 사용하면 화면 크기를 다양하게 바꾸어도 그 크기에 맞게 웹 페이지 모양도 바뀌어 나타난다.

![grid](https://user-images.githubusercontent.com/84573261/126346046-df73cfb8-1c7e-4c10-8637-7d31923c2c9b.PNG)

```hash
1. <div class="row"> 설정
2. <div class="col"> 설정. 
```

**col은 12칸이므로** 위 사진의 경우 `<div class="row">`에서 `<div class="col-9">`와 `<div class="col-3">`으로 나눈 것을 확인할 수 있다.

---

### - Spacing으로 간격 주기

**spacing**기능으로 간격을 조정할 수 있는데, 간격을 조정하는 방법은 **margin**과 **padding**이 있다.

![marpad](https://user-images.githubusercontent.com/84573261/126347547-503de36b-f09e-4aa5-a8ce-93d93b4a7577.jpg)

![mar](https://user-images.githubusercontent.com/84573261/126347672-3844517e-3b56-47b4-8c51-2c6252562f2d.PNG)

```hash
<div class="row my-3">
```

**margin 정리**
- m-숫자: 상하좌우
- mt-숫자: 상 마진 / md-숫자: 하 마진 / my-숫자: 상하 마진
- ml-auto: 좌 마진 최대한 확보 / mr-auto: 우 마진 최대한 확보

---

## 2. 부트스트랩으로 웹 사이트 모양 만들기

### - 블로그 페이지 모양 구현

![blog](https://user-images.githubusercontent.com/84573261/126348538-86d1402d-2582-44c7-b2a2-4fb7db178ac1.PNG)

```hash
1. startbootstrap.com 접속 
2. 네비게이션 바의 Templates -> Blog 접속
3. Blog Post(하나의 게시물을 보여줌) 혹은 Blog home(여러 게시물을 목록 형태로 보여줌) 적용
```

+ startbootstrap.com이 아니더라도 부트스트랩 공식 홈페이지에서도 템플릿 샘플을 제공한다.

---

### - card 구성 요소 

![card](https://user-images.githubusercontent.com/84573261/126349893-50395ebe-be7e-4baf-8385-9d2eebc7c7f4.jpg)

```hash
1. 하나의 카드를 구성하기 위해 <div>태그를 만들고 class에 card md-4를 지정
2. 이미지를 삽입하기 위해 <img>태그를 만들고 class에 card-img-top으로 지정
3. card-body와 그 안에 card-title, card-text를 만들어 내용을 채움
4. card-footer를 만들고 내용을 채움
```

![card2](https://user-images.githubusercontent.com/84573261/126350754-1e54ca94-ccc7-496b-ac4a-17770b698a29.PNG)

---

### - 페이지 이동 버튼

![page](https://user-images.githubusercontent.com/84573261/126350847-4df3dbb5-cf2e-40ae-85d6-0b1489b5150c.PNG)

---

### - 모달로 로그인 창 만들기

`modal`: 웹 브라우저 위에 **팝업 형태**로 나오는 요소.

![modal](https://user-images.githubusercontent.com/84573261/126351299-919eb63b-544a-4ac6-92c1-88e423cf1ba6.PNG)

![modal2](https://user-images.githubusercontent.com/84573261/126351498-c29aa39b-70b6-4fd7-ab2d-5667dd15abf5.PNG)

++버튼에 아이콘 추가하는 법(Font awesome 아이콘 툴킷 서비스 사용)
1. fontawesome.com접속 후 로그인(회원가입)
2. kit code 복사하여 복사한 kit code를 추가

![kitcode](https://user-images.githubusercontent.com/84573261/126352100-f5b685ad-5fb4-4aa2-930c-ed0d41d3119e.PNG)

위 사진처럼 **kit code**를 추가한 뒤, 다시 fontawesome.com에 접속하여 원하는 아이콘을 검색하고 그 아이콘의 코드를 복사하여 첨부하면 된다.

---





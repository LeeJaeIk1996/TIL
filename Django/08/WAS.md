# ✏ WAS 정리

## 1. Web Server

📌 **Web Server**: Web server는 하드웨어, 소프트웨어 혹은 두 개가 같이 동작하는 것을 의미.
1. Web Server(S.W): 웹브라우저와 같은 클라이언트로부터 HTTP 요청을 받아들이고, HTML 문서와 같은 웹 페이지를 반환하는 컴퓨터 프로그램.
2. Web Server(H.W): 위에 언급한 기능을 제공하는 컴퓨터 프로그램을 실행하는 컴퓨터.

```hash
웹 서버의 주된 기능은 웹 페이지를 클라이언트로 전달하는 것이다. 
주로 그림, CSS, JS를 포함한 HTML 문서가 클라이언트로 전달된다.
```


**대표적인 웹 서버**는 Nginx, Apache, GWS가 있다.

📌 **Apache**: Apache HTTP Server는 아파치 소프트웨어 재단에서 관리하는 오픈 소스, 크로스 플랫폼 HTTP 웹 서버 소프트웨어이다.

**HTTP Web Server**는 http 요청을 처리할 수 있는 웹 서버이고, **Apache HTTP Server**는 http 요청을 처리하는 **웹 서버**이다.<br>
클라이언트가 GET, POST, DELETE 등을 이용해 요청을 하면 이 프로그램이 특정 결과를 돌려주는 기능을 한다.

✔ Apache와 Nginx의 차이는 다음과 같다.
- Apache는 request에 대해 process(+thread) 하나씩 사용
- Nginx는 Event-Driven 방식으로 비동기 처리

---

## 2. WSGI와 gunicorn

📌 **WSGI**:  Web Server Gateway Interface는 웹서버와 웹 애플리케이션의 인터페이스를 위한 파이썬 프레임워크.

```hash
WSGI는 서버와 게이트웨이 , 애플리케이션과 프레임워크 양단으로 나눠져있다. WSGI 리퀘스트를 처리하려면, 
서버단에서 환경정보와 콜백함수를 애플리케이션단에 제공해야한다.
애플리케이션은 그 요청을 처리하고 미리 제공된 콜백함수를 통해 서버단에 응답한다. 
WSGI 미들웨어(라고 불린다.)가 WSGI 서버와 애플리케이션 사이를 보충해주는데, 
이 미들웨어는 서버의 관점에서는 애플리케이션으로, 애플리케이션의 관점에서는 서버로 행동한다.
이 미들웨어는 다음과 같은 기능을 가진다.

1. 환경변수가 바뀌면 타겟 URL에 따라서 리퀘스트의 경로를 지정해준다.
2. 같은 프로세스에서 여러 애플리케이션과 프레임워크가 실행되게 한다.
3. XSLT 스타일시트를 적용하는 것과 같이 전처리를 한다.
```

참고: [WSGI](https://ko.wikipedia.org/wiki/%EC%9B%B9_%EC%84%9C%EB%B2%84_%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4_%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4)

전체적으로 보았을 때, 아래 사진과 같이 동작한다고 볼 수 있다.
![was](https://user-images.githubusercontent.com/84573261/131352188-23b49f60-d956-483a-9737-45136f50701e.jpg)

**HTTP requests → WSGI Server(Middleware) → Django(WSGI를 지원하는 Web Application)** 으로 동작하는데,<br>
여기서 **gunicorn**은 **WSGI Server**이다.

📌 **gunicorn**: gunicorn은 Python WSGI HTTP Server이다. gunicorn은 상대적으로 빠르고 가볍고 사용하기 쉽다.

```hash
Django에서는 wsgi.py에서 application = get_wsgi_application() 를 통해 wsgi handler를 가져온다.
wsgi handle r에서는 middleware등 을 처리하고, WSGI server에서는 설정을 읽어 application의 경로를 가져온다.
Django 기본 명령어인 runserver 명령은 WSGI_APPLICATION 설정에서 경로를 가져온다.
```

---

## 3. WAS

📌 **WAS**: Web Server + Web Container

웹 애플리케이션과 서버 환경을 만들어 동작시키는 기능을 제공하는 소프트웨어 프레임워크.<br>
인터넷 상에서 HTTP를 통해 사용자 컴퓨터나 장치에 애플리케이션을 수행해 주는 **미들웨어(소프트웨어 엔진)** 로 볼 수 있다.<br>
웹 애플리케이션 서버는 **동적 서버 콘텐츠를 수행하는 것으로 일반적인 웹 서버와 구별이 되며, 주로 데이터베이스 서버와 같이 수행이 된다.**

Web Server + Web Container로 웹 상에서 사용하는 컴포넌트를 올려놓고 사용하게 되는 서버이다.<br>
**Web Container**란 JSP와 Servlet(서블릿)을 실행시킬 수 있는 S.W를 웹 컨테이너라 한다.

**WAS**의 기능은 다음과 같다.
- 프로그램 실행 환경과 데이터베이스 접속 기능을 제공.
- 여러 개의 트랜잭션을 관리.
- 업무를 처리하는 비즈니스 로직을 수행

![webcontainer](https://user-images.githubusercontent.com/84573261/131354968-a750c4c8-c6c5-4438-ac0e-248fdfa7a4c7.PNG)

📌 **Web Container**: JSP와 Servlet을 실행시킬 수 있는 소프트웨어를 Web Container 혹은 Servlet Container라고 한다.

```hash
웹 서버에서 JSP를 요쳥하면 톰캣에서는 JSP 파일을 Servlet으로 변환하여 컴파일을 수행하고,
Servlet 수행 결과를 웹 서버에게 전달하게 된다.
JSP container가 탑재 되어 있는 WAS는 JSP 페이지를 컴파일 해 동적인 페이지를 생성한다.
```

📌 **tomcat**: tomcat은 흔히 WAS라고 말한다.

tomcat은 웹 서버와 연동하여 실행할 수 있는 자바 환경을 제공하여 자바서버 페이지(JSP)와 자바 서블릿(Servlet)이 실행할 수 있는 환경을 제공하고 있다.

---

## 4. WAS와 Web Server 

💡 **WAS와 Web Server 비교**
- Web Server는 HTML 문서같은 정적 컨텐츠를 처리
- WAS는 asp, php, jsp 등 개발 언어를 읽고 처리하여 동적 컨텐츠, 웹 응용 프로그램 서비스를 처리

💡 **WAS와 Web Server의 차이**
- Web Server는 정적인 데이터를 처리하는 서버. 이미지나 단순 html파일 같은 리소스를 제공하는 서버를 Web Server를 통하면 WAS를 이용하는 것보다 빠르고 안정적이다.
- WAS는 동적인 데이터를 처리하는 서버. DB와 연결되어 데이터를 주고 받거나 프로그램으로 데이터 조작이 필요한 경우에는 WAS를 활용해야 한다.

```hash
우리가 만드는 웹페이지는 정적 컨텐츠와 동적 컨텐츠를 함께 노출해야 한다.
WAS가 정적 데이터를 처리하게 되면, 동적 컨텐츠의 처리가 지연이 될 것이고 
이로 인한 페이지 노출 시간이 늘어나게 된다.
WAS는 동적 처리에 최적화 되어 있는 서비스이기 때문에 처리 속도를 위해,
정적 처리는 웹 서버에서 처리를 하고,
동적 컨텐츠는 WAS에서 처리하게 된다.
```

**사용자가 클라이언트에 요청을 하게 되면 이를 Web Server에서 반응하여 WAS의 처리를 거쳐 웹 페이지로 다시 웹 서버에서 클라이언트에 response 메시지를 주는 것이다.**

💡 **Web Server와 WAS의 구성에 따른 분류**
- WAS와 Web Server를 분리하지 않는 경우.
  + 모든 컨텐츠를 한 곳에 집중시켜 Web Server와 WAS의 역할을 동시에 수행. 사용자가 적을 경우 효율적이다.

- WAS와 Web Server를 분리한 경우.
  + Web Server와 WAS의 기능적 분류를 통해 효과적인 분산을 유도. 정적인 데이터는 Web Server에서 처리, 동적인 데이터는 WAS에서 처리한다.

- WAS 여러 개와 Web Server를 분리한 경우
  + WAS단을 프레젠테이션 로직과 비즈니스 로직으로 구분하여 구성, 특정 logic의 부하에 따라 적절한 대응을 할 수 있지만 설계단계 유지보수 단계가 복잡해 질 수 있다.


**WAS와 Web Server를 분리하는 이유는 다음과 같다.**
1. 기능을 분리하여 서버의 부하를 방지.
2. 물리적으로 분리하여 보안을 강화.
3. 여러 대의 WAS 연결 가능.
4. 여러 Web Application 서비스 가능

즉, 자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성을 위해 Web Server와 WAS를 분리한다.


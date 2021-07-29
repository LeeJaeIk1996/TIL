# ✔ MVC와 MTV 이해하기

## 1. MVC란?

📌 **MVC**: 소프트웨어 공학에서 사용되는 소프트웨어 디자인 패턴으로, 유지보수가 편해지는 코드 구성 방식을 말한다.

**M**odel: **데이터와 관련된 부분.**
- 애플리케이션의 정보(데이터)를 나타낸다.
- 데이터를 처리하며 데이터베이스와 상호 작용하는 인터페이스 역할을 한다.
 
**V**iew: **사용자한테 보여지는 부분.**
- 텍스트, 체크박스 항목 등과 같은 사용자 인터페이스 요소를 나타낸다.
- 웹 응용 프로그램인 브라우저에서 실제 사용자에게 표시되는 프레젠테이션 로직을 처리하여 ui(레이아웃)로 나타낸다.<br>
++ **View는 사용자한테 보이는 UI와 모델로부터 받은 데이터가 합쳐져 만들어진 화면이다.**

**C**ontroller: **Model과 View를 이어주는 부분. 데이터 처리 로직**
- 데이터와 비즈니스 로직 사이의 상호 동작을 관리
- view에서 핸들러의 흐름을 처리하거나 model의 데이터를 업데이트 처리하는 로직을 제공한다.

## 2. MVC를 지키면서 코딩하는 5가지 규칙

1. **Model은 Controller와 View에 의존하지 않아야 된다.**
- 의존하지 않아야 된다 = 모델 내부에 컨트롤러, 뷰에 관련된 코드가 있으면 안된다.
- 모델 클래스에서 컨트롤러와 뷰의 클래스를 import해서 사용하면 안된다.

2. **View에는 Model에만 의존해야 하고, Controller에는 의존하면 안된다.
- View 내부에 Model의 코드만 있을 수 있고, Controller의 코드가 있으면 안된다.

3. **View가 Model로부터 데이터를 받을 때는, 사용자마다 다르게 보여주어야 하는 데이터에 대해서만 받아야 한다.**

4. **Controller는 Model과 View에 의존해도 된다.**
- Controller 내부에는 Model과 View의 코드가 있을 수 있다. 왜냐하면 컨트롤러는 <br>
**모델과 뷰의 중개자 역할을 하면서 전체 로직을 구성하기 때문이다**

5. **View가 Model로부터 데이터를 받을 때, 반드시 Controller에서 받아야 한다.**

## 3. MTV란?

📌 **MTV**: 장고는 **MVC**를 기반으로 한 프레임워크지만, 장고에서는 같은 개념은 **MTV**라고 부르며 **MVC**와 유사하다.
- **MVC**에서 **M**은 **MTV**에서 **Moldel**과 유사하다.
- **MVC**에서 **V**는 **MTV**에서 **Template**과 유사하다.
- **MVC**에서 **C**는 **MTV**에서 **View**와 유사하다.

```hash
장고로 만든 웹 사이트는 Model로 자료의 형태를 정의하고,
View로 어떤 자료를 어떤 동작으로 보여줄지 정의하고,
Template으로 웹 페이지에서 출력할 모습을 정의한다.
```

---

# ✔ Migration 이해하기

## 1. Migration이란?

📌 **Migration**: Model의 변경 내역(필드 추가, 모델 삭제 등)을 **데이터베이스 스키마**에 적용시키는 장고의 방법.<br>
장고는 **ORM**을 사용하기 때문에 models.py와 클래스를 통해 DB 스키마를 생성하고 컨트롤하게 되는데,<br>
이 때 DB 스키마를 git처럼 버전으로 나눠서 관리할 수 있게 해주는 시스템이라 생각하면 된다.

Django 모델 클래스로부터 테이블을 생성하기 위해서는 크게 **Migration을 준비하는 과정**과 **이를 적용하는 과정**으로 나뉘는데,<br>
구체적으로 다음과 같은 절차를 따른다.
- settings.py 파일 안의 **INSTALLED_APPS 리스트**에 **해당 Django App**을 추가한다.
- 모델 클래스로부터 테이블 스키마를 생성 혹은 수정하기 위해 `makemigrations`명령을 실행한다. <br>
이 명령이 실행되면 해당 Django App 안에 migrations라는 서브 폴더를 만들고 테이블 생성 및 수정을 위한 python migration 파일들을 생성한다.
- 모델 클래스로부터 실제 DB에 테이블을 생성하거나 수정하기 위해선 `migrate`명령을 실행한다. **이는 실제 Migration을 DB에 적용하는 명령이다.**


📌 **Schema**: 컴퓨터 과학에서 **DB Schma**는 DB에서 자료의 구조, 자료의 표현 방법, 자료 간의 관계를 형식 언어로 정의한 구조이다.<br>
++ 장고로 치면 한 어플리케이션의 models.py 파일이라고 볼 수 있다.

📌 **ORM**: DB와 객체 지향 프로그래밍 언어 간의 호환되지 않는 데이터를 변환하는 프로그래밍 기법. 객체 지향 언어에서 사용할 수 있는 가상 객체 DB를 구축하는 방법이다. <br>
즉, 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑해주는 것을 말한다.
- 객체 지향 프로그래밍은 **클래스**를 사용하고, 관계형 데이터베이스는 **테이블**을 사용한다.
- 객체 모델과 관계형 모델 간에 불일치가 존재한다.
- **ORM**을 통해 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하여 불일치를 해결한다.

Django에서 Model 클래스를 생성하고 난 후, 해당 Model에 상응하는 테이블을 데이터베이스에서 생성할 수 있다.<br>
Python 모델 클래스의 수정 및 생성을 DB에 적용하는 과정을 Migration이라 한다. <br>
이는 Django가 기본적으로 제공하는 ORM서비스를 통해 진행된다.

## 2. Migration command

- `migrate` : migration을 적용하거나 적용 해제한다.<br>
(migrate, which is responsible for applying and unapplying migrations.)

- `makemigrations`: model에 적용한 변화를 기반으로 새로운 migrations를 만든다.<br>
(makemigrations, which is responsible for creating new migrations based on the changes you have made to your models.)

- `sqlmigrate`: migration에 대한 SQL statements를 보여준다.<br>
(sqlmigrate, which displays the SQL statements for a migration.)

- `showmigrations`: 프로젝트의 migration list들과 그들의 상태를 보여준다.<br>
(showmigrations, which lists a project’s migrations and their status.)



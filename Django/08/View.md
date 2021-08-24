# ✏ Generic View 정리

## 1. Generic display views

📌 **Generic display views**: 두 개의 일반적인 클래스 기반의 View(**ListView, DetailView**)는 데이터를 display하도록 설계되었다.<br>
많은 프로젝트에서 일반적으로 가장 흔하게 사용되는 View이다.

1. **ListView**: 조건에 맞는 객체들의 목록을 보여주는 view이다.
- `setup(request, *args, **kwargs)`: **dispatch()** 전에 초기화를 수행한다. 이 메서드를 **재정의하는 경우 super()를 호출**해야 한다.
- `dispatch(request, *args, **kwargs)`: 요청을 받고 HTTP 응답을 반환하는 메서드이다. **GET 요청은 get()으로**, **POST요청은 post() 메서드로** 호출한다.
- `http_method_not_allowed(request, *args, **kwargs)`: View가 지원하지 않는 HTTP 메서드를 호출한 경우, **http_method_not_allowed()** 메서드가 대신 호출된다.
- `get_template_names()`: template을 rendering할 때 검색할 template 이름 목록을 반환한다. 발견된 첫 번째 template이 사용된다.
- `get_queryset()`: 기본적으로 모델의 모든 객체들을 전부 반환하며, 클래스 변수 queryset이 지정되어 있으면 그 queryset에 맞게 객체를 return한다.
++ QuerySet: 전달받은 모델의 객체 목록을 말한다. 데이터베이스로부터 데이터를 읽고 필터를 걸거나 정렬 등을 할 수 있다. 쿼리셋은 데이터베이스의 여러 레코드를 나타낸다.<br>
++ **get_queryset()와 queryset의 차이**: **queryse**t은 request발생 시 한번만 쿼리셋이 동작하지만, **get_queryset()은** 모든 request마다 동작한다.
- `get_context_object_name(object_list)`
- `get_context_data(**kwargs)`: model의 이름으로 context를 넘겨주는 역할이며, model 이름 외에도 object라는 이름으로도 사용이 가능하다.
- `get(request, *args, **kwargs)`: context에 object_list를 추가한다. 만약 allow_empty가 True이면 빈 목록을 보여준다. 만약 allow_empty가 False이면 404 오류를 발생시킨다.
- `render_to_response(context, **response_kwargs)`

2. **DetailView**: 조건에 맞는 하나의 세부 객체들을 보여주는 view이다.
- `setup(request, *args, **kwargs)`
- `dispatch(request, *args, **kwargs)`
- `http_method_not_allowed(request, *args, **kwargs)`
- `get_template_names()`
- `get_slug_field()`: slug field값을 반환한다.
- `get_queryset()`
- `get_object(queryset=None)`: object를 얻어오는 메소드이다. 만약 queryset이 있다면, 그 queryset이 objects의 source로 사용될 수도 있다.
- `get_context_object_name(object_list)`
- `get_context_data(**kwargs)`
- `get(request, *args, **kwargs)`
- `render_to_response(context, **response_kwargs)`

참고: [Django Documentation](https://docs.djangoproject.com/en/3.2/ref/class-based-views/generic-display/)

---

## 2. Generic editing views

1. **FormView**: Form이 주어지면 해당 Fomr을 출력하는 view이다.

2. **CreateView**: 새로운 객체 Form을 출력하는 view이다.

3. **UpdateView**: 기존의 객체를 수정하는 Form을 출력하는 view이다.

4. **DeleteView**: 기존에 있는 객체를 삭제하는 Fomr을 출력하는 view이다.

✔ (08/24. **form_valid**에 대해 공부한 후 추가 사항)

CreateView, UpdateView는 **django.views.generic.edit.ModelFormMixin**를 상속받는다.

- get_form_class()
- get_form_kwargs(): 현재 인스턴스(self.object)를 표준 get_form_kwargs()로 추가.
- get_success_url(): form이 성공적으로 유효성이 검사될 때 보내주기(redirect)위한 url을 결정한다. 만약 django.views.generic.edit.ModelFormMixin.success_url이 제공된다면 이를 return하고, 그렇지 않다면 객체의 get_absolute_url()을 사용하는 것을 시도한다. 
- **form_valid(form)**: form 인스턴스를 저장하고, get_success_url()로 보내줌(redirect).
- form_invalid(form): form이 유효하지 않다면 렌더링한다.

---

## 3. Base View

1. **View**: 최상위에 있는 부모 제네릭 뷰 클래스이다.

2. **Template View**: 주어진 template으로 rendering해주는 view이다.

3. **Redirect View**: 주어진 URL로 Redirect해주는 view이다.

---

## 4. Generic Date View

1. **ArchiveIndexView**: **가장 최신**에 해당하는 객체를 모아준다.

2. **YearArchiveView**: **주어진 연도**에 해당하는 객체를 모아준다.

3. **MonthArchiveView **: **주어진 월**에 해당하는 객체를 모아준다.

4. **WeekArchiveView**: **주어진 주**에 해당하는 객체를 모아준다.

5. **DayArchiveView**: **주어진 날짜**에 해당하는 객체를 모아준다.

6. **TodayArchiveView**: **오늘 날짜**에 해당하는 객체를 모아준다.

7. **DateDetailView**: **특정한 연,월,일 등**에 해당하는 객체를 모아준다.

---

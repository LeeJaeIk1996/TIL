# โ Generic View ์ ๋ฆฌ

## 1. Generic display views

๐ **Generic display views**: ๋ ๊ฐ์ ์ผ๋ฐ์ ์ธ ํด๋์ค ๊ธฐ๋ฐ์ View(**ListView, DetailView**)๋ ๋ฐ์ดํฐ๋ฅผ displayํ๋๋ก ์ค๊ณ๋์๋ค.<br>
๋ง์ ํ๋ก์ ํธ์์ ์ผ๋ฐ์ ์ผ๋ก ๊ฐ์ฅ ํํ๊ฒ ์ฌ์ฉ๋๋ View์ด๋ค.

1. **ListView**: ์กฐ๊ฑด์ ๋ง๋ ๊ฐ์ฒด๋ค์ ๋ชฉ๋ก์ ๋ณด์ฌ์ฃผ๋ view์ด๋ค.
- `setup(request, *args, **kwargs)`: **dispatch()** ์ ์ ์ด๊ธฐํ๋ฅผ ์ํํ๋ค. ์ด ๋ฉ์๋๋ฅผ **์ฌ์ ์ํ๋ ๊ฒฝ์ฐ super()๋ฅผ ํธ์ถ**ํด์ผ ํ๋ค.
- `dispatch(request, *args, **kwargs)`: ์์ฒญ์ ๋ฐ๊ณ  HTTP ์๋ต์ ๋ฐํํ๋ ๋ฉ์๋์ด๋ค. **GET ์์ฒญ์ get()์ผ๋ก**, **POST์์ฒญ์ post() ๋ฉ์๋๋ก** ํธ์ถํ๋ค.
- `http_method_not_allowed(request, *args, **kwargs)`: View๊ฐ ์ง์ํ์ง ์๋ HTTP ๋ฉ์๋๋ฅผ ํธ์ถํ ๊ฒฝ์ฐ, **http_method_not_allowed()** ๋ฉ์๋๊ฐ ๋์  ํธ์ถ๋๋ค.
- `get_template_names()`: template์ renderingํ  ๋ ๊ฒ์ํ  template ์ด๋ฆ ๋ชฉ๋ก์ ๋ฐํํ๋ค. ๋ฐ๊ฒฌ๋ ์ฒซ ๋ฒ์งธ template์ด ์ฌ์ฉ๋๋ค.
- `get_queryset()`: ๊ธฐ๋ณธ์ ์ผ๋ก ๋ชจ๋ธ์ ๋ชจ๋  ๊ฐ์ฒด๋ค์ ์ ๋ถ ๋ฐํํ๋ฉฐ, ํด๋์ค ๋ณ์ queryset์ด ์ง์ ๋์ด ์์ผ๋ฉด ๊ทธ queryset์ ๋ง๊ฒ ๊ฐ์ฒด๋ฅผ returnํ๋ค.
++ QuerySet: ์ ๋ฌ๋ฐ์ ๋ชจ๋ธ์ ๊ฐ์ฒด ๋ชฉ๋ก์ ๋งํ๋ค. ๋ฐ์ดํฐ๋ฒ ์ด์ค๋ก๋ถํฐ ๋ฐ์ดํฐ๋ฅผ ์ฝ๊ณ  ํํฐ๋ฅผ ๊ฑธ๊ฑฐ๋ ์ ๋ ฌ ๋ฑ์ ํ  ์ ์๋ค. ์ฟผ๋ฆฌ์์ ๋ฐ์ดํฐ๋ฒ ์ด์ค์ ์ฌ๋ฌ ๋ ์ฝ๋๋ฅผ ๋ํ๋ธ๋ค.<br>
++ **get_queryset()์ queryset์ ์ฐจ์ด**: **queryse**t์ request๋ฐ์ ์ ํ๋ฒ๋ง ์ฟผ๋ฆฌ์์ด ๋์ํ์ง๋ง, **get_queryset()์** ๋ชจ๋  request๋ง๋ค ๋์ํ๋ค.
- `get_context_object_name(object_list)`
- `get_context_data(**kwargs)`: model์ ์ด๋ฆ์ผ๋ก context๋ฅผ ๋๊ฒจ์ฃผ๋ ์ญํ ์ด๋ฉฐ, model ์ด๋ฆ ์ธ์๋ object๋ผ๋ ์ด๋ฆ์ผ๋ก๋ ์ฌ์ฉ์ด ๊ฐ๋ฅํ๋ค.
  - โ (08/29. **get_context_data** ์ ๋ํด ๊ณต๋ถํ ํ ์ถ๊ฐ ์ฌํญ)
  
  ```python
  def get_context_data(self, **kwargs):
    context = super(PostList, self).get_context_data()
    context['categories'] = Category.objects.all()
    context['no_category_post_count'] = Post.objects.filter(category=None).count()
    
    return
  ```
  
  ```hash
  1. context = super(PostList, self).get_context_data()๋ก 
     get_context_data์์ ๊ธฐ์กด์ ์ ๊ณตํ๋ ๊ธฐ๋ฅ์ ๊ทธ๋๋ก ๊ฐ์ ธ์ context์ ์ ์ฅ.
  2. ์ํ๋ ์ฟผ๋ฆฌ์์ ๋ง๋ค์ด ๋์๋๋ฆฌ ํํ๋ก context์ ๋ด์(QuerySet: ์ ๋ฌ๋ฐ์ ๋ชจ๋ธ์ ๊ฐ์ฒด ๋ชฉ๋ก)
  ```

- `get(request, *args, **kwargs)`: context์ object_list๋ฅผ ์ถ๊ฐํ๋ค. ๋ง์ฝ allow_empty๊ฐ True์ด๋ฉด ๋น ๋ชฉ๋ก์ ๋ณด์ฌ์ค๋ค. ๋ง์ฝ allow_empty๊ฐ False์ด๋ฉด 404 ์ค๋ฅ๋ฅผ ๋ฐ์์ํจ๋ค.
- `render_to_response(context, **response_kwargs)`

2. **DetailView**: ์กฐ๊ฑด์ ๋ง๋ ํ๋์ ์ธ๋ถ ๊ฐ์ฒด๋ค์ ๋ณด์ฌ์ฃผ๋ view์ด๋ค.
- `setup(request, *args, **kwargs)`
- `dispatch(request, *args, **kwargs)`
- `http_method_not_allowed(request, *args, **kwargs)`
- `get_template_names()`
- `get_slug_field()`: slug field๊ฐ์ ๋ฐํํ๋ค.
- `get_queryset()`
- `get_object(queryset=None)`: object๋ฅผ ์ป์ด์ค๋ ๋ฉ์๋์ด๋ค. ๋ง์ฝ queryset์ด ์๋ค๋ฉด, ๊ทธ queryset์ด objects์ source๋ก ์ฌ์ฉ๋  ์๋ ์๋ค.
- `get_context_object_name(object_list)`
- `get_context_data(**kwargs)`
- `get(request, *args, **kwargs)`
- `render_to_response(context, **response_kwargs)`

์ฐธ๊ณ : [Django Documentation](https://docs.djangoproject.com/en/3.2/ref/class-based-views/generic-display/)

---

## 2. Generic editing views

1. **FormView**: Form์ด ์ฃผ์ด์ง๋ฉด ํด๋น Fomr์ ์ถ๋ ฅํ๋ view์ด๋ค.

2. **CreateView**: ์๋ก์ด ๊ฐ์ฒด Form์ ์ถ๋ ฅํ๋ view์ด๋ค.

3. **UpdateView**: ๊ธฐ์กด์ ๊ฐ์ฒด๋ฅผ ์์ ํ๋ Form์ ์ถ๋ ฅํ๋ view์ด๋ค.

4. **DeleteView**: ๊ธฐ์กด์ ์๋ ๊ฐ์ฒด๋ฅผ ์ญ์ ํ๋ Form์ ์ถ๋ ฅํ๋ view์ด๋ค.

โ (08/24. **form_valid**์ ๋ํด ๊ณต๋ถํ ํ ์ถ๊ฐ ์ฌํญ)

```hash
 CreateView, UpdateView๋ **django.views.generic.edit.ModelFormMixin**๋ฅผ ์์๋ฐ๋๋ค.

 1. get_form_class()
 2. get_form_kwargs(): ํ์ฌ ์ธ์คํด์ค(self.object)๋ฅผ ํ์ค get_form_kwargs()๋ก ์ถ๊ฐ.
 3. get_success_url(): form์ด ์ฑ๊ณต์ ์ผ๋ก ์ ํจ์ฑ์ด ๊ฒ์ฌ๋  ๋ ๋ณด๋ด์ฃผ๊ธฐ(redirect)์ํ url์ ๊ฒฐ์ ํ๋ค. 
    ๋ง์ฝ django.views.generic.edit.ModelFormMixin.success_url์ด ์ ๊ณต๋๋ค๋ฉด ์ด๋ฅผ returnํ๊ณ , 
    ๊ทธ๋ ์ง ์๋ค๋ฉด ๊ฐ์ฒด์ get_absolute_url()์ ์ฌ์ฉํ๋ ๊ฒ์ ์๋ํ๋ค. 
 4. form_valid(form): form ์ธ์คํด์ค๋ฅผ ์ ์ฅํ๊ณ , get_success_url()๋ก ๋ณด๋ด์ค(redirect).
 5. form_invalid(form): form์ด ์ ํจํ์ง ์๋ค๋ฉด ๋ ๋๋งํ๋ค.
```

---

## 3. Base View

1. **View**: ์ต์์์ ์๋ ๋ถ๋ชจ ์ ๋ค๋ฆญ ๋ทฐ ํด๋์ค์ด๋ค.

2. **Template View**: ์ฃผ์ด์ง template์ผ๋ก renderingํด์ฃผ๋ view์ด๋ค.

3. **Redirect View**: ์ฃผ์ด์ง URL๋ก Redirectํด์ฃผ๋ view์ด๋ค.

---

## 4. Generic Date View

1. **ArchiveIndexView**: **๊ฐ์ฅ ์ต์ **์ ํด๋นํ๋ ๊ฐ์ฒด๋ฅผ ๋ชจ์์ค๋ค.

2. **YearArchiveView**: **์ฃผ์ด์ง ์ฐ๋**์ ํด๋นํ๋ ๊ฐ์ฒด๋ฅผ ๋ชจ์์ค๋ค.

3. **MonthArchiveView **: **์ฃผ์ด์ง ์**์ ํด๋นํ๋ ๊ฐ์ฒด๋ฅผ ๋ชจ์์ค๋ค.

4. **WeekArchiveView**: **์ฃผ์ด์ง ์ฃผ**์ ํด๋นํ๋ ๊ฐ์ฒด๋ฅผ ๋ชจ์์ค๋ค.

5. **DayArchiveView**: **์ฃผ์ด์ง ๋ ์ง**์ ํด๋นํ๋ ๊ฐ์ฒด๋ฅผ ๋ชจ์์ค๋ค.

6. **TodayArchiveView**: **์ค๋ ๋ ์ง**์ ํด๋นํ๋ ๊ฐ์ฒด๋ฅผ ๋ชจ์์ค๋ค.

7. **DateDetailView**: **ํน์ ํ ์ฐ,์,์ผ ๋ฑ**์ ํด๋นํ๋ ๊ฐ์ฒด๋ฅผ ๋ชจ์์ค๋ค.

---

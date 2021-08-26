# ✏ Model Field Types, Relation Types 정리

## 1. Model Field Types

- primary key: AutoField, BigAutoField<br>
🏷 `AutoField`: **pk**로 사용 가능한 자동으로 증가하는 IntegerField다.<br>
(**모델의 primary key 필드는 별도로 지정하지 않을 경우 자동으로 추가된다.**)

- 문자열: **CharField**, **TextField**, SlugField

- 날짜, 시간: DateField, TimeField, **DateTimeField**, DurationField<br>
🏷 `DateTimeField`: 옵션으로 **auto_now**와 **auto_now_add**가 있다.
  - **auto_now**: 모델이 **저장될 때 마다** 매번 자동으로 현재 시간이 설정된다.
  - **auto_now_add**: 모델이 **처음 생성될 때** 자동으로 현재 시간이 설정된다.

  🏷 `DurationField`: 시간주기를 위한 필드이며, Python에서 timedelta로 모델링한다.

- 참, 거짓: BooleanField, NullBooleanField

- 숫자: **IntegerField**, SmallIntegerField, PostiveIntegerField, PostiveSmallIntegerField, BigIntegerField, DecimalField, FloatField

- 파일: BinaryField, **FileField**, **ImageField**, FilePathField<br>
🏷 `ImageField`를 넣고 migration을 할 경우 **Pillow가 설치되어 있지 않아 ImageField를 사용할 수 없다**는 오류 메시지가 나온다.<br>
**Pillow**는 Python에서 이미지를 처리하기 위한 라이브러리로, `python -m pip install Pillow`를 통해 Pillow를 설치해야 한다.

- 이메일: **EmailField**<br>
🏷 `EmailField`: 유효한 이메일 주소인지 체크하는 CharField이다. 입력값을 검증하는데 EmailValidator를 사용한다.<br>
EmailValidator 참고: [Django EmailValidator](https://docs.djangoproject.com/en/3.2/ref/validators/#emailvalidator)

- URL: URLField<br>
🏷 `URLField`: 주소를 받을 때 사용. URL을 위한 필드이다.

- UUID: UUIDField<br>
🏷 `UUIDField`: universally unique identifiers를 저장하기 위한 필드다. 

- IP: GenericIPAddressField<br>
🏷 `GenericIPAddressField`: 문자열 형식에 IPv4 나 IPv6 주소이다.




---

## 2. Relation Types

- ForeignKey

- ManyToManyField

- OneToOneField

---

## 3. Field Options

- null 옵션: NULL 허용 여부(기본값: False)

- unique 옵션: 유일성 여부(기본값: False)

- blank 옵션: 입력값 유효성(validation) 검사 시에 empty 허용(기본값: False)

- default : 디폴트 값 지정(혹은 return해줄 함수 지정)

- verbose_name: 필드 레이블. 미지정시 필드명 사용

- validators: 입력값 유효성 검사를 수행할 함수를 다수 지정

- choices: select 박스 사용 시 select box 소스로 사용

- help_text: 필드 입력 도움말

- auto_now_add: 레코드 생성 시, 현재 시간으로 자동 저장

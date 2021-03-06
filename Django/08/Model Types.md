# โ Model Field Types, Relation Types ์ ๋ฆฌ

## 1. Model Field Types

- primary key: AutoField, BigAutoField<br>
๐ท `AutoField`: **pk**๋ก ์ฌ์ฉ ๊ฐ๋ฅํ ์๋์ผ๋ก ์ฆ๊ฐํ๋ IntegerField๋ค.<br>
(**๋ชจ๋ธ์ primary key ํ๋๋ ๋ณ๋๋ก ์ง์ ํ์ง ์์ ๊ฒฝ์ฐ ์๋์ผ๋ก ์ถ๊ฐ๋๋ค.**)

- ๋ฌธ์์ด: **CharField**, **TextField**, SlugField

- ๋ ์ง, ์๊ฐ: DateField, TimeField, **DateTimeField**, DurationField<br>
๐ท `DateTimeField`: ์ต์์ผ๋ก **auto_now**์ **auto_now_add**๊ฐ ์๋ค.
  - **auto_now**: ๋ชจ๋ธ์ด **์ ์ฅ๋  ๋ ๋ง๋ค** ๋งค๋ฒ ์๋์ผ๋ก ํ์ฌ ์๊ฐ์ด ์ค์ ๋๋ค.
  - **auto_now_add**: ๋ชจ๋ธ์ด **์ฒ์ ์์ฑ๋  ๋** ์๋์ผ๋ก ํ์ฌ ์๊ฐ์ด ์ค์ ๋๋ค.

  ๐ท `DurationField`: ์๊ฐ์ฃผ๊ธฐ๋ฅผ ์ํ ํ๋์ด๋ฉฐ, Python์์ timedelta๋ก ๋ชจ๋ธ๋งํ๋ค.

- ์ฐธ, ๊ฑฐ์ง: BooleanField, NullBooleanField

- ์ซ์: **IntegerField**, SmallIntegerField, PostiveIntegerField, PostiveSmallIntegerField, BigIntegerField, DecimalField, FloatField

- ํ์ผ: BinaryField, **FileField**, **ImageField**, FilePathField<br>
๐ท `ImageField`๋ฅผ ๋ฃ๊ณ  migration์ ํ  ๊ฒฝ์ฐ **Pillow๊ฐ ์ค์น๋์ด ์์ง ์์ ImageField๋ฅผ ์ฌ์ฉํ  ์ ์๋ค**๋ ์ค๋ฅ ๋ฉ์์ง๊ฐ ๋์จ๋ค.<br>
**Pillow**๋ Python์์ ์ด๋ฏธ์ง๋ฅผ ์ฒ๋ฆฌํ๊ธฐ ์ํ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ก, `python -m pip install Pillow`๋ฅผ ํตํด Pillow๋ฅผ ์ค์นํด์ผ ํ๋ค.

- ์ด๋ฉ์ผ: **EmailField**<br>
๐ท `EmailField`: ์ ํจํ ์ด๋ฉ์ผ ์ฃผ์์ธ์ง ์ฒดํฌํ๋ CharField์ด๋ค. ์๋ ฅ๊ฐ์ ๊ฒ์ฆํ๋๋ฐ EmailValidator๋ฅผ ์ฌ์ฉํ๋ค.<br>
EmailValidator ์ฐธ๊ณ : [Django EmailValidator](https://docs.djangoproject.com/en/3.2/ref/validators/#emailvalidator)

- URL: URLField<br>
๐ท `URLField`: ์ฃผ์๋ฅผ ๋ฐ์ ๋ ์ฌ์ฉ. URL์ ์ํ ํ๋์ด๋ค.

- UUID: UUIDField<br>
๐ท `UUIDField`: universally unique identifiers๋ฅผ ์ ์ฅํ๊ธฐ ์ํ ํ๋๋ค. 

- IP: GenericIPAddressField<br>
๐ท `GenericIPAddressField`: ๋ฌธ์์ด ํ์์ IPv4 ๋ IPv6 ์ฃผ์์ด๋ค.




---

## 2. Relation Types

- ForeignKey

- ManyToManyField

- OneToOneField

---

## 3. Field Options

- null ์ต์: NULL ํ์ฉ ์ฌ๋ถ(๊ธฐ๋ณธ๊ฐ: False)

- unique ์ต์: ์ ์ผ์ฑ ์ฌ๋ถ(๊ธฐ๋ณธ๊ฐ: False)

- blank ์ต์: ์๋ ฅ๊ฐ ์ ํจ์ฑ(validation) ๊ฒ์ฌ ์์ empty ํ์ฉ(๊ธฐ๋ณธ๊ฐ: False)

- default : ๋ํดํธ ๊ฐ ์ง์ (ํน์ returnํด์ค ํจ์ ์ง์ )

- verbose_name: ํ๋ ๋ ์ด๋ธ. ๋ฏธ์ง์ ์ ํ๋๋ช ์ฌ์ฉ

- validators: ์๋ ฅ๊ฐ ์ ํจ์ฑ ๊ฒ์ฌ๋ฅผ ์ํํ  ํจ์๋ฅผ ๋ค์ ์ง์ 

- choices: select ๋ฐ์ค ์ฌ์ฉ ์ select box ์์ค๋ก ์ฌ์ฉ

- help_text: ํ๋ ์๋ ฅ ๋์๋ง

- auto_now_add: ๋ ์ฝ๋ ์์ฑ ์, ํ์ฌ ์๊ฐ์ผ๋ก ์๋ ์ ์ฅ

## 리스트 자료형

**1. 리스트 연산**

![cal](https://user-images.githubusercontent.com/84573261/126638186-ebac4b6a-a370-4ea5-b9f6-082386043ff1.PNG)

**2. 리스트 수정&삭제**

![del](https://user-images.githubusercontent.com/84573261/126638373-1bec4af1-bb73-4b9f-b7bb-07d2b0c16430.PNG)

- `del 객체` → 객체: Python에서 사용되는 모든 Data Type.<br>
삭제는 `del 객체` 외에도 `remove`와 `pop`을 사용한 방식도 있다.

**3. 리스트 관련 함수**

![fx](https://user-images.githubusercontent.com/84573261/126639936-717b7547-44c1-463c-86a9-ac82be1b0605.PNG)

- `append`: **append(x)** 는 리스트의 맨 마지막에 x를 추가하는 함수
- `sort`: 리스트의 요소를 순서대로 정렬. 문자 역시 알파벳 순서로 정렬 가능
- `reverse`: 현재의 리스트를 그대로 거꾸로 뒤집음
- `index`: 리스트에 x값이 있으면 x의 **위치 값**을 돌려줌
- `insert`: **insert(a,b)** 는 리스트의 a번째 위치에 b를 삽입하는 함수
- `remove`: **remove(x)** 는 리스트에서 첫 번째로 나오는 x를 삭제하는 함수
- `pop`: 리스트의 맨 마지막 요소를 돌려주고 그 요소는 삭제. **pop(x)** 는 리스트의 x번째 요소를 돌려주고 그 요소는 삭제한다.
- `count`: **count(x)** 는 리스트 안에 x가 몇 개 있는지 조사하여 그 개수를 돌려주는 함수
- `extend`: **extend(x)** 에서 x는 리스트만 올 수 있으며 원래의 a 리스트에 x 리스트를 더하게 된다.

---

## 튜플 자료형

**1. 튜플 vs 리스트**

- 튜플: 1개의 요소만을 가질 때 요소 뒤에 콤마(,)를 반드시 붙여야 하며, ()로 둘러싼다.
- 튜플과 리스트의 차이점: **값을 변화시킬 수 있는가(생성,삭제,수정)** 없는가.

**2. 튜플 다루기**

- 인덱싱&슬라이싱 (o)
- 더하기&곱하기&길이 구하기 (o)

---

## 딕셔너리 자료형

**1. 딕셔너리**

- **딕셔너리**: **Key + Value**를 한 쌍으로 갖는 자료형
- 리스트나 튜플처럼 **순차적으로 해당 요솟값을 구하지 않고** Key를 통해 Value를 얻음
- Value에 리스트도 넣을 수 있음(ex: `a = { 'a': [1,2,3]}`). 하지만 Key에 리스트를 넣을 순 없음.
- Key는 고유한 값이므로 중복되는 Key값을 설정해 놓으면 하나를 제외한 나머지는 모두 무시된다.

**2. 딕셔너리 쌍 추가, 삭제**

![image](https://user-images.githubusercontent.com/84573261/126645953-a4681f6d-0cf2-42c6-9521-f8da1ad901a1.png)

- `del a[1]`

**3. 딕셔너리 관련 함수**

![fx2](https://user-images.githubusercontent.com/84573261/126647373-3dcc21c1-1380-49f0-b2df-21d0713009e1.PNG)

- `.keys()`: **Key 리스트 만들기**. key만을 모아서 **dict_keys**객체를 돌려준다.
- `.values()`: **Value 리스트 만들기**. value만을 모아서 **dict_values**객체를 돌려준다.
- `.items()`: Key와 Value의 쌍을 **튜플**로 묶은 값을 **dict_items**객체로 돌려준다.
- `.clear()`: Key:Value쌍 **모두** 지우기
- `.get(key)`: Key로 Value값 얻기. **변수[key]를 사용했을 때와 동일하게 Value값을 돌려 받는다.**
- `in`: 해당 Key가 딕셔너리 안에 있는지 조사

---






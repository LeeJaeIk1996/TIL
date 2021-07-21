# 배열

## 1. 배열과 구성요소, 구성요솟수

**(1) 배열**: 같은 자료형의 변수로 이루어진 구성 요소(component)가 모인 것을 말함.<br>
  ex) `int[] a = new int[5];`
 
**(2) 구성 요소**: 배열 변수 이름[인덱스] <br>
  ex) 구성 요소가 n개인 배열의 구성 요소: `a[0]`, `a[1]`, ... `a[n-1]`
  
  ++ **배열의 구성 요소는 자동으로 0으로 초기화되는 규칙이 있다.**
 
 
**(3) 구성 요솟수**: 배열 변수 이름.length <br>
  ex) `a.length`
  
**(4) 배열의 요솟값을 초기화하며 배열 선언**: 배열 본체는 배열 초기화를 사용하면 배열 본체의 생성과 동시에 각 요소의 초기화가 가능하다.<br>
  ex) `int[] a = new int[]{1,2,3,4,5};`
  
**그 외 배열의 복제(clone)**: clone 메서드를 호출하여 만들 수 있다.<br>
  ex) `a.clone()`
 
 ---
 
 ## 2. 기본적인 배열 코드 예시
 
 ```java
 package array;

public class IntArray {

	public static void main(String[] args) {
		int[] a = new int[5];
		
		a[1] = 37;
		a[2] = 51;
		a[4] = a[1] * 2;
		
		for (int i=0; i<a.length; i++) {
			System.out.println("a[" + i + "] = " + a[i]);
		}

	}

}
```

위의 코드를 보면 `a.length=5`에서 `a[1]`과 `a[2]`, `a[4]`만 값이 있는 것을 확인할 수 있는데,<br>
이를 출력하면 남은 `a[0]`, `a[3]`은 값이 0으로 나오는 것을 확인할 수 있다.<br>
(**배열의 구성 요소는 자동으로 0으로 초기화되는 규칙이 있기 때문**)

![zero](https://user-images.githubusercontent.com/84573261/126479444-6f6dd5b0-0e09-40d4-bd69-47a6065a753a.PNG)

 ---
 
 ## 3. 배열 요소의 최댓값 구하기
 
 ```hash
 max = a[0];
 if(a[1] > max) max = a[1];
 if(a[2] > max) max = a[2];
 ```
 
 위와 같이 **요소 개수가 n이면 if문을 n-1개 작성**해야 한다.
 
 예시 코드는 다음과 같다.
 
 ```java
package array;
import java.util.Scanner;

//배열 요소의 최댓값을 나타낸다.
public class MaxOfArray {
	
  //배열 a의 최댓값을 구하여 반환.
	static int maxOf(int[] a) {
		int max = a[0];
		for (int i = 1; i <a.length; i ++) {
			if(a[i] > max)
				max = a[i];
		}
		return max;
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		
		System.out.println("키 최댓값을 구합니다");
		System.out.print("사람 수: ");
		int num = stdIn.nextInt();          //배열의 요솟수를 입력 받음.
		
		int[] height = new int[num];        //요솟수가 num인 배열을 생성.
		
		for(int i = 0; i <num; i++) {
			System.out.println("height[" + i + "] :" );
			height[i] = stdIn.nextInt();
		}

		System.out.println("최댓값은 " + maxOf(height) + "입니다.");
	}

}
```

++ 난수를 사용하여 배열의 요솟값을 설정하고 싶으면 `import java.util.Random;`을 활용한다.

---

## 4. 배열 요소를 역순으로 정렬

역순으로 정렬함에 있어 핵심은 다음과 같다.

![reverse](https://user-images.githubusercontent.com/84573261/126478579-e0e3f01d-5878-4923-a9aa-c2319d923c09.jpg)

```hash
t = a[idx1];
a[idx1] = a[idx2];
a[idx2] = t;
```

예시 코드는 다음과 같다.

```java
package array;
import java.util.Scanner;

//배열 역순으로 정렬
public class ReverseArray {

	// 배열 요소 a[idx1]과 a[idx2]의 값을 바꿈
	static void swap(int a[], int idx1, int idx2) {
		int t= a[idx1];
		a[idx1] = a[idx2];
		a[idx2] = t;
		
	}

	//배열 a의 요소를 역순으로 정렬
	static void reverse(int[] a) {
		for (int i= 0; i < a.length/2; i++) {
			swap(a, i, a.length-i-1);
		}
	}
	
	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		
		System.out.print("요솟수: ");
		int num = stdIn.nextInt();
		
		int[] x = new int[num];
		
		//배열 x의 값들을 입력
		for(int i=0; i<num; i++) {
			System.out.print("x[" + i + "] : ");
			x[i] = stdIn.nextInt();
		}
		
		reverse(x);
		
		System.out.println("요소 역순으로 정렬");
		for(int i=0; i<num; i++) {
			System.out.println("x[" + i + "] = " + x[i]);
		}
		
	}

}
```

---

## 5. 두 배열의 비교

두 배열의 "모든 요소의 값이 같은가"를 판단하는 메서드를 구현하였으며, <br>
메서드의 반환형(type)은 boolean형이다.

```java
package array;
import java.util.Scanner;

//두 배열이 같은가를 비교
public class ArrayEqual {

	//두 배열 a,b의 모든 요소가 같은가
	static boolean equals(int a[], int b[]) {
		if(a.length != b.length) {
			return false;
		}
		
		for(int i=0; i<a.length; i++) {
			if(a[i] != b[i]) {
				return false;
			}
		}
		
		return true;
	}
	
	
	public static void main(String[] args) {
	Scanner stdIn = new Scanner(System.in);
	
	System.out.print("배열 a의 요솟수");
	int na = stdIn.nextInt();
	
	int[] a = new int[na];
	
	for(int i=0; i<a.length; i++) {
		System.out.println("a[" + i + "] : ");
		a[i] = stdIn.nextInt();
	}
	
	System.out.print("배열 b의 요솟수");
	int nb = stdIn.nextInt();
	
	int[] b = new int[na];
	
	for(int i=0; i<b.length; i++) {
		System.out.println("b[" + i + "] : ");
		b[i] = stdIn.nextInt();
	}
	
	System.out.println("배열 a와 b는 " +
						(equals(a,b) ? "같습니다."
									: "같지 않습니다."));
		
	}

}
```






 

 
 

# 배열(Array)

---

## 1. 배열

> 같은 타입의 데이터를 연속된 공간에 나열시키고, 각 데이터에 인덱스(index)를 부여해 놓은 자료구조

- 학생 30명의 성적을 저장해야 한다면?
  - 변수 30개 필요
  - 코드 비효율적
  - 같은 타입의 많은 양의 데이터 관리 어려움
  >  그래서 배열 등장

---

## 2. 배열 선언

### (1) 실무에서 자주 사용

```java
자료형[] 변수;
```

```java
int[] intArray;
double[] doubleArray;
String[] strArray;
```

### (2) 다른 표현 방식

```java
자료형 변수[];
```

```java
int intArray[];
double doubleArray[];
String strArray[];
```

> 배열 변수는 **참조형** 이므로

```java
int[] arr = null;
```

---

## 3. 배열 생성

### 중괄호 의미

> 중괄호 `{}` 는 주어진 값들로 배열 객체를 Heap 영역에 생성하고  
> 그 객체의 **번지수(주소값)** 를 리턴한다.

---

### (1) 값 목록으로 생성

```java
String[] names = {"홍길동", "자바", "리눅스"};
```

| 인덱스 | 값 |
|--------|------|
| names[0] | 홍길동 |
| names[1] | 자바 |
| names[2] | 리눅스 |

값 변경:

```java
names[0] = "고길동";
```

---

### ⚠ 주의

이미 선언 후에는 중괄호 사용 불가

```java
String[] names;
names = {"홍길동", "자바"}; // 컴파일 에러
```

### 해결 방법

```java
names = new String[] {"홍길동", "자바"};
```

---

### (2) new 연산자 사용

```java
int[] intArray = new int[5];
```

- 5칸 확보
- 자동 기본값 초기화

---

### 자료형별 기본값

| 자료형 | 기본값 |
|--------|--------|
| int | 0 |
| double | 0.0 |
| boolean | false |
| char | '\u0000' |
| 참조형 | null |

---

## 4. 배열의 길이

```java
배열변수.length
```

```java
int[] arr = {10, 20, 30};
int size = arr.length; // 3
```

⚠ `length`는 읽기 전용

```java
arr.length = 10; // 오류
```

### 반복문에서 활용

```java
for(int i = 0; i < arr.length; i++){
    System.out.println(arr[i]);
}
```

> 인덱스 범위: `0 ~ (length - 1)`

초과 시:

```
ArrayIndexOutOfBoundsException
```

---

## 5. 커맨드 라인 입력

```java
public static void main(String[] args)
```

```
java 클래스 hello java
```

| 인덱스 | 값 |
|--------|------|
| args[0] | hello |
| args[1] | java |

---

## 6. 다차원 배열

```java
int[][] scores = new int[2][3];
```

- scores.length → 2
- scores[0].length → 3
- scores[1].length → 3

### 계단식 배열

```java
int[][] scores = new int[2][];
scores[0] = new int[2];
scores[1] = new int[3];
```

⚠ 정확한 길이 확인 필수

```java
scores[0][2]; // 오류
```

---

## 7. 객체를 참조하는 배열

```java
String[] strArray = new String[3];

strArray[0] = "Java";
strArray[1] = "C++";
strArray[2] = "C#";
```

> String 배열은 문자열 자체가 아니라 **객체 주소를 저장**

문자열 비교:

```java
strArray[0] == strArray[1];      // 주소 비교
strArray[0].equals(strArray[1]); // 값 비교
```

---

# 8. 배열 복사

배열은 생성 후 크기 변경 불가  
→ 더 큰 배열 필요 시 새 배열 생성 후 복사

---

## 8-1. 얕은 복사 (Shallow Copy)

```java
int[] origin = {1, 2, 3};
int[] copy = origin;
```

 > 주소값만 복사됨

```java
copy[1] = 99;

System.out.println(origin[1]); // 99 (원본도 바뀜)
```

주소 비교:

```java
System.out.println(origin == copy); // true
```

---

## 8-2. 깊은 복사 (Deep Copy)

### ① for문 이용

```java
int[] origin = {1, 2, 3};
int[] copy = new int[origin.length];

for(int i = 0; i < origin.length; i++){
    copy[i] = origin[i];
}
```

```java
System.out.println(origin == copy); // false
```

---

### ② System.arraycopy()

```java
System.arraycopy(origin, 0, copy, 0, origin.length);
```

매개변수 설명:

```
System.arraycopy(원본, 원본시작, 대상, 대상시작, 복사개수);
```

---

### ③ Arrays.copyOf()

```java
int[] copy = Arrays.copyOf(origin, origin.length);
```

- 두 번째 인자 = 새 배열의 크기

---

### ④ clone()

```java
int[] copy = origin.clone();
```

- 옵션 없이 전체 복사

---

## 배열 출력 팁

```java
System.out.println(Arrays.toString(origin));
```

출력:

```
[1, 2, 3]
```

---

## 참조 타입 배열 복사 주의

```java
String[] origin = {"A", "B"};
String[] copy = origin.clone();
```

> 배열은 깊은 복사되지만, 
내부 객체(String)는 같은 객체 참조

즉, **완전한 객체 복사는 아님**

---

> # 정리

| 구분 | 의미 |
|------|------|
| 얕은 복사 | 주소만 복사 |
| 깊은 복사 | 배열 실체 복사 |
| == | 주소 비교 |
| equals() | 값 비교 |
| length | 배열 크기 |
| Arrays.sort() | 정렬 |
| Arrays.toString() | 예쁜 출력 |

---

# 요약

> 배열은 "같은 타입의 데이터 묶음" 이며,  
> 복사 시에는 반드시 얕은 복사와 깊은 복사를 구분해야 한다.

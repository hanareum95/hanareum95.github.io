---
layout: post
title:  "[C++] Template"
subtitle:   "Template vs Generic"
categories: Programming
tags: C++ JAVA
comments: true
---

### Template

---

템플릿은 함수/클래스를 자동으로 생성한다.

<br/>



```c++
template<typename T>
T max(T a, T b)
{
  return (a > b ? a : b);
}

int main()
{
  int i1 = 5, i2 = 3;
  int i3 = max(i1, i2);
  
  double d1 = 0.9, d2 = 1.0;
  double d3 = max(d1, d2);
  
  return 0;
}
```
<br/>



### C++ vs Java

---
#### 1. 차이점

| C++ Template                             | Java Generic                             |
| ---------------------------------------- | ---------------------------------------- |
| int와 같은 기본 타입을 인자로 넘길 수 있다               | int와 같은 기본 타입을 인자로 넘길 수 없다.<br/>모든 타입은 객체를 상속해야 하며 따라서 int대신 Integer를 사용해야 한다. |
| 인자로 주어진 타입으로부터 객체를 만들어 낼 수 있다.           | 인자로 주어진 타입으로부터 객체를 만들어 낼 수 없다.           |
| -                                        | 실행시간에 타입 인자 정보는 삭제된다.                    |
| 다른 템플릿 타입 인자를 사용해 만든 객체는 서로 다른 타입의 객체이다. | generic 타입 인자가 무엇이냐에 관계없이 전부 동등한 타입이다.   |



####  2. Java 컴파일

- Java - 컴파일 전

  ```java
  ArrayList<String> list = new ArrayList<String>();
  list.add(new String("hello"));
  String str = list.get(0);
  ```

  <br/>

- Java - 컴파일 후

  ```java
  ArrayList list = new ArrayList();
  list.add(new String("hello"));
  String str = (String) list.get(0);
  ```

<br/>

> Generic은 타입제거라는 개념에 근거한다. 
>
> 이 기법은 소스코드를 JVM이 인식하는 바이트 코드로 변환할 때 인자로 주어진 타입을 제거하는 기술이다.
>
> Generic code 들은 컴파일 타임에 모두 제거되고 컴파일러가 자동으로 downcasting을 해준다.
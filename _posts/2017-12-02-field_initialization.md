---
layout: post
title:  "필드 초기화 (field initialization)"
date:   2017-12-02
desc: "Static block"
keywords: "java,initialization,jyeonie"
categories: [Java]
tags: [java,initialization,이것이자바다p.206,이것이자바다p.239]
icon: icon-html
---

------

클래스로부터 객체가 생성될 때 필드는 자동 초기화가 된다. 

만약 다른값으로 초기화를 하고 싶다면 여기 여러가지 방법들이 있다.

필드 선언시 초기값을 주게 되면 동일한 클래스로부터 생성되는 객체들은 모두 같은 데이터를 갖게된다. 객체 생성후 변경할 수 있지만, 객체 생성 시점에는 필드의 값이 모두 같다.

------

# 1. 자동 초기화

**객체 생성시 기본값으로 초기화** 되는 상태이다. 

- int자료형 -> 0
- double자료형 -> 0.0
- 참조자료형 (클래스, 열거형, 배열, 인터페이스) -> null

<br />

# 2. 명시적 초기화

**사용자가 값을 임의로 지정** 해서 초기화 하는 상태이다. **대입(=)연산자** 사용.

```java
public class Sample{
  private int a; //자동 초기화
  private int b = 10; // 명시적 초기화
  private static int c, d = 10;
  
  public int getA(){ //getter
    return this.a; 
  }
  public static int getC(){ //필드와 같은 성격을 가지기 위해 static 넣음.
    return Sample.c;
  }
}
```

<br />

<br />

# 3. 생성자에 의한 초기화

**인스턴스 필드** 에 대해서만 사용가능하다.

객체 생성 시점에 **외부자료에서 제공되는 값을 이용해서 초기화** 가 가능하다.

보통 **생성자의 매개변수 이름은 초기화 시킬 필드 이름과 동일** 하게 설정한다. **매개변수와 필드의 구분을 위해서 this.** 를 사용한다.*(참고: [인스턴스필드와 this](https://jyeonie.github.io/java/2017/11/26/%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%EB%A9%A4%EB%B2%84(Instance-Member)%EC%99%80-this.html))*

```java
public class Sample{
  private int a; // 인스턴스 필드
  public Sample(){ //기본 생성자
    this(10); //10으로 명시적 초기화 : 다른생성자에게 위임
  }
  public Sample(int a){ //매개변수 목록이 있는 생성자: 외부자료 이용해서 초기화
    this.a = a;
  }
  public int getA(){ //getter
    return this.a;
  }
}
```

<br />

<br />

# 4. static 초기화 블럭에 의한 초기화

**static 필드** 에 대해서만 사용 가능하다.

`static { static변수명 = 값; }`

```java
import java.util.Random;
public class Sample{
  private static int[] arr; //static 필드
  static{
    Sample.arr = new int[5]; //배열객체 생성
    Random random = new Random(); //랜덤객체 생성
    for(int i=0;i<arr.length;++i){
      Sample.arr[i] = random.nextInt(11); //배열에 0부터 10까지의 난수할당
    }
  }
  public static int[] getArr(){ //static getter
    return Sample.arr;
  }
}
```

```java
public class Main{
  public static void main(String[] args){
    int[] result = Sample.getArr(); //static 초기화 블럭에 의한 초기화 실행
    System.out.println(Arrays.toString(result)); //[난수1, 난수2, ...]
  }
}
```


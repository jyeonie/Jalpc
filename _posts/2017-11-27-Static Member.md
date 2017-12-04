---
layout: post
title:  "정적 멤버(Static Member)와 static"
date:   2017-11-26
desc: "정적 멤버(Static Member)와 static"
keywords: "java,static,jyeonie"
categories: [Java]
tags: [java,static,class,this,이것이자바다p.236]
icon: icon-html
---

------

정적(Static)은 '고정된' 이란 의미다. 정적 멤버는 **클래스에 고정된 멤버** 로서 **객체를 생성하지 않고 사용** 할 수 있는 필드와 메소드를 말한다. 이들을 각각 **정적 필드** , **정적 메소드** 라고 부른다.

정적 멤버는 객체(인스턴스)에 소속된 멤버가 아니라 **클래스에 소속된 멤버** 이기 때문에 **클래스 멤버** 라고도 한다.

정적(Static)멤버는 메모리에 적재되는 순서와 공유되는 범위가 instance 멤버와 다르다.

**instance 멤버는 객체 생성시에만 메모리에 적재** 되지만, **정적(static) 멤버는 프로그램 실행시 (객체 생성과 관계없이) 메모리에 적재** 되고 종료시 사라진다.

예를들어 2강의실이 메모리라고 치면, 수강생들은 instance 멤버(독립적)이다. 컴퓨터나 책상들은 변하지 않고 2강의실 메모리상에 계속 존재한다. 컴퓨터나 책상들은 여러 수강생들에게 **공유되는 존재** 이다. 이때 컴퓨터나 책상들이 static 멤버이다.

------

# 1. 선언

선언 시 **static** 키워드를 추가적으로 붙인다. 안 붙이면 instance 멤버가 된다.

클래스에 고정된 멤버이므로 클래스 로더가 클래스(바이트 코드)를 로딩해서 메소드 메모리 영역에 적재할 때 클래스별로 관리된다. 따라서 클래스의 로딩이 끝나면 바로 사용할 수 있다.

`[클래스]-----바이트코드읽기----->[클래스 로더]----바이트코드 적재---->[메소드영역(정적필드, 정적메소드)]`

**<br />**

- ## 정적 필드(Static Field)

인스턴스 필드로 선언할 지, 정적 필드로 선언할 지의 **판단 기준** 은 **객체마다 가지고 있어야 할 데이터라면 인스턴스 필드** 로 선언하고, 객체마다 가지고 있을 필요성이 없는 **공용적인 데이터라면 정적 필드** 로 선언한다.

 `접근제한자 static 자료형 변수명;`

`접근제한자 static 자료형 변수명 = 값;`

```java
public class Calculator {
  String color; //instance field. 계산기별로 색깔이 다를수 있다.
  static double pi = 3.141592; //static method. 파이의 값은 어느계산기나 동일하다.
  }
```

- **대표적인 static 필드는 상수(constant)**이다. 접근 시 `클래스명.상수명;`

  > *ex1) Math 클래스의 상수인 PI는 Math.PI로 접근한다.*

<br />

- ## 정적 메소드 (Static Method)

인스턴스 메소드로 선언할 지, 정적 메소드로 선언할 지의 **판단 기준** 은 **인스턴스 필드를 이용해서 실행해야 한다면 인스턴스 메소드** 로, **인스턴스 필드를 이용하지 않는다면 정적 메소드** 로 선언한다.

`접근제한자 static 반환자료형 메소드명(매개변수 리스트){  ...  }`

```java
public class Calculator{
  String color;	//instance field.
  void setColor(String color){ //instance method. 인스턴스 필드를 사용하는 메소드이다.
    this.color = color;
  }
  static int plus(int x, int y){ //static method. 외부에서 주어진 매개값을 이용해서 덧셈 수행.
    return x+y;
  }
  static int minus(int x, int y){ //static method. 외부에서 주어진 매개값을 이용해서 뺄셈 수행.
    return x-y;
  }
}
```

- **대표적인 static 메소드는 main()** 이다. main()메소드를 포함하는 **클래스의 객체 생성 없이** JVM이 **main() 메소드의 자동호출이 가능하도록 하기 위해서 static 키워드가 필요** 하다.

  ```java
  public class Main{
    public static void main (String[] args){
    }
  }
  ```

<br />

<br />

# 2. 사용

객체생성과 상관없이 클래스 이름과 함께 **dot(.) 연산자** 로 접근.

`클래스명.필드명;` 

`클래스명.메소드명( 매개값 리스트);`

​	**instance 멤버는 외부에서 접근시 해당객체 생성후에 접근 가능. `변수명.멤버;`**

<br />

- static 멤버 사용

```java
public class Sample{
  public static void method(){
    System.out.println("Sample 클래스의 static 메소드 호출");
  }
}
```

```java
publci class Main{
  public static void main(String[] args){
    System.out.println(Math.PI); // 대표적인 static 필드인 상수 테스트
    System.out.println(Math.random()); //* Math 클래스의 대표적인 static 메소드 테스트
    Sample.method(); //Sample클래스의 static 메소드 사용
  }
}
```

**Math.random()보단 난수 관련 전용 클래스인 java.util.Random 클래스 사용 권장.*

<br />

- instance 멤버와 static 멤버 사용

  ```java
  public class Sample{
    private int a; //instance field
    private static int b; // static field
    
    public void method1(){ //instance method
      System.out.println(this.a); //*1 instance 멤버에서 instance 멤버 찾아가기
      System.out.println(Sample.b); //*2 instance 멤버에서 static 멤버 찾아가기
    }
    public static void method2(){
      System.out.println(Sample.b); //*3 static 멤버에서 static 멤버 찾아가기
      System.out.println(this.a); //*4 static 멤버에서 instance멤버 찾아가기
      System.out.println(Sample.a); //*5 static멤버에서 instance멤버 찾아가기
    }
  }
  ```

  **1 :  언제든지 가능. this 키워드 사용*

  **2 : 제한적으로 가능. 공유자료를 찾아가는 것이기 때문이다.*

  **3:  언제든지 가능. 클래스명 사용*

  **4,5 :  불가능. 메모리 적재순서가 다르기 때문이다.*

<br />

<br />

# 3. 주의할 점

객체가 없어도 실행되기 때문에, 정적 메소드나 정적 블록을 선언할 때 내부에 인스턴스 필드나 인스턴스 메소드를 사용할 수 없다.

객체 자신의 참조인 this키워드도 사용이 불가능하다.

정적 메소드와 정적 블록에서 인스턴스 멤버를 사용하고 싶다면 객체를 먼저 생성하고 참조 변수로 접근해야 한다.

```java
public class Car{
  int speed; //인스턴스 필드
  void run() { //인스턴스 메소드
  }
}
```

```java
public class Main{
public static void main(String[] args){
    speed = 60; //실행안됨. 컴파일 에러
    run(); //실행안됨. 컴파일 에러
  
  	Car myCar = new Car(); //객체 생성
  	myCar.speed = 60; //실행가능.
  	myCar.run(); //실행가능.
  }
}
```

<br />

<br />
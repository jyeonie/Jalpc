---
layout: post
title:  "상속(Inheritance)"
date:   2017-11-26
desc: "상속(Inheritance)"
keywords: "java,Inheritance,jyeonie"
categories: [Java]
tags: [java,Inheritance,class,이것이자바다p.288]
icon: icon-html
---

------

**상속(Inheritance)** 이란 부모가 자식에게 물려주는 행위를 말한다.

현실에서의 상속은 부모가 자식을 선택해서 물려준다. 객체지향 프로그램에서는 **자식이 부모를 선택** 한다.

**자식은 부모가 물려준 기능을 이용** 할 수 있다. 하지만 부모 클래스의 입장에서는 자식 클래스의 존재를 알 수 없다.

**부모 클래스(Super Class)를 상위 클래스** 라고 하고, **자식 클래스(Sub Class)를 하위 클래스, 또는 파생 클래스** 라고 부른다.

자바의 **final 클래스를 제외한 모든 클래스는 부모 클래스가 될 수 있다.** 하지만 다중상속 (동시에 여러개의 부모 지정)은 지원하지 않는다.

------

<br />

<br />

# 1. 개념

- ## 상속대상

  - 일반적으로 부모 클래스의 **public 메소드** 가 상속대상이 된다.

  - 보통 **public, protected 멤버만 상속** 된다.

  - 제외대상 

    1. **private 접근 제한** 을 갖는 멤버

    2. **생성자**

    3. **부모클래스와 자식 클래스가 다른 패키지에 존재할 때 부모 클래스의 default 접근 제한을 갖는 멤버**

       ```java
       package com.inheritance002;
       public class SuperClass{ //부모 클래스 역할
         int field1; //접근제한자-default
         
         void method1(){ //접근제한자-default
         }
       }
       ```

       ```java
       package com.inheritance002; //부모 클래스와 같은 패키지
       public class SubClass extends SuperClass{ //자식 클래스 역할
         //상속 받은 멤버- field1, method1()
         int field2;
         
         void method2(){
         }
       }
       ```

       ```java
       package com.inheritance002;
       public class Main{
         public static void main(String[] args){
           SubClass sub = new SubClass();
           
           System.out.println(sub.field1); //SuperClass
           System.out.println(sub.field2);
           sub.method1(); //SuperClass
           sub.method2();
         }
       }
       ```

       부모클래스와 자식클래스가 같은 패키지인 경우 부모 클래스의 멤버 중에서 *public, protected, default*의 멤버 상속 가능.

       <결과>

  <br />

- ## 장점

  - **개발 시간 절약** : 새로운 클래스의 기능 구현 시 기존 클래스가 구현하지 않은 기능만 구현
  - **코드의 중복 감소** : 클래스를 재사용 할 수 있어서
  - **유지 보수 시간을 최소화** : 수정할 일이 생기면 부모클래스만 수정해서 부모클래스를 이용하면 된다.

  <br />

- ## 형식

  `class 자식클래스 extends 부모클래스 { ... }`

  <br />

```java
public class SubClass extends SuperClass{ //원하는 클래스를 부모로 지정할 수 있다.
}


```

```java
public class SuperClass{ //
  public void method(){
  }
}


```

```java
public class Main{
  public static void main(String[] args){
    SubClass sub = new SubClass(); //자식 클래스의 객체 생성 : 상속 받은 부모 객체도 같이 생성된다.
    
    System.out.println(sub.toString()); //SubClass에 toString()가 명시적으로 선언되어 있지 않지만 Object 클래스에서 상속받았기 때문에 사용가능.
    //자식클래스의 객체가 가지는 instance 멤버 확인 : dot(.)
    //toString() : 객체의 정보를 반환하는 메소드.
    //Object 클래스는 모든 클래스의 부모 클래스.
    
    sub.method(); //SubClass에 method()가 명시적으로 선언되어 있지 않지만 SuperClass 클래스에서 상속받았기 때문에 사용가능. 
  }
}
```

<결과>

![result]({{ site.img_path }}/2017-11-29-inheritance/result.jpg)

<img src="{{ site.img_path }}/2017-11-29-inheritance/result.jpg" width="75%">


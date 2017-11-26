---
~~~~yourlayout: post
title:  "인스턴스 멤버(Instance Member)와 this"
date:   2017-11-26
desc: "인스턴스 멤버(Instance Member)와 this"
keywords: "java,Instance,jyeonie"
categories: [Java]
tags: [java,Instance,class,this,이것이자바다p.233]
icon: icon-html
---

------

------

------

인스턴스(Instance) 멤버란 **객체(instance)를 생성** 한 후 사용할 수 있는 필드와 메소드를 말한다.

이들을 **인스턴스 필드(instance field)** , **인스턴스 메소드(instance method)** 라고 부른다.

우리가 지금까지 작성한 모든 필드와 메소드는 인스턴스 멤버들이다.

이 인스턴스 멤버들을 사용하기 위해 외부에서 접근할 때와 내부에서 접근할 때의 방법이 다르다.

**외부객체에서 접근** 하기 위해서는 **객체를 생성하고, 그 참조변수를 통해 접근** 해야하고, **내부객체에서 접근** 할 때는 **this.** 키워드를 사용한다.

------

# 1. 객체 외부에서 인스턴스 멤버에 접근

인스턴스 필드와 메소드는 객체에 소속된 멤버이기 때문에 **객체없이는 사용 불가능**.

클래스를 만들고 인스턴스 멤버들을 선언한다.

```java
public class Car{
  int gas; //인스턴스 필드(instance feild)
  
  void setSpeed(int speed){ //인스턴스 메소드(instance method)
    ...
  }
}
```

<br />

선언된 이 인스턴스 멤버들을 **외부 클래스에서 사용하기 위해서 Car객체(instance)를 생성** 한다.

```java
public class Main{
  public static void main (String[] args){
   Car myCar = new Car(); //myCar 객체 생성
   Car yourCar = new Car(); //yourCar 객체 생성
  }
}
```

<br />

객체를 생성 한 후 **참조변수인 myCar로 접근한 뒤 사용** 한다.

```java
public class Main{
  public static void main (String[] args){
    Car myCar = new Car(); 
    myCar.gas = 10; //myCar 객체의 Car클래스의 인스턴스 필드 사용
    myCar.setSpeed(60); //myCar 객체의 Car클래스의 인스턴스 메소드 사용
    
    Car yourCar = new Car();
    yourCar.gas = 20; //yourCar 객체의 Car클래스의 인스턴스 필드 사용
    yourCar.setSpeed(80); //yourCar 객체의 Car클래스의 인스턴스 메소드 사용
}
```

<br />

<br />

<br />

# 1-1. 이 코드가 실행 된 후 메모리 상태

## 인스턴스 필드(instance field)

### 스택(Stack) 영역 

스택(Stack)영역에 객체의 참조변수와 참조주소를 저장한다.

|  참조변수   | 참조주소  |
| :-----: | :---: |
|  myCar  | 참조주소1 |
| yourCar | 참조주소2 |

<br />

### 힙(Heap) 영역

스택(Stack)영역에 있는 참조주소를 가지고 힙(heap)영역에 있는 **각자의 인스턴스 필드(instance field)**를 찾아가서 값을 넣어준다.

| 참조주소  | 객체명  |  인스턴스필드  |
| :---: | :--: | :------: |
| 참조주소1 | Car  | gas : 10 |
| 참조주소2 | Car  | gas : 20 |

<br />

<br />

### 메소드(method)영역

인스턴스 필드(instance field)는 각 객체마다 따로 존재하지만 인스턴스 메소드(instance method)는 **메소드 영역에 저장되어 공유**된다.

|              메소드영역               |
| :------------------------------: |
| void setSpeed(int speed) { ... } |

<br />

<br />

<br />

# 2. 객체 내부에서 인스턴스 멤버에 접근

## **this.** 키워드

**객체 내부에서만 접근** 하는 상황에서 사용.

**인스턴스 필드명과 생성자나 메소드의 매개 변수명이 동일한 경우** , **인스턴스 필드임을 명시** 하고자 할 때 사용.

**자기자신이 객체(instance) 상태인 경우만 사용가능**  

**메소드 자신도 인스턴스 메소드** 여야 한다.

```java
public class Car{
  String model; //인스턴스 필드
  int speed; //인스턴스 필드
  
  Car(String model){ //생성자
    this.model = model; //생성자의 매개변수명과 인스턴스필드명이 같기때문에 this 사용.
  }
  
  void setSpeed(int speed){ //인스턴스 메소드
    this.speed = speed;	//메소드의 매개변수명과 인스턴스필드명이 같기때문에 this 사용.
  }
  
  void run(){
    for(int i=10; i<=50; i+=10) {
      this.setSpeed(i);
      System.out.printf("%s가 달립니다.(시속:%dkm/h)", this.model, this.speed);
    }
  }
}
```

```java
public class Main{
  public static void main (String[] args){
    Car myCar = new Car("포르쉐"); //외부객체에서 접근하기위해 객체 생성
    Car yourCar = new Car("벤츠"); //외부객체에서 접근하기위해 객체 생성
    
    myCar.run(); //참조변수를 통해 내부객체 접근 후 메소드 실행
    yourCar.run(); //참조변수를 통해 내부객체 접근 후 메소드 실행
  }
}
```

<br />

<br />

```java
public class Sample{
  void method1(){
    System.out.println("Sample 객체의 method1() 메소드 호출");
  }
  
  void method2(){
    this.method1();
  }
}
```

```java
public class Main{
  public class void main (String[] args){
    Sample s = new Sample(); // 외부객체에서 접근하기위해 객체 생성
    s.method2(); // //참조변수를 통해 내부객체 접근 후 메소드 실행
  }
}
```


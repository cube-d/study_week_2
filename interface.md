
## # Interface

***
### 객체지향 이란?</br>
**-. 기존의 프로그래밍 언어와 다르지 않다.**</br>
--> 쉽게 익혀 사용 가능하다.</br>

**-. 코드의 재사용성이 높다.**</br>
<img src="https://i.imgur.com/4MDoS4j.png" width="90%"></img></br>
만약, 객체지향이 아니라면 같은 코드를 반복해서 작성해야함.</br>
<img src="https://i.imgur.com/abUBZwg.png" width="90%"></img></br>
**-. 코드 관리가 쉬워졌다.**</br>
--> 만약, 사람이 자지 않아도 된다면 상속Case는 Super Class의 자다 method만 빼면 된다.</br>

**-. 신뢰성이 높은 프로그램 개발이 가능**</br>
--> DATA 보호(제어자,메서드) / 코드중복 제거 및 코드 불일치 예방</br>
***
### 상속/포함 이란?</br>

#### # 상속
````JAVA
class 자손클래스 extends 조상클래스 {
  //..........
}
````
-. 두 클래스를 조상과 자손의 관계를 맺음</br>
-. 조상의 변경은 자손에 영향을 미치지만, 자손의 변경은 조상에 영향이 없음</br>
-. 상속관계 '~은 ~이다.'</br>

#### # 포함
````JAVA
class Point {
  int x; int y;
}

class Circle {
  Point c = new Point();
  int r;
}
````
-. 한 클래스의 멤버변수로 다른 클래스를 선언</br>
-. 포함관계 '~은~을 가지고 있다.'</br>
-. JAVA는 단일상속만을 허용하므로 포함관계를 적절히 이용하여 class를 설계한다.</br>
````JAVA
//Error
//JAVA는 단일상속만을 허용함
class A extends B,C {
  //....
}
````
***
### 다형성(Polymorphism) 이란?</br>
#### # 다형성
````JAVA
class Tv {
  //.....
}

class CaptionTv extends Tv {
  String text;
  //......
}

Tv t = new CaptionTv();
````
-. 조상타입의 참조변수로 자손타입의 객체를 다룰 수 있음.</br>
-. 자손타입의 참조변수로 조상타입의 인스턴스를 참조할 수 없음.</br>

#### # 다형성 형변환
Up-casting : 자손 타입에서 조상타입으로 참조 변경 / **생략가능**</br>
Down-casting : 조상타입에서 자손타입으로 참조 변경 / **생략불가능**</br>

````JAVA
class Car {
  //..
}

class FireEngine extends Car {
  //..
}

class Ambulance extends Car {
  //..
}

public static void main(String args[]) {
  Car car = null;
  FireEngine fe = new FireEngine();
  FireEngine fe2 = null;
  Ambulance = null;
  
  car = fe; //UpCasting
  fe2 = (FireEngine)car //DownCasting
}
````
***
### Interface 란?</br>
#### # 추상클래스 / abstract class / **extends**
-. 인터페이스와 가장 큰 차이로 추상클래스는 공통으로 메서드 정의가 가능하며 </br>
   이를 상속받은 자손은 사용이 가능함</br>
-. 미완성 클래스이며 인스턴스를 생성할 수 없음</br>
-. 상속받은 자식클래스는 추상클래스의 **추상메서드를 오버라이딩** 해야함</br>

````JAVA
//starcraft
abstract class Unit {
  int x,y;
  int speed;
  abstract void move(int x, int y);
  void stop() {
    //정의 완료
  }
}

class Marine extends Unit {
  void move(int x, int y) {
    //재정의 필수
  }
  void stimPack() {
    //마린 스팀팩 정의
 }
 
 class Tank extends Unit {
  void move(int x,int y) {
    //재정의 필수
  }
  void sizmode() {
    //시즈모드 정의
  }
 }
 
 class DropShip extends Unit {
    void move(int x,int y) {
      //재정의 필수
    }
    void load() {
      //태운다
    }
    void unload() {
      //내린다
    }
 }
````
#### # 인터페이스 / interface / **implements**
-. 인터페이스에 정의된 추상메서드를 완성하여야 한다.
-. 상속과 구현이 동시에 가능하다.
````JAVA
class A extends B implements C {
    //..
}
````
-. 인터페이스 타입의 변수로 인터페이스를 구현한 클래스의 인스턴스를 참조할 수 있고,</br>
   인터페이스를 메서드의 매개변수 타입으로 지정할 수 있다.</br>
````JAVA
interface Repairable {
  //no 선언!
}

class Unit {
  int hitPoint;
  final int MAX_HP;
  Unit(int hp) {
    MAX_HP = hp;
  } 
}

class GroundUnit extends Unit {
  GroundUnit(int hp) {
    super(hp);
  }
}

class AirUnit extends Unit {
  AirUnit(int hp) {
    super(hp);
  }
}

class Tank extends GroundUnit implements Repairable {
  Tank() {
    super(150);
    hitPoint = MAX_HP;
  }
}
  
class SCV extends GroundUnit implements Repairable {

  SCV() {
    super(60);
    hitPoint = MAX_HP;
  }
  
  void repair(Repairable r) {
    if ( r instanceof Unit ) {
      Unit u = (Unit)r;
      while(u.hitPoint != u.MAX_HP) {
        u.hitPoint++;
      }
  }
}

public static void main(String[] args) {
  Tank t1 = new Tank();
  Marine m1 = new Marine();
  SCV s1 = new SCV();
  SCV s2 = new SCV();
  
  //동시 리페어
  s1.repair(t1);
  s2.repair(t1);

  //서로 리페어
  s1.repair(s2);
  s2.repair(s1);
  
  //Error!
  s2.repair(m1);
}
````
--> 상기 repairable 인터페이스를 이용하여 repair를 할 수 있는 대상을 간접적으로 결정함.</br>
    인터페이스를 매겨변수로 받음으로써 이를 implements 받은 대상은 모두 scv에 의해 리페어가능</br>


-. 클래스를 인터페이스를 통해 간접적인 관계를 바꾸며 사용한다.
   이를 통해 class DBCon는 Oracle/MSSQL class가 어떠한 행위를 하는지 모르고 사용이 가능하다.
--> 이게 의존성 주입과 관련된건가....?
````JAVA
class DBCon {
    void DBConnection(I i) {
          i.connection();
     }
 }

 interface I {
      public abstract void connection();
 }

 class Oracle implements I {
     public void connection() {
          //오라클 설정
     }
 }

 class MSSQL implements I {
     public void connection() {
          //MSSQL 설정
     }
 }

class InterfaceTest {
	public static void main(String[] args) {
		DBCon a = new DBCon();
		a.connection(new Oracle());
		a.connection(new MSSQL());
	}
}
````








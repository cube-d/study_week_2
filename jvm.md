# Study_Week2_Interface
**
## JVM / Java Virtual Machine</br>
<img src="https://cdn-images-1.medium.com/max/1000/1*slIuYO633BCuBh_gfYRmGg.png" width="90%"></img>
**
### # Class Loader</br>
RunTime 시점에 클래스를 로딩하게 해주며 클래스의 인스턴스를 생성하면 클래스 로더를 통해 메모리에 로드하게 됩니다.</br></br>

### # Runtime Data Areas</br>
JVM이 프로그램을 수행하기 위해 OS로 부터 별도로 할당 받은 메모리 공간을 말하며, Runtime Data Areas는 크게 5가지 영역으로 나눌 수 있습니다.</br></br>

### # Execution Engine</br>
Load된 Class의 ByteCode를 실행하는 Runtime Module이 바로 Execution Engine입니다. </br>
Class Loader를 통해 JVM 내의 Runtime Data Areas 에 배치된 바이트 코드는 Executin Engine에 의해 실행되며, </br>
실행 엔진은 자바 바이트 코드를 명령어 단위로 읽어서 실행합니다.</br>

### # GC / Garbage Collector</br>
할게 많아요... 이건 날잡아 스터디가 따로 필요해보입니다...</br>
   
대충 설명하자면 C언어/C++언어 는 이런 GC가 없습니다.</br>
그래서 객체를 모두 사용하고 난뒤 반환하는 free(); 코드를 수기로 작성해주어야 반납되며</br>
아니면 메모리에 계속해서 남아 OutOfMemory가 발생할 수 있습니다.</br>
하지만 java JVM에서는 GC로 인하여 자동으로 메모리를 정리합니다.</br>
   
실제, 제가 운영하는 GSRetail에서 WAS Version이 올라가면서 GC 동작방식이 바뀌게 되어</br>
이슈아닌 이슈가 발생한 적이 있으며 발표 시 설명드리겠습니다.</br>

## 변수와 메서드 / Variable & Method</br>
 
### # Instance Variable / 인스턴스 변수</br>
- 각 인스턴스의 개별적인 저장공간, 인스턴스마다 다른 값 저장가능</br>
   Heap영역에서 Instance가 생성될 때 Memory에 올라감.</br>

- 참조하지 않으면 Garbage Collector에 의해 자동 소멸됨.</br>

- 즉, 쉽게 설명하면 Person a = new Person(); 일때, a라는 인스턴스가 생성되었고</br>
  이 a라는 인스턴스는 Heap영역에 올라감.</br>

### # Class Variable / 클래스 변수</br>
- 클래스가 Load될 때 생성되고 프로그램이 종료될 때 소멸.</br>
  인스턴스가 아닌 클래스 자체가 Load될 때 Method Area에 올라감</br>
  이 Method Area를 이용하여 Instance 생성 시, Heap에 메모리를 할당함</br>

- 같은 클래스의 모든 인스턴스들이 공유하는 변수, 즉 Static 변수에 해당하며</br>
  Method Area에 할당됨</br>

### # Local Variable / 지역 변수</br>
- Method 내 선언, Method 종료와 함께 소멸됨(GC)</br>
- 조건, 반복문 블럭 내에 선언된 지역변수는 블럭을 벗어나면 소멸(GC)</br>
- 지역 변수도 Heap 영역에 올라가고 소멸됨</br>

## 간단한 실습 / 생각하여 연습장에 써보기</br>
아래 간단한 JAVA Source에 대하여 JVM 내 메모리에 어떻게 할당되는지 추측하여 그려보세요.</br>
결과값도 추측해주세요.</br>
메모리 영역은 총 3개의 구간이며 **Method Area / JAVA Thread(Call Stack) / Heap** 영역입니다.</br>

````JAVA
class CardTest {
    public static void main(String args[]) {
        Card cl = new Card();
        c1.kind = "Heart";
        c1.number = 7;
        Card c2 = new Card();
        c2.kind = "Spade";
        c2.number = 4;
        System.out.println(c1.kind+","+c1.number+","+c1.width+","+c1.height);
        System.out.println(c2.kind+","+c2.number+","+c2.width+","+c2.height);
        c1.width = 50;
        c1.height = 80;
        System.out.println(c1.kind+","+c1.number+","+c1.width+","+c1.height);
        System.out.println(c2.kind+","+c2.number+","+c2.width+","+c2.height);
    }
}

class Card {
    String kind;
    int number;
    static int width = 100;
    static int height = 250;
}
````



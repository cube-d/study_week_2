# Study_Week2_Interface
**
## Interface
<img src="https://cdn-images-1.medium.com/max/1000/1*slIuYO633BCuBh_gfYRmGg.png" width="90%"></img>

**-.Class Loader**</br>
RunTime 시점에 클래스를 로딩하게 해주며 클래스의 인스턴스를 생성하면 클래스 로더를 통해 메모리에 로드하게 됩니다.</br></br>

**-.Runtime Data Areas**</br>
JVM이 프로그램을 수행하기 위해 OS로 부터 별도로 할당 받은 메모리 공간을 말하며, Runtime Data Areas는 크게 5가지 영역으로 나눌 수 있습니다.</br></br>

**-.Execution Engine**</br>
Load된 Class의 ByteCode를 실행하는 Runtime Module이 바로 Execution Engine입니다. </br>
Class Loader를 통해 JVM 내의 Runtime Data Areas 에 배치된 바이트 코드는 Executin Engine에 의해 실행되며, </br>
실행 엔진은 자바 바이트 코드를 명령어 단위로 읽어서 실행합니다.</br>

**-. GC / Garbage Collector**</br>
   할게 많아요... 이건 날잡아 스터디가 따로 필요해보입니다...
   
   대충 설명하자면 C언어/C++언어 는 이런 GC가 없습니다.
   그래서 객체를 모두 사용하고 난뒤 반환하는 free(); 코드를 수기로 작성해주어야 반납되며
   아니면 메모리에 계속해서 남아 OutOfMemory가 발생할 수 있습니다.
   하지만 java JVM에서는 GC로 인하여 자동으로 메모리를 정리합니다.
   
   실제, 제가 운영하는 GSRetail에서 WAS Version이 올라가면서 GC 동작방식이 바뀌게 되어
   이슈아닌 이슈가 발생한 적이 있으며 발표 시 설명드리겠습니다.
   


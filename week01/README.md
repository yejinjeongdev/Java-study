# Java Live Study 1주차
자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기

## 학습 내용
- [JVM이란 무엇인가](#JVM)
- [컴파일 하는 방법](#컴파일-방법)
- [실행하는 방법](#실행-방법)
- [바이트코드란 무엇인가](#바이트-코드)
- [JIT 컴파일러란 무엇이며 어떻게 동작하는지](#JIT-컴파일러)
- [JVM 구성 요소](#JVM-구성-요소)
- [JDK와 JRE의 차이](#JDK와-JRE의-차이)

#
### JVM
JVM(Java Virtual Machine)은 자바를 실행하기 위한 가상 컴퓨터이다. 

가상 컴퓨터(virtual computer)는 실제 컴퓨터(hardware)가 아닌 소프트웨어로 구현된 컴퓨터 속의 컴퓨터라고 이해하면 된다.

**자바 프로그램은 확장자가 .java인 소스 파일을 작성하여 컴파일러(javac.exe)로 컴파일하면 확장자가 .class인 바이트 코드 파일이 생성된다.**

자바로 작성된 애플리케이션은 모두 JVM에서만 실행되기 때문에 실행을 위해서는 반드시 JVM이 필요하다.

![JVM](https://user-images.githubusercontent.com/77982270/105908703-e5e8bd80-6069-11eb-8018-21c82e64a6a2.png)

일반 애플리케이션 코드와 달리 Java 애플리케이션은 JVM을 한 번 더 거쳐서 기계어로 번역되고 실행되기 때문에 속도가 느리다는 단점이 있다.

하지만 요즘에는 바이트 코드를 기계어로 빠르게 변환해주는 JVM 내부의 최적화된 JIT 컴파일러를 통해 속도의 격차가 많이 줄어들었다. 

#
### 컴파일 방법
**1. 화면에 "Hello, welcome to the java world!"를 출력하기 위한 java 소스 코드를 작성한다.**

- 파일명의 첫 글자는 영문 대문자로 작성한다.
- 파일명과 클래스명은 대소문자가 동일해야 한다.
- 문장 끝에는 세미콜론(;)을 붙여야 한다.

![java_compile1](https://user-images.githubusercontent.com/77982270/105908722-eaad7180-6069-11eb-93bf-6e4824b1bda3.PNG)

**2. 명령 프롬프트(cmd)를 실행하여 소스 파일이 있는 디렉터리로 이동한다.**

![java_compile2](https://user-images.githubusercontent.com/77982270/105908724-eaad7180-6069-11eb-93ff-6bc92c2100ce.PNG)

**3. 해당 디렉터리에 Hello.java 소스 파일이 존재하는지 `dir` 명령어를 사용하여 확인한다.**

![java_compile3](https://user-images.githubusercontent.com/77982270/105908725-eb460800-6069-11eb-9c83-d7374040ef61.PNG)

**4. `javac` 명령어를 사용하여 Hello.java 소스 파일을 컴파일한다.**

이때 생성된 .class 파일은 class loder에 의해 JVM 내로 load 된다.

![java_compile4](https://user-images.githubusercontent.com/77982270/105908726-eb460800-6069-11eb-8290-f67eae9924b1.PNG)

**탐색기를 통해 폴더에 생성된 Hello.class 파일을 확인할 수 있다.**

![java_compile5](https://user-images.githubusercontent.com/77982270/105908728-ebde9e80-6069-11eb-8aac-87c5214745ec.PNG)

#
### 실행 방법
**컴파일 이후 생성된 Hello.class 파일을 `java` 명령어를 사용하여 실행한다.**

- 실행 시 바이트 코드의 확장자명(.class)을 포함하지 않도록 주의한다.
- 또한 바이트 코드의 파일명과 대소문자가 반드시 일치해야 한다.

![java_exe](https://user-images.githubusercontent.com/77982270/105908753-f00abc00-6069-11eb-86fa-c661b6fc3ef6.PNG)

실행 엔진(Execution Engine)에 의해 기계어로 번역되어 내부 메모리(Runtime Data Area)에 배치된다.

#
### 바이트 코드
**바이트 코드(Byte Code)는 가상 컴퓨터에서 돌아가는 실행 프로그램을 위한 이진 표현법으로 쉽게 말하면 확장자가 .class인 파일이다.**

모든 JVM에서 동일한 실행 결과를 보장하며 보통 한 번에 하나의 명령어를 읽은 후 실행하는 형태로 **높은 이식성**을 가진다.

소스 코드에 비해 더 **컴퓨터 중심적**이고, 하드웨어가 아닌 소프트웨어에 의해 처리되기 때문에 보통의 기계어보다 **추상적**이다.

의미 분석 단계의 결과를 **부호화**하여 일반적으로 소스 코드를 직접 분석하고 실행하는 것보다 더 좋은 성능을 보여 준다.

![byte_code](https://user-images.githubusercontent.com/77982270/105908761-f26d1600-6069-11eb-8dd2-eda13757184c.PNG)

#
### JIT 컴파일러
JIT(Just-In-Time)란 프로그램을 실제 실행하는 시점에 기계어로 번역하는 컴파일 기법이다.

JIT 컴파일러는 프로그램 실행 시 애플리케이션의 성능을 향상시키는 런타임 환경의 구성 요소이다.

### JIT 동작 원리
JIT 컴파일러는 기본적으로 활성화되어 메소드가 컴파일되면 JVM은 해석하는 대신 해당 메소드의 컴파일 된 코드를 직접 호출한다.

런타임 시 JVM 내부에서 바이트 코드(.class)를 native code로 컴파일하여 JAVA 응용 프로그램의 성능을 향상시킨다.

실행 시점에 생성한 기계어 코드를 캐싱하여 같은 함수가 반복적으로 호출될 때 매번 기계어 코드가 생성되는 것을 방지한다.

**출처** [IBM 지식센터](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.vm.80.doc/docs/jit_overview.html)

#
### JVM 구성 요소
- **Class Loader**

  class 파일을 읽어 링크를 통해 배치하는 작업을 수행한다.
  
  컴파일로 생성된 바이트 코드(.class) 파일을 엮어서 운영체제로부터 할당 받은 메모리 영역인 Runtime Data Area에 적재한다. 

- **Execution Engine**

  Class Loader에 의해 적재된 바이트 코드(.class) 파일들을 기계어로 번역하여 명령어 단위로 실행한다.
  
  기계어를 번역하는 방식은 인터프리터(Interpreter) 방식과 JIT(Just-In-Time) 방식으로 나뉜다.
  
  - **Interpreter 방식** - 실행 엔진은 바이트 코드 단위로 읽어서 실행하여 한 줄씩 수행하기 때문에 속도가 느리다.
  
  - **JIT 방식** - 인터프리터의 단점을 보완하기 위해 등장했으며, 바이트 코드 전체를 native 코드로 변경하여 작업을 수행한다.
  
    한 번 변경한 코드는 캐시에 보관하여 수행 속도가 빠르지만 번역할 때 시간이 걸리기 때문에 자주 수행되는 경우에 유리하다. 

- **Garbage Collector**

  Heap 메모리 영역에 생성된 객체들 중에 참조되지 않은 객체들을 탐색하여 제거하는 역할을 한다.

- **Runtime Data Area**

  자바 애플리케이션 실행 시 사용되는 데이터를 적재하는 메모리 영역이다.
  
![JVM2](https://user-images.githubusercontent.com/77982270/105949208-ab097880-60af-11eb-8ca8-f0767e99bab5.PNG)

### Java 메모리 영역
- **Method area**
    
  필드 정보, 메소드 정보, type 정보, static, final 변수 등이 생성된다.
    
  클래스 정보를 처음 메모리 공간에 올릴 때 초기화되는 대상을 저장하기 위한 메모리 공간이다.
  
- **Heap area**
    
  객체를 저장하는 가상 메모리 공간으로 new 키워드로 생성된 객체와 배열이 저장되어 프로그램이 종료될 때까지 사라지지 않는다. 
    
  method 영역에 로드된 클래스만 생성이 가능하고 Garbage Collector가 참조되지 않은 메모리를 확인하고 제거한다.
    
- **Stack area**
  
  프로그램 실행 시 임시로 할당되었다가 메소드를 빠져나가면 바로 소멸되는 특성을 가지는 데이터 저장 공간이다.
    
  매개변수, 지역변수, 파라미터, 리턴값, 연산 등에 사용되는 값들이 임시로 보관된다.
    
- **Native method stack**
  
  프로그램 컴파일 시 생성되는 바이트 코드가 아닌 실제 실행 가능한 기계어로 작성된 프로그램을 실행시키는 영역이다.
  
  다시 말해 자바가 아닌 언어로 작성된 native 코드를 위한 메모리 영역으로 보통 C/C++ 등의 코드를 수행하기 위한 저장소이다.
    
- **PC register**
  
  Thead가 시작될 때 마다 생성되는 영역으로 스레드(thead) 마다 하나 씩 존재한다.

  Program Counter, 즉 현재 thead가 실행되는 부분의 주소와 명령을 저장한다.

#
### JDK와 JRE의 차이
![JDK](https://user-images.githubusercontent.com/77982270/105950361-9cbc5c00-60b1-11eb-84ef-66fa996445a3.PNG)

- **JRE(Java Runtime Enviroment)**

  컴파일된 자바 프로그램을 실행시킬 수 있는 **읽기 전용**의 자바 환경이다.

  JRE는 JVM이 자바 프로그램을 동작시킬 때 필요한 라이브러리와 기타 파일들을 가지고있으므로 JVM의 실행환경을 구현한다고 할 수 있다.

  자바 프로그램을 실행시키기 위해 JRE를 반드시 설치해야 하지만 자바 프로그래밍 도구는 포함되어있지 않기 때문에 JDK를 설치해야 한다.

- **JDK(Java Development kit)**
  
  JDK는 자바 프로그래밍 개발을 위해 필요한 도구들(javac, java 등)을 포함하며 **읽기 및 쓰기**를 지원한다.

  JDK를 설치하면 JRE이 포함되어 설치되므로 JRE 보다 포괄적인 개념으로 생각하면 된다.

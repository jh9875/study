ch 05 Java 기초
===

# 자바 언어 소개
- Java 언어의 장점 <br>
  - 언어가 탄생한지 오랜 시간이 지나 꾸준히 축적된 노하우로 안정성이 좋음.
  - 오픈 소스 라이브러리가 많다.

- Java 언어의 한계 <br>
  - 정적타입 언어. Python이나 Javascript 같은 동적보다 초심자에게 어렵게 느껴짐.
  - 유연하고 견고한 코드를 만들기 어려움.

- Java 언어의 한계에도 사용하는 이유 <br>
  - 레퍼런스가 많아 배우기 쉬운 객체지향 언어.
  - JVM에 동작하는 언어가 많다. Java를 익히면서 배우는 JVM에 대한 지식은 언어가 바뀌더라도 유효.
  - 안정성이 중요한 기업용 소프트웨어, 대용량 데이터 도구들은 JVM, Javam 기반으로 만들어짐.

# 자바 코드가 실행되는 원리
- 프로그래밍 언어의 실행 원리 <br>
  - 기계어 : 컴퓨터가 이해하는 언어. 하드웨어 종류마다 기계어 종류가 다름. 어렵고 시간도 오래걸리거 가독성도 안좋음.
  - 어셈블리어 : 저급언어 일좀. 컴퓨터 CPU가 이해할 수 있는 언어. 기계어보다 사람이 알아볼 수 있는 의미단위로 코딩할 수 있음. 그래도 여전히 하드웨어 종속적인 언어.
  - 고급어 : 하드웨어 동작을 추상화 해서 프로그래밍 할 수 있는 언어. 사람이 이해하고 작성하기 쉬운 코드를 작성하는걸 지원. Shell script, C, Python, Java 등 ..
- 고급어, 어셈블리어가 기계어가 되는 과정 <br>
  - 고급어의 경우 Compiler 또는 Interpreter에 의해 기계어가 되고, 어셈블리 언어는 Assembler로 기계어로 변환.
- Java 코드 컴파일 <br>
  - javac에 의해 Byte Code(.class)로 변환 (JVM이 이해하는 언어.?)
  - JVM이 동작하는 환경에 따라서 .class 파일을 기계어로 변환
  - JVM에선 런타임에 Class Loader가 메모리에 로드.
  - Bytecode verifier가 byte code를 검사.
  - JIT Compiler는 class에서 기계어로 바꾸는건 실시간으로 실행.?

# 예외, 예외처리 - 예외처리의 목적 & try-catch-finally
- 예외 처리의 목적 <br>
  - 비정상 종료를 막기 위해서
  - 개발자에세 알려서 코드를 보완할 수 있도록 하기 위해
- 자바 예외 클래스 위계구조 <br>
  - 모든 예외 클래스는 Throwable의 자손 클래스.
  - Thrhowable을 상속받는 종류는 크게 Error와 Exception이 있다.
  - Error의 경우 프로그램이 강제 종료되어야 하는 경우.
  - Exception의 경우 프로그램을 종료하지 않고, 예외를 다루기 위해서 사용.

# 예외, 예외처리 - try-with-resource & 예외, 에러처리 퀴즈
- try-with_resource <br>
  - try 옆에 리소스를 이니셜라이징 하는 코드를 넣으면 자동으로 자원을 해제.
  - 만약 finally에서 해제가 안되면 자원을 계속 잡고있기 때문에 나중에 다시 해당 자원을 사용할 때 문제가 생길 수 있음.
  - AutoClosable을 구현한 객체만 try-with-resouce를 사용할 수 있다. (java doc에 해당 내용이 있음.)
- 메소드에서의 예외 선언 <br>
  - throws를 이용해서 사용.

# 날짜와 시간 다루기
- Date 클래스 <br>
  - 전통적으로 시간을 표현하는 클래스.
  - unix epoch time의 milliseconds 단위로 시간을 표현.
  - Epoch Time이란? 1970년 1월 1일 부터 얼마나 지났는지 초, 밀리초, 나노초 단위로 센 카운트 값. 프로그래밍 하면서 어떤 시점을 지역과 상관없이 숫자로 표현하고 싶을 때 사용.
  - Date 클래스의 단점 :
    - Thread safe 하지 않다. 여러 Thread에서 사용하려면 한번에 한 쓰레드 사용이 안됨.
    - API가 이해하거나 사용하기 쉽지 않음.
    - Timezone을 적용하기 어렵다.
- LocalDate, LocalTime, LocalDateTime <br>
  - 시간 없이 연,월,일 날짜만 다루기 위한 클래스.
- 기간 (Period, Duration)
  - 시간이나 날짜 사이의 기간을 type-safe하게 표현.
  - period : 두 날짜 사이의 기간, Duration : 두 시간 사이의 기간.
- Date, Calendar의 호환 <br>
  - Instanct 클래스를 통해서 LocalDate, LocalTime, LocalDateTime과 변환 가능.

# Collection
- Collection 프레임워크 <br>
  - 다수의 데이터를 다루기 위한 클래스의 집합.
  - 데이터를 다루는데 필요한 기능을 제공하기 때문에 많이 유용.
  - Collection 프레임워크의 모든 클래스는 Collection 인터페이스를 구현하는 클래스 또는 인터페이스
- 대표 Collection 인터페이스, 자료구조 <br>
  - List <br>
    - 순서가 있는 데이터의 집합.
    - 데이터 중복을 허용.
    - ArrayList, LinkedList, Stack, ..
  - Set <br>
    - 순서를 유지하지 않음.
    - 중복을 허용하지 않음.
    - HashSet, TreeSet, ..
  - Map <br>
    - 키와 값의 쌍으로 이루어진 데이터 집합.
    - 순서 유지되지 않음.
    - key는 중복 X, value는 중복 O
    - HashMap, TreeMap, ..
  - Stack <br>
    - 마지막에 넣은 데이터를 먼저 꺼내는 자료 구조, LIFO
    - Stack, ArrayDequeu, ..
  - Queue <br>
    - FIFO
  - Collection 인터페이스 <br>
    - 자료 형에 대해서 공통으로 사용할 수 있는 기능을 제공.

# 제네릭스
- Generics란 <br>
  - 클래스나 메소드 레벨에서 동작은 같지만 사용되는 타입만 다른 경우.
  - 객체는 런타임에 생성되지만 객체가 사용하는 타입은 선언적으로 정의함으로써 컴파일 타임의 타입 체크를해서 더 안전하고 유연한 코드를 작성할 수 있음.
  - 객체를 생성할 때 타입을 지정.
  - ex) Set<Integer>, Set<String> 이런식으로 타입을 다르게..
  
# 람다

# 스트림

# 네트워크 기본 개념~Retrofit 라이브러리를 활용하여 API 호출하기

# TCP 소켓 프로그래밍
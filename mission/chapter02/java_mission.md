## static 멤버

- **시간적 특성**
    - 객체마다 생성되는 개념이 아닌, 클래스마다 생성되는 개념
    - 클래스가 JVM에 로딩될 때 공간(메서드 영역: 객체 내부가 아닌 클래스 코드가 적재되는 메모리)을 할당받음
- **시간적 특성**
    - 객체가 생성되기 전에 미리 생성(클래스 내의 static 메서드는 non-static 멤버에 접근 불가)
    - 객체가 생성되기 전에도 사용 가능
    - 객체가 사라져도 static 멤버는 사라지지 않음
    - static 멤버는 프로그램이 종료될 때 소멸
- **공유의 특성**
    - 동일한 클래스의 모든 객체에 의해 공유됨

## JVM 메모리 구조

- **메서드 영역**
    - 프로그램을 실행하는 데  필요한 공통 데이터를 관리함
    - 프로그램의 모든 영역에서 공유함
    - ex) static 영역, 런타임 상수 풀
- **스택 영역**
    - 각 스레드 별로 하나의 실행 스택이 생성됨
    - 각 스택 프레임에서 지역 변수, 중간 연산 결과, 메서드 호출 정보 등을 관리함
- **힙 영역**
    - 객체(인스턴스)와 배열이 생성되는 영역
    - 가비지 컬렉션이 이루어지는 주요 영역
- **PC 레지스터**
    - 현재 실행 중인 JVM 명령 주소를 저장하며, 각 스레드마다 별도로 존재함
- **Native Method Stack**
    - 자바 외 언어로 작성된 Native 코드를 관리하는 영역

## static과 JVM의 관계

- static 멤버는 JVM 메모리의 메서드 영역에 저장됨
- 클래스 로딩 시점에서 static 변수는 초기화되며, 프로그램이 종료될 때까지 소멸되지 않음
- 객체(인스턴스)가 생성되기 전에 static 메서드는 사용 가능(클래스를 통한 호출)
- JVM의 가비지 컬렉션 대상에서 제외됨

## ClassLoader

- JVM에서 클래스 파일(.class)을 로드하고, 해당 클래스의 바이트 코드를 메모리에 적재함
- ClassLoader 동작과정
    - Loading: 클래스 파일의 바이트 코드를  메소드 영역에 저
    - Linking: 클래스가 규칙에 맞춰 제대로 구성되었는지 확인
    - Initialization: 클래스 변수들을 적절한 값으로 초기화
- 자바의 클래스 로딩은 동적 로딩방식을 사용함 → JVM은 모든 클래스에 대한 정보를 메모리에 로딩하지 않지 않고 코드 실행 시점에 로딩함

## static과 Class Loader의 관계

- ClassLoader가 클래스 파일을 메모리에 로드한 후 JVM이 클래스를 초기화하는데, 이때 static 멤버가 초기화가 이루어지고 static 블록이 실행됨
- ClassLoader가 클래스를 언로드하지 않으면 해당 class의 static 멤버는 메모리에서 해제되지 않으므로 메모리 누수로 연결될 수 있음

## Collection Framework

- 자바에서 Collection은 데이터의 집합을 의미
- Collection Framework는 데이터를 효율적으로 저장하고 조작하기 위해 사용됨

## Collection이 제공하는 인터페이스

**Collection**

- 컬렉션 프레임워크의 기본적인 인터페이스로, 대부분의 컬렉션 클래스가  컬렉션 인터페이스를 상속받음
- add, remove, size, isEmpty 등의 기본 메서드를 정의함

**Set**

- 순서가 없는 데이터 집합으로, 데이터 중복을 허용하지 않음
- 구현체: HashSet, TreeSet

**List**

- 순서가 있는 데이터 집합으로, 중복을 허용함
- 구현체: ArrayList, LinkedList

**Queue**

- FIFO(선입선출) 방식의 데이터 집합
- 구현체: LinkedList, PriorityQueue

**Map**

- 키와 값이 쌍을 이루는 데이터 집합으로, 순서가 없으며 데이터의 중복을 허용함
- Collection 인터페이스를 상속받지 않음
- 구현체: HashMap, TreeMap, LinkedHashMap

## 면접 질문

**static멤버와 non-static 멤버의 차이점**

- 생성: static → 클래스 로딩 시, non-static → 객체(인스턴스) 생성 시
- 소멸: static → 프로그램 종료 시, non-static → 객체 소멸 시
- 공간: static → 메서드 영역, non-static → 힙 영역
- 공유: static → 동일한 클래스의 객체들에 의해 공유, non-static → 각 객체 내에 멤버별 고유 공간 유지 및 공유X
- 사용: static → 객체를 통해 or 객체 없이 클래스를 통해 사용 가능, non-static → 객체를 통해서 사용 가능
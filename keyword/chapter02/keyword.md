# 추가 과제

## JVM 메모리의 구조

JVM은 Static, Heap, Stack 영역으로 나뉜다.

### Static 영역

클래스가 로드 될 때 생성됨, 클래스 변수와 **static 변수**가 저장된다.

### Heap 영역

객체와 인스턴스 변수가 저장되는 공간이다.

### Stack 영역

메서드 호출 시 생성되는 지역변수와 매개변수가 저장되는 공간이다.

## Class Loader

### 역할

자바 컴파일러에 의해 컴파일된 .class 파일을 JVM으로 로드하여 런타임 영역에 배치한다.

### 과정

1. Loading: .class 파일을 읽고, JVM의 메모리에 로드
2. Linking: 클래스 파일을 사용하기 위해 검증한다.
3. Initializing: **static 변수**를 비롯한 클래스 변수들을 적절한 값으로 초기화한다.

## Collection Interface

![collection](./2-1.png)

### 정의

- Collection은 Java에서 데이터의 그룹, 즉 여러 개의 객체를 하나의 단위로 표현하는 인터페이스
- List, Set, Queue, Map 인터페이스의 상위 인터페이스로, 컬렉션 프레임워크의 root 인터페이스 역할을 한다.

## 하위 인터페이스

1. List

- 순서가 있는 데이터의 집합으로, 데이터의 중복을 허용한다.
- ArrayList, LinkedList, Vector, Stack 등의 클래스가 List 인터페이스를 구현한다.

2. Set

- 순서가 없고, 데이터의 중복을 허용하지 않는 데이터의 집합이다.
- HashSet, TreeSet, LinkedHashSet 등의 클래스가 Set 인터페이스를 구현한다.

3. Queue

- F~IFO(First In First Out) 형태의 자료구조로, 데이터의 중복을 허용한다.
- PriorityQueue, Deque, ArrayDeque 등의 클래스가 Queue 인터페이스를 구현한다.

4. Map

- key-value 쌍으로 이루어진 데이터의 집합으로, key는 중복을 허용하지 않는다.
- HashMap, TreeMap, LinkedHashMap, Hashtable 등의 클래스가 Map 인터페이스를 구현한다.

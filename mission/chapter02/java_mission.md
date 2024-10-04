2주차 추가과제입니다.

### **1. static과 JVM 메모리, ClassLoader**

### **JVM 메모리 구조**

JVM(Java Virtual Machine)은 자바 프로그램이 실행될 때 사용하는 메모리 공간을 여러 영역으로 나누어 관리

- **Heap**: 객체와 인스턴스 변수가 저장되는 공간입니다. 자바에서 new키워드로 생성한 모든 객체는 이곳에 저장
- **Stack**: 각 스레드마다 존재하며, 메서드 호출 시 로컬 변수와 메서드 호출 정보를 저장
- **Method Area (or Class Area)**: 클래스 메타데이터, 즉 클래스 정보(클래스 이름, 메서드, 변수 정보 등)가 저장되는 영역. 또한, 이곳에 **static 변수와 static 메서드**도 저장
- **PC Register**: 현재 실행 중인 명령을 가리키는 레지스터
- **Native Method Stack**: 자바 외의 네이티브 코드(C/C++)를 실행할 때 사용하는 메모리 공간

### **static과 Method Area**

static 키워드는 클래스 로딩 시에 해당 필드나 메서드가 **Method Area**에 저장됨을 의미

프로그램 실행 동안 메모리에 고정되어 있으며, 객체의 생성과 관계없이 클래스 자체이다.

- **static 변수**는 클래스 로딩 시 한 번만 초기화되며, 모든 객체가 공유
- **static 메서드**는 인스턴스와 무관하게 호출할 수 있으며, 객체를 생성하지 않고도 사용

### **ClassLoader와 static**

Classloader는 자바 클래스 파일(.class)을 JVM 메모리로 로딩하는 역할

static 변수나 메서드는 클래스가 처음 **로드**될 때 메모리(주로 Method Area)에 올라가고 Classloader가 클래스를 로드하는 시점에서, static 요소들이 메모리 상에 존재하게 되며, 이후 해당 클래스의 static 메서드나 변수는 인스턴스화 없이 바로 사용

- 각 클래스는 로드될 때 Classloader에 의해 메모리 공간을 할당받으며, 이때 static 변수나 메서드가 **Method Area**에 저장
- 클래스는 최초 로드될 때만 메모리로 올라가며, static 필드와 메서드 또한 클래스 로딩 시점에 메모리에 존재

### **2. Collection Interface**

자바에서 Collection 인터페이스는 여러 객체를 저장하고 관리하는 데 사용되는 자료구조(컬렉션 클래스)들을 추상화한 것

1. **List**: 순서가 있는 데이터를 관리하며, 중복된 데이터를 허용 (ArrayList , LinkedLis  등)
2. **Set**: 중복을 허용하지 않으며, 순서가 없는 데이터를 관리 (HashSet, TreeSet 등)
3. **Queue**: FIFO(First-In-First-Out) 방식으로 데이터를 관리 (LinkedList, PriorityQueue 등)
4. **Map :** 키(Key), 값(Value)의 쌍으로 이루어진 데이터의 집합(HashMap, HashTable 등)

### **List**

- **ArrayList**: 내부적으로 배열을 사용하여 데이터를 관리

  크기가 고정된 배열을 사용하므로, 배열 크기가 꽉 차면 새로운 배열을 만들어 기존 데이터를 복사하는 방식으로 확장

- **LinkedList**: 각 요소가 이전/다음 요소의 참조를 가지고 있는 노드로 구성된 리스트

  삽입과 삭제가 빈번한 경우 유리


### **Set**

- **HashSet**: HashMap을 기반으로 동작하며, 요소들을 해시함수로 관리하여 중복을 방지
- **TreeSet**: 이진 트리 구조를 사용하여 데이터를 정렬된 상태로 관리하며, NavigableSet 인터페이스를 구현

### **Queue**

- **PriorityQueue**: 각 요소들이 우선순위를 가지고 있으며, 우선순위가 높은 요소가 먼저 처리되는 구조
- **LinkedList**: Queue 인터페이스도 구현하여 FIFO 방식으로 사용

### Map

- **Hashtable :** HashMap보다는 느리지만 동기화 지원 null 불가
- **HashMap :** 중복과 순서가 허용되지 않으며 null값이 허용

## 면접 질문

- **static 메서드와 일반 메서드의 차이점은 무엇인가요?**
    - 예상 답변: static 메서드는 객체의 인스턴스와 관계없이 클래스 이름으로 바로 호출할 수 있습니다. 반면 일반 메서드는 객체를 생성한 후에만 호출할 수 있습니다. 또한, static 메서드는 인스턴스 변수에 접근할 수 없고, 오직 static 변수만 접근할 수 있습니다.
- **ClassLoader와 static의 관계를 설명해 주세요.**
    - 예상 답변: ClassLoader는 자바 클래스 파일을 JVM에 로드하는 역할을 합니다. 클래스가 처음 로드될 때  static 변수와 메서드가 메모리(Method Area)에 저장됩니다. 이로 인해 static 요소는 객체 없이도 클래스 로딩 이후 바로 사용할 수 있습니다.
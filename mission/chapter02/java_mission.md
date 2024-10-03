# static & jvm메모리 & classloader

<blockquote>
<h2>static</h2> 
&Rightarrow; '정적 변수' = '클래스 변수'
<ul>
    <li>클래스 내부에 선언</li>
    <li>프로그램이 실행되어 메모리에 올라갔을 때 딱 한 번 메모리 공간 할당</li>
    <li>모든 인스턴스가 값을 공유</li>
    <li>메소드 영역에 저장</li>
    <li>인스턴스 생성 없이 클래스 이름으로 접근 가능</li>
    <li>static 메소드는 인스턴스 변수에 접근 불가
    &rightarrow; 객체를 생성해서 접근해야 함</li>
</ul>
<h2>jvm 메모리</h2>
<h3>JVM (Java Virtual Machine)</h3>
<ul>
    <li>자바 프로그램을 실행하기 위한 가상 머신</li>
    <li>운영체제나 하드웨어에 독립적으로 동작
        &rightarrow; wora (write once, run anywhere)</li>
    <li>자바 소스 코드 &rightarrow; 자바 컴파일러 &rightarrow; 자바 가상 머신(JVM)</li>
</ul>
<h3>JVM 메모리</h3>
<ul>
    <li>JVM은 java 프로그램이 사용하는 메모리를 자동으로 관리</li>
        <ul>
            <li>가비지 컬렉터를 통해 사용하지 않는 객체를 자동으로 해제</li>
        </ul>
    <li>직접 메모리 관리를 할 필요가 없어짐</li>
</ul>
<h3>JVM 메모리 구조</h3>
<ul>
    <li>힙 영역</li>
        <ul>
            <li>객체, 인스턴스 변수가 저장</li>
            <li>모든 객체는 힙 영역에 동적 할당</li>
            <li>가비지 컬렉션에 의해 관리</li>
            <li>모든 스레드가 공유</li>
        </ul>
    <li>메소드 영역</li>
        <ul>
            <li>클래스 메타데이터, static 변수, 상수 등이 저장</li>
            <li>클래스가 로드 될 때 처음 이 영역에 로드되고 프로그램 실행동안 유지</li>
            <li>모든 스레드가 공유</li>
        </ul>
    <li>스택 영역</li>
        <ul>
            <li>스레드마다 개별적으로 할당</li>
            <li>메소드 호출 시 생성되는 지역 변수, 파라미터, 반환 주소 등이 저장</li>
            <li>빠른 접근, 제한된 크기</li>
        </ul>
    <li>PC 레지스터</li>
        <ul>
            <li>각 스레드가 실행 중인 명령의 주소를 저장</li>
            <li>모든 스레드는 독립적인 pc 레지스터를 가짐</li>
        </ul>
    <li>네이티브 메소드 스택</li>
        <ul>
            <li>Java 외부 네이티브 코드(C/C++ 등)에서 호출되는 메소드를 위한 스택</li>
            <li>네이티브 라이브러리와 연동되는 메소드의 호출을 처리</li>
        </ul>
</ul>
<h2>classloader</h2>
&Rightarrow; JVM이 클래스를 메모리에 올리고 실행할 수 있게 준비하는 역할
<ul>
    <li>동적 로딩 구현</li>
    <li>필요한 시점에 메모리에 로드되도록 함</li>
    <li>.class 파일을 찾아 메모리에 적재</li>
</ul>
<h3>classloader 종류</h3>
<ul>
    <li>부트스트랩 클래스 로더</li>
        <ul>
            <li>기본적인 클래스 로더</li>
            <li>JVM이 실행되는 데 필요한 필수적인 클래스 로드</li>
            ex) java.lang, java.util 등
            <li>Java로 접근하거나 확장 불가</li>
        </ul>
    <li>확장 클래스 로더</li>
        <ul>
            <li>JDK 확장 기능 제공하는 클래스 로드</li>
            <li>java.lang.ClassLoader 클래스에 의해 구현</li>
            <li>사용자가 직접 확장하거나 접근 가능</li>
        </ul>
    <li>애플리케이션 클래스 로더</li>
        <ul>
            <li>JVM 기본 클래스 로더</li>
            <li>사용자가 작성한 대부분의 클래스가 적재됨</li>
        </ul>

</ul>
</blockquote>

# Collection interface
<blockquote>
<h2>Collection</h2>
<ul>
    <li>Java의 Collection Framework 중 가장 상위에 위치하는 인터페이스 중 하나</li>
    <li>여러 객체를 모아 관리할 수 있는 자료 구조 정의</li>
    <li>List, Set, Map, Queue, Deque 등의 기본 동작 방식을 규정</li>
</ul>
<h2>Collection interface 특징</h2>
<ul>
    <li>객체의 그룹을 나타냄</li>
    <li>크기가 유동적이며 다양한 타입의 요소들을 저장하고 관리</li>
    <li>객체 간 중복 허용 여부나 저장 순서에 대한 명확한 규정이 없음</li>
</ul>
</blockquote>
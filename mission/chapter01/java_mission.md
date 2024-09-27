<h1>자바의 접근제어자 4가지</h1>

| 접근제어자      | private | default  |   protected    | public |
|------------|:-------:|:--------:|:--------------:|:------:|
| 같은 패키지 클래스 |    X    |    O     |       O        |   O    |
| 다른 패키지 클래스 |    X    |    X     |       X        |   O    |
| 접근 가능 영역   |  클래스 내  | 동일 패키지 내 | 동일 패키지와 자식 클래스 | 모든 클래스 |
<blockquote>
<h2>public &Rightarrow; 외부 클래스 어디에서나 접근 가능</h2>
<h2>protected &Rightarrow; 같은 패키지 내부와 상속 관계의 클래스에서만 접근 가능</h2>
<h2>default &Rightarrow; 같은 패키지 내부에서만 접근 가능</h2>
<h2>private &Rightarrow; 같은 클래스 내부에서만 접근 가능</h2>
</blockquote>

<h1>클래스와 인터페이스</h1>
<blockquote>
<h2>객체 &Rightarrow; 클래스 모양대로 생성된 실체(==instance)</h2>
<h2>클래스 &Rightarrow; 객체의 속성과 기능을 코드로 구현한 것</h2>
<ul>
<li>객체를 생성하기 위한 목적</li>
<li>멤버변수와 메서드로 구성</li>
<ul>
<li>멤버변수 : 객체가 가지는 속성을 선언하는 변수</li>
<li>메서드 : 함수의 종류로 클래스 기능을 구현</li>
</ul>
<li>생성자를 사용하여 인스턴스 생성</li>
<ul>
<li>상속, 오버로딩, 오버라이딩 등으로 확장이 가능</li>
</ul>
</ul>
<h2>인터페이스 &Rightarrow; 클래스, 프로그램이 제공하는 기능을 명시적으로 선언하는 역할</h2>
<ul>
<li>추상메서드와 상수로만 구성</li>
<li>구현코드가 없기 때문에 인스턴스 생성 불가</li>
<li>implements 예약어를 사용해 클래스에서 인터페이스를 사용</li>
</ul>
<h3>사용 이유</h3>
<ul>
<li>표준화 가능</li>
<li>다중 상속이 가능</li>
<li>다형성의 장점을 극대화</li>
</ul>
</blockquote>

```java
class Car {
    String company;
    String color;
    int speed;
    void upSpeed(int value) {
        speed += value;
    }
    void downSpeed(int value) {
        speed -= value;
    }
}
```
```java
interface Animal {
    void eat();
    void sleep();
}
```
```java
class Dog implements Animal {
    public void eat() {
        System.out.println("먹는다");
    }
    public void sleep() {
        System.out.println("잔다");
    }
}
```
<h1>상속</h1>
<blockquote>
<h2>상속 &Rightarrow; 서브클래스가 슈퍼클래스의 필드와 메서드를 받아 계층적 관계를 형성하는 것</h2>
<ul>
<li>extends 예약어를 사용하여 상속</li>
<li>자바에서는 다중상속이 불가</li>
</ul>
<h3>사용 이유</h3>
<ul>
<li>코드의 재사용성 증가</li>
<li>코드의 중복을 줄여 유지보수성 증가</li>
<li>서브클래스를 사용해 기존 클래스를 수정하지 않고 새로운 기능을 추가 가능</li>
</ul>
</blockquote>

```java
class People {
    String name;
    void print() {
        System.out.println("사람입니다.");
    }
}
```
```java
class Student extends People {
    String school;
    void study() {
        System.out.println("공부합니다.");
    }
    void print() {
        System.out.println("학생입니다.");
    }
}
```



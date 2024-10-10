# 제네릭
<blockquote>
<h2> 
제네릭 프로그래밍 &Rightarrow; 값이 하나의 참조 자료형이 아닌 여러 참조 자료형을 사용할 수 있도록 프로그래밍 하는 것
</h2>
<ul> 
    <li>자료형을 필요에 따라 변경하며 사용할 수 있도록 함</li>
    <li>자료형 변환 시 검증을 컴파일러가 하므로 안정적임</li>
    <li>다이아몬드 연산자 (< >)를 사용하여 제네릭 클래스 정의</li>
    <li>T의 자료형이 정해지는 순간은 제네릭 클래스의 인스턴스가 생성되는 순간</li>
    <ul>
        <li>static은 T보다 자료형이 결정되는 순간이 빠르기 때문에 static 변수나 static 메서드 내부 변수에는 T 사용 불가</li>
    </ul>
</ul>   
</blockquote>

```java
public class GenericClass<T> {
    
    private T variable;

    public void setVariable(T variable) {
        this.variable = variable;
    }
    
    public T getVariable(){
        return variable;
    }
}

```

# 와일드카드

<blockquote>
<h2>와일드카드 &Rightarrow; 하나의 참조변수로 다른 타입변수를 가진 제네릭 클래스 객체를 참조할 수 있는 방법</h2>
<ul>
    <li>여러 타입을 안전하게 처리해 타입 안정성을 유지</li>
    <li>잘못된 타입을 추가하는 오류 방지</li>
    <li>유연성 제공</li>
</ul>
<h3>1. Unbounded Wildcard (?)</h3>
<ul>
    <li>어떤 타입이든 상관없이 모든 타입을 허용하는 와일드카드</li>
    <li>주로 메서드에서 다양한 타입 객체를 처리할 때 사용</li>
</ul>
<h3>2. Upper Bounded Wildcard (? extends T)</h3>
<ul>
    <li>해당 타입의 후손 클래스의 인스턴스라면 무엇이든 참조 가능</li>
    <li>T 또는 T의 하위 클래스만 허용</li>
    <li>주로 읽기 전용 데이터를 다룰 때 사용</li>
</ul>
<h3>3. Lower Bounded Wildcard (? super T)</h3>
<ul>
    <li>해당 타입의 조상 클래스의 인스턴스라면 무엇이든 참조 가능</li>
    <li>T 또는 T의 상위 클래스만 허용하는 와일드카드</li>
    <li>주로 값을 추가할 때 사용</li>
</ul>

</blockquote>

```java
class Item<T> {
    T data;
    
    public T getData() {
        return data;
    }
    
    public void setData(T data) {
        this.data = data;
    }
}

static void printItem(Item<?> item){
    String data = item.toString();
    System.out.println(data);
}


static void printItem(Item<? extends Number> num) { //upper bounded wildcard
    Item<? extends Number> y = new Item<Number>();
    y = new Item<Integer>();
    y = new Item<Double>();
}

static void printItem() {
    Item<? Super Number > x = new Item<Number>(); //lower bounded wildcard
    
}
```


# 래퍼 클래스

<blockquote>
    <h2>Wrapper &Rightarrow; 자바에서 기본 자료형처럼 사용할 수 있도록 제공하는 클래스</h2>

|   기본형   | Wrapper 클래스 |
|:-------:|:-----------:|
| boolean |   Boolean   |
|  byte   |    Byte     |
|  char   |  Character  |   
|  short  |    Short    |
|   int   |   Integer   |
|  long   |    Long     |
|  float  |    Float    |
| double  |   Double    |

<ul>
    <li>기본 타입은 객체가 아니기 때문에 API나 데이터 구조에서 값을 직접 사용 불가</li>
    <li>value는 final 변수이기 때문에 한번 생성하면 값을 변경할 수 없음</li>
    <li>언박싱, 오토박싱</li>
        <ul>
            <li>언박싱 : 객체형 &rightarrow; 기본형</li>
            <li>오토박싱 : 기본형 &rightarrow; 객체형</li>
        </ul>
</ul> 
</blockquote>

```java
    
    Integer integer = new Integer(10); // 이 방식은 Java9부터 사용하지 않는 방식
    
    Integer integer = Integer.valueOf(10);
                   or
    Integer integer = 10; //이런 식으로 선언해야함
```

# 옵셔널

<blockquote>
<h2>
    Optional &Rightarrow; 값이 있을 수도 있고 없을 수도 있는 객체를 감싸는 역할
</h2>
<ul>
    <li>주로 NULL 처리를 안전하고 명시적으로 다루기 위해 사용</li>
    <li>NullPointerException 방지</li>
</ul>
    
</blockquote>

```java

import java.util.Optional;

Optional<String> optional = Optional.of("JAVA");

Optional<String> optional = Optional.ofNullable(null);

```
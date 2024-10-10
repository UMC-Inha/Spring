# 추가 과제

---

## 제네릭

- 데이터 타입이 클래스 내부가 아닌 외부에서 사용자 의해 지정되는 것
- 타입 안정성과 재사용성을 높이기 위해 사용

```java
public class Box<T> {
    private T item;

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
}

Box<String> stringBox = new Box<>(); //타입 지정하기
String item = stringBox.getItem(); 
```

## 제네릭의 장점

- 제네릭을 이용하면 컴파일 시점에 타입을 체크하여 런타임 오류를 줄일 수 있음
- 클래스 외부에서 타입을 지정하여 사용하므로 타입을 체크하고 변환할 필요가 없음
- 동일한 코드를 다양한 데이터 타입에 적용할 수 있으므로 코드의 중복이 줄고, 재사용성이 높아짐
- 타입 캐스팅을 줄일 수 있어 성능이 향상됨

## 제네릭의 단점

- 제네릭은 클래스와 인터페이스에만 적용되기 때문에 기본 데이터 타입은 사용이 불가능함
- 제네릭은 컴파일 시점에 타입 정보를 유지하지만, 런타임 시점에서는 정보가 사라지므로 제약을 받는 경우가 생길 수 있음
- 여러개의 제네릭 타입이 얽혀 있는 경우, 디버깅 메세지가 복잡해져 디버깅에 어려움이 생길 수 있음

## Wrapper 클래스

- 자바의 기본 타입을 클래스화 한 8개의 클래스
- Byte, Short, Integer, Long, Character, Float, Double, Boolean 존재
- 위의 8개의 클래스를 지원하여 기본 타입의 값을 객체로 다룰 수 있도록 함

## Wrapper 클래스 특징

- null값 허용
- 불변성 : Wrapper 클래스가 생성된 이후에는 상태를 변경할 수 없음
- 유틸리티 메서드 지원
- equal() 메서드를 통해 객체 간의 값 비교 가능 (일반 객체는 참조를 비교)

## Wrapper 클래스가 필요한 이유

- 프로그램에 따라 데이터를 객체로만 처리해야하는 경우가 있는데, 이 경우 기본 데이터 타입을 처리할 수 없음 → 기본 데이터를 객체로 다룰 수 있도록 하는 Wrapper 클래스가 필요함
- 기본 데이터 타입에 대해 유틸 메서드들을 제공해주어 사용에 용이함
- Wrapper 클래스는 null값을 가질 수 있으므로  기본타입이 아닌 상태를 나타낼 수 있음

## 박싱과 언박싱

- **박싱:** 기본 타입의 데이터를 Wrapper 클래스 객체(인스턴스)로 변환하는 것
- **언박싱:** Wrapper 클래스에 저장된 값을 기본 타입의 데이터로 꺼내는 것
- **필요한 이유:**  Wrapper 클래스는 산술 연산을 위해 정의된 클래스가 아니기 때문에, 객체(인스턴스)에 지정한 값을 변경할 수 없으며 값을 변경하기 위해서는 새로운 인스턴스에 새로운 값을 지정해야 한다.  박싱을 통해 기본 데이터를 객체로 변환하고 언박싱을 통해 필요한 상황에서 기본 데이터로 변환하여 연산을 수행한다.

## 오토 박싱과 오토 언박싱

- JDK 1.5부터 자바 컴파일러는 박싱, 언박싱이 필요한 상황에서 자동으로 처리를 해줌

```java
Integer num = new Integer(17); // 박싱
int n = num.intValue();        // 언박싱

Integer num2 = 17; // 오토박싱
int n2 = num2;        // 오토언박싱
```

## Wrapper 클래스와 기본 타입 둘다 사용하는 이유?

- 기본 데이터 타입이 Wrapper 클래스보다 메모리에 더 효율적으로 저장되며, 연산 속도가 빠름
- Wrapper 클래스는 값을 변경할 수 없으므로 변경이 잦은 경우에는 비효율적임
- 간단한 연산의 경우에는 기본 타입의 데이터를 사용하는 것이 더 직관적임
- 경우에 따라 객체만을 다루는 경우가 있으므로 기본 데이터 타입을 객체로 사용할 수 있어야 함.

⇒ 성능, 메모리 효율이 중요한 경우 기본 타입을 많이 사용하고, 객체로 다루면서 null값을 처리해야 할 때는 Wrapper 클래스를 사용함

## Optional

> `Optional` is primarily intended for use as a method return type where there is a clear need to represent "no result," and where using `null` is likely to cause errors. A variable whose type is `Optional` should never itself be `null`; it should always point to an `Optional` instance.
>
- Optional은 리턴 시 “결과 없음”을 명확하게 나타낼 필요가 있는 메서드의 리턴 타입으로 사용되도록 의도됨.
- Optional 타입의 변수는 절대 null이 될 수 없고, Optional 객체(인스턴스)를 가리키고 있어야 함

⇒  null로 인한 문제가 발생하는 것을 방지하고자 사용됨.

## Optional의 장점

- 리턴 값이 비어있는 경우를 명확히 알 수 있음
- null을 리턴하는 메서드보다 Optional을 리턴하는 메서드가 더 안전함(오류 가능성이 적음)
- null을 예외처리할 때보다 더 깔끔하고 가독성 있는 코드를 작성할 수 있음(Optional에서 값이 없으면 예외를 발생시켜 처리하는 방식으로 처리 가능)

## Optional의 단점

- Optional로 받은 변수값 존재여부를 확인하지 않을 시 NoSuchElementException이 발생할 수 있음.
- Optional이 감싸는 객체에 필요한 메모리는 물론, Optional 객체를 저장하기 위한 추가적인 메모리가 필요함 ⇒ 공간적 비용 증가
- Optional을 통해 내부의 객체에 접근해야 함 ⇒ 시간적 비용 증가

## Optioanl 사용 시 주의할 점

- Optional 변수에 null값을 할당하면 안됨(값 없으면 Optional.empty() 사용)
- Optional 내의 값만 얻는 목적으로 사용하는 것은 좋지 않음. (낭비 발생)
- 생성자, 수정자, 매개변수로 Optional을 사용하는 것은 비효율적임. (Optional은 반환 타입으로 이용하는 것이 가장 효과적)
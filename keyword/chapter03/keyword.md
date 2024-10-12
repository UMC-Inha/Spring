## 1. 제네릭 (Generics)

### 제네릭(Generics)란?

클래스나 메서드에서 사용할 데이터 타입을 미리 지정하지 않고, 코드 작성 시점이 아닌 실행 시점에 타입을 지정할 수 있도록 하는 Java의 기능.

### 장점

- **컴파일 타임 타입 체크**: 컴파일 시점에 타입 검사를 수행하여 런타임 시 발생할 수 있는 타입 오류를 방지할 수 있음.
- **형변환 생략**: 명시적 형변환(casting) 없이도 원하는 타입으로 데이터를 다룰 수 있어 코드의 가독성이 높아짐.
- **코드 재사용성 증가**: 다양한 타입을 받아 처리할 수 있어 동일한 로직을 여러 타입에 대해 적용할 수 있음.

### 예시 코드

```java
public class Box<T> {
    private T content;

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }

    public static void main(String[] args) {
        Box<String> stringBox = new Box<>();
        stringBox.setContent("Hello World");
        System.out.println(stringBox.getContent());

        Box<Integer> intBox = new Box<>();
        intBox.setContent(100);
        System.out.println(intBox.getContent());
    }
}
```

---

## 2. 와일드카드 (Wildcard)

### 와일드카드(`?`)란?

제네릭 타입을 보다 유연하게 사용할 수 있도록 하는 문법 요소. 제네릭 타입을 정의할 때 특정한 타입 범위를 제한하거나 어떤 타입이든 수용할 수 있는 클래스를 정의할 수 있음.

### 종류

- `?` : 어떤 타입도 가능
- `? extends T` : T 또는 T의 하위 타입을 허용
- `? super T` : T 또는 T의 상위 타입을 허용

### 예시 코드

```java
import java.util.List;

public class WildcardExample {

    // <? extends Number>는 Number의 하위 타입만 수용 가능
    public static void printNumbers(List<? extends Number> list) {
        for (Number n : list) {
            System.out.println(n);
        }
    }

    public static void main(String[] args) {
        List<Integer> intList = List.of(1, 2, 3);
        printNumbers(intList); // 출력: 1, 2, 3

        List<Number> numberList = List.of(1.1, 2.2, 3.3);
        printNumbers(numberList); // 출력: 1.1, 2.2, 3.3
    }
}
```

---

## 3. 래퍼 클래스 (Wrapper Class)

### 래퍼 클래스(Wrapper Class)란?

기본형(Primitive Type) 데이터를 객체처럼 다룰 수 있도록 제공하는 클래스. Java에서는 `int`, `double`, `char` 같은 기본형 데이터 타입을 객체로 변환하여 처리할 수 있도록 `Integer`, `Double`, `Character` 등의 래퍼 클래스를 제공.

### 장점

- **컬렉션 사용 가능**: 기본형은 `List`나 `Set`과 같은 컬렉션 프레임워크에 직접 사용할 수 없지만, 래퍼 클래스를 사용하면 가능함.
- **객체로서의 장점**: 기본형은 메서드를 가지지 않지만, 래퍼 클래스는 다양한 메서드를 제공하여 데이터 처리가 용이함.

### 예시 코드

```java
public class WrapperExample {
    public static void main(String[] args) {
        int num = 10; // 기본형
        Integer wrappedNum = Integer.valueOf(num); // 기본형 -> 래퍼 클래스

        System.out.println("Wrapped Integer: " + wrappedNum); // 출력: 10

        int unwrappedNum = wrappedNum.intValue(); // 래퍼 클래스 -> 기본형
        System.out.println("Unwrapped Integer: " + unwrappedNum); // 출력: 10

        // 오토박싱과 오토언박싱
        Integer autoBoxedNum = num; // 자동으로 기본형 -> 객체화
        int autoUnboxedNum = wrappedNum; // 자동으로 객체 -> 기본형화
    }
}
```

---

## 4. 옵셔널 (Optional)

### Optional이란?

`Optional`은 Java 8에서 도입된 클래스로, `null` 값을 명시적으로 처리하기 위해 사용 객체가 존재할 수도 있고 존재하지 않을 수도 있는 경우, `Optional`을 사용하여 `null` 체크를 더 효율적이고 안전하게 할 수 있음.

### 장점

- **NullPointerException 방지**
- **가독성 향상**: `null` 체크를 코드 곳곳에서 반복하는 대신, `Optional` 메서드를 통해 가독성이 좋은 코드를 작성할 수 있음.

### 예시 코드

```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {

        Optional<String> optionalString = Optional.of("Hello");

        // 값이 존재할 때만 실행
        optionalString.ifPresent(value -> System.out.println("Value: " + value));

        // 기본값 설정
        String defaultValue = optionalString.orElse("Default Value");
        System.out.println("Default Value: " + defaultValue); // 출력: Hello

        // 값이 없는 경우
        Optional<String> emptyOptional = Optional.empty();
        String result = emptyOptional.orElse("Empty Optional");
        System.out.println("Result: " + result); // 출력: Empty Optional
    }
}
```

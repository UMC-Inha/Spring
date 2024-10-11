## 제네릭

제네릭(Generics)는 자바에서 **타입의 안전성**을 높이고, 코드의 **재사용성**을 높이기 위해 도입된 기능

제네릭은 클래스나 메서드를 선언할 때 **데이터 타입을 일반화**를 할수있게 도와준다

→ 다양한 타입에 대해 같은 코드를 사용 가능

→ 컴파일 시 타입 체크를 통해 오류를 미리 방지

```java
// 제네릭 클래스를 사용한 예
public class Box<T> {
    private T item;
    
    public void set(T item) {
        this.item = item;
    }

    public T get() {
        return item;
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Integer> intBox = new Box<>();
        intBox.set(123);
        System.out.println(intBox.get()); // 123

        Box<String> strBox = new Box<>();
        strBox.set("Hello");
        System.out.println(strBox.get()); // Hello
    }
}

```

## 래퍼 클래스(wrapper class)

래퍼 클래스(Wrapper Class)는 기본 자료형(primitive type)을 **객체로 감싸는 클래스**

기본 자료형은 객체가 아니므로 자바의 컬렉션 프레임워크 같은 **객체를 필요로 하는 API**에서 사용할 수 없다.

래퍼 클래스를 이용하면 기본 자료형을 객체로 다룰 수 있습니다. ex)  int→integer, double→Douoble

박싱 : **기본타입**의 데이터 -> **래퍼 클래스**의 인스턴스로 변환하는 과정

언박싱 : **래퍼 클래스**의 인스턴스에 저장된 값 -> **기본 타입**의 데이터로 꺼내는 과정

→ jdk 1.5 이상부터 자바 컴파일러가 자동으로 처리해주기 때문에 오토박싱 오토 언박싱이 가능하다

```java
// 박싱
// Integer 래퍼 클래스 num 에 21 의 값을 저장
Integer num = new Integet(21);

// 언박싱
// 래퍼 클래스 num 의 값을 꺼내 가져온다.
int n = num.intValue();
```

## 옵셔널(Optional)

옵셔널(Optional)은 자바 8에서 도입된 클래스로 **null 값을 처리**할때 사용

기존에는 객체가 null일 가능성을 항상 고려하고, 그에 따른 **NullPointerException**을 처리

→Optional 클래스를 사용하면 **null 처리**를 더욱 안전하게 할 수 있고, 코드의 가독성을 높일 수 있다

```java
import java.util.Optional;

public class Main {
    public static void main(String[] args) {
        Optional<String> optionalString = Optional.of("Hello");

        // 값이 있는 경우 처리
        optionalString.ifPresent(value -> System.out.println("Value: " + value));

        // 값이 없을 때 기본값 제공
        String result = optionalString.orElse("Default Value");
        System.out.println(result);

        // 값이 없을 수도 있는 상황
        Optional<String> emptyOptional = Optional.empty();
        System.out.println(emptyOptional.orElse("No Value"));
    }
}
```
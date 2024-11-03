## 함수형 인터페이스

**오직 하나의 추상 메서드만 포함하는 인터페이스**

Java 8 이후로 @FuctionalInterface 애노테이션을 사용하여 함수형 인터페이스를 정의→ 인터페이스가 하나의 추상 메서드만 포함하도록 강제, 그렇지 않으면 컴파일 오류 발생

주로 람다 표현식이나 메서드 참조와 함께 사용

→ 코드의 가독성을 높이고, 코드의 양을 줄임

java.util.function 패키지는 여러 가지 함수형 인터페이스를 제공합니다:

- Function<T,R> : 입력을 받아서 결과를 반환하는 함수형 인터페이스로, 인자의 타입 T를 받아 결과 R을 반환합니다.
- Predicate<T> : 입력값을 받아 boolean 값을 반환하는 인터페이스로, 주로 필터링 조건을 지정하는 데 사용됩니다.
- Supplier<T> : 값을 생성하여 반환하는 역할을 하며, 인자는 없고 반환 값이 있는 함수형 인터페이스입니다.
- Consumer<T> : 값을 받아서 사용하지만, 반환값이 없는 인터페이스로, 주로 출력 작업에 활용됩니다.

**질문**: 함수형 인터페이스와 람다 표현식은 기존 인터페이스와 어떤 점에서 다른가요?

→ 함수형 인터페이스는 단 하나의 추상 메서드만 가지므로, 이를 람다 표현식으로 간단하게 구현할 수 있습니다. 기존 인터페이스는 일반적으로 메서드를 여러 개 가질 수 있고, 구현 클래스가 이를 모두 구현해야 합니다. 하지만 함수형 인터페이스는 단일 기능을 갖고 있어서 람다 표현식으로 간결하게 처리할 수 있고, 특히 고차 함수 형태로 다른 메서드에 전달하거나 사용할 수 있어 함수형 프로그래밍을 지원합니다.

```java
import java.util.function.Function;

public class mission {
    public static void main(String[] args) {

        // 익명 클래스 사용
        Function<Integer, String> anonymousFunction = new Function<Integer, String>() {
            public String apply(Integer i){
                return "익명 클래스: " + i.toString();
            }
        };

        // 클래스 상속
        class MyFunction implements Function<Integer, String> {
            @Override
            public String apply(Integer i) {
                return "클래스 상속: " + i.toString();
            }
        }
        Function<Integer, String> myFunction = new MyFunction();

        // 람다식으로 정의
        Function<Integer, String> lambdaFunction = i -> "람다식: " + i.toString();

        // 메서드 참조로 정의
        Function<Integer, String> referenceFunction = String::valueOf;

        Integer input = 10;
        System.out.println(anonymousFunction.apply(input));
        System.out.println(myFunction.apply(input));
        System.out.println(lambdaFunction.apply(input));
        System.out.println("메서드 참조: " + referenceFunction.apply(input));
    }
}

```

## Stream Api

**데이터 컬렉션을 더 효율적이고 직관적으로 처리할 수 있도록 도와주는 API**

스트림은 데이터 소스(컬렉션, 배열, 파일 등)에서 생성

요소들을 **필터링, 매핑, 정렬, 집계** 등의 다양한 작업을 적용할 수 있다

스트림의 주요 특징

- 선언형 코드 스타일 : 기존의 반복문을 사용해 조건을 추가하고 결과를 수동으로 모으던 방식과 달리, 스트림은 메서드 체이닝 방식으로 직관적이고 간결한 선언형 코드 스타일을 제공합니다.
- 내부 반복 사용:  for 루프와 같은 외부 반복 대신 스트림이 내부 반복을 사용하여 작업을 수행하며, 병렬 처리를 간편하게 적용할 수 있습니다
- 지연 실행: 스트림은 중간 연산(예: filter, map)이 지연 실행을 통해 최적화되므로 필요할 때만 실제로 연산을 수행합니다. 최종 연산이 호출될 때까지 중간 연산이 실행되지 않아 불필요한 연산을 줄이고 성능을 최적화합니다.
- 병렬 처리: parallelStream 메서드를 사용해 병렬 처리를 간편하게 적용, 대량 데이터 처리 시 성능을 크게 향상시킬 수 있습니다.

질문: Stream API를 사용하면 코드가 간결해지지만, 내부적으로 성능은 어떻게 최적화되나요?

Stream API는 내부 반복과 지연 실행을 통해 성능을 최적화합니다. 중간 연산은 최종 연산이 호출될 때까지 실행을 지연하여 불필요한 계산을 피하고, 병렬 스트림을 통해 멀티코어 환경에서 병렬 처리가 가능하여 대량 데이터 처리 성능을 높입니다.

```java
import java.util.Arrays;
import java.util.stream.Collectors;

public class mission {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

        // 원본 배열 출력
        System.out.println("원본 배열: " + Arrays.toString(numbers));

        // 배열 요소 모두를 2배로 만든 배열
        int[] doubledArray = Arrays.stream(numbers)
            .map(num -> num * 2)
            .toArray();
        System.out.println("2배로 만든 배열: " + Arrays.toString(doubledArray));
        
        // 배열 중 짝수만 "X is even number"로 변환하여 String 배열로 생성
        String[] evenNumbersArray = Arrays.stream(numbers)
            .filter(num -> num % 2 == 0)
            .mapToObj(num -> num + " is even number")
            .toArray(String[]::new);

        // 결과 출력
        System.out.println("짝수 변환 배열: " + Arrays.toString(evenNumbersArray));
    }
}

```
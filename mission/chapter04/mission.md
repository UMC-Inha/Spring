## 추가 과제 1번

### 함수형 인터페이스 (Functional Interface)

정의: 함수형 인터페이스는 하나의 추상 메서드만을 가지는 인터페이스

```java
public class FunctionExamples {
    public static void main(String[] args) {
        Integer input = 10;


        Function<Integer, String> anonymousFunction = new Function<Integer, String>() {
            @Override
            public String apply(Integer t) {
                return String.valueOf(t);
            }
        };
        System.out.println("익명 클래스: " + anonymousFunction.apply(input));


        MyFunction myFunction = new MyFunction();
        System.out.println("클래스 파일: " + myFunction.apply(input));


        Function<Integer, String> lambdaFunction = t -> String.valueOf(t);
        System.out.println("람다식: " + lambdaFunction.apply(input));

        Function<Integer, String> methodReferenceFunction = String::valueOf;
        System.out.println("메서드 참조: " + methodReferenceFunction.apply(input));
    }
}
```

## 추가 과제 2번

### 정의

- Stream API는 Java 8에서 도입된 기능으로, 컬렉션이나 배열과 같은 데이터를 처리하기 위한 연속적인 데이터 흐름을 제공.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExamples {
    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

        int[] doubledArray = Arrays.stream(array)
                                   .map(i -> i * 2)
                                   .toArray();

        System.out.println("원본 배열: " + Arrays.toString(array));
        System.out.println("2배된 배열: " + Arrays.toString(doubledArray));

        List<String> evenStringList = Arrays.stream(array)
                                            .filter(i -> i % 2 == 0)
                                            .mapToObj(i -> i + " is even number")
                                            .collect(Collectors.toList());
        System.out.println("짝수만 고른 배열: " + evenStringList);
    }
}
```

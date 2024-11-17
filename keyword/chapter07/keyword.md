- RestContollerAdvice

  `@RestControllerAdvice`는 Spring Framework에서 사용되는 어노테이션으로, REST API에서 전역적으로 예외를 처리하기 위해 사용

  이를 통해 애플리케이션의 오류를 통일된 형식으로 관리하고, 사용자에게 적절한 응답을 반환

  ### 기능 및 특징

    - **예외 처리 전역화**: `@RestControllerAdvice`는 애플리케이션 전반에서 발생하는 예외를 전역적으로 처리, 코드에서 개별적으로 예외 처리를 하지 않아도 됩니다.
    - **JSON 응답 형식**: REST API에서 사용되므로, 예외가 발생하면 기본적으로 JSON 형태로 오류 메시지를 반환합니다.
    - **커스터마이징 가능**: 예외 처리 방식을 커스터마이징하여 특정 예외에 대해 다른 HTTP 상태 코드나 메시지를 반환

  ### 주요 어노테이션

    - **`@ExceptionHandler`**: 특정 예외 유형을 처리하는 메소드에 사용됩니다. 각 예외에 대한 처리 로직을 정
    - **`@InitBinder`**: 요청 데이터 바인딩 전에 특정 동작을 수행하도록 설정
    - **`@ModelAttribute`**: 모든 컨트롤러에서 공통적으로 사용될 모델 데이터를 설정
- lombok

  Lombok 은 Java에서 반복적인 코드를 줄여주는 라이브러리

  Lombok을 사용하면 getter, setter, toString, equals, hashCode, 생성자 등을 자동으로 생성

  →코드의 가독성을 높이고 유지보수를 쉽게 할 수 있습니다.

  ### 주요 어노테이션

    - @Getter / @Setter: 필드에 대해 getter와 setter 메소드를 생성합니다.
    - @ToString : 객체의 tostring() 메소드를 자동으로 생성합니다.
    - @EqualsAndHashcode: 객체의 equals와 hashcode() 메소드를 자동으로 생성합니다.
    - @NoArgsConstructor / @AllArgsConstructor / @RequiredArgsConstructor: 다양한 형태의 생성자를 자동으로 생성합니다.
    - @Builder: 빌더 패턴을 적용하여 객체를 생성할 수 있습니다.
    - @Slf4j: 로깅을 위해 SLF4J Logger 객체를 자동으로 생성합니다.

  ### 장점

    - 코드 간결화
    - 개발 속도 향상
    - 유지보수 용이

  ### 단점

    - 런타임 의존성
    - 컴파일러 의존성
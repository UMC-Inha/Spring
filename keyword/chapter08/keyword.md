- java의 Exception 종류들
    
    checked Exception
    
    - 컴파일 시점에 반드시 처리해야 하는 예외.
    - exception 클래스를 상속받은 예외들 중 `RuntimeException`을 제외한 예외들이 해당.
    - 예외를 처리하지 않으면 컴파일 에러가 발생.
    - **예시:**
        - `IOException`: 파일 읽기/쓰기, 네트워크 통신 등에서 발생할 수 있는 예외.
        - `SQLException`: 데이터베이스 접근 중 발생할 수 있는 예외.
        - `ClassNotFoundException`: 클래스 파일을 찾지 못할 때 발생.
        - `InterruptedException`: 스레드가 중단되었을 때 발생.
    
    unchecked exception
    
    - 실행 시점에 발생하는 예외.
    - `RuntimeException` 클래스를 상속받은 예외들.
    - 예외를 처리하지 않아도 컴파일 시 에러가 발생하지 않음.
    - **예시:**
        - `NullPointerException`: `null` 객체를 참조하려고 할 때 발생.
        - `ArrayIndexOutOfBoundsException`: 배열의 잘못된 인덱스에 접근할 때 발생.
        - `IllegalArgumentException`: 잘못된 인수(argument)가 전달될 때 발생.
        - `ArithmeticException`: 0으로 나누는 등의 산술 오류가 발생할 때.
    
    Error
    
    - 심각한 시스템 수준의 문제를 나타내며, 일반적으로 복구할 수 없음.
    - `Error` 클래스는 `Throwable`의 하위 클래스이며, 주로 JVM에서 발생.
    - **예시:**
        - `OutOfMemoryError`: JVM 메모리가 부족할 때 발생.
        - `StackOverflowError`: 재귀 호출이 너무 깊어 스택이 넘쳤을 때 발생.
        - `VirtualMachineError`: JVM이 치명적인 문제를 만났을 때 발생
- @Valid
    
    `@Valid`는 Java Bean Validation을 위한 어노테이션으로, 객체의 필드를 유효성 검증하는 데 사용
    
    **특징**
    
    - `@Valid`는 Spring MVC 및 Spring Boot에서 유효성 검증(Validation) 용도로 사용.
    - 컨트롤러 메서드의 매개변수 앞에 사용하여 입력 데이터의 유효성을 검사.
    - `javax.validation` 패키지에 속해 있으며, 일반적으로 `Bean Validation` 표준(JSR-303, JSR-380)에 따라 사용.
    1. 엔티티 클래스에 유효성 검증 어노테이션 추가:
        - `@NotNull`, `@Size`, `@Pattern` 등의 제약 조건을 필드에 지정.
    2. 컨트롤러에서 `@Valid` 어노테이션을 사용:
        - `@Valid`를 사용하여 DTO(Data Transfer Object)나 엔티티에 적용된 검증 규칙이 체크되도록 함.
        - 검증 실패 시, 예외가 발생하여 에러 메시지를 반환할 수 있음.
    
    ex)
    
    - `@NotNull`: 필드가 `null`이 아닌지 확인.
    - `@NotEmpty`: 필드가 비어 있지 않은지 확인 (문자열 길이가 0이 아닌지).
    - `@NotBlank`: 필드가 공백이 아닌지 확인 (공백만으로 이루어지지 않았는지).
    - `@Size`: 문자열, 컬렉션 등의 크기 범위를 지정.
    - `@Min`, `@Max`: 숫자 값의 최소/최대 값을 지정.
    - `@Email`: 이메일 형식이 올바른지 확인.
    - `@Pattern`: 정규 표현식을 사용한 패턴 일치 검사.
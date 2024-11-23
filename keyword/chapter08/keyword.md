# @Valid

@Valid는 Java Bean Validation을 기반으로 한 어노테이션으로, 주로 스프링에서 사용됨.

## Valid의 검사 과정
1. 어노테이션 선언 -> DTO 클래스나 엔티티 클래스의 필드에 제약 조건을 정의
2. 컨트롤러 매개변수, 서비스 계층, 또는 임의의 객체에서 @Valid를 사용하여 유효성 검사를 수행
3. 	@Valid 어노테이션은 객체의 각 필드를 확인하며, 선언된 제약 조건을 Hibernate Validator에 전달해 검사
4. 유효성 검사 실패 시 예외(ConstraintViolationException 또는 MethodArgumentNotValidException)가 발생함

# Java Exception의 종류
## 1. Checked Exception

- 컴파일 시점에 반드시 처리해야 하는 예외.
- 예외를 처리하지 않으면 컴파일 에러가 발생.
- 따라서 throw나 try catch로 예외 처리를 꼭 해야함.

###  종류
- IOException
- SQLException
- FileNotFoundException

## 2. Unchecked Exception

- 런타임 시 발생하는 예외.
- 컴파일러가 강제로 처리하도록 요구하지 않음.
- 주로 프로그래머의 실수로 인해 발생.

### 종류
- NullPointerException
- ArrayIndexOutOfBoundsException
- ArithmeticException
- Valid 같은 경우 Unchecked Exception인 ConstraintViolationException, 	MethodArgumentNotValidException을 발생시킴

## ConstraintViolationException vs MethodArgumentNotValidException

| **구분** |**ConstraintViolationException**|**MethodArgumentNotValidException** |
|---------|------------------------------|------------------------|
| **발생 위치**| 서비스 계층(Service Layer) 및 비-컨트롤러 환경| 컨트롤러 계층(Controller Layer)|
| **유효성 검사 대상** | 직접 호출한 `Validator` 또는 메서드 파라미터, 반환값 검사 | 컨트롤러 메서드의 `@Valid`와 `@RequestBody` 또는 `@ModelAttribute`를 통한 객체 |
| **예외 발생 조건**  | 명시적으로 Validator 호출하거나 서비스/메서드 매개변수에서 검사 실패 시 발생 | 컨트롤러에서 유효성 검사 실패 시 발생 |
| **유효성 검사 방식** | `javax.validation.Validator`의 직접 호출로 발생 | Spring MVC의 메서드 매개변수 자동 바인딩 및 유효성 검사 실패로 발생  |
| **제공 정보** | 실패한 **제약 조건**(`ConstraintViolation`) 정보 포함 | 실패한 **필드 값**(`BindingResult`) 정보 포함 |
| **Checked/Unchecked** | Unchecked Exception (`ValidationException` 하위 클래스) | Unchecked Exception (`RuntimeException` 하위 클래스)|
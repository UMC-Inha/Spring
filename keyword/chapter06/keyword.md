# 지연 로딩(Lazy Loading)과 즉시 로딩(Eager Loading)의 차이

## 지연 로딩
데이터가 실제로 필요할 때 쿼리를 실행하여 연관된 데이터를 불러옴.

## 연관 로딩
연관된 엔티티를 하나의 쿼리로 즉시 조회하며, 연관된 엔티티를 전부 갖고 옴.

# Fetch Join

## 정의
Fetch Join은 JPQL에서 사용되는 문법으로, 한 번의 쿼리로 연관된 엔티티를 함께 조회할 수 있게 해줌.

## 사용법
```java
@Query("SELECT u FROM User u JOIN FETCH u.posts WHERE u.id = :userId")
User findUserWithPosts(@Param("userId") Long userId);
```

# EntityGraph

## 정의
@EntityGraph는 특정 엔티티에 대해 쿼리 시 연관된 엔티티를 함께 조회하는 방법을 정의하는 어노테이션

## 특징
Fetch Join과 달리 JPQL을 사용하지 않고 선언적으로 설정할 수 있음.

## 사용법
```java
@EntityGraph(attributePaths = {"posts"})
@Query("SELECT u FROM User u WHERE u.id = :userId")
User findUserWithPosts(@Param("userId") Long userId);
```

# JPQL
## 정의
객체 지향 쿼리 언어로, 엔티티 객체를 대상으로 하는 SQL과 유사한 쿼리를 작성할 수 있게 해줌. 차이점은 엔티티 클래스와 필드를 사용해, 테이블이 아닌 도메인 모델을 기준으로 동작함.

## JPQL을 사용할 때 SQL과의 차이점은?
JPQL은 객체 기반이므로 테이블 대신 엔티티를 사용하고, 필드에 대한 참조도 객체 필드명을 사용해야 함. 또한 JPQL은 데이터베이스 독립적이라는 점에서 SQL과 차별화됨.

# QueryDSL
## 정의
QueryDSL은 코드 기반으로 타입 안전한 쿼리를 작성할 수 있는 프레임워크.

## 특징
- 동적 쿼리를 작성할 때 유용함.
- 코드 기반 쿼리 작성을 통해 컴파일 타임에 쿼리의 오류를 발견할 수 있음.
- @Query에 의존하지 않고 메서드 체이닝을 통해 쿼리를 작성하므로 유지 보수성과 가독성이 높음.
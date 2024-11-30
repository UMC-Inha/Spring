# Spring Data JPA의 Paging

Spring Data JPA는 데이터베이스에서 페이징 처리를 간단히 구현할 수 있도록 도와줌.
대표적으로 **Page**와 **Slice** 객체를 사용하여 페이징을 처리함.

---

## 1. Page

`Page`는 페이징 결과와 함께 전체 데이터 개수, 페이지 수 등의 정보를 포함하고 있음.
`JpaRepository`의 `findAll(Pageable pageable)` 메서드를 사용하여 반환

### 특징
- **Content**: 현재 페이지의 데이터 리스트.
- **Total Elements**: 데이터베이스의 총 데이터 개수.
- **Total Pages**: 전체 페이지 개수.
- **Pageable**: 요청한 페이지 정보(페이지 번호, 크기, 정렬 기준 등).
- **Has Next**: 다음 페이지가 있는지 여부.
- **Has Previous**: 이전 페이지가 있는지 여부.

### 단점
- `Total Elements`를 계산하기 위해 추가 쿼리가 실행되므로 데이터가 많을 경우 성능에 영향을 줄 수 있음.

### 사용처
- 복잡한 페이징에 주로 사용함.

### 사용 예시
```java
Page<User> users = userRepository.findAll(PageRequest.of(0, 10));
System.out.println("Total Pages: " + users.getTotalPages());
System.out.println("Total Elements: " + users.getTotalElements());
System.out.println("Users: " + users.getContent());
```

---

## 2. Slice

`Slice`는 `Page`와 유사하지만, 전체 데이터 개수(`Total Elements`)를 계산하지 않음.  
`findAll(Pageable pageable)` 메서드로 반환되며, 다음 페이지가 있는지 여부만 확인할 때 유용함.

### 특징
- **Content**: 현재 페이지의 데이터 리스트.
- **Pageable**: 요청한 페이지 정보.
- **Has Next**: 다음 페이지가 있는지 여부.

### 장점
- `Total Elements`를 계산하지 않아 성능이 더 우수.
- 필요한 데이터만 가져오므로 메모리 사용량이 적음.

### 단점
- 전체 데이터 개수를 알 수 없으므로 총 페이지 수를 표시하는 UI를 구성하기 어렵습니다.

### 사용처
- 무한 스크롤처럼 다음 페이지의 존재 여부가 중요할 때 용이.

### 사용 예시
```java
Slice<User> users = userRepository.findAll(PageRequest.of(0, 10));
System.out.println("Has Next: " + users.hasNext());
System.out.println("Users: " + users.getContent());
```

---

## Page vs Slice

| 특징                 | Page                          | Slice                 |
|----------------------|-------------------------------|-----------------------|
| **전체 데이터 개수 제공** | Yes                           | No                    |
| **성능**              | 느림 (추가 쿼리 발생)         | 빠름                  |
| **적합한 상황**        | 전체 데이터 관련 UI 제공 시    | 간단한 데이터 조회 시 |

---

# 객체 그래프 탐색 (Object Graph Navigation)

객체 그래프 탐색은 **JPA 엔티티 간의 관계를 통해 객체를 탐색**하며 데이터를 조회하는 과정.  
연관된 데이터를 조회할 때, JPA는 **지연 로딩(Lazy Loading)**과 **즉시 로딩(Eager Loading)**을 사용.

---

## 정의
- **객체 그래프 탐색**: 엔티티 간의 연관 관계를 따라 필요한 데이터를 조회하는 행위.
  예: `Member` 엔티티에서 연관된 `Team` 엔티티를 탐색.
- **Fetch 전략**:
  - **Lazy Loading**: 연관 데이터를 실제로 사용할 때 조회 (기본 설정).
  - **Eager Loading**: 연관 데이터를 함께 조회.

---

## 장단점

### 장점
- **편리성**: 엔티티 간의 관계를 통해 데이터를 직관적으로 조회할 수 있음.
- **유연성**: Fetch 전략에 따라 데이터를 효율적으로 가져올 수 있음.

### 단점
- **N+1 문제**: Lazy 로딩 시 연관된 데이터를 개별적으로 조회하여 성능 문제가 발생할 수 있음.
- **복잡성**: Fetch 전략 설정을 잘못하면 예상치 못한 쿼리 발생.

---

## 해결 방법

1. **Fetch Join**  
   JPQL에서 `join fetch`를 사용해 연관된 엔티티를 한 번에 조회.
   ```java
   @Query("SELECT m FROM Member m JOIN FETCH m.team")
   List<Member> findAllWithTeam();
   ```

2. **EntityGraph**  
   Spring Data JPA의 어노테이션으로 Fetch Join을 간단히 대체.
   ```java
   @EntityGraph(attributePaths = "team")
   List<Member> findAll();
   ```

3. **BatchSize**  
   Lazy 로딩 시 한 번에 가져올 엔티티 수를 설정해 N+1 문제를 완화.
   ```java
   @BatchSize(size = 10)
   @OneToMany(mappedBy = "member")
   private List<Order> orders;
   ```

---
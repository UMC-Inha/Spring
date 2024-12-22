## **1. Spring Security란?**
**Spring Security**는 Spring Framework 기반 애플리케이션의 보안을 책임지는 프레임워크로, **인증(Authentication)** 과 **인가(Authorization)** 를 중심으로 보안 기능을 제공한다. 주요 기능은 다음과 같다:

- **인증(Authentication):** 사용자의 신원을 확인한다.  
- **인가(Authorization):** 인증된 사용자의 권한을 검사한다.  
- **CSRF (Cross-Site Request Forgery) 보호:** 악성 요청을 방지한다.  
- **Session 관리:** 사용자 세션을 효과적으로 관리한다.  
- **암호화(Encryption):** 비밀번호 및 중요한 데이터를 암호화한다.  
- **ACL (Access Control List):** 세분화된 접근 제어를 제공한다.  

---

## **2. Spring Security의 주요 구성 요소**
### **2.1 SecurityContext**
- **SecurityContext**는 인증된 사용자의 보안 정보를 저장한다.  
- 인증된 사용자의 `Authentication` 객체를 포함한다.

### **2.2 Authentication**
- 인증된 사용자의 정보를 나타내는 인터페이스다.  
- `Principal`: 인증된 사용자 객체  
- `Credentials`: 인증에 사용된 자격 증명 (예: 비밀번호)  
- `Authorities`: 사용자의 권한 목록  

### **2.3 UserDetailsService**
- 사용자 정보를 데이터베이스나 외부 리소스에서 가져오는 서비스다.  
- 주로 `UserDetails` 객체를 반환한다.

### **2.4 PasswordEncoder**
- 사용자 비밀번호를 안전하게 저장하기 위해 암호화를 수행한다.  
- `BCryptPasswordEncoder`가 일반적으로 사용된다.

### **2.5 AuthenticationManager**
- 인증을 처리하는 핵심 구성 요소다.  
- 사용자의 자격 증명을 검증하고, `Authentication` 객체를 반환한다.

---

## **3. 인증(Authentication)**
### **3.1 인증 흐름**
1. 사용자가 애플리케이션에 로그인 요청을 전송한다.  
2. Spring Security의 **AuthenticationManager**가 요청을 검증한다.  
3. 검증된 정보는 **SecurityContextHolder**에 저장된다.  

### **3.2 인증 방법**
- **Form Login:** 로그인 폼 사용  
- **HTTP Basic Auth:** HTTP 헤더 사용  
- **Token-Based Auth:** JWT(JSON Web Token) 사용  

---

## **4. 인가(Authorization)**
### **4.1 인가 흐름**
1. 인증된 사용자는 접근을 요청한다.  
2. Spring Security는 사용자의 권한을 확인한다.  
3. 접근이 허용되거나 거부된다.  

### **4.2 인가 방법**
- **Role-Based Access Control (RBAC):** 역할(Role) 기반으로 인가한다.  
- **Authority-Based Access Control:** 권한(Authority) 기반으로 인가한다.  

---

## **5. 주요 보안 기능**
### **5.1 CSRF Protection**
- CSRF 공격을 방지한다.

### **5.2 CORS (Cross-Origin Resource Sharing)**
- 다른 출처에서의 요청을 제어한다.

### **5.3 Session Management**
- 세션 고정 공격을 방지한다.

---

## **6. 필터 (Filters)**
### **6.1 UsernamePasswordAuthenticationFilter**
- 사용자 이름과 비밀번호를 사용하여 인증을 처리한다.

### **6.2 JwtAuthenticationFilter**
- JWT 토큰을 사용하여 인증을 처리한다.

---


## **7. 인증과 인가의 차이점**
| **구분** | **인증(Authentication)** | **인가(Authorization)** |
|----------|--------------------------|-------------------------|
| **목적** | 사용자의 신원을 확인한다. | 리소스 접근 권한을 확인한다. |
| **기반** | 사용자 이름, 비밀번호     | 역할(Role), 권한(Authority) |
| **결과** | `Authentication` 객체 생성 | 접근 권한 부여/거부    |

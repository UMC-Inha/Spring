## Spring Security

### Spring Security?
- Spring Security는 스프링 기반 애플리케이션의 보안을 담당하는 강력하고 유연한 프레임워크이다.
- 기본적으로 인증(Authentication)과 인가(Authorization)을 중심으로 설계되어 있으며, 애플리케이션 보안을 강화하기 위한 다양한 기능을 제공한다. Spring Security는 쉽게 확장 가능하며, 커스터마이징이 용이하다는 점에서 개발자들에게 큰 인기를 끌고 있다.

### Spring Security 특징
- **인증(Authentication):** 사용자의 신원을 확인하는 프로세스를 지원한다. ID와 비밀번호를 사용하는 전통적인 인증 방식뿐만 아니라 OAuth, SSO(Single Sign-On) 등 최신 인증 방식도 지원한다.
- **인가(Authorization):** 사용자 권한을 검증하여 리소스에 대한 접근을 제어한다. 이를 통해 사용자별로 애플리케이션 내에서 접근 가능한 범위를 제한할 수 있다.
- **보안 필터 체인:** HTTP 요청을 처리하기 위한 강력한 보안 필터 체인을 제공한다. 이 필터 체인은 요청이 서버로 전달되기 전에 여러 보안 정책을 적용한다.
- **CSRF(Cross-Site Request Forgery) 방어:** CSRF 공격을 방지하기 위한 기본적인 보호 기능을 제공한다.
- **세션 관리:** 세션 고정 공격 방지, 동시 세션 제어, 세션 만료 정책 등의 세션 보안 기능을 지원한다.
- **다양한 인증 메커니즘 지원:** 기본 인증, JWT(Json Web Token), OAuth2, SAML(Security Assertion Markup Language) 등 다양한 인증 방식을 제공한다.
- **암호화 지원:** 비밀번호 암호화를 위한 Bcrypt 등 여러 암호화 알고리즘을 내장하고 있다.

### 구성 요소
1. **SecurityContext:**
    - Spring Security의 핵심 구조로, 현재 인증된 사용자의 정보를 저장하고 공유하는 역할을 한다.
    - `SecurityContextHolder`를 통해 접근할 수 있으며, 애플리케이션 내에서 인증 정보가 필요할 때 사용된다.
    - 인증된 사용자의 세션 정보를 관리하여 인증 상태를 유지한다.

2. **AuthenticationManager:**
    - 인증 요청을 처리하는 핵심 컴포넌트이다.
    - 다양한 인증 방식을 지원하며, 여러 `AuthenticationProvider`를 결합하여 사용한다.
    - 요청된 자격 증명을 검증하고 인증 결과를 반환한다.
    - 예: ID와 비밀번호를 확인하거나 OAuth 토큰을 검증하는 작업을 수행한다.

3. **GrantedAuthority:**
    - 사용자가 가지는 권한의 목록을 정의한다.
    - 권한은 문자열로 표현되며, "ROLE_USER" 또는 "ROLE_ADMIN"과 같은 형태로 사용된다.
    - 인가(Authorization) 과정에서 사용자의 요청이 허용 가능한지 판단하는 데 사용된다.

4. **UserDetailsService:**
    - 사용자 정보를 데이터베이스나 외부 저장소에서 로드하는 역할을 한다.
    - 사용자 이름(ID)을 기반으로 사용자 정보를 반환하며, `UserDetails` 객체를 생성한다.
    - 개발자는 이 인터페이스를 구현하여 애플리케이션의 요구 사항에 맞는 사용자 인증 로직을 작성할 수 있다.
      ```java
      @Service
      public class CustomUserDetailsService implements UserDetailsService {
          @Override
          public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
              // 사용자 정보를 데이터베이스에서 조회
              User user = userRepository.findByUsername(username);
              if (user == null) {
                  throw new UsernameNotFoundException("User not found");
              }
              return new org.springframework.security.core.userdetails.User(
                      user.getUsername(),
                      user.getPassword(),
                      Collections.singletonList(new SimpleGrantedAuthority("ROLE_USER"))
              );
          }
      }
      ```

5. **PasswordEncoder:**
    - 비밀번호를 안전하게 저장하고 검증하기 위한 컴포넌트이다.
    - 비밀번호를 해싱하는 데 사용되며, 대표적으로 Bcrypt 알고리즘이 많이 사용된다.
    - Spring Security는 다양한 `PasswordEncoder` 구현체를 제공하며, 애플리케이션 요구 사항에 따라 선택하여 사용한다.
   
      ```java
      @Bean
      public PasswordEncoder passwordEncoder() {
          return new BCryptPasswordEncoder();
      }
      ```

### 기본 설정 예시
- Spring Security를 사용하는 기본적인 설정 예시이다. 
- HTTP 요청에 대한 인증과 인가 규칙을 정의한다

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .csrf().disable() // CSRF 보호 비활성화 (테스트 목적)
            .authorizeRequests()
                .antMatchers("/public/**").permitAll() // 특정 URL에 대한 접근 허용
                .anyRequest().authenticated() // 나머지 요청은 인증 필요
                .and()
            .formLogin()
                .loginPage("/login") // 커스텀 로그인 페이지 설정
                .permitAll()
                .and()
            .logout()
                .logoutUrl("/logout")
                .permitAll();
    }
}
```

### 응용 예제
Spring Security는 다양한 유형의 애플리케이션에서 사용될 수 있다!
- **전자상거래 사이트:** 사용자 로그인 및 권한에 따라 쇼핑 카트와 결제 기능 접근 제어.
- **기업 내부 시스템:** 직원의 역할(Role)에 따라 각기 다른 리소스에 대한 접근 권한 설정.
- **API 보안:** JWT를 사용하여 RESTful API 보호.

### 확장성
- Spring Security는 기본적인 보안 기능 외에도 필요에 따라 다양한 방식으로 확장할 수 있다.
- 커스텀 인증 필터, 사용자 정의 권한 정책, 외부 인증 시스템 연동 등으로 애플리케이션의 요구 사항에 맞는 보안을 구현할 수 있다.

---

## 인증(Authentication)과 인가(Authorization)

### 인증(Authentication)

#### 정의
인증은 사용자의 신원을 확인하는 과정이다. 애플리케이션은 사용자가 제공한 자격 증명(예: 아이디와 비밀번호)을 통해 사용자가 누구인지 판단한다. 인증은 보안의 첫 번째 단계로, 시스템에 접근하려는 사용자가 유효한 사용자임을 보장한다.

#### 인증 과정
1. 사용자가 로그인 폼이나 API 요청을 통해 자격 증명(예: 아이디와 비밀번호)을 제출한다.
2. 서버는 제공된 자격 증명을 데이터베이스나 외부 인증 시스템과 비교하여 유효성을 검증한다.
3. 검증이 성공하면, 시스템은 사용자에 대한 인증 토큰이나 세션을 생성한다.

#### 주요 특징
- **다양한 인증 방식 지원:**
    - 기본 인증(Basic Authentication): HTTP 헤더를 사용하여 사용자 이름과 비밀번호 전달.
    - 폼 기반 인증(Form-based Authentication): 커스텀 로그인 폼을 사용.
    - 토큰 기반 인증(Token-based Authentication): JWT를 사용하여 무상태(stateless) 인증을 구현.
    - OAuth2: 제3자 인증 제공자와 연동하여 인증 처리.
- **확장 가능성:** 커스텀 인증 필터를 추가하여 특정 요구 사항에 맞는 인증 로직 구현 가능.

#### 인증 실패 처리
인증 실패 시 애플리케이션은 보통 사용자에게 인증 실패 메시지를 반환하거나 로그인 페이지로 리디렉션한다.
```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .exceptionHandling()
            .authenticationEntryPoint((request, response, authException) -> {
                response.sendError(HttpServletResponse.SC_UNAUTHORIZED, "Unauthorized");
            });
}
```

```java
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
    auth.inMemoryAuthentication()
        .withUser("user")
        .password(passwordEncoder().encode("password"))
        .roles("USER");
}
```

---

### 인가(Authorization)

#### 정의
인가란 인증된 사용자가 애플리케이션 내의 특정 리소스에 접근할 수 있는 권한을 가지고 있는지 확인하는 과정이다. 이를 통해 사용자가 접근 가능한 리소스와 동작을 제어할 수 있다.

#### 인가 과정
1. 사용자가 요청한 리소스와 사용자의 권한 정보를 비교한다.
2. 사용자가 해당 리소스에 접근할 권한이 있으면 요청을 허용하고, 그렇지 않으면 접근을 거부한다.

#### 주요 특징
- **역할 기반 접근 제어(Role-based Access Control, RBAC):** 사용자의 역할(Role)에 따라 접근 권한 설정.
- **속성 기반 접근 제어(Attribute-based Access Control, ABAC):** 사용자 속성과 요청 정보를 바탕으로 세밀한 접근 제어.
- **정책 기반 접근 제어:** 규칙과 정책을 사용하여 복잡한 권한 부여 시나리오 처리.

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()
            .antMatchers("/admin/**").hasRole("ADMIN")
            .antMatchers("/user/**").hasAnyRole("USER", "ADMIN")
            .anyRequest().authenticated();
}
```

#### 접근 거부 처리
인가 실패 시 애플리케이션은 접근 거부 메시지를 반환하거나 에러 페이지로 리디렉션한다.
```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .exceptionHandling()
            .accessDeniedHandler((request, response, accessDeniedException) -> {
                response.sendError(HttpServletResponse.SC_FORBIDDEN, "Forbidden");
            });
}
```

---

### 인증과 인가의 차이점

| **항목**         | **인증(Authentication)**         | **인가(Authorization)**           |
|------------------|----------------------------------|------------------------------------|
| **목적**        | 사용자의 신원 확인               | 사용자의 권한 검증                |
| **시점**        | 시스템 접근 전                  | 시스템 접근 후                    |
| **결과**        | 사용자 신원 인증 성공/실패       | 권한에 따른 접근 허용/거부        |
| **사용 기술**   | OAuth, JWT, SAML                | RBAC, ABAC                       |

---

### 관련 기술 및 표준
- **JWT (JSON Web Token):** 인증과 인가 모두를 처리할 수 있는 경량화된 토큰 기반 기술.
- **OAuth2:** 인증과 인가를 위한 표준 프로토콜로, Google, Facebook 등에서 널리 사용.
- **SAML (Security Assertion Markup Language):** 기업 환경에서 많이 사용되는 XML 기반 인증 프로토콜.
- **LDAP (Lightweight Directory Access Protocol):** 디렉터리 서비스를 사용하여 인증 및 인가를 처리.

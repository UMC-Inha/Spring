- **Spring Security**
    
    Spring Security는 애플리케이션의 보안(인증 및 인가)을 제공하기 위한 강력하고 유연한 프레임워크다.
    
    스프링 기반 애플리케이션에서 주로 사용되며, 다양한 보안 관련 기능을 제공합니다.
    
    ### 주요 특징:
    
    1. **보안 기능 제공**
        - 인증(Authentication): 사용자의 신원을 확인하는 과정.
        - 인가(Authorization): 사용자에게 특정 리소스에 대한 접근 권한을 부여하는 과정.
    2. **구성 가능한 보안**
        - XML 또는 Java Config 기반 설정 가능.
    3. **다양한 인증 방식 지원**
        - 기본 인증(Username/Password)
        - OAuth2, JWT, SAML, LDAP 등.
    4. **강력한 커스터마이징**
        - 사용자 정의 필터 및 인증/인가 로직을 쉽게 구현 가능.
- **인증(Authentication)과 인가(Authorization)**
    
    ### **인증(Authentication)**
    
    **Authentication**은 사용자가 누구인지 신원을 확인하는 과정입니다.
    
    ### 주요 개념:
    
    - **Principal**: 인증된 사용자 정보(예: 사용자 ID).
    - **Credentials**: 사용자의 비밀번호와 같은 비밀 정보.
    - 인증 성공 시, 인증된 사용자 정보를 **SecurityContext**에 저장하여 애플리케이션 전반에서 접근 가능하게 합니다.
    
    ### Spring Security에서의 흐름:
    
    1. **AuthenticationManager**: 인증을 처리하는 핵심 인터페이스.
    2. **AuthenticationProvider**: 다양한 인증 방식을 구현하는 프로바이더.
    3. **UserDetailsService**: 사용자 정보를 가져오는 서비스.
    
    ---
    
    ### **인가(Authorization)**
    
    **Authorization**은 사용자가 특정 리소스 또는 기능에 접근할 권한이 있는지 확인하는 과정입니다.
    
    ### 주요 개념:
    
    - 권한(Role): 사용자가 가진 권한(예: `ROLE_USER`, `ROLE_ADMIN`).
    - 접근 제어: 사용자의 권한에 따라 특정 기능 또는 리소스 접근을 허용/차단.
    
    ### Spring Security에서의 흐름:
    
    1. **AccessDecisionManager**: 요청과 사용자 권한을 비교하여 접근 가능 여부를 결정.
    2. **Method Security**: 메서드 레벨에서 접근 제어 처리(`@PreAuthorize`, `@PostAuthorize`).
    3. **URL Security**: URL 기반 접근 제어(`httpSecurity.authorizeRequests()`).
    
    ### **Spring Security의 인증 및 인가 시나리오**
    
    1. 사용자가 로그인 요청.
    2. `AuthenticationManager`가 요청을 `AuthenticationProvider`로 전달.
    3. `AuthenticationProvider`가 사용자 정보를 확인하고 인증.
    4. 인증 성공 시, `SecurityContext`에 사용자 정보 저장.
    5. 사용자가 리소스 요청 시, `AccessDecisionManager`가 요청과 권한을 비교.
    6. 인가 성공 시, 요청 처리.

## 홈화면

###  API EndPoint
GET /user/{user-id}/home

### Request Header
Authorization : accessToken(String)

### Request Body
없음

### query String
없음

### Path variable
{user-id}


## 마이 페이지 리뷰 작성

### API EndPoint
POST /users/{user-id}/my-page/reviews

### Request Header
Authorization : accessToken(String)

### Request Body
```json
{
    "user-id" : "작성자 id",
    "mission-id" : "미션 id"
    "title" : "리뷰 제목",
    "content" : "리뷰 내용",
    "score" : "별점",
    "review-image" : "리뷰 이미지"
}
```
### query String
없음

### Path variable
{user-id}

## 미션 목록 조회(진행중, 진행완료)

### API EndPoint
GET /users/missions

### Request Header
Authorization : accessToken(String)

### Request Body
없음

### query String
?mission-state='진행중 or 진행완료'

### Path variable
없음

## 미션 성공 누르기

### API EndPoint
PATCH /users/{user-id}/missions/{mission-id}

### Request Header
Authorization : accessToken(String)

### Request Body
```json
{
    "mission-state" : "성공"
}
```
### query String
없음

### Path variable
{user-id}, {mission-id} 


## 회원가입 하기

### API EndPoint
POST /users

### Request Header
없음

### Request Body
```json
{
    "agree" : "이용약관 동의",
    "name" : "회원 이름",
    "gender" : "성별",
    "birth" : "생년월일",
    "address" : "주소",
    "prefer-food" : "선호 음식"
}
```
### query String
없음

### Path variable
없음
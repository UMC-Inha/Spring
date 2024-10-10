# 홈 화면
    
|        API Endpoint         |                                                            Request Body                                                            |            Request Header            | Query String | Path Variable |
|:---------------------------:|:----------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------:|:------------:|:-------------:|
|    GET /home/{memberId}     |                                                                 -                                                                  | Authorization : accessToken (String) |      -       |     회원 id     |
|    POST /myInfo/reviews     |                                      content : String <br/>rating : double<br/>image : String                                      | Authorization : accessToken (String) |      -       |       -       |               |
|   GET /missions/{status}    |                                                                 -                                                                  | Authorization : accessToken (String) |      -       |   미션 완료 여부    |
| PATCH /missions/{missionId} |                                                          member_id : Long                                                          | Authorization : accessToken (String) |      -       |   성공한 미션 ID   |
|      POST /members/new      | name : String<br/>gender : String<br/>address : String<br/>birth : Date<br/>location_terms : boolean<br/>marketing_terms : boolean |                  -                   |      -       |       -       |



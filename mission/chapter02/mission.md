1. 내가 진행중, 진행 완료한 미션 모아서 보는 쿼리(페이징 포함)
```sql
SELECT mm.status AS mission_status, m.content AS mission_content, 
				m.point AS mission_point, r.name AS restaurant_name 
FROM member_mission AS mm
JOIN mission AS m ON mm.id2 = m.id 
JOIN restaurant AS r ON m.id2 = r.id 
WHERE mm.id = 나의 ID
ORDER BY mm.id DESC
LIMIT ? OFFSET ?;
```

2. 리뷰 작성하는 쿼리, 사진의 경우는 일단 배제
```sql
//ERD - review 테이블에 member_id 추가 필요
INSERT INTO review (restaurant_id, member_id, score, content, created_at, updated_at)
VALUES (식당ID, 회원ID, 별점, 리뷰내용, NOW(), NOW());
```

3. 홈 화면 쿼리 (현재 선택 된 지역에서 도전이 가능한 미션 목록, 페이징 포함)
```sql
//ERD - mission 테이블에 deadline 추가 필요
SELECT ( SELECT COUNT(*) 
	    FROM member_mission AS mm
	    JOIN mission AS m ON m.id = mm.id2 
	    JOIN restaurant AS r ON m.id2 = r.id
	    WHERE mm.id = '회원ID' AND m.status = '완료' AND r.address = '선택한 지역' ) 
	    AS successful_mission_count, //선택한 지역에서 성공한 미션 개수를 column으로 생성 
	    m.content AS mission_content, m.point AS mission_point, 
	    m.deadline AS mission_deadline, r.name AS restaurant_name, 
	    r.type AS restaurant_type
FROM mission AS m
JOIN restaurant AS r ON m.id2=r.id  //식당별로 올라온 미션 
LEFT JOIN member_mission AS mm ON mm.id2 = m.id AND mm.status = '미완료' //위 테이블 + 회원이 진행하는 미션 중 완료되지 않은 미션 정보 추가
WHERE r.address = '선택한 지역'
ORDER BY m.created_at DESC
LIMIT ? OFFSET ?;
```

4. 마이 페이지 화면 쿼리
```sql
SELECT m.name, m.email, m.phone_number, m.point
FROM member AS m
```
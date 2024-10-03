# 진행중, 진행 완료한 미션
```mysql
select b.name, b.content, b.point, a.status, r.name 
from member_mission as a join mission as b on a.id2 = b.id 
    join (select id, name 
          from restaurant) as r on b.id2 = r.id
where a.member_id = '내 id'
limit 10 offset 0*10;
```

# 리뷰 작성
```mysql
insert into REVIEW(id,restaurant_id,score,content)
values (id,restaurant_id,5,
        '음 너무 맛있어요 포인트도 얻고 맛있는 맛집도 알게 된 것 같아 너무나도
행복한 식사였답니다. 다음에 또 올게요!!');
```
# 홈 화면 쿼리
```mysql
select m.address, complete_mission.complete
from member as m 
    join (select member_id, count(*)/10 as complete
          from member_mission
          where member_id = 1 and status = '완료' 
          group by member_id ) as complete_mission
    on m.member_id = complete_mission.member_id;

select m.content,m.point, res.name, res.type, m.deadline
from mission as m join (
    select r.id,r.name,r.address, r.type
    from restaurant as r 
    where address = (select address
                     from member
                     where member_id = 1)
    ) as res on m.id2 = res.id
where m.id not in (
    select m_m.id2
    from member_mission as m_m
    where member_id = 1 and status = '진행 중'
) 
limit 10 offset 0*10;
```
# 마이 페이지
```mysql
select name, nickname, point, phone_number, email
from member
where id = 1;
```
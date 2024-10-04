2주차 미션입니다.

```sql
select id, reward, state, content
from mission join on mission.id = MemberMisson.mission_id
	(select misson_id, state
	from MemberMission
	where member_id = "user_id")
where state = 1 or state = 2// 진행 중, 진행 완료
order by state, id 
limit 10 offset 0;
```

```sql
insert into review
values(
	cur_Id,
	user_Id,
	store_Id,
	contents,
	rating,
)
```


```sql
select 
	m.id as id, 
	m.lower_price as lower_price, 
	m.reward as reward,
	m.deadlime as deadline,
	s.name as store_name,
	s.info as store_info
from mission m join store s on s.id = m.store_id
where m.state = 'possible' and s.address = 'cur address'
order by id
limit 10 offset 1 * 10;
```

```sql
select nickname,email,phone_number,point_value
from member where id=012;
```